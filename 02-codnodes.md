---
layout: page
title: Using the CEES HPC resources
subtitle: Using the cod nodes
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Log in to the cod nodes, check who is running jobs on it and how busy the node is
> * Reserve the node for use
> * Run a simple job on the node and follow its progress
> * Start long-running jobs
> * Cancelling jobs

Open your terminal program and write - replacing `username` with your UiO username:

~~~ {.bash}
ssh username@cod5.hpc.uio.no
~~~

This should show something like this:

~~~ {.output}
Last login: Wed Sep  9 12:44:45 2015 from bioxxxxx.uio.no
  Research Computing Services, University of Oslo - ABEL
  Info: http://hpc.uio.no/    Help: hpc-drift@usit.uio.no
                           ,__
                           |  `'.
        __           |`-._/_.:---`-.._
        \='.       _/..--'`__         `'-._
         \- '-.--"`      ===        /   o  `',
          )= (                 .--_ |       _.'
         /_=.'-._             {=_-_ |   .--`-.
        /_.'    `\`'-._        '-=   \    _.'5
                 )  _.-'`'-..       _..-'`
                /_.'        `/";';`|
                             \` .'/
                              '--'

                     Welcome to cod5

~~~
Enjoy the ASCII fish, courtesy of USIT!

> ## Skipping your username {.callout}
>
> If you logged in on the computer you run this command using the same username as on the cod nodes or abel, you can skip the username: `ssh cod5.hpc.uio.no`. For abel, you can even skip the `uio.no` part when you are on the UiO network and simply type `ssh abel`. Unfortunately, with the cod nodes, you will always have to write the `hpc.uio.no` part.

###Checking node usage

Let's see how busy the node is. Write this command:

~~~ {.bash}
top
~~~

You are presented with an output similar to (but not identical with) this:

~~~ {.output}
top - 08:01:08 up 22 days, 16:27,  4 users,  load average: 6.62, 6.96, 7.50
Tasks: 1997 total,   2 running, 1994 sleeping,   1 stopped,   0 zombie
Cpu(s): 10.9%us,  0.1%sy,  0.0%ni, 89.0%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
Mem:  1588217204k total, 1048199928k used, 540017276k free,   310708k buffers
Swap: 10485756k total,   318964k used, 10166792k free, 963947960k cached

   PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
  8125 hannibal  20   0  907m 214m 186m S 595.9  0.0  14435:09 blastx
 73043 superman  20   0 48.7g  48g 508m R 100.0  3.2   3309:44 samtoh5
 75259 username  20   0 31144 2956 1092 R  1.6  0.0   0:00.21 top
 75260 root      20   0  105m 4496 3368 S  1.3  0.0   0:00.04 sshd
 14786 root      20   0  491m 4296 1020 S  0.3  0.0 107:08.12 collectd
 30359 smrtpersn 20   0 4726m 341m 5408 S  0.3  0.0  58:39.62 jsvc
     1 root      20   0 27740 1384 1152 S  0.0  0.0   3:51.23 init
     2 root      20   0     0    0    0 S  0.0  0.0   0:00.23 kthreadd
     3 root      RT   0     0    0    0 S  0.0  0.0  96:08.17 migration/0
     4 root      20   0     0    0    0 S  0.0  0.0   0:31.94 ksoftirqd/0
     5 root      RT   0     0    0    0 S  0.0  0.0   0:00.00 stopper/0
     6 root      RT   0     0    0    0 S  0.0  0.0   4:16.09 watchdog/0
     7 root      RT   0     0    0    0 S  0.0  0.0  90:52.10 migration/1
     8 root      RT   0     0    0    0 S  0.0  0.0   0:00.00 stopper/1
     9 root      20   0     0    0    0 S  0.0  0.0   8:30.06 ksoftirqd/1
    10 root      RT   0     0    0    0 S  0.0  0.0   3:42.04 watchdog/1
    11 root      RT   0     0    0    0 S  0.0  0.0  93:12.74 migration/2
~~~ 

The content will refresh itself every few seconds. To get back to the command line, press the `q` key

Here is a description of the different parts:

~~~ {.output}
top - 08:01:08 up 22 days, 16:27,  4 users,  load average: 6.62, 6.96, 7.50
~~~

This first line explains how long the node has been running since the last restart, how many users are logged in, and the load, roughly the average number of CPUs busy during the last one, five, and fifteen minutes. A rule of thumb for keeping a cod node happy is not to submit jobs if it will make  the  15 min load average to surpass 32. It should be sought to avoid to run more than 32 processes at the same time. The cod nodes have 32 two dual cores and do manage to run 64 processes and even to keep further processes in queue but faces then the risk of being inefficient. It is recommended to run only one process per core.

> ## Reference {.callout}
> Further reading is found here: <http://blog.scoutapp.com/articles/2009/07/31/understanding-load-averages>

~~~ {.output}
Tasks: 1997 total,   2 running, 1994 sleeping,   1 stopped,   0 zombie
~~~

The next line lists the number of tasks (or processes) and their state: total, running, sleeping (blocked or waiting for something) stopped or 
[zombie](https://en.wikipedia.org/wiki/Zombie_process).

~~~ {.output}
Cpu(s): 10.9%us,  0.1%sy,  0.0%ni, 89.0%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
~~~

The first number represents the percentage the CPUs are busy for the different user processes. An explanation of the other numbers can be found [here](http://www.unixtutorial.org/commands/top/) (look for 'CPU(s) status').

~~~ {.output}
Mem:  1588217204k total, 1048199928k used, 540017276k free,   310708k buffers
Swap: 10485756k total,   318964k used, 10166792k free, 963947960k cached
~~~

These lines describe memory usage and swap usage. The first line is a but misleading as it also represent virtual memory, which is available to other programs if needed. See the 'tips and tricks' lesson for more details.

Swap memory is define [here](https://www.centos.org/docs/5/html/5.2/Deployment_Guide/s1-swap-what-is.html):

>Swap space in Linux is used when the amount of physical memory (RAM) is full. If the system needs more memory resources and the RAM is full, inactive pages in memory are moved to the swap space. [...] Swap space is located on hard drives, which have a slower access time than physical memory.

The second part of the `top` output shows the most active user processes.

~~~ {.output}
   PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
  8125 hannibal  20   0  907m 214m 186m S 595.9  0.0  14435:09 blastx
 73043 superman  20   0 48.7g  48g 508m R 100.0  3.2   3309:44 samtoh5
 75259 username  20   0 31144 2956 1092 R  1.6  0.0   0:00.21 top
...
...
~~~

Explanation of the different columns:

* `PID` – process ID, a unique number for each process
* `USER` – username for the owner of each process
* `PR` and `NI` – deal with 'priority' in the internal unix queueing system for access to the CPU
* `VIRT`, `RES`, `SHR` – deal with memory usage. `RES` stands for the *resident part* of a process – how much of it resides in the physical memory and this number is most relevant for the actual memory usage of processes. `VIRT` stands for *virtual* size, and 'represents how much memory the program is able to access at the present moment'. `SHR` can be ignore. For more details, see for example [this explanation](http://mugurel.sumanariu.ro/linux/the-difference-among-virt-res-and-shr-in-top-output/)
* `S` – the current state of each process: `R` = running, `S` = sleeping, `D` = uninterruptible sleep, `T` = traced or stopped, `Z` = zombie
* `%CPU` – percentage of the time CPU spends running a particular process. Note that 100% represents one CPU in full use, so the `blastx` process in the example above uses the equivalent of almost 6 CPUs
* `%MEM` – percentage of the physical memory of your system which is used by each process, i.e. the number from the `RES` column as a fraction of the total memory
* `%TIME+` – Total CPU time the task has used since it started. Note that if a process uses more than one CPU the time reported does not represent 'wall clock' time, but CPU time
* `COMMAND` – the command used to initiate each process

So, for the three most active users, we see:

* user `hannibal` runs `blastx` with almost 6 CPUs and very little memory
* user `superman` runs `samtoh5` with one CPU and 48 GB of memory
* user `username` just has started running the `top` command

###`top` tips

After typing `top`, you can use some keys to change what is displayed:

* If you only want to show the processes that belong to you, you can run `top` and type the `u` key followed by your username.
* if you type `shift-f`, you can select a column to sort the output on. Very useful is sorting on the `%MEM` column
* type `c` to show more of the last column, the command used
* 

> ## Making `top` show your processes only {.callout}
>
> use `top -u username` to start top with only showing processes belonging to you. Inside `top`, press `u` and enter to show processes for all users again.

> ## Exercise {.challenge}
>
> Run `top` and check the different users that are on the system. Who do you think user `root` is?

> ## Reference {.callout}
> A good reference for the `top` command is this webpage: <http://www.computerhope.com/unix/top.htm>

###Starting and monitoring a simple job

We are going to use a small script that writes some simple output to the screen, and which allows us to control how long it runs. In an appropriate folder (e.g., your home folder), make a file called `rounds.sh` with the following content - you can use the `nano` editor for this	:

```
rounds=$1
seconds=$2
for i in $(seq 1 $rounds)
	do
	echo round $i of $rounds
	sleep $seconds
