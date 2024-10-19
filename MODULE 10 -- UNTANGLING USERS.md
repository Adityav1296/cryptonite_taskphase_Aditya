There are many users on a typical Linux system.  The full list of users on a Linux system is specified in the /etc/passwd file.

`hacker:x:1000:1000::/home/hacker:/bin/bash`

The line contains, separated by :s, the username, an x as a placeholder for where the password used to be (we'll cover where it actually is later), the numerical user ID, the numerical default group ID, long-form user details, the home directory, and the default shell.

---

# Becoming Root With su

 There are two utilities used for becoming the root user : su and sudo.

 su : It is an older utility and now it is not typically used to elevate to root access anymore.
 Because it has the SUID bit set, su runs as root. su is a setuid binary:
```
hacker@dojo:~$ ls -l /usr/bin/su
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/su
hacker@dojo:~$
```

Before allowing the user to elevate privileges to root, 'su' checks to make sure that the user knows the root password.
But this does not work well with the modern systems as modern systems very rarely have root passwords.

***Commands:***

1) `hacker@users~becoming-root-with-su:~$ ls -l`

2) `hacker@users~becoming-root-with-su:~$ su`  *output: Password:*

3) ` root@users~becoming-root-with-su:/home/hacker# cat /flag`

***Flag:***

>pwn.college{8NcjZp5LQANfThtVGLZhWOr_vay.dVTN0UDLygjN0czW}
---

# Other Users With su

With no arguments, su will start a root shell (after authenticating with root's password). 
However, we can also give a username as an argument to switch to that user instead of root.

***Commands:***

1) `hacker@users~other-users-with-su:~$ su zardus`*output: Password:* 

2) `zardus@users~other-users-with-su:/home/hacker$ /challenge/run`

***Flag:***

>pwn.college{YmYbzsbT7xalh4N1E38U3E0Yqqn.dZTN0UDLygjN0czW}
---

# Cracking Passwords

When we enter a password for su, it compares it against the stored password for that user. 
These passwords used to be stored in /etc/passwd, but because /etc/passwd is a globally-readable file, this is not good for passwords, these were moved to /etc/shadow.

Eg:
```
sshd:*:19901:0:99999:7:::
hacker::19916:0:99999:7:::
zardus:$6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1.:19921:0:99999:7:::
```

Separated by :s, the first field of each line is the username and the second is the password. A value of * or ! functionally means that password login for the account is disabled, 
a blank field means that there is no password and the long string such as Zardus' $6$bEFkpM0w/6J0n979$47ksu/JE5QK6hSeB7mmuvJyY05wVypMhMMnEPTIddNUb5R9KXgNTYRTm75VOu1oRLGLbAql3ylkVa5ExuPov1. is the result of one-way-encrypting.
When we input a password into su, it one-way-encrypts (hashes) it and compares the result against the stored value. If the result matches, su grants us access to the user!

If we have the hashed value of the password, we can crack it! 
The cracking can be done via the famous John the Ripper, as so:
```
hacker@dojo:~$ john ./my-leaked-shadow-file
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Will run 32 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password1337      (zardus)
1g 0:00:00:22 3/3 0.04528g/s 10509p/s 10509c/s 10509C/s lykys..lank
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

***Commands:***

1) `hacker@users~cracking-passwords:~$ cat /challenge/shadow-leak`

2) `hacker@users~cracking-passwords:~$ john /challenge/shadow-leak`

3) `hacker@users~cracking-passwords:~$ john --show /challenge/shadow-leak`
*output: hacker:NO PASSWORD:20000:0:99999:7:::
zardus:aardvark:20015:0:99999:7:::
2 password hashes cracked, 0 left*

4) `hacker@users~cracking-passwords:~$ su zardus`

5) `zardus@users~cracking-passwords:/home/hacker$ /challenge/run`

***Flag:***

>pwn.college{gVGpCjQkBNMWkS0iM7T84tzyT_a.ddTN0UDLygjN0czW}

***Observations:***

1) We can not echo the entire encrypted password of the zardus user into a file of our choice and then use 'john' to decrypt the password.

2) A file name has to given after the '--show' special argument.

---

# Using Sudo

Since while using 'su', we require a root password which don't lend themselves well to larger environments, in the recent times 
the world has moved from administration via su to administration via sudo (superuser do).
Unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root:

Also unlike su, rather than authenticating via password, sudo relies on policies that it checks to determine the user's authorization run things as root. These policies are defined in /etc/sudoers.

***Commands:***

1) `hacker@users~using-sudo:~$ cat /flag` *output: cat: /flag: Permission denied*
   
2) `hacker@users~using-sudo:~$ sudo cat /flag`

***FLag:***

>pwn.college{YRvubegD2nCk9YlqIRiZOI1ZMYM.dhTN0UDLygjN0czW}
---
