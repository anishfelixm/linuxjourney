## USERS AND GROUPS

  In every OS, there's users and groups which is mainly for access and permissions. When running a process, it is run as owner of the process. Each user has their home directory where the user specific files are saved. This is usually in /homes/username but can be different in other distributions.
  The system uses User IDs \(UID\) to manager users. The system uses groups to manage permissions where groups are just sets of users who are granted permission set by the group. They are identified by system using their group id \(GID\).
  In Linux, along with normal Users there are other system users as well ie system daemons which run their processes to keep the system functioning continuously. One of the most important system user is **root** or **superuser**. It is the most powerful user on the system and can access and manage every file in system as well as manage any process ie terminate or run a process on the system.
> Makes it dangerous to work as root user all the time since if you delete any system critical files the system can stop working.

  When the user has root access, they can run the command without using sudo \(superuser do\). The sudo command is used to run a command with root access. When the user tries to access files belonging to other groups or belonging to root group, permission is denied till the user gets root access. Once they have the root access, they can work with the contents in the file.

  One way to get superuser access is using "sudo". Another way is by using the "**su**" command which stands for "substitute users" and is used to substitute another user in place of current user as long as the password of the other user is known. The default is root ie if no user is specified the system substitutes user as root user as long as correct password is entered.
> $su

  But working as superuser all the time is dangerous and is better to stick to sudo for root access at times. The system doesn't let every random person run commands as superuser. The list of users with sudo access is listed in **/etc/sudoers** file. This file can be edited using the "**visudo**" command.
> $sudo visudo


  Usernames are not the identification of an user, UIDs are the identification of the user. UIDs are matched to users and this can be found in "**/etc/passwd/**" file.
> $cat /etc/passwd/

  This file contains detailed information about each user in each line. Each line output will look like:
> root:x:0:0:root:/root:/bin/bash

  The contents are separated by ":". The content in the file is :
+ Username
+ User's password - Password isn't saved in this file, rather in /etc/shadow. Here the content will be "x" when password is in /etc/shadow file. If content is "*", then it means user doesn't have login access and a blank block means the user doesn't have a password.
+ UserID - Root has UID 0
+ GroupID
+ GECOS field - Comment on User's real name, etc and content inside is separated by ","
+ User's home directory
+ User's shell - Most will have bash shell

/etc/passwd will show users other than human users as users are just system processes running with different permissions. The contents of /etc/passwd can be edited by hand using the **vipw** tool to add or modify users, but it's better to do these tasks using other tools like useradd and userdel.

  "**/etc/shadow**" is used to save data about user authentication. Needs superuser access to read data in /etc/shadow. 
> $sudo cat /etc/shadow

The file looks similar to /etc/passwd file and each line will look something like this :
> root:MyEPTEa$6Nonsense:15000:0:99999:7:::

The contents are separated by ":". The fields are :
+ Username
+ User's encrypted password
+ Date of last password changed - Value is number of days from Jan 1, 1970. If the value is 0, the user should change the password next time they log in.
+ Minimum password age - Minimum number of days user should wait before changing password
+ Maximum password age - Maximum number of days before user has to change the password.
+ Password warning period - Number of days before password expires.
+ Password Inactivity period - Number of days after a password has expired to log in with that password.
+ Account expiration date - Date from which user won't be able to log in.
+ Future use

  Nowadays Linux uses other mechanisms such as **PAM** \(Pluggable Authentication Modules\) along with /etc/shadow to manage authentication.


"**/etc/group**" is used in User management for managing different groups with different permissions.
> $cat /etc/group

This output will look similar to /etc/shadow , etc where fields are separated with ":". The fields are : 
+ Group name
+ Group Password - No neccesity to have group password. Default is "*".
+ Group ID \(GID\)
+ List of Users - Group of users in a specific group.

Command "groups" can be used to see the groups that the current user belongs to.
> $groups


