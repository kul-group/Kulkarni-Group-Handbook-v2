### High Performance Computers

> This section is under construction. You may find the [Running Jobs](Running_Jobs.md) and [Learning ASE/Python/HPC](Learning_ASE-Python-HPC.md) sections useful for now. Of course, asking group members for help is also useful!

High Performance Computer or HPC is just a term for much larger, faster, computers, stored in a different location, which can be assigned computational tasks. Here is an overview of the HPC's we use and how to use them effectively.

#### Best Practices

- storing data
- transferring data
- getting jobs through quickly


#### Installing Anaconda on Stampede

1. type `wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh` into your command line
2. type `bash ~/Downloads/Anaconda3-2020.02-Linux-x86_64.sh`
3. type `source ~/.bashrc` so the anaconda installation starts working

### NERSC

### Stampede

### HPC1/HPC2

#### Useful Commands

`sl` to see a choo-choo train

modify your .bashrc to include these shortcuts:

#### Useful scripts

#### Interactive mode

When testing scripts that require VASP, it is useful to use interactive mode. This allows you to run a VASP calculation on a node as though you were working in a normal directory, so messages will be printed to your screen as the job runs. Another window can be opened to monitor the file structure, inspect VASP output files, etc. This is done by running

    alias interactive='srun --nodes=1 --ntasks-per-node=16 --time=04:00:00 --pty bash -i'

and then running your script (with Python, for example. Not sbatch.).

#### Outside References

Nersc wait times

Nersc documentation

Stampede documentation
