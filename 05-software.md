---
layout: page
title: Software use  
subtitle: Software use  
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Use of the module system
> * Use of Abel-wide and local modules
> * Local scripts and other programs
> * Adding folders to your $PATH
> * Using your own scripts/programs

## Software availability  

## Software installed on abel  

A large number of programs is already installed on abel, and can also be used when logged in to the cod nodes. These programs have been installed and are maintained by people at USIT and are available for all users of abel (not just CEES). This software is available through the `module` system, which is explained in more detail in this manual. If you're logged in to abel or the cod nodes, type module avail and you'll see a list of all the available programs (it will take a few seconds until the list is loaded).

### Software installed by CEES users  

As USIT people are too busy to answer every request for software installation on abel, an increasing amount of software has been installed by CEES users. This software lives in `/projects/cees/bin`, and in order to keep things organized, we also follow the `module` system. If you have properly set up your environment (see FIXME), this type of software also shows up in the list that you see when typing 

```
module avail
```
You'll see it at the top of the list, under the heading 

FIXME

'--- /projects/cees/bin/modules ---', while the modules maintained by USIT appear below, under heading '--- /cluster/etc/modulefiles ---'. 

Some software in `/projects/cees/bin` is not yet accessible through modules, but only because we haven't gotten around to that yet. If you need to use software that's installed in `/projects/cees/bin`, but has no module associated with it, please contact FIXME (cees-hpc-core?), and we'll prepare one.


### Software not installed yet  

If you need to use software that's not installed on abel and the cod nodes yet, there are two ways to make it available. If you're not the only one who needs this software and it is likely to be used by many researchers, it might be worth asking people at USIT whether they could install it for you. To do so, send an email to hpc-drift@usit.uio.no with a polite request, and they'll see what they can do. If you seem to be the only one interested in this software, or if USIT people are too busy to care, you can install the program yourself, in `/projects/cees/bin/`, and with the corresponding module. To do so, please see the instructions given here.

FIXME add link

