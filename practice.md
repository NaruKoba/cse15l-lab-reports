# Practice


## The command with no arguments


![Image](noarg.png)

For the first line of the command cd, my working directory was ~/lecture1/messages, messages directory. I didn't put any argument for cd command, so no argument behaved like home directory and my working directory was changed to home directory. The output indicates this is not an error. 

For the second line of the command: ls, my working directory  was ~, home directory. ls command lists all of the files and directories inside the directory I refer to, home directory in this case. Therefore it showed lecuture1 directory inside the home directory. The output indicates this is not an error.

For the third line of the command: cat, my working directory was ~, home directory. Cat command prints the contents of a file or files, and concatenates the contents if multiple files are provided as arguments to cat command. Since I don't put any argument, it waits for an input from standard input, and prints input if I write words in next line. I simply typed ^C to exit from the command without typing any words before ^C. In the following example, I typed "hello world" before I exited and it returned the same message in the next line. The output indicates this is not an error.

![Image](directoryex.png)


![Image](fileex.png)




if cd has no arguments, space refer to homedirectory similar to ~.
