### Learning ASE/Python/HPC

#### ASE

##### Getting Started with ASE
- make sure you have ase downloaded and on your anaconda PATH -> the `import ase` command in the python command line should give no errors

##### ASE Practice Problems
- First, download a structure from the internet (e.g. from this [zeolite database](https://asia.iza-structure.org/IZA-SC/ftc_table.php)) or from someone in the group
- Move the structure file to the folder where you are writing and running practice scripts
- Write a new script with the following lines included:

``` 
# This reads your file into an Atoms object 'a'
from ase.io import read, write
a = read('STRUCTUREFILE') 
```
Where STRUCTUREFILE is the name of the structure file you downloaded.
'a' is an object with the positions of the atoms in your structure, you can manipulate this to complete the practice problems below.

##### ASE GUI

With the ASE python package downloaded, navigate to the folder of the file you want to view with ASE GUI in your terminal. Now type `ase gui STRUCTUREFILE` and hit enter. STRUCTUREFILE is the full name of the atomic structure file you want to view. 
Common commands:
- scroll up/down to zoom
- two finger click-and-drag to rotate
- one finger click or one finger drag to highlight atoms
- pressing numbers 1, 2, 3 orients along x, y, z directions respectively
- Ctrl-B toggles between bond view and atom view
- Ctrl-M allows you to move highlighted atoms with the arrow keys
- Ctrl-R allows you to rotate highlighted atoms with the arrow keys

#### Python

##### Getting started with Python
Make sure you have Anaconda downloaded and an IDE to write code in. Set up your folders and path ... 
See [this page](Programming.md) for group coding guidelines.

##### Python Practice Problems
- see [here](http://www.practicepython.org/) for good python practice problems. Once you are comfortable with manipulating lists, for loops, and if/else statements, focus on the ASE practice problems.

#### HPC

##### Getting Started on HPC: Logging in
Make sure you have an account with the HPC you want to log in to. HPC account creation [here](Account_Setup.md#essential). You will need your account information and (possibly) your 2FA set up to log in.
- In your command line, type ```ssh -XY username@address``` and hit enter. where 'username' is your account username and 'address' differs based on the hpc you are logging into:
HPC1: address=hpc1.cse.ucdavis.edu (OR 'hpc1.engr.ucdavis.edu' check your account)
Stampede: address=stampede2.tacc.utexas.edu
Cori: address=cori.nersc.gov

- you will be prompted for your password and your 2FA, no dots or letters will show up as you type, just type each and press enter.

##### Getting Started on HPC: Basic Commands
This is a basic introduction to the most commonly used bash commands. A more detailed tutorial can be found [here](Command_Line.md#command-line). You can practice most of this on your local machine. Essentially, the command line allows you to move around your computer, make new files, edit documents, and run simple programs. While this is easy to do on your local machine using Finder or Anaconda, when using a HPC, almost everything must be done using the command line. To start, open iTerm or other terminal software.

###### Moving Around
- See what directory you are in at anytime by typing `pwd` (and then pressing enter)
- See what items are in your current directory by typing `ls`
- Move to one of the subdirectories by typing `cd [directory_name]` for example, in your home directory (the one you start in when you open iTerm) `cd Desktop` will take you to your Desktop, and then typing ```ls``` will show you the same files that you see on your Desktop normally.
- Return to your home directory at anytime by typing `cd ~/` or just `cd`
- Go from your current directory to the one that contains it (or 'above' it) by typing `cd ../`
- Go to a particular directory by typing ```cd path/to/dir``` where 'path/to/dir' is the string you get when you type ```pwd``` in the particular directory you wish to go to

###### Moving Files 
 - copy a file from one location to another using `cp path/to/source path/to/destination`
 - copy a folder from one location to another using `cp -r path/to/source path/to/destination`
 - copy a file from one location to another using `mv path/to/source path/to/destination`
 - copy a folder from one location to another using `mv path/to/source path/to/destination`
 - delete a file using `rm filename`. Be careful, there is no way to undo this action!!
 - delete a folder using `rm -r foldername`. Be careful, there is no way to undo this action!!
 
Note that in the previous examples, 'path/to/folder' and 'path/to/file' refer to the file paths you would need to navigate to that item. For example if you wanted to copy 'zeolite.traj' from the Documents folder to the Desktop, you could use `cp ~/Documents/zeolite.traj ~/Desktop/.`. However, if you are already in the Documents folder, you do not need to type the entire path, you can instead write `cp zeolite.traj ~/Desktop/.` since the terminal will automatically copy the file named 'zeolite.traj' in your current folder.

###### Opening Files
- make a new file by typing 'vi filename' where filename is the title of the file you want to create. This will open a blank file in the vi editor, more details on using vi in the next section. 
- open and existing file by typing 'vi filename' where filename is the title of the file you want to open. Once again this will open the file in a vi editor.

###### Editing Files
The vi editor seems simple but has many important commands. A more thorough list can be found [here](https://www.cs.colostate.edu/helpdocs/vi.html). 
The basic commands are:
- move around using the arrow keys
- edit part of the file by pressing the 'i' key, in the lower left corner you will see the word 'INSERT' indicating that you are in insert mode. Here you can delete characters, write new ones, and add new lines. However, your changes do not automatically save! Get out of insert mode by pressing the escape key.
- quit vi and save your work by holding down the shift key and pressing Z twice (shift + ZZ)



