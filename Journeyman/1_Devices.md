When a device is connected to a system, it needs a device driver to function properly. In Linux, one can interact with the device drivers using "**device files**" or "**device nodes**" which are just some special files used for this purpose. They work like regular files and so one can use normal linux commands to work with them. These "device files" are stored in "**/dev**" directory and each device driver will have it's own file here. To see the device files:
> $ls /dev

We have already seen "/dev/null" in "stderr". When output is sent to "/dev/null", it kernel knows that the device takes all the input, discards it and returns nothing. In past, one would have to add the device files in "/dev". But over a long run this becomes a problem. Also device drives were assigned files in the order that kernel finds them. So after re-booting, the device could be given different device file. Nowadays, we use a dynamic method of adding and removing devices that are being used in the system.

To look at more details of devices:
> $ls -l /dev
>
> brw-rw----   1 root disk      8,   0 Dec 20 20:13 sda
>
> crw-rw-rw-   1 root root      1,   3 Dec 20 20:13 null
>
> srw-rw-rw-   1 root root           0 Dec 20 20:13 log
>
> prw-r--r--   1 root root           0 Dec 20 20:13 fdata

The columns are as follows:
| Permissions | Owner | Group | Major Device Number | Minor Device Number | Timestamp | Device Name |
|-|-|-|-|-|-|-|

The first bit in "ls" command here will tell the type of file. Device files are denoted as:
+ b : block

These devices transfer data in large fixed-sized blocks. Mostly has devices that utilize data blocks as block devices, such as harddrives, filesystems, etc.
+ c : charachter

These devices transfer data one a character at a time. There will be a lot of pseudo devices \(/dev/null\) as character devices and devices aren't really physically connected to the machine, but they allow the operating system greater functionality.
+ s : socket

Socket devices facilitate communication between processes, similar to pipe devices but they can communicate with many processes at once.
+ p : pipe

Named pipes allow two or more processes to communicate with each other. These are similar to character devices, but instead of having output sent to a device, it's sent to another process.

Devices are charachterized using "major device number" and "minor device number". The "major device number" represents the device driver that's used \(like 8 which is used for sd block devices\) while the "minor device number" informs the kernel which unique device it is in the driver class \( like 0 which represents 1st device\).

The most common device names in Linux:
1. SCSI Devices : Most mass storage devices use the "SCSI" protocol. "SCSI" protocol stands for **S**mall **C**omputer **S**ystem **I**nterface. It's a protocol used for communication between system and other peripherals like dics, printer, etc. Linux system corresponds SCSI disks with hardrive disks in /dev. These disks are prefixed with "sd", which stands for  SCSI disk. Common SCSI disk files are "/dev/sda" \(First hard disk\), "/dev/sdb" \(Second hard disk\), "/dev/sda3" \(Third partition on First hard disk \).
2. Pseudo Devices : These devices aren't physically connected to the system. Common pseudo devices are usually "charachter" devices like "/dev/zero" \(accepts and discards all input, produces a continuous stream of NULL bytes\), "/dev/null" \(accepts and discards all input, produces no output\), "/dev/random" \(produces random numbers\).
3. PATA Devices : In older devices, hardrive devices are prefixed with "hd" like "/dev/hda" \(First hard disk\), "/dev/hdd2" \(Second partition on 4th hard disk\).

"**sysfs**" was created to better manage devices on the system which "/dev" fails to do. "sysfs" is a virtual filesystem that's mounted to the "/sys" directory. It gives more information about devices in the "/dev" directory. While "/dev" and "/sys" seem to be similar, they actually have major differences. "/dev" is a simple file system which allows other programs to access devices while "/sys" filesystem is used to view information and manage the devices. The "/sys" filesystem basically contains all the information for all devices on your system, such as the manufacturer and model, where the device is plugged in, the state of the device, etc. These files aren't device nodes, so we don't interact with devices from the "/sys" directory, rather managing devices. To look at "/sys" directory:
> $ls /sys/block/sda

In the past, "mknod" was used to create device files in "/dev". We would have to specify device type \(like "b"\) and then major and minor number. To remove device we would have to "rm" device file from "/dev".
> $mknod /dev/sdb1 b 8 3

But nowadays, we use the "**udev**" command. "udev" system dynamically creates and removes device files depending on whether or not they are connected. There is a "udevd" daemon which is constantly listening any messages from kernel about any devices connected to system. "Udevd" will parse that information and it will match the data with the rules that are specified in "/etc/udev/rules.d", depending on those rules it will most likely create device nodes and symbolic links for the devices. One can write the own "udevd" rules, but "udevd" rules mostly cover everything and there's no need to do so. To view the "udev" and "sysfs" database, use the "udvadm" command.
> $udevadm info --query=all --name=/dev/sda

To list information about devices:
> $lsusb  -\> usb devices
>
> $lspci  -\> pci devices
>
> $lsscsi  -\> scsi devices

