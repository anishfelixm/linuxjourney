## File Permissions

Files have different permissions and file modes. One can see the file permission by doing a simple "**ls -l**". The "ls -l" command will usually have the following output : 

> drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .

The first block in the above output shows the file permissions. The file permissions ie "drwxr-xr-x" can be divided into 4 blocks ie<br>
| d | rwx | r-x | r-x |<br>
The first bit shows type of file. "d" represents a directory while a regular file will have "-". The next 3 blocks represent User permissions, group permissions and other permissions. These 3 blocks represent the actual file permissions.

|charachters|permission|
|---|---|
|r|Read|
|w|Write|
|x|Executable|
|-|Empty|

So in above example we can say user pete has :
+ read, write, execute as user permissions
+ read, execute as group permissions
+ read, execute as other permissions

To change or modify permissions, use the "**chmod**" command. We need to pick whether permission is for user, group or other and then use "+" to add permission and "-" to remove permission.

> $chmod u+w myfile

This is to be interpreted as change/modify permissions on the file named "myfile" for user by adding write permission

> $chmod u-x myfile

This is to be interpreted as change/modify permissions on the file named "myfile" for user by removing executing permission.

> $chmod ug+w myfile

This is to be interpreted as change/modify permissions on the file names "myfile" for user and group by adding write permission.

Permissions can be changed also using a numerical format which makes easier to change all permissions at once. The numerical values for r, w, x are
 + 4 : read permission
 + 2 : write permission
 + 1 : execute permission

Each permission set is a sum of numerical values of permission ie to add read, write permission we use value 4 + 2 = 6.
> $chmod 755 myfile

This is to be interpreted as adding read, write, executing (4+2+1) permission for user; then read, execute (4+1) permission for group and read, execute (4+1) permission for other.
Be careful while giving permissions using chmod so that everyone isn't given permission to write to sensitive files.

One can change user and group ownership of file.
> $sudo chown Anish myfile

This changes owner of myfile to user named "Anish"

> $sudo chgrp whales myfile

This changes group of myfile to group named "whales"

> $sudo chown Anish:whales myfile

This changes group and owner of myfile to "Anish" and "whales" at same time

There's a default list of permissions that's given to every file that's created. But in situation when you want to change this default permission use the "**umask**" command. "umask" doesn't add permissions but removes them away. It takes a 3 number parameter as permission bits. The 3 numbers are user, group and other permissions. Also the numerical values of permissions are used in parameters.
> $umask 021

This means that the default permissions given to new files created will change as follows:
+ no change in user permission
+ removal of write permission for groups
+ removal of executing permissions for others

Default umask is usually 022. If you want the changed default permissions to stay in system, we have to change the ".profile" file.

It is very annoying for the system to go into root access everytime we need to access a protected file. So to deal with this users are given an elevated access to files using the Set User Id (SUID) permission bit. SUID allows other users to access file as if the user is the owner of the file. For example, the command "passwd" to change passwords is basically modifying a set of files ie /etc/shadow. To open this file we need root access since root is the owner, however passwd command does this without needing to change user to root user. That's because it has been given the SUID permission bit. This can be checked :
> $ls -l /usr/bin/passwd

The output would look like:
> -rwsr-xr-x 1 root root 47032 Dec 1 11:45 /usr/bin/passwd

Focussing on the permission bits, we notice the user permissions has a "**s**" permission bit. This is the SUID. When a file has this permission bit, it allows the user to basically run as though the user is the owner of the file. If the permission bit is removed, then "passwd" won't be able to change your own password and only root ie the owner of /etc/shadow will be able to change the password.
To modify the SUID permissions :
> $sudo chmod u+s myfile
>
> $sudo chmod 4755 myfile

The number 4 is pre-appended to permission set. If permission bit shows as "**S**", its same as "s" but without executing permission.

Similar to SUID, there's SGID or Set Group ID permission bit. This allows the program or file to run as though it is a member of that group. For example :
> $ls -l /usr/bin/wall
>
> -rwxr-sr-x 1 root tty 19024 Dec 14 11:45 /usr/bin/wall

Notice the permission bit is in group. To modify SGID:
> $sudo chmod g+s myfile
>
> $sudo chmod 2555 myfile

SGID is represented by 2.

Now when a user is running a file or program with SUID it doesn't mean that the user is temporary root user and so can do other root tasks. That's because Linux uses 3 types of UIDS:
+ When the user launches a process it runs with the same permissions as the user or group that ran it, this is known as an effective user ID. This UID is used to grant access rights to a process. This is basically the UID of user using the program at the moment.
+ There is another UID, called the real user ID. This is the ID of the user that launched the process. These are used to track down who the user who launched the process is. This is basically the UID of original user.
+ One last UID is the saved user ID, this allows a process to switch between the effective UID and real UID, vice versa. This is useful because we don't want our process to run with elevated privileges all the time, it's just good practice to use special privileges at specific times.

Let's use the above UIDs to understand why using passwd command we can't change others passwords if we are not the root.
> So when user Anish launches the program passwd, the real User id UID is 500. Since the program passwd has SUID permission, the effective UID is 0 \(root UID is 0\). So the user Anish is able to change his password. But now if user Anish wants to change user Darren password whose UID is 600, he won't be able to do so as the real UID of user Anish is 500 and not 0. When user Anish launches passwd, the system saves his real UID \(ie 500\) and switches to root UID \(ie 0\).

> ### Cool Stuff
> 1. Open one terminal window, and run the command: watch -n 1 "ps aux | grep passwd". This will watch for the passwd process.
> 2. Open a second terminal window and run: passwd
> 3. Look at the first terminal window, you'll see a process come up for passwd

There's also a "**sticky bit**" permission bit. This sticks the file or directory ie only the owner or root user can delete and modify the file. Useful for shared directories. This can be seen by the permission bit "**t**" at the end of permission bits \(seen using ls -l\). To modify sticky bit which is represented by 1:
> $sudo chmod +t mydir
>
> $sudo chmod 1755 mydir

---
---
