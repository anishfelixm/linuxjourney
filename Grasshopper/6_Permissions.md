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
> changes owner of myfile to user named "Anish"
> 
> $sudo chgrp whales myfile
> changes group of myfile to group named "whales"
> 
> $sudo chown Anish:whales myfile
> changes group and owner of myfile to "Anish" and "whales" at same time

There's a default list of permissions that's given to every file that's created. But in situation when you want to change this default permission use the "**umask**" command. "umask" doesn't add permissions but removes them away. It takes a 3 number parameter as permission bits. The 3 numbers are user, group and other permissions. Also the numerical values of permissions are used in parameters.
> $umask 021

This means that the default permissions given to new files created will change as follows:
+ no change in user permission
+ removal of write permission for groups
+ removal of executing permissions for others

Default umask is usually 022. If you want the changed default permissions to stay in system, we have to change the ".profile" file.

