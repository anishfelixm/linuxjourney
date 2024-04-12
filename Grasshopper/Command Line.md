  The **Shell** is a computer program which takes commands from the keyboard and sends to the Operating system to execute. System programs such as "_terminal_" or "_console_" launch a shell for you. Most Linux distributions have a shell called ***bash***, which stands for **B**ourne **A**gain **Sh**ell. There are other shell programs as well like zsh, tsh, etc.

  When a shell is opened the prompt may look like :
>pete@icebox:/home/pete $

The "$" symbol points to normal user and varying on distribution and user access other symbols may be used. There's no need to add the symbol before a command since the symbol will be there.

|**Commands**|**Application**                                |**Usage**         |**Result**                           |
|------------|-----------------------------------------------|------------------|-------------------------------------|
|echo        |Echoes back the message to terminal             |$ echo Hello world|HelloWorld                           |
|date        |Displays today's date, day and time on terminal|$date             |Tuesday 09 April 2024 07:18:31 AM IST|
|whoami      |Displays the username on terminal              |$whoami           |anish                                |

---

**pwd**
  
  Everything in Linux is a file organized in a hierarchical order. The 1st or topmost directory is the root directory, represented by "/". The location to the files and folders is called path. It's useful to know the path so that you can navigate using terminal itself. To find path to current file, use the ***pwd*** command. pwd stands for "print working directory".
Syntax:
> $pwd
> /home/user/Desktop

---

**cd**

  To move around files in Linux, you'll need file path and the command "cd", which stands for change directory. There's 2 types of paths :
+ Absolute path : The path starts from root directory, represented using "/". eg - cd /home/anish/Desktop/
+ Relative path : The path is respect to current directory ie any movement will happen from current path. eg - cd ./Desktop/
Syntax :
> $cd /home/anish/Desktop //absolute path
> $cd ./Downloads/  //relative path

  There's some additional option symbols as well which shorten the commands to write.
| Symbol | Description      |
|--------|------------------|
|1. .    |current directory |
|2. ..   |parent directory  |
|3. ~    |home directory    |
|4. -    |previous directory|

> $cd Just this command goes to root directory

---

**ls**

  To see all files and folders inside a file path we use the ls command, which stands for list directories. 
Syntax :
> $ls -> shows files and folders in current path
> $ls /home -> shows files and folders in /homes

  Not all files and folders will be visible. If filenames start with ".", then normal ls won't display the object as it treats it as hidden content. To view these contents can use "-a" flag, which shows all files in path. 
|flags|Application                           |
|-----|--------------------------------------|
|-a   |Show all files                        |
|-l   |Display as long list with many details|
|-R   |Recursively show directory elements   |
|-r   |reverse order while sorting by name   |
|-t   |sort by last modification times       |
Flags are options given to commands to extend their applications. THey can be combined as well but ordering matters. eg - ls -a then ls -l can be combined as ls -al

---

**touch**

  To make new files, a simple command is touch. It creates new empty files. It updates file timestamps as well.
Syntax :
> $touch newfile

---

**file**

  Normally, like in Windows, files will have filenames such as .jpeg, .gif, etc. This isn't required in Linux, ie filenames are not required to represent the type of content in file. So we can have a .gif file without the filename being .gif. To get the type of file, use the "file" command.
Syntax :
> $file banana.jpg

---

**cat**

  Command to only read a file. Stands for concatenate as one can view multiple files as well by concatenating them. Not the best tool to read large files, other tools exist.
Syntax :
> $cat dog.txt cat.txt

---

**less**

  If the contents in a file is very large, then the "less" command can be used to view it in a paged manner. To navigate after using less command :
+ q - quit
+ PageDown, PageUp, Up and Down - navigate 
+ g - moves to begining of file
+ G - moves to end of file
+ /search - to search for any word or string in file like /word
+ h - help
Syntax :
> $less /home/Anish/Desktop/try.c

---

**history**

  To look at the history of commands on shell, use the "history" command. Useful to search what command one had used. To move to a previous command, just use the *Up arrow key*.
There's another way to search and use a previous used command on shell. Press *CTRL + R* and then start filling in parts of command to see previous commands. Then use *CTRL + R* to navigate till the command of choice and then press Enter to immediately execute it. Can use "!!" command to immediately execute the exact previous command.
Syntax :
> $history

