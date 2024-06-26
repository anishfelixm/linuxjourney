**Processes** are programs that are running on the machine. They are managed by the kernel and each process has a **process ID** or **PID**. The PID is assigned in the order of process creation. To see the list of running processes, use the "**ps**" command. 
> $ps

The output shows a table on terminal with the following columns:
|PID|TTY|STAT|TIME|CMD|
|-|-|-|-|-|
|Process ID|Controlling terminal|Process status code|Total CPU Usage time|Name of executable/command|

The man page of "ps" would show a lot of options for "ps" command. These vary based on what we use ie BSD, GNU or Unix. BSD is most popular option. The difference in these is just the amount of dashes, flags and gaps. 
> $ps aux

This is more popular way of seeing the process. The "a" flag shows all processes running on system, including those run by other users. The "u" flag shows more details of each process. The "x" flag shows all processes that don't have a TTY associated with it and instead will show"?" as TTY of the process. This is common for daemon process which are part of system startup and maintanance. The output of "ps aux" shows a lot more fields. These are :
+ USER: The effective user
+ PID: Process ID
+ %CPU: CPU time used divided by the time the process has been running
+ %MEM: Ratio of the process's resident set size to the physical memory on the machine
+ VSZ: Virtual memory usage of the entire process
+ RSS: Resident set size, the non-swapped physical memory that a task has used
+ TTY: Controlling terminal associated with the process
+ STAT: Process status code
+ START: Start time of the process
+ TIME: Total CPU usage time
+ COMMAND: Name of executable/command

The most useful fields usually are PID, STAT, COMMAND. 
Another very important command is "**top**". This gives real time information of processes running on system and by default it refreshes every 10 seconds. This is useful to check which process is using up resources.
> $top

The TTY field shows the terminal that executed the command. There are 2 types of terminals:
1. **Regular terminal devices** - These are native terminal device which we can type into and send output to our system. But this is not same as the terminal that we are using till now. To see this, do ctrl+alt+f1. A new terminal will be seen with no graphics, this is terminal TTY1. This is a regular terminal device. Exit the terminal by ctrl+alt+f7.
2. **Pseudoterminal devices** - These terminals are the ones we use. They emulate terminals with the shell terminal window and are denoted by "PTS". The shell process is denoted by "pts/*".

Processes are usually bound to a controlling terminal. There are special processes such as daemon processes, which are used to keep the system running. They start at system boot and terminate at system shutdown. They run in background. We do not want these system processes to terminate and hence are not associated with any controlling terminal. The TTY output "?" in ps command means the process has no controlling terminal.
