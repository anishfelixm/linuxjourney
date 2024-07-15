When a device is connected to a system, it needs a device driver to function properly. In Linux, one can interact with the device drivers using "**device files**" or "**device nodes**" which are just some special files used for this purpose. They work like regular files and so one can use normal linux commands to work with them. These "device files" are stored in "**/dev**" directory and each device driver will have it's own file here. To see the device files:
> $ls /dev

We have already seen "/dev/null" in "stderr". When output is sent to "/dev/null", it kernel knows that the device takes all the input, discards it and returns nothing. In past, one would have to add the device files in "/dev". But over a long run this becomes a problem. Also device drives were assigned files in the order that kernel finds them. So after re-booting, the device could be given different device file. Nowadays, we use a dynamic method of adding and removing devices that are being used in the system.

