---
layout: page
title: Using the CEES HPC resources  
subtitle: Logging in for the first time  
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Log in to the abel computer cluster
> * Locate the most important folders

<!--- referencing other files: [key word 1](reference.html#key-word-1) --->

Let's get started! Open your terminal program and write - replacing `username` with your UiO username:

~~~ {.bash}
ssh username@abel.uio.no
~~~

This should show something like this:

~~~ {.output}
Last login: Wed Sep  9 11:47:54 2015 from bioxxxxx.uio.no

Welcome to Abel, a supercomputing service by UiO/USIT/UAV/ITF

################################################################################

IMPORTANT INFORMATION

Abel login nodes run an automatic nice daemon so that your actions do not
impact other user's interactive work.  Any process consuming more than 30
minutes of CPU time on the login nodes will automatically be killed.

Please note that files stored under the temporary area /work/users/$USER are
deleted if older than 45 days. For more information please see:
http://www.uio.no/english/services/it/research/hpc/abel/help/user-guide/data.html

Help on various apects of using Abel can be found here:
http://www.uio.no/english/services/it/research/hpc/abel/

If you want to receive Abel operational information by e-mail you can subscribe
to the abel-operations e-mail list by following this URL:
https://sympa.uio.no/usit.uio.no/subscribe/abel-operations

################################################################################

[login-0-2 ~]$
~~~

> ## Callout Box {.callout}
>
> If you logged in on the computer you run this command using the same username as on abel, you can skip the username: `ssh abel.uio.no`. If you are on the UiO network, you don't have to write the `uio.no` part. So, you may be able to just write `ssh abel`!

Now let's check who we are, and where we are:

~~~ {.bash}
pwd
~~~
~~~ {.output}
/usit/abel/u1/username
~~~
~~~ {.bash}
whoami
~~~

This should return your username

~~~ {.bash}
hostname
~~~
~~~ {.output}
login-0-1.local
~~~
Here you can have either `login-0-1.local`, or `login-0-2.local`. This indicates there are two physical servers, so-called 'login nodes' and the system assigns one of them to you randomly.

Let's log out:

~~~ {.bash}
exit
~~~

> ## Callout Box {.callout}
>
> You can also type `logout`, or type the ctrl-key together with the `d` key.


> ## Exercise {.challenge}
>
> Log in and out a few times and notice which login server is assigned to you
