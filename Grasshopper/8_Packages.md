Our system is comprised of many packages like internet browsers, text editors, etc. These packages are managed by "**package managers**", which install and maintain the software on the system.
> Don't always need package managers to install all packages. Some can be directly installed using the source code.

The most common variety of packages are Debian \(.deb\) and Red Hat \(.rbm\). Debian style packages are for distributions like Debian, LinuxMint, Ubuntu, etc while Red Hat style packages are seen in Linux, CentOS, Fedora, etc.

Packages technically are just lots and lots of files compiled into one unit. The developers who develop the software, compile them and document how to use them are called "upstream providers". When the newer or updated packages are ready to be released, they are sent to "package maintainers" who handle getting the software into user hands. The package maintainers review, manage and distribute the software as packages.

While we can install each and every package that we need in the system, the task can be tedious. So there's "**package repositories**" which are a central storage location of packages. All these repositories can be found on internet. The machine needs to be told where to look for repositories. For example, let's say we want WackyWidgets Software on the system. Well WackyWidgets manages their own repositories for their widget packages, inside this repository are 10 packages, the CoolWidget package, the SuperWidget package, etc. WackyWidgets hosts this repository at a source link called: http://download.widgets/linux/deb/ . Now instead of going to their website to download the package directly, we can tell the system to find WackyWidgets software from the source link. Our distribution already comes with pre-approved sources to get packages from and this is how it installs all the base packages in our system. On a Debian system, this sources file is the /etc/apt/sources.list file. The system will check that location for any source repositories that we add.

An archive is a collection of files. It's like a single file comes with multiple files inside it \(like .rar, .zip, .gz\). 
"**gzip**" is the program used to compress files in Linux. The compressed files end with ".gz" extension. To compress a file down:
> $gzip filename

To decompress the file:
> $gunzip filename.gz

"gzip" cannot archive multiple files. Instead, we use the "**tar**" program. "tar" program can archive multiple files in an archive which will have ".tar" extension.
> $tar cvf archiveName.tar file1 file2

The "c" flag stands for create, "v" flag stands for verbose \(ie informs program to tell us what it is doing\) and "f" flag stands for file name of archive which comes immediately after this flag.
To extract the contents of the file, where "x" stands for extract:
> $tar xvf archiveName.tar

Archives usually get compressed as well. These can be noticed with the ".tar.gz" extension at the end of archive names. One option is to first decompress using "gunzip" and the extract using "tar". But both of these things can be done in tar command by using the "z" flag \(which stands for zee files\) instead of "v" flag. The "z" flag tells "tar" to use "gzip" or "gunzip" utility.
> $tar czf archivename.tar.gz file1 file2
>
> $tar xzf archivename.tar.gz

😁[Joke](https://xkcd.com/1168/)

> Note : Tar is one of the most important commands in linux. Use man page to see more functionalities.

There are other archive and compression types too like bzip2, compress, zip, unzip, etc which will require different commands but these are not very common in Linux.

