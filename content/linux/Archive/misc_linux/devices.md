---
title: Devices
date: 2023-11-06T06:20:36-07:00
draft: true
---
/dev directory

You can interact with device drivers through device files  or device nodes, these are special files that look like regular files. You can use ls,cat, etc to interact with them. Generally stored in /dev directory

$ ls /dev

When you send output to /dev/null, the kernal knows that this device takes all of our input and just discards it, so nothing gets returned.

Device Types

$ ls -l /dev

brw-rw----  1 root disk  8,  0 Dec 20 20:13 sda

crw-rw-rw-  1 root root  1,  3 Dec 20 20:13 null

srw-rw-rw-  1 root root  0 Dec 20 20:13 log

prw-r--r--  1 root root  0 Dec 20 20:13 fdata

The columns are as follows from left to right:

Permissions

Owner

Group

Major Device Number

Minor Device Number

Timestamp

Device Name

Device files are denoted as the following:

c - character

b - block

p - pipe

s - socket

Character Device

These devices transfer data one character at a time. You'll see a lot of pseudo devices (/dev/null) as character devices, these devices aren't really physically connected to a machine, but they allow the operating system greater functionality.

Block Device

These devices transfer data in large fixed-sized blocks. You'll most commonly see devices that utilize data blocks as block devices, such as harddrives, filesystems, etc.

Pipe Device

Named pipes allow two or more processes to communicate with each other, these are similar to character devices, but instead of having output sent to a device, it's sent to another process.

Socket Device

Socket devices facilitate communication between processes, similar to pipe devices but they can communicate with many processes at once.

Device Characterization

Devices are characterized using two numbers, major device number and minor device number.

The major device number represents the device driver that is used. The minor number tells the kernal which unique device it is in this driver class.

Device Names

SCSI Devices

Protocol used to allow communication between disks, printers, scanners, and other peripherals to your system. Linux systems correspond SCSI disks with hard disk drives in /dev. They are represented by a prefix of sd (SCSI disk)

Common SCSI device files

\- /dev/sda - first hard disk

\- /dev/sdb - Second hard disk

\- /dev/sda3 - Third partition on the first hard disk

Pseudo Devices

Pseudo devices aren't really connected to your system. Most common pseudo devices are character devices.

\- /dev/zero - accepts and discards all input, produces a continuous stream of NULL (zero value) bytes.

\- /dev/null - accepts and discards all input, produces no output

\- /dev/random - produces random numbers

PATA Devices

Sometimes in older systems you may see hard drives being referred to with an hd prefix

/dev/hda - First hard disk

/dev/hdd2 - Second partition on 4th hard disk

sysfs

A virtual filesystem, most often mounted to the /sys directory. It gives us more detailed information than what we would be able to see in the /dev directory.

The /dev directory is simple, it allows other programs to access devices themselves. The /sys filesystem is used to view information and manage the device.

/sys filesystem contains all  the information for all devices on your system, such as the manufacturer, model, where the device is plugged in, the state of the device, the hierarchy of devices, and more.

You don't really interact with devices here, you just manage them.

udev

Dynamically creates and removes device files depending on whether or not they are connected. There is a udev daemon that is running on the system and it listens for messages from the kernel about devices connected to the system. Udevd will parse that information and it will match the data with the rules that are specified in /etc/udev/rules.d. Depending on those rules it will most likely created device nodes and symbolic links for the devices. You can write your own udev rules. But comes with it's on rules by default.

$ udevadm info --query=all --name=/dev/sda

To view the udev database and sysfs

lsusb, lspci, lssci

$ lsusb

List USB devices

$ lspci

List PCI devices

$ lsscsi

List scsi devices

dd

Useful tool for converting and copying data. It reads input from a file or data stream and writes it to a file or data stream.

$ dd if=/home/pete/backup.img of=/dev/sdb bs=1024

This command is copying the contents of backup.img to/dev/sdb. It will copy the data in blocks of 1024 bytes until there is no more data to be copied.

\- if=file - input file, read from a file instead of standard input

\- of=file - Output file, write to a file instead of standard output

\- bs=bytes - Block size, it reads and writes this many bytes of data at a time. You can use different size metrics by denoting the size with a K for kilobyte, m for megabyte, etc, so 1024 bytes is 1k.

\- count=number - number of blocks to copy.

Some dd commands use the count option.

You can use dd to backup whole disk drives, restoring disk images and more.
