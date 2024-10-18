In modern computing, this software is split into two categories: operating system kernels and processes.
When Linux starts up, it launches an init (short for initializer) process that, in turn, launches a bunch of other processes which launch more processes until, eventually,
we are looking at the command line shell, which is also a process!
The shell, of course, launches processes in response to the commands we enter.

---

#  Listing Processes

We can use the 'ps' command to list the processes running in the terminal. But this command is not very useful on it's own. Hence, we use the following two methods to make it more useful:

1) Standard" Syntax: in this syntax, you can use -e to list "every" process and -f for a "full format" output, including arguments. These can be combined into a single argument -ef.

2) "BSD" Syntax: in this syntax, you can use a to list processes for all users, x to list processes that aren't running in a terminal, and u for a "user-readable" output. These can be combined into a single argument aux.

These two methods, ps -ef and ps aux result in slightly different, but cross-recognizable output.

There are many commonalities between ps -ef and ps aux: 

1) Both display the user (USER column), the PID, the TTY, the start time of the process (STIME/START), the total utilized CPU time (TIME), and the command (CMD/COMMAND).

2) ps -ef additionally outputs the Parent Process ID (PPID), which is the PID of the process that launched the one in question.

3) ps aux outputs the percentage of total system CPU and Memory that the process is utilizing.

NOTE: Both ps -ef and ps aux truncate the command listing to the width of your terminal.

***Command:***

1) `hacker@processes~listing-processes:~$ ps -ef`

2) `hacker@processes~listing-processes:~$  /challenge/11026-run-14463`


***Flag:***

>pwn.college{U3PBPW_sWD3febm2qSMxHsJnmpP.dhzM4QDLygjN0czW}
---

# Terminating Processes

To terminate processes, Linux uses the aggressively-named kill command. We can use kill to terminate a process by passing the process identifier (the PID from ps) as an argument.

***Commands:***

1) `hacker@processes~killing-processes:~$ ps -ef`

2) `hacker@processes~killing-processes:~$ kill 73`

3) `hacker@processes~killing-processes:~$ ps -ef`

4) `hacker@processes~killing-processes:~$ /challenge/run`

***Flag:***

>pwn.college{kgYLY2D3MY_HSKSMv3pPACFa-3-.dJDN4QDLygjN0czW}
---

# Interrupting Processes

Sometimes we just want to get rid of the process that's clogging up your terminal! Luckily, terminals have a hotkey for this: Ctrl-C (e.g., holding down the Ctrl key and pressing C) sends an "interrupt" to whatever application is waiting on input from the terminal and, typically, this causes the application to cleanly exit.

***Commands:***

1) `hacker@processes~interrupting-processes:~$ /challenge/run`
*output: I could give you the flag... but I won't, until this process exits. Remember,
you can force me to exit with Ctrl-C. Try it now!*

***Flag:***

>pwn.college{Ecloyg1cF2beQbQH_soKq8XXyaL.dNDN4QDLygjN0czW}
---

# Suspending Processes

We can suspend processes to the background with Ctrl-Z. To suspend a process we must first invoke it and then use Ctrl Z.

***Commands:***

1) `hacker@processes~suspending-processes:~$ /challenge/run` 
*output:To pass this level, you need to suspend me and launch me again! You can
background me with Ctrl-Z or, if you're not ready to do that for whatever
reason, just hit Enter and I'll exit!*

2) `ctrl z`

3) `hacker@processes~suspending-processes:~$ /challenge/run`

***Flag:***

>pwn.college{In48AP4btbszUArFyRkRrgr5FXj.dVDN4QDLygjN0czW}
---

# Resuming Processes

To resume processes, your shell provides the fg command, a builtin that takes the suspended process, resumes it, and puts it back in the foreground of your terminal.

***Commands:***

1) `hacker@processes~resuming-processes:~$ /challenge/run`
*output:Let's practice resuming processes! Suspend me with Ctrl-Z, then resume me with
the 'fg' command! Or just press Enter to quit me!*

2) `ctrl z`

3) `hacker@processes~resuming-processes:~$ fg /challenge/run`

***Flag:***

