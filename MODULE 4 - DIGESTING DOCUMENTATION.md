# Learning From Documentation

The typical need you'll have for documentation is just to figure out how to use all the programs, and a specific case of that is figuring out what arguments to specify on the command line.
The correct usage of programs depends, in a large part, in the proper specification of arguments to them.

***Commands:***

1) `hacker@man~learning-from-documentation:~$ cd /challenge`

2) `hacker@man~learning-from-documentation:/challenge$ ./challenge`
*output: Incorrect usage! You must pass an argument to me (read the challenge
description for details).*

3) `hacker@man~learning-from-documentation:/challenge$ ls -a`
*output: .  ..  .init  DESCRIPTION.md  challenge*

4) `hacker@man~learning-from-documentation:/challenge$ ./challenge --giveflag`
*output: Correct argument! Here is your flag:*

***Flag:***
>pwn.college{UENIZmjl2wg-yuZYu4AcgSFU3it.dRjM5QDLygjN0czW}
---

# Learning Complex Usage

While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk are entire programs in an esoteric programming language!

Some programs may take arguments for their arguments as well. Eg: find -name.

***Commands:***

1) `hacker@man~learning-complex-usage:~$ cd /challenge`

2) `hacker@man~learning-complex-usage:/challenge$ ls -a`
*output: .  ..  .init  DESCRIPTION.md  challenge*

3) `hacker@man~learning-complex-usage:/challenge$ cd /`

4) `hacker@man~learning-complex-usage:/$ ls -a`

5) `hacker@man~learning-complex-usage:/$ /challenge/challenge --printfile /flag`
*output: Correct argument! Here is the /flag file:*

***Flag:***

>pwn.college{EYuGuo8ruEgvxHwYBCA5ljVQk3V.dVjM5QDLygjN0czW}

***Observations:***

Sometimes we might not be able to find the required paths in the current directory. The best option at such times is to go to the root directory and find the flag path there by using 'ls'.

1) `hacker@man~learning-complex-usage:/challenge$ ./challenge --printfile /challenge/challenge`

In the above command, I was able to open the file as it is a readable file. But since it was not the correct path for the flag, I wasn't able to get the flag through this command.

---

# Reading Manuals

'man' is short for manual, and will display (if available) the manual of the command you pass as an argument. Whedone reading the manpage, you can hit q to quit.The arguments to the man command aren't file paths, but just the names of the entries themselves

The database for the man command is found in /usr/share/man directory, but you never need to interact with it directly: you just query it using the man command.

***Commads:***

1) `hacker@man~reading-manuals:~$ cd /`

2) `hacker@man~reading-manuals:/$ man challenge`

3) `hacker@man~reading-manuals:/$ /challenge/challenge --obbahy 628`

***Flags:***

> pwn.college{obVbBPa6hQyssBv2m8yvHR2BLBZ.dRTM4QDLygjN0czW}
---

# Searching Manuals

You can scroll man pages with the arrow keys (and PgUp/PgDn) and search with /. After searching, you can hit n to go to the next result and N to go to the previous result. Instead of /, you can use ? to search backwards!

***Commands:***

1) `hacker@man~searching-manuals:~$ cd /`

2) `hacker@man~searching-manuals:/$ man challenge`

3) `hacker@man~searching-manuals:/$ /challenge/challenge  --sfimm`

***Flag:***

> pwn.college{02N-3u7HD8Yzux1KcsX65zxenm3.dVTM4QDLygjN0czW}
---

# Searching For Manuals

All of the man pages are gathered in a searchable database. We can read the man page manpage by doing: man man. It reads all the information of the man command.

***Commands:***

1) `hacker@man~searching-for-manuals:~$ man man`

2) `hacker@man~searching-for-manuals:~$ man -K /challenge/challenge`

3) `hacker@man~searching-for-manuals:~$ /challenge/challenge  --sxcpln 915`

***Flag:***

> pwn.college{EsMxcMG9H1pMTlD-5VS4On2cCya.dZTM4QDLygjN0czW}

***Observation:***

The man -K (search string) command can be used to find a hidden manpage easily if we know the string to be searched for.

---

# Helpful Programs

Some programs don't have a man page, but might tell you how to run them if invoked with a special argument. Usually, this argument is --help, but it can often be -h or, in rare cases, -?, help, or other esoteric values like /?

***Commands:***

1) `hacker@man~helpful-programs:~$ cd /`

2) `hacker@man~helpful-programs:/$ /challenge/challenge --help`

3) `hacker@man~helpful-programs:/$ /challenge/challenge --p`
*output:The secret value is: 356*

4) `hacker@man~helpful-programs:/$ /challenge/challenge --g 356`

***Flag:***

> pwn.college{EZVn3bex5oCDW6U550oIjGs5zDM.ddjM4QDLygjN0czW}

***Extra Info:***

1) `hacker@man~helpful-programs:/$ /challenge/challenge --fortune`
*output:To err is human; to forgive is simply not our policy.
                -- MIT Assasination Club*
---

# Help For Builtins

Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin help.

You can get help on a specific one by passing it to the help builtin. Eg: help cd.

***Commands:***

1) `hacker@man~help-for-builtins:~$ cd /`

2) `hacker@man~help-for-builtins:/$ help`

3) `hacker@man~help-for-builtins:/$ help challenge`

4) `hacker@man~help-for-builtins:/$ challenge   --secret Aw2QTdGT`

***Flag:***

>pwn.college{Aw2QTdGT-tkgwKX9yUvkpWz1cyN.dRTM5QDLygjN0czW}
---
