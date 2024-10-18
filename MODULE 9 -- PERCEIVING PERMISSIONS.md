In Linux, files have different permissions or file modes. You can check out a permissions of a file or directory using ls -l.

```
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
```

1) The File Type : 
The first character of each line represents the file type.
In pwn_directory's case, the d indicates that it's a directory, and in college_file's case, the - represents that it's a normal file.

2) The Permissions
The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting the permissions that the user who owns the file (termed the "owner") has to the file,
3 characters denoting the permissions that the group that owns the file (termed the "group") has to the file,
and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

3) Ownership Information
There are two columns showing the user that owns the file (in this case, user hacker) and then the group that owns the file (in this case, also group hacker).

---

# Changing File Ownership

First things first: file ownership. Every file in Linux is owned by a user on the system. Most often, in your day-to-day life, that user is the user you log in as every day.

The two most important user accounts are:

1) Your user account! (On pwn.college, this is the hacker user, regardless of what your username is.)

2) root. This is the administrative account and, in most security situations, the ultimate prize. If you take over the root user, you've almost certainly achieved your hacking objective!

We can change the ownership of files! This is done via the chown (change owner) command: chown [username] [file]

***commands:***

1) `hacker@permissions~changing-file-ownership:~$ ls -l`

2) `hacker@permissions~changing-file-ownership:~$ chown hacker /flag`

3) `hacker@permissions~changing-file-ownership:~$ cat /flag`

***Flag:***

>pwn.college{o0OhrL7ez9atfaKbic6cEp0YYRg.dFTM2QDLygjN0czW}
---

# Groups and Files

Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups.
You can check what groups you are part of with the id command.
The most common use-case for groups is to control access to different system resources.
Group ownership can be changed with the chgrp (change group) command! Unless you have write access to the file and membership in the new group, this typically requires root access.

***Commands:***

1) `hacker@permissions~groups-and-files:~$ id`  *output: uid=1000(hacker) gid=1000(hacker) groups=1000(hacker)*

2) `hacker@permissions~groups-and-files:~$ ls -l`

3) `hacker@permissions~groups-and-files:~$ ls -l /flag`  *output: -r--r----- 1 root root 58 Oct 18 12:49 /flag*

4) `hacker@permissions~groups-and-files:~$ chgrp hacker /flag`

5) `hacker@permissions~groups-and-files:~$ cat /flag`

***Flag:***

>pwn.college{wYiTUbOhjwq6gHiwe4UVWNklR7O.dFzNyUDLygjN0czW}
---

# Fun With Group Names

There is a convention in Linux that every user has their own group, but this does not have to be the case always. For example, many computer labs will put all of their users into a single, shared users group.

***Commands:***

1) `hacker@permissions~fun-with-groups-names:~$ ls -l /flag`  *output: -r--r----- 1 root root 58 Oct 18 13:06 /flag*

2) `hacker@permissions~fun-with-groups-names:~$ id`  *output: uid=1000(hacker) gid=1000(grp16910) groups=1000(grp16910)*

3) `hacker@permissions~fun-with-groups-names:~$ chgrp grp16910 /flag`

4) `hacker@permissions~fun-with-groups-names:~$ cat /flag`

***Flag:***

>pwn.college{IDFu8CwMqXdKOhqVj4KVaKQy29w.dJzNyUDLygjN0czW}
---

# Changing Permissions

`-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file`

The first character there is the file type. The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting permissions for the owning user, 
3 characters denoting the permissions for the owning group, and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.

Each character of the three represent permission for a different type:
```
r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - nothing
```

Like ownership, file permissions can also be changed. This is done with the chmod (change mode) command. The basic usage for chmod is: chmod [OPTIONS] MODE FILE

You can specify the MODE in two ways: 
1) As a modification of the existing permissions mode
2) As a completely new mode to overwrite the old one.

Eg (case 1): 
1) u+r, as above, adds read access to the user's permissions
2) g+wx adds write and execute access to the group's permissions
3) o-w removes write access for other users
4) a-rwx removes all permissions for the user, group, and world

***Commands:***

1) `hacker@permissions~changing-permissions:~$ ls -l /flag`  *output: -r-------- 1 root root 58 Oct 18 13:22 /flag*

2) `hacker@permissions~changing-permissions:~$ chmod u+rwx *`

3) `hacker@permissions~changing-permissions:~$ chmod g+rwx *`

4) `hacker@permissions~changing-permissions:~$ chmod o+rwx *`  *(Main Command)*

5) `hacker@permissions~changing-permissions:~$ cat /flag`

***Flag:***

>pwn.college{snCqfdzaz79Gvt2si4I3mQhArWt.dNzNyUDLygjN0czW}
---

# Executable Files

When you invoke a program, Linux will only actually execute it if you have execute-access to the program file.
If we remove these permissions, the execution will fail!

***Commands:***

