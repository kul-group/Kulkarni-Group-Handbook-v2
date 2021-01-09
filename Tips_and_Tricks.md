
### Tips
- jupyter trick for code dev on hpc
<pre><code>1. Run jupyter notebook on remote (say HPC1) using 
jupyter notebook --no-browser --port=8888
2. Listen to the remote port using ssh
ssh -N -f -L localhost:8888:localhost:8888 $USER@hpc1.engr.ucdavis.edu
If you get an error saying that port 8888 is busy, use the following command to find and kill the process
 lsof -ti:8888 | xargs kill -9

3. Run the jupyter notebook using the local browser by copy pasting the token
</pre></code>

- automate logins to hpc
- use ase.db
- automated rsync
- scripts on hpc to quickly do repetitive tasks
- code for getting papers off campus
- folder organization
- reading papers and organizing lit
- presentation tips, how to do a lit review
- use [queue wait times](https://my.nersc.gov/queuewaittimes.php) for submitting jobs on cori.
- configuring pycharm: make sure to configure your conda environment with pycharm follow [these directions](https://docs.anaconda.com/anaconda/user-guide/tasks/pycharm/#configuring-a-conda-environment-in-pycharm) and use the path you obtain by typing `which python` in your command line as the interpreter.
- [chmod reference](https://chmodcommand.com/)
- chgrp reference:

### Sticking points
- vasp scripts crashing (check header is correct, use debug queue, fix environment variable, make sure modules are loaded)
- optimization/vibration output is bad, how to fix
- neb tips (opt fs and use vasprun for is .. )
- python scripts crashing (start with really simple problem, make sure PATH is set up, break into separate subtestable scripts, print internal variables)
- python code not running on hpc: make sure utf8 header is there, chmod u+x, in bin folder

HPC1 
There seems to be difference between different CPUs. I find that c6-XX (Intel(R) Xeon(R) Silver 4110 CPU @ 2.10GHz) is faster than c5-XX ( Intel(R) Xeon(R) CPU E5-2630 v3 @ 2.40GHz). If you find similar behavior with other codes (I tested cp2k), please let me know. 


CP2K 
Metadynamics - Be careful about the units being used. CP2K defaults into internal_cp2k while providing output, we usually care about Ang. 
Indexing - cp2k counts from index 1 .. N, while ASE/VMD starts from index 0 

Packages not loaded in NERSC: Make sure to download the .bashrc file and .bash.ext file from the repo_shared folder to your account
Cannot get Pulse Secure to connect: Sam still has problems with this
scipy.optimize.minimize not working: function to optimize must be a function of one argument containing all the parameters you want to optimize
python can't call ase: make sure ase has the correct path variable
math eqns in python don't work: make sure things are written as ```2*x``` not ```2x``` and ```x**3``` instead of ```x^3```
weird things happen during vasp vibrational calculation: set NSW to 1