To clear the screen, use the "clear" command.
Syntax :
> $clear

One more very useful feature is the use of __TAB__ key to autocomplete words. If there's multiple stuff with same or similar names, pressing *TAB* key will fill part which matches and then expect you to fill the part thats different. Pressing *TAB* twice will show the multiple matches too.

---

**cp**

  Copying files can be done in terminal itself by using "cp" command, which stands for copy.
Syntax :
> $cp myfile /home/anish/Desktop/  //copies file named myfile to location /home/anish/Desktop/

  One can copy files, folders and also use wildcards. Wildcards are symbols that can be used in place of other charachters to make up a pattern. This helps in searching files. They can be used be any command.
|----|-------------------------------------------|
|*   |Represents any charachter/s of a string    |
|?   |Represents a single charachter             |
|[]  |Represents any charachters between brackets|

> $cp *.jpg /home/anish/Pictures/

This copies all jpg files in current directory to a new location
To copy a folder holding many files, we cannot do a simple cp. A flag "-r" which stands for recursively must be used along with cp.
> $cp -r myfolder /home/anish/Documents/

By default, cp replaces file with same file name in new location. So to avoid being overwritten, use the "-i" flag ie interractive to prompt the user.

---

**mv**

  Used to move files and folders to different locations and also maybe rename them. mv stands for move
Syntax :
> $mv file location

Same flags used in cp command can be used here.
|Syntax                                     |Action                                                                                               |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|
|$mv myfile /home/anish/Documents/          |Move myfile to new location ie /home/anish/Documents/                                                | 
|$mv myfile1 myfile2 /home/anish/Documents/ |Moves myfile1, myfile2 to new location ie /home/anish/Documents/                                     |
|$mv oldfile newfile                        |Renames oldfile to newfile                                                                           |
|$mv dir1 dir2                              |Renames directory dir1 to directory dir2                                                             |
|$mv -b dir1 dir2                           |Renames directory dir1 to directory dir2 and moves dir1 content to dir2 while keeping backup at ~dir2|

---

**mkdir**

  To make new directories, use "mkdir" command which stands for make directory.
Syntax : 
> $mkdir folder1

Multiple directories can be made too. Also subdirectories can be made at same time using the "-p" ie parent flag
> $mkdir -p folder1/child1/child1_1

---

**rm**

  To remove files in Linux, use the "rm" command. But once deleted there's no way of getting them back. One protection against accidently deleting important files is that if the files are write-protected then they won't be deleted by normal rm command. For that "-f" flag, which stands for force is to be used.
Syntax :
> $rm file1
> $rm -f file1    // to remove any file, even if write protected, forcefully without any prompt
> $rm -i file1    // will prompt the user to confirm delete before doing so

To delete folders, there's 2 ways :
> $rm -r folder1   // recursively deletes everything inside folder1
> 
> $rmdir folder1

---

**find**

  To find a file or folder within a specified folder use the "find" command. The directory to be searched in must be specified as well as the name of file must be specified using the "-name" flag. The file type can also be specified using the "-type" flag. One cool thing to know is that, the system will not just search only that folder but all the subfolders as well.
Syntax : 
> $find /home -name cat.jpg
> $find /home -type d -name myfolder     // d for directory

---

**help**

  To find more details about some command, using "--help" option with the command or "help" command is the best shot to do so. 
Syntax :
> $help echo
> $help find --help

---

**man**

  "man" command is used to get documentation of commands ie "man" command gives the manual to use a command.
Syntax : 
> $man ls

---

**whatis**

  Gives a brief description of the command. The content gets sourced from the man page and is like a quick description for any confusion on the command.
Syntax :
> $whatis cat

---

**alias**

  To avoid repetitive use of some long commands or common commands, an alias name can be given to that command which can be done using the "alias" command. This alias is temporary however and is lost upon doing a logoff. To make a permanent change, the alias needs to be added to "~/.bashrc" file. The alias can be removed using the "unalias" command.
Syntax : 
> $alias foo="ls -la"
> $unalias foo

---

**exit**

  To exit from the shell use the "exit" or "logout" or close the terminal on GUI.
Syntax :
> $exit
> $logout

---
---
