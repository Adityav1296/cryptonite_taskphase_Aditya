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

# LISTING FILES

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided.

Eg: hacker@dojo:~$ ls

Desktop    Downloads  Pictures  Templates

Documents  Music      Public    Videos

***Commands:***

1) `hacker@commands~listing-files:~$ ls /challenge`
*output: 8-renamed-run-7449  DESCRIPTION.md*

2) `hacker@commands~listing-files:~$ cd /challenge`
   
3) `hacker@commands~listing-files:/challenge$ cat 8-renamed-run-7449`
*output: #!/opt/pwn.college/bash echo "Yahaha, you found me! Here is your flag:" cat /flag*

4) `hacker@commands~listing-files:/challenge$ ./8-renamed-run-7449`
*output: Yahaha, you found me! Here is your flag:*

***Flag:***

>pwn.college{cssMThFsqvesuaS8polUhHWx_dl.dhjM4QDLygjN0czW}

***Problem:***

1) `hacker@commands~listing-files:/challenge$ cd /flag`
*output: ssh-entrypoint: cd: /flag: Not a directory*

2) `hacker@commands~listing-files:/challenge$ cat /flag`
*output: cat: /flag: Permission denied*

***Solution:***

1) Flag is a file name that we have to find. Hence don't use it with change directory command unless specified.

2) In this particular challenge, the flag file has been renamed. Therefore, when a file name is changed, make sure to use the new name with all the programs instead of the old one. 
__________________________________________________________________________________________________________________________________________________________________

# TOUCHING FILES

 You can create a new, blank file by touching it with the touch command: 

 Eg:hacker@dojo:/tmp$ touch pwnfile

    hacker@dojo:/tmp$ ls

    pwnfile





























