---
layout: page
title: Using the CEES HPC resources
subtitle: Accessing and using the cod nodes
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Log in to the cod nodes, check who is running jobs on it and how busy the node is
> * Reserve the node for use
> * Run a simple job on the node and follow its progress
> * Start long-running jobs
> * Follow progress of jobs and cancel them


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

> ## Callout Box {.callout}
>
> If you logged in on the computer you run this command using the same username as on abel, you can skip the username: `ssh cod5.hpc.uio.no`. While for abel, you can skip the uio.no part when you are on the UiO network, unfortunately, with the cod nodes, you will always have to write the `hpc.uio.no` part. 

We are going to use a small script that writes some simple output to the screen, and allows us to control how long it runs. In an appropriate folder (e.g., your home folder), make a file called `rounds.sh` with the following text:

```
stop=$1
seconds=$2
for i in $(seq 1 $stop)
	do
	echo round $i of $stop
	sleep $seconds
done
```
This script will sleep (unix `sleep` command) a user-defined amount of times (variable `stop`) for a user-defined amount of seconds (variable `seconds`).

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
> Run the script a few times using different settings for the number of rounds and seconds. If the script takes very long, cancel it using `ctrl-c`
