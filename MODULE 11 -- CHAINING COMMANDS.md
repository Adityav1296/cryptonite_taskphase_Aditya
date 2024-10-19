# Chaining With Semicolons

The easiest way to chain commands is ;. In most contexts, ; separates commands in a similar way to how Enter separates lines.

Basically, when you hit Enter, your shell executes your typed command and, after that command terminates, give you the prompt to input another command. The semicolon is analogous, just without the prompt and with you entering both commands before anything is executed.

***Command:***

1) `hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college`

***Flag:***

>pwn.college{chJTAp0oACppOeHg9VTDXik4e5K.dVTN4QDLygjN0czW}
---

# Your First Shell Script

For writing multiple commands while also making the program look clean, we can write the commands in a shell script.

By convention, shell scripts are frequently named with a 'sh' suffix. And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.

***Commands:***

1) Created a script file x.sh in vscode to write the two commands in it.
   
2) `hacker@chaining~your-first-shell-script:~$ bash x.sh`

**Flag:***

>pwn.college{suiU9g90rmAk9wrG1Zxj5HHbBTn.dFzN4QDLygjN0czW}
---

# Redirecting Script Output

As far as the shell is concerned, your script is just another command. That means you can redirect its input and output using the piping commands.

All of the various redirection methods work: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.

***Commands:***

1) Created a script file x.sh in vscode to write the two commands in it.

2) `hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve`

***Flag:***

>pwn.college{stqYcyft6FbSmdA4DnAsb0PmGw_.dhTM5QDLygjN0czW}
---

# Executable Shell Scripts

When you invoke bash script.sh, you are, of course launching the bash command with the script.sh argument. This tells bash to read its commands from script.sh instead of standard input, and thus your shell script is executed.

It turns out that you can avoid the need to manually invoke bash. If your shell script file is executable, you can simply invoke it via its relative or absolute path! 

***Commands:***

1) Created a script file x.sh in vscode to write the command in it.

2) `hacker@chaining~executable-shell-scripts:~$ touch x.sh`

3) `hacker@chaining~executable-shell-scripts:~$ ls -l x.sh` *output: -rw-r--r-- 1 hacker hacker   34 Oct 19 05:48 x.sh*

4) `hacker@chaining~executable-shell-scripts:~$ chmod u+x x.sh`

5) `hacker@chaining~executable-shell-scripts:~$ ./x.sh` *output: Congratulations on your shell script execution! Your flag:*

***Flag:***

>pwn.college{kLZFUv3pN9AXUPNyfO0-V9vQXRU.dRzNyUDLygjN0czW}
---
