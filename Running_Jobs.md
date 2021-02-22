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

### Nudged Elastic Band (Climbing Image)
1. The nudged elastic band workflow begins with defining initial and final states, i.e. your reactants together and your products together in the same cell, with matching indices (for interpolation). While automated construction of the states in the works at the Kulkarni lab, constructing your is.traj and fs.traj manually works fine. Ensure that the species in your system are in their favored bonding positions (for example: a CH3\* reactant should be in an 'ontop' position for surface calculations). Place both species close enough together that there are no additional diffusion barriers for reaction, but not so close that optimizating the structure might yield a change in bonding. Once these are made and saved as is.traj and fs.traj, optimize both geometries.
2. Next, make a transition state. You may want to use ASE's interpolation tools for this if it is complex. However, you can also use your intuition about chemical bonding to find an intermediate high-energy state that works as an initial guess for the initial state. This is an important step and choosing the correct transition state has a significant effect on how quickly your CI-NEB will converge. Save this as ts.traj.
3. Now you will make a set of interpolated images for VASP. You can use interp\_neb.py as a command line tool for this. Examples:
    interp_neb.py is 3 2 (interpolate between is.traj and neb3.traj with 2 images in between)
    interp_neb.py 3 fs 3 (interpolate between neb3.traj and fs.traj with 3 images in between)
    interp_neb.py is fs 7 (interpolate between is.traj and fs.traj with 7 images in between)
So rename your is.traj appropriately. You may want to have six images, with your ts.traj as neb3.traj. Or eight with neb4.traj. Or whatever.
4. You have your optimized endpoints and a set of images between them, so you're ready to run a VASP CI-NEB. Note the settings used in vasp\_neb.py. Look up the VASP settings you're not familiar with. Note that the number of nodes you use should be equal to the number of images you are using, or VASP will throw an error.
5. These calculations are very time-consuming, so be careful. You may also want to use ML-NEB instead.

VASP elastic band and nudged elastic band: https://cms.mpi.univie.ac.at/vasp/vasp/Elastic_band_method.html
Henkelman group VASP NEB tools: https://theory.cm.utexas.edu/vtsttools/neb.html#neb

### ML-NEB
Expensive nudged elastic band calculations can be greatly accelerated with a machine-learning optimization method. This is implemented in SUNCAT's Catlearn ML-NEB module: https://github.com/SUNCAT-Center/CatLearn. The .ipynb file in tutorials > 11\_NEB > 00\_Tutorial is a good start.

As of January 2021, ML-NEB is a bit buggy.

### Monte Carlo

### Metadynamics

