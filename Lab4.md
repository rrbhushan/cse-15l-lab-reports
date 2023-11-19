# Lab Report 4

### Step 4

![Image](/lab4images/s4.png)

Keys pressed: ````<up><enter>````

The `ssh cs15lfa23sm@ieng6.ucsd.edu` command was 1 up in my search history while not logged in so I used the up arrow once to access it, followed by pressing enter to run the command. 

***

### Step 5

![Image](/lab4images/s5-1.png)
![Image](/lab4images/s5-2.png)

Keys pressed: ````<control><r>, <g><i><t><space><c><l><enter>````

I used the Ctrl+R to be able to search through my history. Once I entered that history search mode, I typed in `git cl`, which autofilled the rest of the line to show `git clone git@github.com:rrbhushan/lab7.git` (shown by the first screenshot), to which I pressed enter to run the autofilled command in order to clone my fork (shown by the second screenshot). Also for this and later steps, I had ran all the commands in previous trials, which is why I am able to apply the Ctrl+R shortcut on those specific commands.

***

### Step 6

![Image](/lab4images/s6.png)

Keys pressed: ````<c><d><space><l><tab><enter>, <control><r>, <j><a><v><a><c><enter>, <control><r>, <j><a><v><a><space><-><enter>````

I first used `cd l` to be able to go into the cloned repository, pressing tab and enter right after to autofill (autofills to `cd lab7/`) and enter the directory. I then used the Ctrl+R to be able to search through my history to search for `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` by typing `javac` then enter. Once that compiled, I used Ctrl+R again this time searching for `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests` by typing `java -` then enter to run the tests.

***

### Step 7

![Image](/lab4images/s7-1.png)
![Image](/lab4images/s7-2.png)

Keys pressed: ````<v><i><m><space><shift><L><tab><.><tab><enter>, <?><i><enter>, <e>, <r><2>, <:><w><q><enter>````

To change the file in order to fix the bug, I first used `vim L` and tabbed to autofill, which gave me `vim ListExamples`. To complete the autofill, I had to add a "." at the end and then tab again, so the complete filled line was `vim ListExamples.java`, which I then press enter to open (as this is the behavior of vim). After opening the file, I used `?i` to search from the bottom (using `?` which searches in the reverse direction) and started looking for the lastmost entry of `index1`, which it was found just after typing `i`. Then after pressing enter, it sent me to the keyword (`index1`), to which I then press `e` to go to the last character of the keyword, where I then use `r2` to replace `1` with `2` (changes shown in 2nd image). After making those changes, I then use `:wq` to save and exit the file. 

***

### Step 8

![Image](/lab4images/s8-1.png)

Keys pressed: ````<up><up><up><enter>, <up><up><up><enter>````

To run the tests again, I just need to perform the same commands as I did for Step 6. As I used the `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java` 3 commands prior, I just needed to press the up key 3 times and then press enter. For `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`, it was also used 3 commands ago, so I pressed the up key again 3 more times, then pressing enter to rerun the tests (which now pass). 

***

### Step 9

![Image](/lab4images/s9.png)

Keys pressed: ````<g><i><t><space><a><d><d><space><.><enter>, <g><i><t><space><c><o><m><tab><-><m><space><"><f><i><x><e><d><"><enter>, <g><i><t><space><p><u><s><h><enter>````

In order to push the changes, I need to first add all the changes files, which I did by using `git add .` where the "." indicates staging all files in the current directory. After pressing enter on that, I could then commit the staged files through `git commit` by typing `git com`, then tab to autofill, and then adding a message of "fixed" by typing `-m`. Once I entered that, I could then push these changes over to my Github account by typing `git push`, which then makes the changes over on Github after pressing enter once more. 
