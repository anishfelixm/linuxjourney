## USERS AND GROUPS

  In every OS, there's users and groups which is mainly for access and permissions. When running a process, it is run as owner of the process. Each user has their home directory where the user specific files are saved. This is usually in /homes/username but can be different in other distributions.
  The system uses User IDs \(UID\) to manager users. The system uses groups to manage permissions where groups are just sets of users who are granted permission set by the group. They are identified by system using their group id \(GID\).
  In Linux, along with normal Users there are other system users as well ie system daemons which run their processes to keep the system functioning continuously. One of the most important system user is **root** or **superuser**. It is the most powerful user on the system and can access and manage every file in system as well as manage any process ie terminate or run a process on the system.
> Makes it dangerous to work as root user all the time since if you delete any system critical files the system can stop working.

  When the user has root access, they can run the command without using sudo \(superuser do\). The sudo command is used to run a command with root access. When the user tries to access files belonging to other groups or belonging to root group, permission is denied till the user gets root access. Once they have the root access, they can work with the contents in the file.

  One way to get superuser access is using "sudo". Another way is by using the "**su**" command which stands for "substitute users" and is used to substitute another user in place of current user as long as the password of the other user is known. The default is root ie if no user is specified the system substitutes user as root user as long as correct password is entered.
> $su

  But working as superuser all the time is dangerous and is better to stick to sudo for root access at times. The system doesn't let every random person run commands as superuser. The list of users with sudo access is listed in **/etc/sudoers** file. This file can be edited using the visudo command.

  
