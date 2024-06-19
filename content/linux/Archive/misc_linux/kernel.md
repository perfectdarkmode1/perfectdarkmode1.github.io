---
title: Linux Kernel
date: 2023-11-06T06:20:36-07:00
draft: true
---
Overview

Linux systems can be organized into 3 levels of abstraction

1 Hardware (physical Layer)

Memory, Hard disks, networking, parts, etc.

2 Kernel (Kernel Mode)

\- Process and memory management, device communication, system calls, sets up filesystem,etc.

\- Talks to hardware to make sure ut does what processes need it to do

3 User Space

\- Shell, Programs that you run, graphics, etc.

Privilege Levels (protection rings)

Kernel Mode (ring 0)

\- complete access to hardware/ controls everything

User Mode (ring 3)

\- small amount of safe memory & CPU that user has access to

System calls

allow ring 3 to access ring 0 temporarily

System calls

\- Lets user space processes request an action from the kernel

\- Allow us to read/ write a file, modify memory usage, and modify network

\- Code inside a program contains a system wrapper

\- Trap gets caught by the system call handler and references system call in the system call table

stat() system call

\- identified by syscall ID

\- Query the states of a file

\- After first switching to kernel mode, it finds your syscall # in the syscall ID table then executes the function you ran

\- Then returns to user mode

\- Process receives return status (success or error)

View syscalls that a process makes

$ strace ls

-useful for debugging

Kernel Installation

Installing and modifying kernels

\- multiple kernels can be installed

\- choose which one to boot to in GRUB

View Kernel version

$ uname -r

Print system info

$ uname

Ways to install the kernel

\- Package manager

$ sudo apt install linux-generic-lts-vivid

\- then reboot into new kernel

\- You can specify version #

\- other packages will need to be installed

\- linux headers, linux-image-generic, etc.

Update kernel version

$ sudo apt dist-upgrade

\- Upgrades all packages

Kernel Location

\- New files are added to the /boot directory when new kernel is installed

/boot

vmlinuz

\- the linux kernel

initrd

system.map

\- lookup table

config

\- kernel config settings

\- You can see which modules are loaded if you install by compiling

\- Can delete old versions if directory runs out of space (be careful!)

Kernel Modules

\- Kernel is a monolithic peice of software

Kernel Modules

\- Peices of code that can be loaded/ unloaded into the kernel on demand

\- extend functionality of the kernel without adding to core kernel code

\- Can usually add Kernel modules without rebooting

View Currently loaded modules

$ lsmod

Load a module

$ sudo modprobe bluetooth

\- modprobe tries to load module from /lib/modules/(kernel version)/kernel/drivers

\- Modules may also have dependencies that modprobe will load if needed.

Remove a module

$ sudo modprobe -r bluetooth

Load on bootup

Modify the /etc/modprobe.d directory and add a configuration profile

$ /etc/modprobe.d/peanutbutter.conf

Options: peanut_butter = module

type: almond = Kernel Parameter

Do not load on bootup

add this config file

$ /etc/modprobe.d/peanutbutter.conf

Blacklist peanut_butter
