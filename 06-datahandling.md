
---
layout: page
title: Software use  
subtitle: Copying, moving and getting data  
minutes: 10
---
> ## Learning Objectives {.objectives}
>
> * Copying files between servers and network discs
> * Accessing files on your PC
> * Moving files
> * Downloading large files from the internet
> * Compressing files

* `cp`, `mv` versus `rsync`
* `wget` `curl`
* `sshfs`
* `gzip`, `tar`, `pbzip2`


Log into abel and `cd` into the folder **151102\_cees-hpc_LLT/**. Make a directory called **temp** and enter the folder.

```
mkdir temp
```

In **temp**, create a file called _data.txt_ using `nano` and write some random text.

```
nano data.txt
```

To quit nano do ```ctrl + x```, choose "Yes" (```y```) and press enter.


###Moving/renaming files using 'mv'

`mv` is used to move or rename files. The first parameter given ```mv``` points to the file of interest. The second parameter points to where the file is going and what it should be named. If no name is given the file keeps it current name.

Move _data.txt_ from **temp** to the **velvet** folder.

```
mv data.txt ../velvet/
```

Check if the file is located in the velvet folder 

```
ls ../velvet/
```

Now, move the file back, renaming it to *results.txt*.

```
mv ../velvet/data.txt results.txt
```


```..``` points to one step up from your current directory.

NB! ```mv``` will overwrite a file with the same name (without warning). If ```mv -i``` is used, the user is asked for confirmation.


###Copying files using 'cp'

First, make a new file called data.txt, using nano like before.

Try to make a copy of the file using ```cp```, renaming the copy in the process.

```
cp data.txt copy1.txt
```

If you do not rename, you will get this error:

```
cp: `data.txt and `data.txt' are the same file
```

Repeat the process to get three copies of *data.txt* (*copy1.txt*, *copy2.txt* etc.)

Now, make a folder called **junk** inside the **temp** folder and copy all the copies except the original to the copies folder.

```
cp copy1.txt copy2.txt copy3.txt junk/
```

```cp``` can take thousands of files as input, but the last parameter given will be the path of the copies.

 All the copies are still in the **temp** folder, so we should probably have used the ```mv``` command instead of ```cp```.

Move all the copies into the junk/ folder, using the -i command.

```
mv -i copy* junk
```
```
mv: overwrite `junk/copy1.txt'?
```
Press ```y``` and ```enter``` to overwrite the files.


###Copying files using 'rsync'

`rsync`is another way you may copy files from their source to a new destination. Unlike `cp`and `mv`, the `rsync` command allows you to copy files from abel or from the cod nodes to your local drive and vice versa.

The syntax is basically

```
rsync source destination
```

Copy the content of the **temp** folder to your local drive (open a new terminal window and do ```pwd``` to see where you are).

```
rsync username@abel.uio.no:/151102_cees-hpc_LLT/temp/* .
```
Did you get all the files? Since there is a folder inside the **temp** folder, ```rsync -r``` need to be used. The '-r' stands for recursive. Repeat the command with the -r option.

Try to copy the **junk** folder back to abel and follow the progress.

```
rsync -r --progress junk/ username@abel.uio.no:/151102_cees-hpc_LLT/temp/
```



