# Lab Report 1
Command `cd` example: No arguments

![Image](/lab1images/l1cd1.png)

The working directory upon using this command was `/home/lecture1`. After running the `cd` command with no arguments, it sent us back to the parent directory, being `/home`, which is intended and not an error as no arguments will always send us back to the home directory, no matter where the working directory is. 

***

Command `cd` example: Directory argument

![Image](/lab1images/l1cd2.png)

The working directory upon using this command was `/home/lecture1`. After running the `cd` command with a directory `messages/` as an argument, it sent us to the new directory, being `/home/lecture1/messages`, which is intended as typing a child directory from a parent directory always sends us to the child directory. 

***

Command `cd` example: File argument

![Image](/lab1images/l1cd3.png)

The working directory upon using this command was `/home/lecture1/messages`. After running the `cd` command with a file as the argument, it gave us a bash error. The reason for this error is due to the argument not being a directory, but a file. The `cd` command standing for "change directory" will only change between directories, not files which is why this produced an error.

***

Command `ls` example: No arguments

![Image](/lab1images/l1ls1.png)

The working directory upon using this command was `/home/lecture1`. After running the `ls` command with no arguments, it printed all the files and directories present in the current directory, which is intended. Further, `messages` is highlighted as it is another directory, differentiating it from a typical file.

***

Command `ls` example: Directory argument

![Image](/lab1images/l1ls2.png)

The working directory upon using this command was `/home/lecture1`. After running the `ls` command with a directory `messages/` as an argument, it listed all the files present within the directory `/home/lecture1/messages`, showing all the .txt files present. This is intended behavior as another property of the `ls` command is when you provide a directory as an argument, it will list all the contents within that directory.

***

Command `ls` example: File argument

![Image](/lab1images/l1ls3-1.png)

The working directory upon using this command was `/home/lecture1/messages`. After running the `ls` command with a file as the argument, it just lists the file name. This is the case because `ls` only lists contents within a directory and since this argument is a file and not a directory, it will just default to printing the name of the file, as the file isn't a directory. Further, if we try using a different filepath as the argument, the output will be the filename of the other specified filepath for the same reason.

***

Command `cat` example: No arguments

![Image](/lab1images/l1cat1-2.png)

The working directory upon using this command was `/home/lecture1`. After running the `cat` command with no arguments, it will cause the terminal to go in this state, where typing something and pressing enter will cause it to echo the typed message back. In order to escape this state I used Control+D, but this is intended as `cat` will wait until the end-of-file operator is received, which is done by entering Control+D. Until then, it will repeat anything I type after pressing enter. 

***

Command `cat` example: Directory argument

![Image](/lab1images/l1cat2.png)

The working directory upon using this command was `/home/lecture1`. After running the `cat` command with a directory `messages/` as an argument, the terminal prints out that the provided argument is a directory, so this is an error message. The reason for this is due to the `cat` command being designated towards files and not directories, so it will not deal with directories.

***

Command `cat` example: File argument

![Image](/lab1images/l1cat3.png)

The working directory upon using this command was `/home/lecture1/messages`. After running the `cat` command with a file as the argument, it displays the contents of that file. This is intended behavior as the `cat` command is used to view the contents of a preexisting file when the only argument is a filename. Since the file exists, it will print out the contents of that existing file, otherwise it would have said it does not exist.

