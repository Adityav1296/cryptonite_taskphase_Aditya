# The PATH Variable

There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands.

If you blank out the variable, this could happen:
```
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```

Without a PATH, bash cannot find the ls command.

***Commands:***

1) `hacker@path~the-path-variable:~$ ls`  *output: Desktop  f  not-the-flag  the-flag  x.sh*

2) `hacker@path~the-path-variable:~$ rm x.sh`

3) `hacker@path~the-path-variable:~$ ls`  *output: Desktop  f  not-the-flag  the-flag*

4) `hacker@path~the-path-variable:~$ PATH=" "`

5) `hacker@path~the-path-variable:~$ /challenge/run`

6) `hacker@path~the-path-variable:~$ ls`  *output: ssh-entrypoint: ls: command not found*

7) `hacker@path~the-path-variable:~$ rm f`  *output: ssh-entrypoint: rm: command not found*

***Flag:***

>pwn.college{Em-j237lFeXS1vhUmg097NLaQe6.dZzNwUDLygjN0czW}
---

# Setting PATH

We can use the PATH shell variable to add a new directory of programs to our command repertoire. PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path.

Hence to launch a command with it's bare name, we can use 'PATH' to add it's directory to the list.

***Commands:***

1) `hacker@path~setting-path:~$ PATH=/challenge/more_commands/`

2) `hacker@path~setting-path:~$ /challenge/run win`
*output: Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!*

***Flag:***

>pwn.college{8E7-cmiAbCqe6ZZbDGlGoQCXMjU.dVzNyUDLygjN0czW}
---

# 
