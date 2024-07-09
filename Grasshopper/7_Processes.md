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

A signal is a notification to a process that something has happened. Signals are way that processes use to communicate. They are helpful in interrupt cases like:
- An user can use special termination charachters like Ctrl+C and Ctrl+Z to kill, interrupt or suspend process
- Kernel wants to notify processes that some hardware issue has occured
- Kernel wants to notify processes that some software issue has occured

When a signal is generated, it has to be delivered to the processes. Until it is delivered it's in pending state. When process is run on system, it's considered delivered. However, processes have signal masks and so they can set signal delivery to be blocked if specified. When a signal is delivered, a process can ignore the signal, or "catch" the signal and perform signal handling routine, or terminate the process, or block the signal \(depending on signal mask\). Each signal is defined by integers and named in the format "SIGxxx". Common signals are:
+ SIGHUP or HUP or 1: Hangup
+ SIGINT or INT or 2: Interrupt
+ SIGKILL or KILL or 9: Kill
+ SIGSEGV or SEGV or 11: Segmentation fault
+ SIGTERM or TERM or 15: Software termination
+ SIGSTOP or STOP: Stop

Some signals are unblockable like SIGKILL \(which destroys the process\).

There's a command to send a signal to kill/terminate the process. It's "**kill**". 
> $kill PID

PID is the Process ID of the process. By default "kill" sends a TERM or SIGTERM signal to request a process to terminate cleanly by releasing its resources and saving its state. But using flag "9" allows to run the SIGKILL signal and kill the process.
> $kill -9 PID

Difference between SIGHUP, SIGINT, SIGTERM, SIGKILL, SIGSTOP:
+ SIGHUP - Hangup, sent to a process when the controlling terminal is closed.
+ SIGINT - Is an interrupt signal, so you can use Ctrl-C and the system will try to gracefully kill the process
+ SIGTERM - Kill the process, but allow it to do some cleanup first
+ SIGKILL - Kill the process, doesn't do any cleanup
+ SIGSTOP - Stop/suspend a process

When there are multiple processes running on a system, they don't all run together at same time. Instead each process is given a "**time slice**" ie a small amount of time the process is given the CPU processing access. Then they pause for few milliseconds and another process gets the time slice. By default, this scheduling happens in "Round Robin" fashion. Each process keeps getting a time slice until processing is finished. The kernel handles the switching of processes. 
If all processes were equal, each would get the same time slice. But they aren't, so we use "**nice**" value to basically assign priority to processes so that processes are able to decide who gets the CPU. A higher nice value means less priority while lower nice value means higher priority \(think that process isn't nice to CPU and it wants to get rid of it\). The "NI" column when we use "top" command stands for "Nice" value. To change the "Nice" value, use the "**nice**" and "**renice**" command. "nice" command is to set nice value for a new process and "renice" is to update "Nice" value for existing process.
> $nice -n 5 apt upgrade
>
> $renice 10 -p PID

The "**STAT**" column when we do "ps aux" shows the states the processes are in. The following are the states a process can be in :
+ R: running or runnable, it is just waiting for the CPU to process it
+ S: Interruptible sleep, waiting for an event to complete
+ D: Uninterruptible sleep, processes that cannot be killed or interrupted with a signal
+ Z: Zombie, zombies are terminated processes that are waiting to have their statuses collected
+ T: Stopped, a process that has been suspended/stopped

Everything is a file in Linux, including processes. Process information is stored in file-system known as "**/proc**". "ls /proc" will display multiple sub directories, one for each PID. 
> $cat /proc/PID/status

This gives detailed information \(state information, etc\) about the process with that PID. The "/proc" directory is how the kernel views the system.

We can control how processes run with "**jobs**". To send a process to run in background, we append the "**ampersand \(&\)**" at the end of the command. This will tell the kernel to run the process in background, allowing us to use the shell for other work.
> $sleep 1001 &

To view process sent to background, use the "jobs" command. The first column shows the Job ID, then the status and then the command. The "+" next to Job ID means it was most recent job started and "-" next to Job ID means it was the 2nd last job started.
> $jobs

To send an already running process to background, there's no need to terminate the process and start it again in background. Instead, suspend the process using Ctrl+Z and then run "**bg**" command to send to background.
> $sleep 1001
> 
> ^Z
> 
> $bg

To move a job from background to foreground we use the "**fg**" command along with the Job ID. If fg is run without any parameter, it will bring the most recent background job to foreground.
> $fg %1

To kill background process use the "kill" command with syntax similar to "fg" along with their Job Id.
> $kill %1

---
---
