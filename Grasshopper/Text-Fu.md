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

  
