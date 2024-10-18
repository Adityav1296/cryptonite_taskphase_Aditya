The Linux command line interface can be used to write actual programs. The command line is usually known as "shell"
while the programs written in this language are known as "shell scripts".
Variables are the names that may hold the directories or some useful information.
Spaces have special significance in the shell, and there are places where you can't use them spuriously.

---

# Printing Variables

Echo is the command that is used to print the arguments given to it. 
You can also print out variables with echo, by prepending the variable name with a $.
The $ is only prepended to access variables.
In shell terms, this prepending of $ triggers what is called variable expansion.

***Commands:***

1) `hacker@variables~printing-variables:~$ cd /challenge`

2) `hacker@variables~printing-variables:/challenge$ echo $FLAG`

***Flag:***

>pwn.college{AEKr6od7R9mt10CRR_IEGw5miq4.ddTN1QDLygjN0czW}
---

# Setting Variables

We can write valus to the variables using '='. Note that there are no spaces around the =! If you put spaces the shell won't recognize a variable assignment.

***Commad:***

1) `hacker@variables~setting-variables:~$ PWN=COLLEGE`

***Flag:***

>pwn.college{YRbaQYl50Jpw0VNSURBGL4ByDCz.dlTN1QDLygjN0czW}
---

# Multi-Word Variables

When the shell sees a space, it ends the variable assignment and interprets the next word as a command.
For multi-word variables, we need to quote them in "".

***Commands:***

1) `hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"`

***Flag:***

>pwn.college{gcKeMYJcW9gwH5FRtj97tOZLn3g.dBjN1QDLygjN0czW}
---

# Exporting Variables

By default, variables that you set in a shell session are local to that shell process. That is, other commands you run in a different shell won't inherit them.
We can explicitly export the variables using the 'export' command.
When you export your variables, they are passed into the environment variables of child processes. 

***Commands:***

1) `hacker@variables~exporting-variables:~$ COLLEGE=PWN` *output: You've set the COLLEGE variable to the proper value!*

2) `hacker@variables~exporting-variables:~$ export PWN=COLLEGE`  *output:You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!*

3) `hacker@variables~exporting-variables:~$ /challenge/run`

***Flag:***

>pwn.college{Qz7C-LLAd6D9yFgaSBmYL2_K8zU.dJjN1QDLygjN0czW}
---

# Printing Exported Variables

There are multiple ways to access variables in bash. Eg: echo, env, etc.

The env command can be used to print out every exported variable set in the shell.

***Command:***

1) `hacker@variables~printing-exported-variables:~$ env`

***Flag:***

>pwn.college{U8VhYxjUbqa8pr-iOmADpxcPLfr.dhTN1QDLygjN0czW}
---

# Storing Command Output

Command Substitution : If we want to store the outputs of a command into a variable, we use command substitution.

Eg: ```hacker@dojo:~$ FLAG=$(cat /flag) -->
hacker@dojo:~$ echo "$FLAG"  -->
pwn.college{blahblahblah}```

***Commands:***

1) `hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)`

2) `hacker@variables~storing-command-output:~$ echo $PWN`

***Flag:***

>pwn.college{42MbLQhmpxLpP5CY7uteF2KTosy.dVzN0UDLygjN0czW}

***Observation:***

1) We can not cat a variable as it is not a file or directory.
---

# Reading Input

To read the input, we can use the 'read' builtin, which reads input.
We can use -p argument, which lets us specify a prompt.
(NOTE: -p is necessary if we want to specify a prompt like 'INPUT' as done in the below commands.)

***Commands:***

1) `hacker@variables~reading-input:~$ read -p  "INPUT:" PWN`   *output: INPUT:COLLEGE*

***Flag:***

>pwn.college{8M90dKY50brd1ObrAZaBe1L_CHT.dhzN1QDLygjN0czW}
---

# Reading Files

We can use the 'read' builtin along with input and output redirection (<,>) to read the contents of a file into a variable.

***Command:***

 1) `hacker@variables~reading-files:~$ read PWN < /challenge/read_me`

***Flag:***

>pwn.college{wXvRzcWF5raXWGaHa4ughOW8KrC.dBjM4QDLygjN0czW}
---
