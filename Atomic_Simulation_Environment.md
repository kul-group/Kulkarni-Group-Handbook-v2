### Atomic Simulation Environment

ASE is a python package we use for manipulating atomic structures. Documentation can be found [here](https://wiki.fysik.dtu.dk/ase/#). This page lists a basic review for using ASE and ASE gui.

#### Using ASE

##### Reading/Writing Files

Read files in Python with:
```
from ase.io import read
structure = read('atoms_file.cif')  # creates atoms object named 'structure'
```
Write new files with `structure.write('new_file.traj')` or `write('new_file.traj', structure)` where 'new_file.traj' is the name of the file which will be written.

##### Adding or Deleting Atoms/Molecules/Slabs

You can combine two atoms objects using the `+` operator: `combined_atoms = atoms1 + atoms2`. 'combined_atoms' will have the unit cell shape of atoms1, so order of addition matters!

So, for example, you can add a hydrogen atoms using:

```
from ase import Atom
h_atom = Atom('H', (1, 1, 1)) # Creates an H atom at the (1, 1, 1) position
structure_with_hydrogen = structure + h_atom  # new atoms object which has all the atoms in 'structure' and an H atom at (1, 1, 1)
```

You can make a molecule using:

```
from ase.build import molecule
ch3oh = molecule('CH3OH')
```
Note that only some simple molecules work with build. See the documantation for the [full list](https://wiki.fysik.dtu.dk/ase/ase/build/build.html?highlight=build#ase.build.molecule)

You can build a metal surface slab using:

```
from ase.build import surface
s1 = surface('Au', (2, 1, 1), 9)  # makes a gold surface along the [2 1 1] plane with 9 layers
s1.center(vacuum=10, axis=2)  # centers the slab in the unit cell with 10 angstroms of vacuum along the y-axis
```

##### Moving/Rotating Atoms

Move a set of atoms using `atoms.translate([x,y,z])` where x,y,z are the amounts to move in x/y/z direction (in angstroms).

Rotate a set of atoms using:
```
atoms.rotate(90, 'z')  # rotates atoms 90 degrees around z-axis
atoms.rotate(90, (0, 0, 1))  # rotates atoms 90 degrees around (0, 0, 1) vector (The z-axis)
atoms.rotate('x', 'y')  # rotates the x-axis into the y-axis
atoms.rotate((1, 0, 0), (0, 1, 0))  # rotates the (1, 0, 0) axis into the (0, 1, 0) axis
```

##### Neighbors

Obtain the indicies of the neighbors of a particular atom using:
```
from ase.neighborlist import NeighborList, natural_cutoffs
nl = NeighborList(natural_cutoffs(atoms), self_interaction=False, bothways=True)
nl.update(atoms)  # rerun this line anytime atoms in structure move
neighbors = nl.get_neighbors(atom_index)[0] # list of neighbor indicies around the atom at atom_index. the '[0]' is important!
```

##### Constraints

Constrain the positions of atoms using:
```
from ase.constraints import FixAtoms
index_list = [1, 2, 3, 99]  # list of atom indicies you want to constrain
c = FixAtoms(indices=index_list)
atoms.set_constraint(c)
```
This will prevent the atoms at the specified indicies from moving in any simulation.

Constrain bondlengths between pairs of atoms using:
```
c = FixBondLengths([[0, 1], [0, 2]])
atoms.set_constraint(c)
```
This will prevent the distance between atom 0 and atom 1 as well as the distance between atom 0 and atom 2 from changing.

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