1) `hacker@permissions~executable-files:~$ ls -l /challenge/run`  *output: -r--r--r-- 1 hacker hacker 32 Jul  4 06:37 /challenge/run*

2) `hacker@permissions~executable-files:~$ chmod o+x *`  *output: chmod: changing permissions of 'not-the-flag': Operation not permitted*

3) `hacker@permissions~executable-files:~$ chmod ugo+x /challenge/run`

4) `hacker@permissions~executable-files:~$ /challenge/run`

***Flag:***

>pwn.college{gwBiHtx9XjC8AMPYmTZNb-5USRc.dJTM2QDLygjN0czW}
---

# Permission Tweaking Practice

***Commands:***

1) `pwn.college{4ukdS2oPDZl9cT9AbfPT55Xuokk.dBTM2QDLygjN0czW}`

2) `hacker@permissions~permission-tweaking-practice:~$ /challenge/run`

3) ```
    hacker@permissions~permission-tweaking-practice:~$ chmod u-w /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod u+x /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod o+x /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod u-r /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod o+w /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod og-r /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod ug+r /challenge/pwn
    hacker@permissions~permission-tweaking-practice:~$ chmod u-r /challenge/pwn
   ```

4) `hacker@permissions~permission-tweaking-practice:~$ ls -l /flag` *output: ---------- 1 hacker hacker 58 Oct 18 14:07 /flag*

5) `hacker@permissions~permission-tweaking-practice:~$ chmod oug+rwx /flag`

6) `hacker@permissions~permission-tweaking-practice:~$ cat /flag`

***Flag:***

>pwn.college{4ukdS2oPDZl9cT9AbfPT55Xuokk.dBTM2QDLygjN0czW}
---

# Permission Setting Practice

Chmod can also simply set permissions altogether, overwriting the old ones. This is done by using = instead of - or +.
We can use it to set different permissions for the user, group and others.

Eg: 
1) chmod u=rw,g=r /challenge/pwn will set the user permissions to read and write, and the group permissions to read-only.
2) chmod a=r,u=rw /challenge/pwn will set the user permissions to read and write, and the group and world permissions to read-only.
3) chmod u=rw,g=r,o=- /challenge/pwn will set the user permissions to read and write, the group permissions to read-only, and the world permissions to nothing at all.

Keep in mind, that -, appearing after = is in a different context than if it appeared directly after the u, g, or o.

***Commands:***

1) `hacker@permissions~permissions-setting-practice:~$ /challenge/run`

2) ```
   hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=w,o=rx /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=w,g=wx,o=w /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=wx,g=x,o=wx /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=rx,o=- /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=r,g=-,o=x /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=-,g=-,o=- /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=rwx,g=-,o=rw /challenge/pwn
   hacker@permissions~permissions-setting-practice:~$ chmod u=rx,g=x,o=rw /challenge/pwn
   ```

3) `hacker@permissions~permissions-setting-practice:~$ ls -l /flag`  *output: ---------- 1 hacker hacker 58 Oct 18 14:22 /flag*

4) `hacker@permissions~permissions-setting-practice:~$ chmod u=r /flag`

5) `hacker@permissions~permissions-setting-practice:~$ cat /flag`

***Flag:***

>pwn.college{gqH8DfyopfpAO4t6jVmORX124xW.dNTM5QDLygjN0czW}
---

# The SUID Bit

There are many cases in which non-root users need elevated access to do certain system tasks. The system admin can't be there to give them the password every time a user wanted to do a task that only root/sudoers can do. 
The "Set User ID" (SUID) permissions bit allows the user to run a program as the owner of that program's file.

The permission of a file with SUID list look like this:
```
hacker@dojo:~$ ls -l /usr/bin/sudo
-rwsr-xr-x 1 root root 232416 Dec 1 11:45 /usr/bin/sudo
hacker@dojo:~$
```
The s part in place of the executable bit means that the program is executable with SUID. 
It means that, regardless of what user runs the program (as long as they have executable permissions), the program will execute as the owner user.

As the owner of a file, you can set a file's SUID bit by using chmod: `chmod u+s [program]`

***Commands:***

1) `hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot`  *output: -rwxr-xr-x 1 root root 155 Jul 12 10:30 /challenge/getroot*

2) `hacker@permissions~the-suid-bit:~$ chmod ugo+s /challenge/getroot`

3) `hacker@permissions~the-suid-bit:~$ ls -l /challenge/getroot`  *output: -rwsr-sr-x 1 root root 155 Jul 12 10:30 /challenge/getroot*

4) `hacker@permissions~the-suid-bit:~$ /challenge/getroot`
*output: SUCCESS! You have set the suid bit on this program, and it is running as root!
Here is your shell...*

5) `root@permissions~the-suid-bit:~# cat /flag`

***Flag:***

>pwn.college{UlTRmWGrk6yubofH86O-gJeUD_U.dNTM2QDLygjN0czW}
---
