# Lab Report 1
Command `cd` example: No arguments

![Image](/lab1images/l1cd1.png)

The working directory upon using this command was `/home/lecture1`. After running the `cd` command with no arguments, it sent us back to the parent directory, being `/home`, which is intended and not an error as no arguments will always send us back to the home directory, no matter where the working directory is. 

***

Command `cd` example: Directory argument

![Image](/lab1images/l1cd2.png)

The working directory upon using this command was `/home/lecture1`. After running the `cd` command with a directory `messages` as an argument, it sent us to the new directory, being `/home/lecture1/messages`, which is intended as typing a child directory from a parent directory always sends us to the child directory. 

***

Command `cd` example: File argument

![Image](/lab1images/l1cd3.png)

The working directory upon using this command was `/home/lecture1/messages`. After running the `cd` command with a file as the argument, it gave us a bash error. The reason for this error is due to the argument not being a directory, but a file. The `cd` command standing for "change directory" will only change between directories, not files which is why this produced an error.

***
