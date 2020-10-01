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
- MOF's: Oftentimes you will have to find crystallographic data from the SI of a paper which synthesized the MOF you are interested in. [Here](https://cmcp-group.github.io/CoRE-MOFs/) is a small, computationally ready, database of MOF structures.[This](https://www.ccdc.cam.ac.uk/structures/) is a large, messy database of MOF structures.
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

### Nudged Elastic Band

### Monte Carlo

### Metadynamics

