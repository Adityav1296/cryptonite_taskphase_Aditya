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

 Eg: hacker@dojo:/tmp$ touch pwnfile
-->  hacker@dojo:/tmp$ ls --> pwnfile

***Commands:***

 1) `hacker@commands~touching-files:~$ cd /tmp`

 2) `hacker@commands~touching-files:/tmp$ touch pwn`

3) `hacker@commands~touching-files:/tmp$ touch college`
   
4) `hacker@commands~touching-files:/tmp$ ls`
*output: bin  college  hsperfdata_root  pwn  tmp.G9qthVCks5*

5) `hacker@commands~touching-files:/tmp$ /challenge/run`

***Flag:***

>pwn.college{gX1hh6rL7hh_O2wArcpBhUniA41.dBzM4QDLygjN0czW}
____________________________________________________________

# REMOVING FILES

In Linux, you remove files with the rm command. 

***Commands:***

1) `hacker@commands~removing-files:~$ ls`
 *output: Desktop  delete_me  f*

2) `hacker@commands~removing-files:~$ rm delete_me`

3) `hacker@commands~removing-files:~$ ls`
*output: Desktop  f*

4) `hacker@commands~removing-files:~$ /challenge/check`
*output: Excellent removal. Here is your reward:*

***Flag:***

>pwn.college{g2LFXvTOVeixPVN8KqtaYB1JBr2.dZTOwUDLygjN0czW}
______________________________________________________________
 
 # HIDDEN FILES

Interestingly, ls doesn't list all the files by default. Linux has a convention where files that start with a . don't show up by default in ls and in a few other contexts. To view them with ls, you need to invoke ls with the -a flag.  

Eg: hacker@dojo:~$ ls -a  -->
.college	pwn

***Command:***

1) `hacker@commands~hidden-files:~$ cd /` 

2) `hacker@commands~hidden-files:/$ ls` *output: no  .flag-31329371812044 and  .dockerenv   files shown*

3) `hacker@commands~hidden-files:/$ ls -a` *output:  .flag-31329371812044 and  .dockerenv   files shown along with rest of the files*

4) `hacker@commands~hidden-files:/$ cat  .flag-31329371812044`

***Flag:***

>pwn.college{ENUHPf4mZQZBpuXOkmVelFdBbnZ.dBTN4QDLygjN0czW}
---

# AN EPIC FILESYSTEM QUEST

***Commands:***

1) `hacker@commands~an-epic-filesystem-quest:~$ cd /`

2) `hacker@commands~an-epic-filesystem-quest:/$ ls` 

3) `hacker@commands~an-epic-filesystem-quest:/$ cat flag`
*output: cat: flag: Permission denied*

4) `hacker@commands~an-epic-filesystem-quest:/$ cat NOTE`
*output: Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/networkx/algorithms/isomorphism*

5) `hacker@commands~an-epic-filesystem-quest:/$ ls  /usr/lib/python3/dist-packages/networkx/algorithms/isomorphism`

6) `hacker@commands~an-epic-filesystem-quest:/$ cat /usr/lib/python3/dist-packages/networkx/algorithms/isomorphism/SPOILER-TRAPPED` *output: Tubular find!
The next clue is in: /usr/lib/python3/dist-packages/mpl_toolkits/axes_grid*

7) `hacker@commands~an-epic-filesystem-quest:/$ ls  /usr/lib/python3/dist-packages/mpl_toolkits/axes_grid`

8) `hacker@commands~an-epic-filesystem-quest:/$ cd /usr/lib/python3/dist-packages/mpl_toolkits/axes_grid`
   
9) `hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/mpl_toolkits/axes_grid$ cat LEAD` *output:
Tubular find!
The next clue is in: /usr/share/racket/pkgs/scribble-lib/scribble/lncs/compiled*

10) `hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/mpl_toolkits/axes_grid$ cd /usr/share/racket/pkgs/scribble-lib/scribble/lncs/compiled`

11) `hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/lncs/compiled$ ls` *output:
ALERT  lang_rkt.dep  lang_rkt.zo*

12) `hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/lncs/compiled$ cat ALERT`
*output: Yahaha, you found me!
The next clue is in: /opt/linux/linux-5.4/Documentation/devicetree/bindings/regulator*

14) `hacker@commands~an-epic-filesystem-quest:/usr/share/racket/pkgs/scribble-lib/scribble/lncs/compiled$ cd  /opt/linux/linux-5.4/Documentation/devicetree/bindings/regulator`

15) `hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/Documentation/devicetree/bindings/regulator$ la -a`

16) `hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/Documentation/devicetree/bindings/regulator$ cat .BRIEF` *output: 
Great sleuthing!
The next clue is in: /usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco/text*

17) `hacker@commands~an-epic-filesystem-quest:/opt/linux/linux-5.4/Documentation/devicetree/bindings/regulator$ cd /`

18) `hacker@commands~an-epic-filesystem-quest:/$ ls -a /usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco/text`