>pwn.college{EWjqWvtH0BcFKd7ibCKvzTdJgzT.dZDN4QDLygjN0czW}
---

# Backgrounding Processes

You can also resume processes in the background with the bg command! This will allow the process to keep running, while giving you your shell back to invoke more commands in the meantime.

The differences between suspended and backgrounded properties are as follows:

```
hacker@dojo:~$ sleep 1337
^Z
[1]+  Stopped                 sleep 1337
hacker@dojo:~$
```

The sleep process is now suspended in the background. We can see this with ps by enabling the stat column output with the -o option:

```
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker       702 Ss   bash
hacker       762 T    sleep 1337
hacker       782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$ 
```
See that T? That means that the process is suspended due to our Ctrl-Z. The S in bash's STAT column means that bash is sleeping while waiting for input. the R in ps's column means that it's actively running, and the + means that it's in the foreground!

Now, if we resume the sleep process in the background using the 'bg' builtin, the 'T' in the STAT column will be replaced by 'S' which shows that the process is no longer suspended.

***Commands:***

1) `hacker@processes~backgrounding-processes:~$ /challenge/run`
*output: I'll only give you the flag if there's already another copy of me running *and
not suspended* in this terminal... Let's check!*

2) `Ctrl z`

3) `hacker@processes~backgrounding-processes:~$ bg /challenge/run`

4) `hacker@processes~backgrounding-processes:~$ /challenge/run`
```
output:
UID          PID STAT CMD
root          82 S    bash /challenge/run
root          92 S    sleep 6h
root         111 S+   bash /challenge/run
root         113 R+   ps -o user=UID,pid,stat,cmd
```
***Flag:***

>pwn.college{Iuu_navUDZU7IsQtZykqBnpF6Ip.ddDN4QDLygjN0czW}
---

# Foregrounding Processes

If a process is running in the background, we can easily foreground it using the 'fg' builtin.

***Commands:***

1) `hacker@processes~foregrounding-processes:~$ /challenge/run`
*output: To pass this level, you need to suspend me, resume the suspended process in the
background, and *then* foreground it without re-suspending it! You can
background me with Ctrl-Z*

2) `Ctrl Z`

3) `hacker@processes~foregrounding-processes:~$ bg /challenge/run`

4) `hacker@processes~foregrounding-processes:~$ fg /challenge/run`

***Flag:***

>pwn.college{I7xCdJ2G8k2cTXM5Ith2A-AF2d0.dhDN4QDLygjN0czW}
---

# Starting Backgrounded Processes

We don't have to suspend processes to background them: we can start the backgrounded right off the bat! It's easy; all we have to do is append a '&' to the command at the end.

```
hacker@dojo:~$ sleep 1337 &
[1] 1771
hacker@dojo:~$ ps -o user,pid,stat,cmd
USER         PID STAT CMD
hacker      1709 Ss   bash
hacker      1771 S    sleep 1337
hacker      1782 R+   ps -o user,pid,stat,cmd
hacker@dojo:~$
```

***Commands:***

1) `hacker@processes~starting-backgrounded-processes:~$ /challenge/run &`

***Flag:***

>pwn.college{E0hcPM7iUVNh1jokWCsClixS81y.dlDN4QDLygjN0czW}
---

# Process Exit Codes

Every shell command, including every program and every builtin, exits with an exit code when it finishes running and terminates. This can be used by the shell, or the user of the shell to check if the process succeeded in its functionality.

You can access the exit code of the most recently-terminated command using the special ? variable (don't forget to prepend it with $ to read its value).
Commands that succeed typically return 0 and commands that fail typically return a non-zero value, most commonly 1 but sometimes an error code that identifies a specific failure mode.

***Commands:***

1) `hacker@processes~process-exit-codes:~$ /challenge/get-code`
*output:Exiting with an error code!*

2) `hacker@processes~process-exit-codes:~$ echo $?` *output:66*

3) `hacker@processes~process-exit-codes:~$ /challenge/submit-code 66`

***Flag:***

>pwn.college{wA4bLlFVcn24XKgqob-3BtacFYi.dljN4UDLygjN0czW}
---
