**stdout**

  stdout stands for standard out. Processes use I/O streams to take inputs and display output. Let's use following code to understand this better :
> $echo hello world > myoutput.txt

  By default echo takes standard input \(stdin\) from keyboard and returns standard output\(stdout\) on screen. But here we don't see the output. That's because of the ">" symbol, which stands for redirection. So the output stream, "hello world" string is redirected to a file called myoutput.txt. If this file didn't exist, then it would be created automatically. Also if the file already exists, then this results in file being overwritten. To instead redirect but append output stream to file, we use ">>" operator. So to append to same file would look like :
> $echo Bye World >> myoutput.txt

---

**stdin**

  stdin stands for standard in. Just like there are multiple output streams ie screen, files, etc; there are multiple input streams as well like keyboard, file, terminal, etc. Here the "<" operator stands for stdin redirection. Eg :
> $cat < myoutput.txt > newoutput.txt

Here the myoutput data becomes the input stream which is redirected to newoutput.txt and then cat command displays it.

---

**stderr**

  stderr stands for standard error. Along with stdin and stdout, there's another IO stream ie stderr or standard error. By default, it displays output on screen and to redirect output we need to use file descriptors. 0 -> stdin, 1 -> stdout, 2 -> stderr. So to redirect output of stderr to a file :
> $ls ./fake/directory/ 2> output.txt

  stderr is a different stream than stdin and stdout. If one wants to redirect output of both stdout and stderr to a file, then they can do either one of this :
> $ls ./fake/directory/ > output.txt 2>&1    //basically stderr is redirected to stream pointed by stdout which is the file here and both are written there
>
> $ls ./fake/directory/ &> output.txt

/dev/null is a special type of file which will discard all output.
> $ls ./fake/directory/ 2> /dev/null

---

**pipe and tee**

  Using the pipe operator, we can use the stdout stream of an operation as the stdin stream of the next operation instead of saving to a file and then doing next operation in a second operation. The pipe operator is represented by the "|" operator. One of the most useful linux kernel operators.
> $ls -al /etc | less

  To write the output in 2 different streams we can use the "tee" command.
> $ls | tee output.txt

---

**env**

  There's environment variables in an operating system, including Linux systems; which are used by processes and system to do operations. To see all the environment variables in a system, use the "env" command. 
> $env

  There are many environment variables and all of them have "$" as a prefix like $HOME, $PATH, etc. One very important variable is $PATH. For a command or package to work in linux, the kernel should be able to locate where the code of the command is located and for this it uses $PATH variable. When a command is typed, the kernel searches the binary file of the command in all locations mentioned in the $PATH. So upon adding new packages or commands and saving in different locations than usual, the path to that location must be added to $PATH in order to run that command. To just see values of some variables :
> $echo $HOME
> $echo $USER
> $echo $PATH

---
> to add tab space while using terminal, do ctrl+v + tab

---

**cut**

  To extract parts of text from a file, use the "cut" command. It has to be used along with flags like "-c", "-f", "-d". The -c flag tells to cut at the nth charachter ie :
> $cut -c 5 sample.txt  // gives 5th charachter of every line in sample.txt

  The -f flag tells to cut fields of text that is blocks of text separated by a special charachter. By default it is tab space, but can be changed using the -d flag.
> $cut -f 2 sample.txt  // gives the second block of text in sample.txt which are separated by tab space from 1st block
> 
> $cut -f 1 -d ";" sample.txt  // gives the 1st block of text in sample.txt separated from 2nd block by ";" charachter
>
> $cut -c 4-11 sample.txt  // gives the 4th to 11th charachters of every line in sample.txt
>
> $cut -c -5 sample.txt  // gives 1st 5 charachters of every line in sample.txt
>
> $cut -c 6- sample.txt  // gives all charachters from 6th charachter to end of every line in sample.txt

---

**paste**

  Similar to cat. Just attaches lines of text together. By default tab space is the delimiter, which can be changed using the -d flag.
> $paste -s sample.txt
>
> $paste -d " " -s sample.txt
>
> $paste -d "\n" try.c try.cpp   // prints content in try.c and try.cpp together separating them using a line

---

**head**

  Useful to see starting few lines of a long file. By default, it shows first 10 lines which can be changed using the "-n" flag. The "-c" flag shows number of charachters.
> $head /var/log/syslog
>
> $head -n 15 /var/log/syslog
>
> $head -c 5 /var/log/syslog

---

**tail**

  Similar to "head" command, but shows last few lines which can be adjusted using the "-n" flag. The "-f" flag stands for follow and basically keeps updating the output if the file grows ie new content is appended.
> $tail -n 5 /var/log/syslog
>
> $tail -f -n 5 /var/log/syslog

---

**expand and unexpand**

  These two commands will be used to interchange between spaces and Tab space.
> $expand sample.txt
>
> $unexpand -a sample.txt

---

**join and split**

  "join" command can be used to join to files by a common field. The data in this column must be common. If the common field has values that are not common, then those rows won't be in output.
> $join file1.txt file2.txt

  Let's say the 2nd column of file1 and 1st column of file2 is common field. Then we can use "-1" flag to set field of first file and "-2" flag to set field/column of second file, ie :
> $join -1 2 -2 1 file1.txt file2.txt

  Incase, field wasn't common it can be sorted. File can also be split into different files using "split" command. By default, it will split into files when each file reaches the 1000 line limit. The files will be named x** by default.
> $split fileName

---

