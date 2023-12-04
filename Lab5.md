# Lab Report 5
## Part 1

![Image](/lab5images/l5symp.png)

Student: I was working on an autograde bash script from lab 6, however I keep running into a weird situation where I get the message posted above whenever I run the command `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-compile-error`. I'm not sure why I'm getting this output as I made sure to copy over the `lib` files with `-r`, and still I run into the situation where I cannot progress further. Could I get some help here?

TA: Have you tried providing the absolute path to the files? If that does not help, see if you made sure to copy the `lib` directory rather than just the files.

![Image](/lab5images/l5symp2.png)

Student: Thank you for your help, it turns out the bug was not copying the lib directory over; I was just copying its contents instead. With that said, I've run into a new error where it gives me a "Compilation successful" message when the provided directory is intended to run into a compilation error. 

TA: You may want to revisit how you check whether you have a compilation error or not. For example, what exit code should you be checking for?

![Image](/lab5images/l5sol.png)

Student: That helped! I forgot I should be checking for 0, which indicates success, and instead I had it checking for code 1, which indicates failure. Now my bash script runs perfectly fine!

### Information relevant for setup:
#### File & Directory Structure:



#### Contents of Files before fixing the bug:



#### Command to trigger bug:



#### Fixes:



***

## Part 2
One very interesting thing I found out about was pertaining Github. I was introduced to Github and how to push/pull from it in one of my prior classes, however I never learned how to connect it to VS Code, which in turn made things a lot more difficult to work with and further having a fear towards it. So with finding out about Github desktop, it became a lot more easier to deal with Git and Github, making things much more organized than previously from directly using the terminal.
