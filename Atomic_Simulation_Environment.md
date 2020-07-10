### Atomic Simulation Environment

ASE is a python package we use for manipulating atomic structures. Documentation can be found [here](https://wiki.fysik.dtu.dk/ase/#). This page lists some advice for using ASE and ASE gui.

#### Using ASE

#### ASE GUI

ASE GUI is used to visualize and manipulate atoms. It can even be used to visualize atoms on an HPC, but this is slow.

To use ASE GUI, navigate to the file you want to view on the command line, then type ```ase gui [FILENAME]``` and hit enter. A window should pop up.

##### Useful Commands

two finger click and drag will allow you to rotate the atoms object.

Cntl + B: toggles between bond view and atom view, bond view is more useful

Click an atom: displays atom properties

Select Multiple atoms: 1-finger click and drag to highlight atoms, or Cntl + click to select individual atoms

Move: Cntl + M will allow you to move selected atoms using your arrow keys. Viewing direction changes what your arrow keys do.

Rotate: Cntl + R will allow you to rotate selected atoms using your arrow keys. Viewing direction changes what your arrow keys do.

Save: Cntl + S

Full documentation can be found [here](https://wiki.fysik.dtu.dk/ase/ase/gui/gui.html?highlight=ase%20gui#module-ase.gui)
