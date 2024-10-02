# THE ROOT

The filesystem starts at '/'. You can invoke a program by providing its path on the command line. This style of path, one that starts with the root directory, is referred to as an "absolute path".

***Command:***

`hacker@paths~the-root:~$ /pwn`

***Flag:***

>pwn.college{gwYTXFirh6NVsvwocG3j5is4eEp.dhzN5QDLygjN0czW}
___________________________________________________________

# PROGRAM AND ABSOULTE PATHS

 The path to any directory is thus, /(directoryname). The path to a challenge inside a directory is /(directoryname)/(challengename). 

 ***Command:***

1) `hacker@paths~program-and-absolute-paths:~$ /challenge`   *output:  ssh-entrypoint: /challenge: Is a directory*

2) `hacker@paths~program-and-absolute-paths:~$ /challenge/run`   *output:Correct!!!/challenge/run is an absolute path! Here is your flag:*

***Flag:***

>pwn.college{wRZ7scgbEd04iaXvhkt1mxWt4eb.dVDN1QDLygjN0czW}
______________________________________________________________

# POSITION THY SELF

You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument. Now you can see what the ~ was in the prompt! It shows the current that your shell is located at.

***Command:***

1)`hacker@paths~position-thy-self:~$ cd /usr/bin`

2)`hacker@paths~position-thy-self:/usr/bin$ /challenge/run`  *output:Correct!!!/challenge/run is an absolute path, invoked from the right directory!Here is your flag*

***Flag:***

>pwn.college{02PuCN54GP6Nsr38VA2PNiyQ88J.dZDN1QDLygjN0czW}
________________________________________________________________

# POSITION ELSEWHERE

***Command:***

1)`hacker@paths~position-elsewhere:~$ cd /usr/include`

2)`hacker@paths~position-elsewhere:/usr/include$ /challenge/run`

***Flag:***

>pwn.college{AubZPnK7xom9_aOhNLL7tvKL9vI.ddDN1QDLygjN0czW}
___________________________________________________________

# POSITION YET ELSEWHERE

***Command:***

1)`hacker@paths~position-yet-elsewhere:~$ cd /usr/share/build-essential`

2)`hacker@paths~position-yet-elsewhere:/usr/share/build-essential$ /challenge/run`

***Flag:***

>pwn.college{wfiCufvGX0d2GCBHfqflAmUQhJU.dhDN1QDLygjN0czW}
_______________________________________________________________

# IMPLICIT RELATIVE PATHS FROM '/'

A relative path is any path that does not start at root (i.e., it does not start with /). 
Your cwd is the directory that your prompt is currently located at.

Imagine we want to access some file located at /tmp/a/b/my_file.

If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
If my cwd is /tmp, then a relative path to the file is a/b/my_file.

***Command:***

1)`hacker@paths~implicit-relative-paths-from-:~$ cd /`

2)`hacker@paths~implicit-relative-paths-from-:/$ challenge/run` 

***Flag:***

>pwn.college{o9Eby5PtSXj0aAOh07y3Qt4MuDd.dlDN1QDLygjN0czW}

***Problem:***

1)hacker@paths~implicit-relative-paths-from-:/$ cd c

ssh-entrypoint: cd: c: No such file or directory

2)hacker@paths~implicit-relative-paths-from-:/$ /challenge/run

Incorrect...You invoked this challenge with an absolute path. This challenge needs a relative path!
___________________________________________________________________________________________________________

# EXPLICIT RELATIVE PATHS FROM '/'

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory

***Command:***

1)`hacker@paths~explicit-relative-paths-from-:~$ cd /`

2)`hacker@paths~explicit-relative-paths-from-:/$ ./challenge`  *output: ssh-entrypoint: ./challenge: Is a directory*

3)`hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run`

***Flag:***

>pwn.college{AXdMDHxYj7gZodGEdUiPJInfWK_.dBTN1QDLygjN0czW}

***Problems:***

1)`hacker@paths~explicit-relative-paths-from-:~$ ./challenge/run`
*output: ssh-entrypoint: ./challenge/run: No such file or directory*

2)`hacker@paths~explicit-relative-paths-from-:~$ ./challenge`
*output: ssh-entrypoint: ./challenge: No such file or directory*

3)`hacker@paths~explicit-relative-paths-from-:~$ /.challenge`
*output: ssh-entrypoint: /.challenge: No such file or directory*

***Solution:***

Follow correct format to use '.' for relative paths.
_________________________________________________________

# IMPLICIT RELATIVE PATH

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. This is actually a safety measure.

***Command:***

1)`hacker@paths~implicit-relative-path:~$ cd /challenge`

2)`hacker@paths~implicit-relative-path:/challenge$ ./run`   *output: Correct!!! ./run is a relative path, invoked from the right directory!*

***Flag:***

>pwn.college{Eoow8R418nc9XiyBy6NFM7ZURK_.dFTN1QDLygjN0czW}
_____________________________________________________________

# HOME SWEET HOME

Every user has a home directory, typically under /home in the filesystem. The ~ in this prompt is the current working directory, with ~ being shorthand for /home/hacker. 

Note that the expansion of ~ is an absolute path, and only the leading ~ is expanded. This means, for example, that ~/~ will be expanded to /home/hacker/~ rather than /home/hacker/home/hacker.

***Command:***

1)`hacker@paths~home-sweet-home:~$ /challenge/run ~/f` *output: Writing the file to /home/hacker/f! ... and reading it back to you:*

***Flag:***

>pwn.college{MilrmyDBSIEimk5Qges34x51O-o.dNzM4QDLygjN0czW}

***Problem:***

1)`hacker@paths~home-sweet-home:~$ /challenge/run ~`   *output: Writing the file to /home/hacker! /challenge/run: line 29: /home/hacker: Is a directory 
... and reading it back to you:
cat: /home/hacker: Is a directory*

***Solution:***

Instead of writing just the '~' character after /challenge/run, use '~/' or '~/f'.
_______________________________________________________________________________________
