---
title: Boot
date: 2023-11-06T06:20:36-07:00
draft: true
---
#### Boot Process Overview

4 stages

1 BIOS
- initialize hardware and use POST to check hardware

2 Bootloader
- loads kernel into memory
- starts kernel w/ parameters
- GRUB is a common bootloader

3 Kernel
- initializes devices and memory
- load up the init process

4 init
- starts and stop essential service process on the system

3 major implementations of init
- Boot process: BIOS

BIOS

performs integrity checks

main goal: find the system bootloader

boots hard drive > search for boot block > look at MBR or GPT

Majority of Linux uses BIOS

MBR

located in the 1st 512 bytes of 1st sector on HD

contains code to load the program that loads the bootloader

GPT

Intended for use with EFI

UEFI > succesor to BIOS

1st sector is reserved for a “protective MBR”

Makes it possible to boot to a BIOS-based machine

UEFI

stores startup info in a .efi file

.efi is stored on EFI system partition on the hardware

EFI system partition

\- contains boot loader

Boot process: Bootloader

responsible for:

\- booting into an OS

\- selecting kernel to use

\- Specify Kernel Parameters

\- GRUB, LILO, efilinux, coreboot, SYSLINUX

View kernel parameters

enter GRUB menu on startup using ‘e’ key

\- initrd - Location of initial RAM disk

\- BOOT_IMAGE - location of kernel image

\- root - root filesystem location

kernel is often represented here by UUID or device name such as /dev/sda1

\- ro - mounts the filesystem as read-only

Boot Process: Kernel

initd vs initramfs

Initrd (initial RAM disk)

\- was used as a temporary root folder to get bootup drivers

Initramfs

\- Temporary root filesystem built into the kernel to load drivers for root filesystem

Mounting the root filesystem

\- Creates the root device and mounts thge root partition

\- Root partition is first mounted in read-only mode

\- so fsck can safely check system integrity

\- Then root system is mounted in read-write mode

\- Kernel then locates init program and executes it

Boot Process: Init

3 implementations of init

1\. System V init (sysv)

\- traditional version

\- Sequencially starts and stops processes based on startup scripts

\- state of machine is denoted by run levels

\- Each run level starts/stops machine in a different way

2\. Upstart

\- found on older Ubuntu installations

3\. Syst

\- new standard for init

\- goal oriented

\- attempts to satisfy goal's dependencies
