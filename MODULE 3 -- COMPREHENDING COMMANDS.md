# CAT: NOT THE PET, BUT THE COMMAND

cat is most often used for reading out files. cat will concatenate (hence the name) multiple files if provided multiple arguments.

***Command:***

`hacker@commands~cat-not-the-pet-but-the-command:~$ cat /flag`

***Flag:***

>pwn.college{4Euzpsea2ACCmgGGIBfrG07PuF9.dFzN1QDLygjN0czW}

***Observation:***

Just put the file name after cat. Eg: If '.md' is not given in the file name, no need to write it with the file name when writing after cat.
_____________________________________________________________________________________________________________________________________________

# CATTING ABSOLUTE PATHS

cat's arguments can be specified as absolute paths: hacker@dojo:~$ cat /challenge/DESCRIPTION.md

***Command:***

`hacker@commands~catting-absolute-paths:~$ cat /flag`

***Flag:***

>pwn.college{8_4T8GkgZKqPNMV-fHNoI2lcglx.dlTM5QDLygjN0czW}
________________________________________________________________

# MORE CATTING PRACTICE

***Command:***

1) `hacker@commands~more-catting-practice:~$ cd /`
 *output: You used 'cd'! In this level, I don't allow you to change the working directory
--- you MUST chase pass 'cat' the absolute path of where I put it on the
filesystem (which is /opt/radare2/sys/flag).*

2) `hacker@commands~more-catting-practice:~$ cat /opt/radare2/sys/flag`

***Flag:***

>pwn.college{oloVUkLDSU-zKQOXauntz3yh7Ys.dBjM5QDLygjN0czW}
______________________________________________________________

# GREPPING FOR A NEEDLE IN A HAYSTACK

Sometimes, the files that you might cat out are too big. We have the grep command to search for the contents we need!
Eg: hacker@dojo:~$ grep SEARCH_STRING /path/to/file. the grep command will search for file with letters SEARCH_STRING in the location specified after it.

***Command:***

`hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt`

***Flag:***

>pwn.college{8VxLjaUtYXxbwLxzM9i3RCzv5n7.ddTM4QDLygjN0czW}
__________________________________________________________________






