---
layout: page
title: Using the CEES HPC resources  
subtitle: Running jobs on abel  
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Slurm scripts versus interactive jobs
> * Submitting a job to abel through a slurm script
> * Checking the status of a job
> * Cancelling a job
> * Interactive use of abel resources 

In [HPC-lesson nr 1](http://uio-cees.github.io/hpc-lessons/01-login.html) you have seen that after you have logged in you are on one of the two logim nodes (login-0-1.local or login-0-2.local). These are shared resources and are only used for running small commands, checking progress on your current jobs, or moving around the data folders available on abel.

The login nodes are not meant for processes requiring much more memory, such as a genome assembly or blasting thousands of sequences. In order to run such jobs you need to request for computing resources.  The system assigning computing resources on abel is called [SLURM](http://slurm.schedmd.com/).  You can communicate with this system in two ways:
>* Slurm script
>*  interactive qlogin

###Slurm scripts
A slurm script is a little text file containing the instructions that specify what computing resources you need and for how long. It also contains the commands to start and run your analysis.

Below you find and example slurm script.
~~~{.bash}
#!/bin/bash
#SBATCH --account=cees
#SBATCH --time=00:30:00
#SBATCH --mail-user=thhaverk at ibv.uio.no
#SBATCH --mail-type=ALL

##memory specs
#SBATCH --mem-per-cpu=3800M
#SBATCH --cpus-per-task=1
#SBATCH --job-name=test

## Set up job environment
source /cluster/bin/jobsetup

## where am I?
pwd

echo 

sleep 30m

echo finished with sleeping.
~~~

The lines starting with _#SBATCH_  specify the conditions for your job. The necessary conditions are:
* --account : Which project is used to run the job. Here it is "cees".
* --time : Time to run the job stated in:  hours:minutes:seconds.
* --mail-user: the e-mail address from the submitter.
* --mail-type: What kind of notifications are send to the submitter, start, end or failing of the job. "All" is all of these.
* --mem-per-cpu: The memory used for your job by one cpu.
* --cpus-per-task: Number of cpu's used for the job. When using more cpus's E.g. 4 cpu's than memory asked for is 4 x 3800M = 15200M.
*#SBATCH --job-name= speaks for itself.

finally, in order to start the job you need to give the command:
~~~
source /cluster/bin/jobsetup
~~~
Without it, nothing will happen.
