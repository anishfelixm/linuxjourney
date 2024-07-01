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

A process is an instance of a running program on system \(precisely system allocation memory, CPU and I/O to make program run\). To better understand this, open "cat" on 2 different terminals \(It runs as it's waiting for stdin\). On 3rd terminal run "ps aux | grep cat". There will be 2 instances \(process\) of "cat" even though they are the same program. The kernel is in charge of the process. When process is made to run, the kernel loads the program code into memory then allocates resources and keeps tabs/status on each process. It notes:
+ Status of process
+ Resources it's using and recieving
+ Process owner
+ Signal handling
+ etc

Every process wants the system resources but it's the job of kernel to decide who gets it and how much they get. When process terminates, those resources used by that process are freed up and other processes are allocated to them.

When a new process is created, an existing process clones itself using a **fork** system call. A fork system call creates an identical child process, which gets an unique process id \(PID\) and the orignal process becomes its parent process and has Parent process ID \(PPID\). The child process can use the same program as the parent or \(more often\) use the **execve** system call to launch a new program. This system call destroys memory management set up for the process by kernel and puts a new one for the program. To see the PPID:
> $ps l

In the output of above command we can see that there's a bash process running and there's "ps l" process running whose PPID is the PID of bash process.
Since every process has a parent process, the mother of all processes is process called **init**. Every process is technically just a fork of this process. When system boots up, the kernel creates the "init" process whose PID is 1. It can't terminate unless system terminates. It has root access and runs many processes that are essential to keep system running.

A process can exit using the **_exit** system call which will free up the resources that process used to fork. When the process is ready to terminate, it let's the kernel know why it's terminating using the termination status. If termination status is 0, then it means process was successful. However, the kernel also needs the parent process to acknowledge the termination of child process to complete the termination of the process. The parent process acknowledges the termination of child process by using the "wait" system call and checks the termination status of child process. It's essential to do this since every parent process must know why the child process died.
> another way to do process termination is by using signals

- **Orphan process** : 
When the parent process dies before the child process, there won't be a "wait" system call from parent. So the kernel, makes these processes "orphans" and assigns "init" as their parent. "init" will raise the "wait" system call when these child processes terminate.

- **Zombie process** :
When the child process terminates, there's time till parent process calls "wait" system call.  The kernel makes these processes as "Zombie proceess". The resources of the child process would have been freed up but there's still an entry of child process in the process table. So zombie processes can't be killed since it's technically a "dead" process. When the parent calls "wait" system call, the zombie will disappear and this is called "reaping". If parent doesn't call "wait" then "init" will adopt them and do the "wait" call to remove the zombie. Too many zombie processes is bad, as they fill up process table and then prevent other processes from running.

