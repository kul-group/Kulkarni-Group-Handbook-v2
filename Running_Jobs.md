> This page is still under construction!

### Chapter Contents
- Getting Atomic Structures
- Running and Checking on Jobs
- Optimization
- Vibrations
- Molecular Dynamics
- Nudged Elastic Band
- Monte Carlo
- Metadynamics
- Microkinetic Modelling

This is a basic summary of how to run some common calculations. 
More detailed instructions can be found in the documentation of the software package you are using: 
- The group uses VASP for many calculations, [the VASP wiki](https://www.vasp.at/wiki/index.php/The_VASP_Manual) will be useful for these jobs
- [LAMMPS](https://lammps.sandia.gov/) is used for some Molecular Dynamics.

### Getting Atomic Structures
There are several ways of getting initial atomic structures for your research. 
- [Open Quantum Materials Database](http://oqmd.org/) and the [Materials Project](https://materialsproject.org/) have theoretical crystal structures for many inorganic compounds. Try to search compositions and download the .cif file for a structure of interest.
- Zeolites: the International Zeolite Association maintains a [database](https://asia.iza-structure.org/IZA-SC/ftc_table.php) of known zeolite structures and should allow you to download a .cif file.
- MOF's: Oftentimes you will have to find crystallographic data from the SI of a paper which synthesized the MOF you are interested in. [Here](https://cmcp-group.github.io/CoRE-MOFs/) is a small, computationally ready, database of MOF structures. [This](https://www.ccdc.cam.ac.uk/structures/) is a large, messy database of MOF structures.
- Surfaces: ASE allows you to build elemental surfaces with the ase.build.surface method. 
- Molecules: ASE has preset molecules you can create using the ase.build.molecule method. For small variations on these, you can create a preset molecule in ASE and then edit it in ASE GUI.

### Optimization
#### theory
- optimization finds the lowest energy configuration of your atoms.
- the energy of the optimized state is the electronic energy of the state and is used in energy diagrams.
#### how-to
- set encut to [], set ibrion to [] ...
- kul-group code for optimization [link]
#### tips
- start with a reasonable initial structure, a bad guess can lead to adsorbates falling apart
- submit jobs for the right amount of time so your job isn't in the queue too long
- check the final structure after optimization to make sure it is reasonable

### Vibrations

#### tips
- make sure the optimization before vibration run has the same ENCUT and ediff
- set NSW=1 !!!
### Molecular Dynamics

- http://devonwa.com/2016/09/01/installing-and-using-LAMMPS-with-ASE/

### Nudged Elastic Band Workflow (Climbing Image)
1. The nudged elastic band workflow begins with defining initial and final states, i.e. your reactants together and your products together in the same cell, with matching indices (for interpolation). Ensure that the species in your system are in their favored bonding positions (for example: a CH3\* reactant should be in an 'ontop' position for surface calculations). Place both species close enough together that there are no additional diffusion barriers for reaction, but not so close that optimizating the structure might yield a change in bonding. Once these are made and saved as is.traj and fs.traj, optimize both geometries.
2. Next, make a transition state. You will likely want to use ASE's interpolation tools for this (Ambar's interp_neb.py tool can be very helpful for manipulating structures from the terminal). You should also use your intuition about chemical bonding to find an intermediate high-energy state that works as an initial guess for the initial state. This is an important step and choosing the correct transition state has a significant effect on how quickly your CI-NEB will converge. Save this as ts.traj. *Unstable transition states or other images you use in your initial guess will cause your NEB to fail.*
3. Now you will make a set of interpolated images for VASP. You can use interp\_neb.py as a command line tool for this. Examples:
```
interp_neb.py is 3 2 # interpolate between is.traj and neb3.traj with 2 images in between
interp_neb.py 3 fs 3 # interpolate between neb3.traj and fs.traj with 3 images in between
interp_neb.py is fs 7 # interpolate between is.traj and fs.traj with 7 images in between
```
So rename your is.traj appropriately. You may want to have six images, with your ts.traj as neb3.traj. Or eight with neb4.traj. Or whatever. It is best to start with a small amount of images (one to three images between is and fs).

4. You have your optimized endpoints and a set of images between them, so you're ready to run a VASP NEB. You can use Henkelman's VASP tools to run a climbing-image NEB, but convergence may be better if you run a standard NEB for a few iterations first.
5.  The number of nodes you use should be evenly divisable by the number of images you are using, or VASP will throw an error. These calculations are very time-consuming and computationally intensive, so be careful.

#### Setting up a NEB
The initial state should be saved as a POSCAR in a directory called 00, and the middle images should be POSCARs in directories, in order, named 01, 02, 03, etc. (up to the amount of images you have). The final state POSCAR goes in the last directory named in the same way. This should be taken care of in the vasp_neb.py script. *If you are running a climbing-image NEB you need a CONTCAR and a POSCAR in the directory too. It doesn't matter what they are, but there is a bug in VASP NEB with ASE that will cause the calculation to fail.*

#### VASP Settings for NEB and CI-NEB
"Pre-NEB"/NEB: ibrion=3, iopt=0, lclimb=False, potim=0.05
    POTIM is the step size for MD. Make sure you have a CONTCAR and OUTCAR in the directory. Just copy over from your opt_is and opt_fs calcs.

CI-NEB: ibrion=3, iopt=7, lclimb=True, potim=0.0
    This combination of ibrion and iopt is the FIRE (Fast Intertial Relaxation Engine) algorithm, the fastest for CI-NEB. 

Fore more detail:

VASP elastic band and nudged elastic band: https://cms.mpi.univie.ac.at/vasp/vasp/Elastic_band_method.html

Henkelman group VASP NEB tools: https://theory.cm.utexas.edu/vtsttools/neb.html#neb

#### Pre-optimizing your transition state and "pre-NEB"
It is a good idea to pre-optimize your transition state. This involves:
1. Constraining the atoms that are part of bonds that break through the reaction and relaxing the unconstrained atoms (20-30 steps), then
2. Constraining the atoms that are not part of the bonds that break through the reaction and relaxing the unconstrained atoms (10 steps).
3. Running a "pre-NEB" (standard NEB without the climbing-image) for 10 steps. (Be careful with this - too many steps will cause the transition state to move away from the maximum energy along the band)
This is done before running the full climbing-image NEB and improves your initial guess.

#### Tips for NEB Success
 - Pay close attention to the structures you provide NEB. Checking the NEB periodically can be helpful as well, as you may need to terminate the job and make changes to them.
 - Convergence can be improved (provided your structures are okay and you are confident in the transition state) by increasing the spring constant (SPRING) from the default 5 up to 7 or even 10. However, if the spring constant is too high, the NEB may get stuck.

#### Troubleshooting
*The structures in my NEB make no sense. They have gone all over the place.*

In this case, you likely made a mistake with your initial guess. Check that the indices match across the structures. Use the ASE GUI to label the indices and make sure they are the same. The other possibility is that you put atoms in places that make them unhappy. This will always throw off the NEB.

*I cannot converge my NEB, although there are no clear issues with it.*

There are a couple things you may try. If you increase your spring constant, you can narrow down your search of the PES. You can also try using only one image. This reduces the effect of unhappy images and simplifies the optimization problem. Only do this if you are confident about your TS and are relatively close to convergence (< .5 eV).

*MPI errors/SLURM errors/VASP errors with CI-NEB*

Climbing image NEB in VASP with ASE currently has a bug that requires a CONTCAR and OUTCAR in the same directory as the calculation. The CONTCAR and OUTCAR should be for similar structures (just copy over from opt_is or opt_fs), but calcs will fail with them. Another possibility is that the number of nodes you request on the cluster is not an even divisor of the number of images.

*My reaction-energy diagram has multiple peaks.*

Your NEB will require a restart. If you look at the final set of images, you will likely see that two disconnected images have started to look very similar. Double check your structures and try increasing the spring constant. Another possibility is that there are two reactions or diffusion steps taking place, with two activation energies.

*I have no idea where the transition state is and VASP can't find it.*

Try using many images. This allows you to sample energies in more images along the band, giving you more possibilities for a TS. Reduce the number of images once you are confident you've found it.

#### Analyzing a reaction-energy diagram out of a NEB
You will likely not converge in your NEB in one attempt. You will have to be careful how you choose the images for your next iteration. Look at the reaction-energy diagram (using neb_plot.py) for your calculation and check that there is a hill-like trend (may look like a peak, but just check the tangents) and that the transition state is 1) at the highest energy point, and 2) has a horizontal tangent. If an image is at nearly the same energy as the initial state, get rid of it and/or interpolate more closely to the TS. Same with the final state. If the diagram looks good and fmax is reasonable, you can try interpolating images to be more close to the TS (e.g. use your final images [0, 1, 2, 3, 4] in the first iteration to make images [0, 1.5, 2, 2.5, 4] for the next iteration). Reduce the number of images if you are close to convergence.

#### ML-NEB
Expensive nudged elastic band calculations can be greatly accelerated with a machine-learning optimization method. This is implemented in SUNCAT's Catlearn ML-NEB module: https://github.com/SUNCAT-Center/CatLearn. The .ipynb file in tutorials > 11\_NEB > 00\_Tutorial is a good start.

As of January 2021, ML-NEB does not work out of the box.

### Monte Carlo

### Metadynamics

