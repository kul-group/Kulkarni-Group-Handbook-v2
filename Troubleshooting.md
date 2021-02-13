### Troubleshooting

#### ASE

This is a list of random issues people have experienced and their solutions to the problem. Please add any issues you have come across and fixed as well. 

- a list of atoms objects won't write when I try, `atoms_list.write('name.traj')` -> use the `write('name.traj', atoms_list)` syntax instead

- constraints: using a mask in FixAtoms:

```
mask_constrain = \[atom.index for atom in atoms_in if atom.tag in \[4, 3\]\]
constraints = FixAtoms(mask = mask_constrain)
atoms.set_constraint(constraints)
```
  This method is buggy. Just use indices instead.

```
constraints = FixAtoms(indices = mask_constrain)
atoms.set_constraint(constraints)
```

##### VASP/Clusters

- Files are not written/jobs appear to be running but nothing is happening: Check that you have not reached your quota on the cluster. On Cori, type < myquota > to check this. You may want to move files to a different directory on the system - your $HOME directory is not where you should store completed calculations. Refer to cluster websites/the group for info about quotas and different directories.

- SIGTERM error with VASP (looks something like this:)

```
forrtl: error (78): process killed (SIGTERM)
Image              PC                Routine            Line        Source
vasp_std           0000000026DAC80E  Unknown               Unknown  Unknown
vasp_std           000000002568C6E0  Unknown               Unknown  Unknown
vasp_std           0000000026D22656  Unknown               Unknown  Unknown
vasp_std           0000000026BCB60F  Unknown               Unknown  Unknown
```
    
   VASP isn't happy running your job with your SLURM settings. Something is wrong with your atoms objects, node specifications, etc. Check that you aren't dividing a NEB over an inappropriate number of nodes, or that your atoms objects have issues. Check VASP files, starting with op.vasp. Check your VASP_COMMAND environmental variable.
 
 - op.vasp message:
 
 ```
     ERROR: number of potentials on File POTCAR incompatible with number of species
     INCAR :           7 POTCAR:            4
 ```
 
   This is an ordering issue. Try re-ordering your atoms object. You will notice your POSCAR has a repeated atom type (because, for example, your Hydrogens are not indexed together [36, 37, 39] and not [36, 37, 38]), and this confuses VASP. You can do this by manually reconstructing your atoms object with the ASE GUI, or piece-by-piece with ASE, e.g.
 
```
atoms = H_atoms.copy()
atoms += C_atoms.copy()
atoms += O_atoms.copy()
```