done
```
This script will sleep (using the unix `sleep` command) a user-defined amount of times (variable `rounds`) for a user-defined amount of seconds (variable `seconds`).

Now make the script executable:

~~~ {.bash}
chmod u+x rounds.sh
~~~

And try it out:

~~~ {.bash}
./rounds.sh 3 2
~~~

~~~ {.output}
round 1 of 3
round 2 of 3
round 3 of 3
~~~

Here the script ran 3 `sleep` commands, which each took 2 seconds.

> ## Exercise {.challenge}
>
> Run the script a few times using different settings for the number of rounds and seconds. If the process takes very long, cancel it using `ctrl-c`

Our goal is to start the script and then use `top` to monitor it. But, if the script is running, you can't type anything anymore in the terminal until the script is finished. There are several solutions to this problem, and we will go through some of them.

The easiest way is to simply open another terminal window, log into the same node, and start `top -u username` there.

Now, in your first terminal, start the script with 10 rounds of three seconds:

~~~ {.bash}
./rounds.sh 10 3
~~~
~~~ {.output}
round 1 of 10
round 2 of 10
round 3 of 10
round 4 of 10
round 5 of 10
round 6 of 10
round 7 of 10
round 8 of 10
round 9 of 10
round 10 of 10
~~~

and check in the other window what is happening: you should see the `sleep` command appear.

> ## Exercise {.challenge}
>
> Check the `PID` number (in the first column of the `top` output), i.e. the process ID, for the `sleep` command. Why is it changing while the `rounds.sh` script is running?

> ## Exercise {.challenge}
>
> Is the `sleep` command the only new process one appearing in the `top` output when you start the script?

###Using `screen` for long running jobs

If you are starting a long running job you cannot close the terminal window because the job will be cancelled. A solution to this problem is using the so-called unix `screen`. `screen` starts a virtual terminal that can be kept 'alive' while disconnection from the server.

To use `screen`, simply type 

~~~ {.bash}
screen
~~~

You now started a 'new' terminal. Start your job in this new window. After you have started your job you can *detach* from this screen by pressing `ctrl-a-d` (The ctrl key with the `a` key, followed by the `d` key). Now you're back in the terminal where you started. But anything that you started 'inside' the screen will continue!

You can close this terminal or even the computer and the 'new' terminal will still exist and continue to run your job. 

If you want to get 'back into' the now hidden screen type:

~~~ {.bash}
screen -rd
~~~

You can start multiple virtual terminals this way by just repeating the `screen` command. If you have multiple screens running, the `screen -rd` command will give you a list of the windows available:

~~~ {.bash}
 screen -rd
~~~

~~~ {.output}
There are several suitable screens on:
	133548.pts-10.cod5	(Detached)
	119179.pts-47.cod5	(Detached)
Type "screen [-d] -r [pid.]tty.host" to resume one of them.
~~~

To choose one of the screens just add the screen 'name' after the command:

~~~ {.bash}
screen -rd 45142.pts-15.cod5
~~~

Using the first part of the screen 'name' also works, as long as it is unique. Here we would could simply use:

~~~ {.bash}
screen -rd 45142.pts-15.cod5
~~~

When your job is finished you can to close the virtual terminal by reattaching to it and typing `exit`, or `ctrl-d`.

> ## Callout Box {.callout}
>
> you can also name screens using `screen -S somename` and reattach using the same name: `screen -rd somename`. `screen -list` shows all your active screens on the node

> ## Exercise {.challenge}
>
> * in a screen, run this command: `./rounds.sh 10 5`
> * detach using `crtl-a-d`
> * run `top -u username` to check the script is running
> * reattach to the screen to see the output of the job

###Cancelling a job

When you started a long running job in the terminal, you usually can stop it by pressing `ctrl-c`. 

> ## Exercise {.challenge}
>
> * in a screen, run this command: `./rounds.sh 10 5`
> * detach using `crtl-a-d`
> * run `top -u username` to check the script is running
> * reattach to the screen to see the output of the job
> * cancel the job using `ctrl-c`
> * detach using `crtl-a-d`
> * run `top -u username` to check the script is no longer running
> * reattach to the screen 
> * exit the screen using `exit` or `ctrl-d`

###Following output of running jobs

Using `top` will show you the processes that are running, but not necessarily much detail on what they are doing. Many programs will generate output to the screen or write to log files. In this part, you'll learn how to inspect the log files, including how to see new output being added as it happens.

First, let's start a long running process with the `rounds.sh` script inside a screen, but this time we write the output it gives to a file:

~~~ {.bash}
screen
./rounds.sh 1000 1 >rounds.out
~~~

Note how we choose 1000 rounds of 1 second sleeping. Now you can follow the progress by typing 

~~~ {.bash}
cat rounds.out
~~~

~~~ {.output}
round 1 of 1000
round 2 of 1000
round 3 of 1000
round 4 of 1000
round 5 of 1000
round 6 of 1000
round 7 of 1000
~~~

If you do this repeatedly, you'll see where the process is. Alternatively, you can type

```
tail rounds.out
```
~~~ {.output}
round 13 of 1000
round 14 of 1000
round 15 of 1000
round 16 of 1000
round 17 of 1000
round 18 of 1000
round 19 of 1000
round 20 of 1000
round 21 of 1000
round 22 of 1000
~~~
Having to do this repeatedly is cumbersome, so let's ask the `tail` command to help us, by continuing to show the end of the file while new content is being added:

```
tail -f rounds.out
```

You'll now see how the output of is added at the end, just as if you were running the command itself and letting the output go to the screen.

Note how it is safe to cancel the `tail -f` command using `crtl-c`, as this does not stop the actual process (which runs in a `screen`). In fact, if you let the `rounds.sh` script finish, the `tail -f` command still will wait for new input, which in this case never comes. So, you'll have to cancel the `tail -f` to get back to being able to use the terminal.

###Reserving the node

There are a few ground rules on when you need tell the other users you will be using one of the cod nodes. These are explained on the wiki. Use the cod-nodes mailing list (cod-nodes@ibv.uio.no) for this. The subject should reflect the node you want to use. Say a few words on:

* what you are going to run (program name suffices)
* how much CPUs you are going to use
* how much memory you need (this is often an estimate)
* how long you think the job will take

Here is an example message:

>From: firstname.lastname@ibv.uio.no  
>Subject: Cod5 Usage  
>To: cod-nodes@ibv.uio.no  
>
>Running assembly with SPADES using 20 CPUs and around 125 GB of memory. The job will last around 24 hrs.

FIXME add link to wiki where 'rules' for when to send an email to form on use of a cod node.
