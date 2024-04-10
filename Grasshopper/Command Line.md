  The **Shell** is a computer program which takes commands from the keyboard and sends to the Operating system to execute. System programs such as "_terminal_" or "_console_" launch a shell for you. Most Linux distributions have a shell called ***bash***, which stands for **B**ourne **A**gain **Sh**ell. There are other shell programs as well like zsh, tsh, etc.

  When a shell is opened the prompt may look like :
>pete@icebox:/home/pete $

The "$" symbol points to normal user and varying on distribution and user access other symbols may be used. There's no need to add the symbol before a command since the symbol will be there.

|**Commands**|**Application**                                |**Usage**         |**Result**                           |
|------------|-----------------------------------------------|------------------|-------------------------------------|
|echo        |Echoes back the messageto terminal             |$ echo Hello world|HelloWorld                           |
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

