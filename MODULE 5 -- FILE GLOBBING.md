# Matching With *

When it encounters a * character in any argument, the shell will treat it as "wildcard" and try to replace that argument with any files that match the pattern.
When zero files are matched, by default, the shell leaves the glob unchanged.
The * matches any part of the filename except for / or a leading . character.

***Commands:***

1) `hacker@globbing~matching-with-:~$ cd /c*`

2) `hacker@globbing~matching-with-:/challenge$ /challenge/run`
*output:You ran me with the working directory of /challenge! Here is your flag:*

***Flag:***

>pwn.college{AqvkLx552oBZvGpjO8W6IrA_f0C.dFjM4QDLygjN0czW}
---

# Matching With ?

When it encounters a ? character in any argument, the shell will treat it as single-character wildcard.
This works like *, but only matches one character.

***Commands:***

1) `hacker@globbing~matching-with-:~$ cd /?ha??enge`

2) `hacker@globbing~matching-with-:/challenge$ /challenge/run`

***Flag:***

>pwn.college{sdlxHqrj9l72fsaYWI7nH4lEaCA.dJjM4QDLygjN0czW}
---

# Matching With []

The square brackes are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets.
For example, [pwn] will match the character p, w, or n.

***Commands:***

1) `hacker@globbing~matching-with-:~$ cd /challenge/files`

2) `hacker@globbing~matching-with-:/challenge/files$ ls`

3) hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[absh]`
*output:You got it! Here is your flag!*

***Flag:***

>pwn.college{U6-gYzQfSC0S_ny-J3LgghbBKs9.dNjM4QDLygjN0czW}
---

# Matching Paths With []

Globbing happens on a path basis, so you can expand entire paths with your globbed arguments.

***Commands:***

1) `hacker@globbing~matching-paths-with-:~$ ls /challenge/files`

2) `hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]`

***Flag:***

>pwn.college{gpnF7WJDLCZk0uVJj6eFzbxoSzl.dRjM4QDLygjN0czW}

***Observation:***

Providing the correct path is necessary to avoid ant error.

1) `hacker@globbing~matching-paths-with-:~$ /challenge/run file_[absh]`

*output: Error: you will need to specify the path to the files as part of your glob
argument, since they are in a different directory than your current working
directory!*

---

# Mixing Globs

***Commands:***

1) `hacker@globbing~mixing-globs:~$ cd /challenge/files`

2) `hacker@globbing~mixing-globs:/challenge/files$ ls`

3) `hacker@globbing~mixing-globs:/challenge/files$ /challenge/run  [cep]*`

***Flag:***

>pwn.college{8o5fcAKGFcRjasYbLF4ZyGXKkn2.dVjM4QDLygjN0czW}

***Observations:***

When mixing up the globs, we can place the globs in any order to make the program run. There is no fixed position to place the glob.
The globs are used to access the files with minimum input, hence we can try and find different positions to place the globs at as per our convinience.

Eg: 1) `hacker@globbing~mixing-globs:/challenge/files$ /challenge/run  [c*e*p*]`

2) `hacker@globbing~mixing-globs:/challenge/files$ /challenge/run  [cep*]`

3) `hacker@globbing~mixing-globs:/challenge/files$ /challenge/run  c*e*p*`

The above are some of the examples of the different positions I tried placing the globs at to get the required output.

---

# Exclusionary Globbing

Sometimes, you want to filter out files in a glob!Luckily.
[] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.

The ! character has a different special meaning in bash when it's not the first character of a [] glob.
^ character does not have this problem but is also not compatible with the older shell versions.

***Commands:***

1) `hacker@globbing~exclusionary-globbing:~$ cd /challenge/files`

2) `hacker@globbing~exclusionary-globbing:/challenge/files$ ls`

3) `hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [!pwn]*`

***Flag:***

>pwn.college{E-h5hu4FmwaXcxML5ycPN7V15Mj.dZjM4QDLygjN0czW}
---