19) `hacker@commands~an-epic-filesystem-quest:/$ cat /usr/local/lib/python3.8/dist-packages/setuptools/_vendor/jaraco/text/DI` *output: 
SPATCH-TRAPPED
Yahaha, you found me!
The next clue is in: /usr/share/zoneinfo/posix/Arctic*

20) `hacker@commands~an-epic-filesystem-quest:/$ cd  /usr/share/zoneinfo/posix/Arctic`
    
21) `hacker@commands~an-epic-filesystem-quest:/usr/share/zoneinfo/posix/Arctic$ ls -a`

22) `hacker@commands~an-epic-filesystem-quest:/usr/share/zoneinfo/posix/Arctic$ cat INFO`
*output: Great sleuthing!
The next clue is in: /usr/lib/python3/dist-packages/cairo*

23) `hacker@commands~an-epic-filesystem-quest:/usr/share/zoneinfo/posix/Arctic$ cd  /usr/lib/python3/dist-packages/cairo`

24) `hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/cairo$ ls -a`

25) `hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/cairo$ cat .TEASER`
*output: Congratulations, you found the clue!
The next clue is in: /opt/aflplusplus/nyx_mode/libnyx/libnyx/target/release/.fingerprint/config-9071a9273268cefc*

26) `hacker@commands~an-epic-filesystem-quest:/usr/lib/python3/dist-packages/cairo$ cd  /opt/aflplusplus/nyx_mode/libnyx/libnyx/target/release/.fingerprint/config-9071a9273268cefc`

27) `hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx/target/release/.fingerprint/config-9071a9273268cefc$ ls -a`

28) `hacker@commands~an-epic-filesystem-quest:/opt/aflplusplus/nyx_mode/libnyx/libnyx/target/release/.fingerprint/config-9071a9273268cefc$ cat .SECRET` *output: 
CONGRATULATIONS! Your perserverence has paid off, and you have found the flag!*

***Flag:***

> pwn.college{Mb-ZxWNtXS6_gdmjBHbeby8zM5q.dljM4QDLygjN0czW}
---

# MAKING DIRECTORIES

You make directories using the mkdir command. hacker@dojo:/tmp$ mkdir my_directory -->
hacker@dojo:/tmp$ ls -->
my_directory

***Commands:***

1) `hacker@commands~making-directories:~$ cd /tmp`

2) `hacker@commands~making-directories:/tmp$ mkdir pwn`

3) `hacker@commands~making-directories:/tmp$ ls` *output: 
bin  hsperfdata_root  pwn  tmp.G9qthVCks5*

4) `hacker@commands~making-directories:/tmp$ cd pwn`

5) `hacker@commands~making-directories:/tmp/pwn$ touch college`

6) `hacker@commands~making-directories:/tmp/pwn$ ls` *output: college*

7) `hacker@commands~making-directories:/$ /challenge/run` *output: Success! Here is your flag:*

***Flag:***

>pwn.college{0ir90qOMcyEi7hfpQcJ6Vb6MHGY.dFzM4QDLygjN0czW}
---

# FINDING FILES

The find command takes optional arguments describing the search criteria and the search location. If you don't specify a search criteria, find matches every file. If you don't specify a search location, find uses the current working directory (.).

Eg: hacker@dojo:~$ find -name my_subfile  -->  ./my_directory/my_subdirectory/my_subfile

***Commands:***

1) `hacker@commands~finding-files:~$ cd /`

2) `hacker@commands~finding-files:/$ find -name flag`

3) `hacker@commands~finding-files:/$ cat ./usr/share/racket/pkgs/snip-lib/racket/snip/flag`

***Flag:***

>pwn.college{IKDzX6o3BDRR4kptqJ7EtgCLe9x.dJzM4QDLygjN0czW}
---

# LINKING FILES

Links come in two flavors: hard and soft (also known as symbolic) links. We'll differentiate the two with an analogy:

1) A hard link is when you address your appartment using multiple addresses that all lead directly to the same place (e.g., Apt 2 vs Unit 2).

2) A soft link is when you move appartments and have the postal service automatically forward your mail from your old place to your new place.

A hard link is an alternate address that indexes that data --- accesses to the hard link and accesses to the original file are completely identical, in that they immediate yield the necessary data. A soft/symbolic link, instead, contains the original file name. When you access the symbolic link, Linux will realize that it is a symbolic link, read the original file name, and then (typically) automatically access that file.

Symbolic links are created with the ln command with the -s argument, 

The file command, which takes a filename and tells you what type of file it is, will recognize symlinks.

***Commands:***

1) `hacker@commands~linking-files:/$ ln -s /flag /home/hacker/not-the-flag`

2) `hacker@commands~linking-files:/$ /challenge/catflag`
*output: About to read out the /home/hacker/not-the-flag file!*

***Flag:***

>pwn.college{gDT7W4mspYjtlp0Hq7su1Ui2fnc.dlTM1UDLygjN0czW}
---













