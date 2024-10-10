# Redirecting Output 

You can accomplish this with the > character, as so: `hacker@dojo:~$ echo hi > asdf`

This will redirect the output of echo hi (which will be hi) to the file asdf which can be read through the cat command.

***Commands:***

1) `hacker@piping~redirecting-output:~$ touch COLLEGE`

2) `hacker@piping~redirecting-output:~$ echo PWN > COLLEGE`

***Flag:***

>pwn.college{80eofOqut2ofR_7XNw_4eavsldS.dRjN1QDLygjN0czW}
---

# Redirecting More Output

You can redirect the output of any command.

***Commands:***

1) `hacker@piping~redirecting-more-output:~$ cd /challenge`

2) `hacker@piping~redirecting-more-output:/challenge$ ./run` *output: It gave the instructions to solve the program.

3) `hacker@piping~redirecting-more-output:/challenge$ cd ~`

4) `hacker@piping~redirecting-more-output:~$ /challenge/run > myflag`

5) `hacker@piping~redirecting-more-output:~$ cat myflag`

***Flag:***

> pwn.college{Apma4zug9IUZIjES3K2NW2zCOIg.dVjN1QDLygjN0czW}
---

# Appending Output 

A common use-case of output redirection is to save off some command results for later analysis.
Often times, you want to do this in aggregate: run a bunch of commands, save their output, and grep through it later.

We can use the append mode to write the contents in a file and display them all together.

Caution: Make sure to use >> after using > for this first append. '>' will create a new output file every time, deleting the old contents.

***Commands:***

1) `hacker@piping~appending-output:~$ /challenge/run >> the-flag`

2) `hacker@piping~appending-output:~$ cat the-flag`

***Flag:***

>pwn.college{ouGcUaK2Z-CRDtSpmjJhi1o1euY.ddDM5QDLygjN0czW}
---

# Redirecting Errors 

Just like standard output, you can also redirect the error channel of commands.

A File Descriptor (FD) is a number the describes a communication channel in Linux. 

Eg: 1. FD 0: Standard Input

  2) FD 1: Standard Output

  3) FD 2: Standard Error

You can redirect multiple file descriptors at the same time! For example:
`hacker@dojo:~$ some_command > output.log 2> errors.log`

***Commands:***

1) `hacker@piping~redirecting-errors:~$ touch myflag instructions`

2) `hacker@piping~redirecting-errors:~$ cat instructions`

3) `hacker@piping~redirecting-errors:~$ cat myflag`

***Flag:***

> pwn.college{wli1RBlChfOD1bW-HfT9VUIl4jE.ddjN1QDLygjN0czW}
---

# Redirecting Input

Just like you can redirect output from programs, you can redirect input to programs! This is done using <.

***Commands:***

1) `hacker@piping~redirecting-input:~$ touch PWN`

2) `hacker@piping~redirecting-input:~$ echo COLLEGE > PWN`

3) `hacker@piping~redirecting-input:~$ /challenge/run < PWN`

***Flag:***

>pwn.college{IUgR5UGwwOE6cV02gddlvUpjHk0.dBzN1QDLygjN0czW}
---

# Grepping Stored Result

Sometimes when we redirect the output to a different file, we may encounter multiple text lines already stored in that file.
Hence, here we can use the grep command to search for the particular file we require.

***Commands:***

1) `hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt`

2) `hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt`

***Flag:***

>pwn.college{ssQh57KZbmfqzaZ1mus3vkGAkmv.dhTM4QDLygjN0czW}
---

# Grepping Live Output

It turns out that you can "cut out the middleman" and avoid the need to store results to a file.
You can use this using the | (pipe) operator. 
Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. 

***Commands:***

1) `hacker@piping~grepping-live-output:~$ cd /challenge`

2) `hacker@piping~grepping-live-output:/challenge$ ./run | grep pwn.college`

***Flag:***

>pwn.college{4gt43VZtLRu6u00nAaVUX6yYAEA.dlTM4QDLygjN0czW}
---

# Grepping The Error

There is no operator that can be used to pipe an error.
Therefore, the shell has a >& operator, which redirects a file descriptor to another file descriptor.

***Commands:***

1) `hacker@piping~grepping-errors:~$ cd /challenge`

2) `hacker@piping~grepping-errors:/challenge$ 2>& 1`

3) `hacker@piping~grepping-errors:/challenge$ ./run 2>&1 | grep pwn.college`

***Flag:***

>pwn.college{UmIh5guFiKZBfrquUwRcW8XTdsl.dVDM5QDLygjN0czW}

***Problems:***

1) `hacker@piping~grepping-errors:/challenge$ stderr 2>& stdout`

2) ` hacker@piping~grepping-errors:/challenge$ cat stderr | grep pwn.college`

3) `hacker@piping~grepping-errors:/challenge$ ./run stderr | grep pwn.college`

In the above three given commands, I tried accessing the stderr file which does not exist. As a result, the program did not pass me the flag required.
When we change the file descriptor to a different one and want to pipe the answer it's important that we mention the changed FD (here 2>&1) and not the old one.

---

# Duplicating Piped Data With Tee

The tee commandduplicates data flowing through your pipes to any number of files provided on the command line.

***Commands:***

1) `hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee data | /challenge/college`

2) `hacker@piping~duplicating-piped-data-with-tee:~$ cat data` *output:
Usage: /challenge/pwn --secret [SECRET_ARG]
SECRET_ARG should be "U2yeLBob"*

3) `hacker@piping~duplicating-piped-data-with-tee:~$  /challenge/pwn --secret U2yeLBob | /challenge/college`

***Flag:***

>pwn.college{U2yeLBobi2z24KVgYXiQQgzkD78.dFjM5QDLygjN0czW}
---

# Writing To Multiple Programs

***Commands:***

1) `hacker@piping~writing-to-multiple-programs:/challenge$ /challenge/hack | tee >/challenge/the >/challenge/planet`
*output: ssh-entrypoint: /challenge/the: Permission denied*

2) `hacker@piping~writing-to-multiple-programs:/challenge$ /challenge/hack | tee >(/challenge/the ) >(/challenge/planet)`

***Flag:***

>pwn.college{EXT9vQ2hRu0brDlCUojyUM11cmF.dBDO0UDLygjN0czW}
---

# Split Piping Stderr and Stdout

***Commands:***

1) `hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack > >(/challenge/planet) 2>(/challenge/the)`
*output: You must redirect my standard error into '/challenge/the'!*

2) `hacker@piping~split-piping-stderr-and-stdout:~$  /challenge/hack > >(/challenge/planet) 2> >(/challenge/the)`

***Flag:***

>pwn.college{MLrstJaNQJkpQS4_JSoBr03_xtP.dFDNwYDLygjN0czW}
---
  
