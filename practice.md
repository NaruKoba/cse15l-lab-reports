# Practice


## The command with no arguments

![Image](noarg.png)

For the first command: cd, my working directory was ~/lecture1/messages, messages directory. Cd command changes a working directory to the directory given as an argument to the cd command. I didn't put any argument for cd command, so no argument behaved like home directory and my working directory was changed to home directory. The output indicates this is not an error. 

For the second command: ls, my working directory  was ~, home directory. ls command lists all of the files and directories inside the directory I refer to as an argument. Since I didn't put any argument for ls command, the command refers to the working directory, home directory in this case. Therefore it showed lecuture1 directory inside the home directory. The output indicates this is not an error.

For the third command: cat, my working directory was ~, home directory. Cat command prints the contents of a file or files, and concatenates the contents if multiple files are provided as arguments to cat command. Since I don't put any argument, it waits for an input from standard input, and prints input if I write words in next line. I simply typed ^C to exit from the command without typing any words before ^C. In the following example, I typed "hello world" before I exited and it returned the same message in the next line. The output indicates this is not an error. 

![Image](noarga3.png)


## the command with a path to a directory as an argument

![Image](directoryex.png)

For the first command: cd, my working directory was ~, home directory. Cd command changes a working directory to the directory given as an argument to the cd command. I put a path to the subdirectory of home directory by using the relative path ./lecture1. Therefore, my working directory changed to lecture1 directory. The output indicates this is not an error.  

For the second command: ls,  my working directory  was ~/lecuture1, lecuture1 directory. ls command lists all of the files and directories inside the directory I refer to as an argument. In this case, I typed the relative path to messages directory as argument: ./ messages, and it showed all of the files and directories inside the messages directories. The output indicates this is not an error.  

For the third command: cat, my working directory was ~/lecture1, lecuture1 directory.  Cat command prints the contents of a file or files, and concatenates the contents if multiple files are provided as arguments to cat command. Since I typed the relative path to directory not the path to the file, it outputted error message saying "./messages is directory". The output indicates this is an error.   

![Image](fileex.png)




if cd has no arguments, space refer to homedirectory similar to ~.
