<p style="text-align: center;">
  
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

Packages usually don't work by themselves and have dependencies to help them run. These dependencies can be other packages or shared libraries. Shared libraries are just libraries of code that packages use to avoid rewriting lots of code. It's essential to have the dependencies in the system for the package to run. Just like how ".exe" is a single executable file, so is "**.deb**" and "**.rpm**". If we use package repositories, we may not see these files but if we directly download then we will see these formats. ".deb" is exclusive for Debian based and ".rpm" is for Red Hat based distribution. To install these direct packages, use the "**rpm**" and "**dpkg**" commands. These tools will install the package files, but they won't install the dependencies, each of which we will have to install separately. To install a package, where "-i" stands for instal \(--install is discontinued\):
> $dpkg -i package_name.deb
>
> $rpm -i package_name.rpm

To remove a package, where "-r" stands for remove and "-e" stands for erase:
> $dpkg -r package_name.deb
>
> $rpm -e package_name.rpm

To list installed packages, where "-l" stands for list, "-q" stands for query and "-a" stands for all:
> $dpkg -l
>
> $rpm -qa

Two most popular package management systems are "**yum**" and "**apt**". Package managers come with all fixins that make package installations, removal and changes easier including installing package dependencies. "yum" is exclusive for Red Hat family while "apt" is exclusive to Debian family. To install a package from a repository:
> $apt install package_name
>
> $yum install package_name

To remove a package:
> $apt remove package_name
>
> $yum erase package_name

To update package for a repository:
> $apt update; apt upgrade
>
> $yum update

To get information about an installed package:
> $apt show package_name
>
> $yum info package_name

Sometimes, the software package comes as raw source code. These source code package have to be compiled and then install a package on the system manually \(using some commands, ofc\). Firstly, we need the software that we need to install our tools to compile the software. So:
> $sudo apt install build-essential

Then we will need to extract the contents from the package. So:
> $ tar -xzvf package_name.tar.gz

Sometimes these will have README or INSTALL files inside the extracted file. It's important to read these before proceeding as they might have more specific instructions. The compile method depends on what the developer used, like cmake or make, etc. Usually a simple make compilation is enough. Inside the package, there will be a "**configure**" script. This script will check for dependencies on the system and upon running the script if any dependency is missing, it will show up as an error. To run the script in the current directory:
> $./configure

Inside the package, there usually will be a file called "**Makefile**" which contains the rules to building the software. Running the "make" command will get the system to take a look at this file to build the software.
> $make

Then doing a "**make install**" will actually install the software. It copies the correct files to the correct locations on the system.
> $sudo make install

To uninstall the package, use:
> $sudo make uninstall

It's necessary to be careful while using "make install". There are a lot of processes going on in the background. So in case we remove the package, everything that was added to the system may not be removed as we don't know what was added to the system. Instead it's safer to use the "**checkinstall**", which will use the "make install" and then create a ".deb" package which we can easily install and uninstall. This makes it easier to install and uninstall the package.
> $sudo checkinstall

---
---
