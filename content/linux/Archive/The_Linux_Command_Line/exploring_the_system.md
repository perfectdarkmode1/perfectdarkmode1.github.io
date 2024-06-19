cd/ ls/ less/ wildcards/ cp/ mv

\# prompt = superuser

Display current time/date

$ date

Calendar

$ cal

see disk space

$ df

See free memory

$ free

Close Terminal

$ exit

or

ctrl+d

Navigation

single files tree regardless of drives/ storage devices

absolute pathnames

begins with \ (root) & follows full path

relative pathnames

starts from working directory

how to use a relative pathname

$ cd ./bin (./ is implied)

$ cd bin

cd shortcuts

$ cd -

previous

$ cd ~username

home directory of user

# Exploring the system

specify directory to ls

$ ls /usr

multiple directories

$ ls ~ /usr

sort by modification time

$ ls -lt

reverse order

$ ls -lt --reverse

View all even hidden

$ ls -a or --all

all except for . and ..

$ ls -A

view details about the directory itself

$ ls -d or --directory (/)

display file sizes in a human readable format

$ ls -h or --human-readable

reverse order results

ls -r or --reverse

sort by file size

ls -s

sort by modification time

ls -t

# File Access Rights

\- rw- r-- r--

type of file | file owner | group | everyone else

Determine file type

$ file filename

\- brief description of file's contents

# View text files

## less

$ lesss /etc/passwd

\- press “q” to quit out of less

less commands

PAGE UP or b

Scroll back one page

PAGE DOWN or space

Scroll forward one page

Up arrow

Scroll up one line

Down arrow

Scroll down one line

G

Move to the end of the text file

1G or g

Move to the beginning of the text file

/characters

Search forward to the next occurance of characters

n

earch the next occurance of the previous search

h

Display help screen

q

Quit less

pagers

programs that allow the easy viewing of long text documents in a page-by-page manner

# Take a guided tour

\- you can doubleclick a filename to copy it and middle click to paste

\- enter reset to clear a messy terminal

## Directories

/

root

/bin

binaries that must be present for the system to boot and run

/boot

Linux kernel, initial RAM disk image (for drivers needed at boot time), and the boot loader.

/boot/grub/grub.conf or /boot/grub/menu.lst

used to configure the bootloader

/boot/vmlinuz

Linux Kernel

/dev

device nodes

list of all devices the kernel understands

/etc

Contains all system-wide configuration files

Contains shell scripts that start system services at boot

Everything is readable text

/etc/crontab

defines when automated jobs will run

/etc/fstab

table of storage devices and their associated mount points

/etc/passwd

list of user accounts

/home

where user home directorie are stored

/lost+found

used for recovery

/media

Mount points for removable media

/mnt

mount point on older systems for manually added removable media

/opt

used to install optional (commercial) software

/proc

virtual filesystem maintained by the Linux kernel

files within are peepholes into the Kernel itself

/root

home directory of the root account

/sbin

contains system binaries

programs that perform vital system tasks usually reserved for the superuser

/tmp

storage of temporary files

can be configured to empty on every reboot

/usr

very large

programs and support files used by regular users

/usr/bin

contains executables installed by your linux distro

/usr/lib/

shared libraries for programs in /usr/bin/

/usr/local

system wide programs not included with distro

/usr/local/bin

programs compiled from source code

empty unless you put something in it.

/usr/sbin

sys admin programs

/usr/share

shared data used by programs in /usr/sbin

default config files

icons

backgrounds

soundfiles

etc.

/usr/share/doc

documentation files organized by package

/var

where data likely to change is stored

databases

spool files

user mail

etc.

/var/log

log files

notable:

/var/log/messages

/var/log/syslog

may need admin to view log files

# Symbolic Links

## soft link (symlink)

file referenced by multiple names

\- used for version change

\- don't have to point programs to new file

\- can revert link if newer version has a bug

Hard Links

\- allow files to have multiple names

# Chapter 4: Manipulating Files and Directories

copy only files that do not exist in the destination directory or are newer than the versions in the destination directory.

$ cp -u *.html destination

# Wildcards

using wildcards is also known as globbing

select filenames based on patterns of characters

Meanings

*

match any characters

?

match any single character

\[characters\]

matches any character that is a member of the set characters

\[!characters\]

matches any character that is not a member of the set characters

\[\[:class:\]\]

matches any character that is a member of the specified class

Common character classes

\[:alum:\]

alphanumeric

\[:alpha:\]

alphabetic character

\[:digit:\]

numeral

\[:lower:\]

lowecase letter

\[:upper:\]

uppercase letter

Wildcard Examples

*

all files

g*

any file beginning with g

b*.txt

any file begginning with b followed by any characters ending with .txt

Data???

begins with data followed by 3 characters

\[abc\]*

begins with a, a b, or a c

BACKUP.\[0-9\]\[0-9\]\[0-9\]

begins with BACKUP followed by exactly 3 numerals

\[\[:upper:\]\]*

any beginning with an upper case letter

\[!\[:digit:\]\]*

any not beginning with numeral

*\[\[:lower:\]123\]

any ending with lowercase letter or 1, 2 or 3

Wildcards work in the GUI

nautilus (the file manager for GNOME)

select files by pressing ctrl-S and enter a file selection

pattern with wildcards and the files in the currently selected directory will be selected

Dolphin and Konqueror (file managers for KDE)

enter wildcards on the location bar

wildcards can be used on any command that accepts filenames as arguments

## mkdir

$ mkdir dir1 dir2 dir3

## cp

copy files or directories

$ cp item1 item2

$ cp item.. dir

cp options

-a, --archive

copy files and directories and their attributes

Normally, copies take on the default attributes of the user performing the copy.

-i, --interactive

prompt Before overwriting

cp will silently (meaning there will be no warning) overwrite files.

-r, --recursive

Recursively copy directories and their contents

This option (or the -a option) is required when copying directories

-u, --update

When copying files from one directory to another, only copy files that either don’t exist or are newer than the existing corresponding files n the destination directory.

-v, --verbose

Display informative messages

cp Examples

cp file1 file2

If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created

cp -i file1 file2

prompted

cp file1 file2 dir1

Copy file1 and file2 into directory dir1. The directory dir1 must already exist.

cp dir1/* dir2

copy all the files in dir1 into dir2. The directory dir2 must already exist

cp -r dir1 dir2

Copy the contents of directory dir1 to directory dir2. If directory dir2 does not exist, it is created and, after the copy, will contain the same contents as directory dir1. If directory dir2 does exist, then directory dir1 (and its contents) will be copied into dir2.

mv

file moving and file renaming

the original filename no longer exists after the operation

mv Options

-i, --interactive

prompt

If this option is not specified, mv will silently overwrite files

-u, --update

When moving files from one directory to another, only move files that either don’t exist or are newer than the existing corresponding files in the destination directory.

-v, --verbose

Display informative messages as the move is performed

mv Examples

mv file1 file2

Move file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created. In either case, file1 ceases to exist.

mv -i file1 file2

Same as the previous command, except that if file2 exists, the user is prompted before it is overwritten.

mv file1 file2 dir1

Move file1 and file2 into directory dir1. The directory dir1 must already exist

mv dir1 dir2

If directory dir2 does not exist, create directory dir2 and move the contents of directory dir1 into dir2 and delete directory dir1. If directory dir2 does exist, move directory dir1 (and its contents) into directory dir2

## rm—Remove Files and Directories

rm item...

Useful Options and Examples

-i, --interactive

Before deleting an existing file, prompt the user for confirmation. If this option is not specified, rm will silently delete files.

-r, --recursive

Recursively delete directories. This means that if a directory being deleted has subdirectories, delete them too. To delete a directory, this option must be specified.

-f, --force

Ignore nonexistent files and do not prompt. This overrides the --interactive option.

-v, --verbose

Display informative messages as the deletion is performed.

Linux do not have an undelete command

test the wildcard first with ls.

rm Examples

rm file1

Delete file1 silently.

rm -i file1

Same as the previous command, except that the user is prompted for confirmation before the deletion is performed.

rm -r file1 dir1

Delete file1 and dir1 and its contents.

rm -rf file1 dir1

Same as the previous command, except that if either file1 or dir1 does not exist, rm will continue silently.

## LN - Create Links

ln file link

Create a hard link

ln -s item link

Create a symbolic link

### Hardlinks

Cannot reference a file outside of it's own filesystem

Can't reference a directory

### Symbolic Links

Link will point to nothing if original file gets deleted

Operates like a windows shortcut

# Lab: Building a playground

#### Create Directories

cd

mkdir playground

cd playground

mkdir dir1 dir2

#### Copy files

cp /etc/passwd .

ls –l

cp -v /etc/ passwd . (with –v just to see what it does)

Overwrote first copy with no warning

To get a warning

-I option

## Moving and renaming files

Moving fun around

Vagrant@server1:~$ mv passwd fun

vagrant@server1:~$ ls

dir1  dir2  fun  playground

vagrant@server1:~$ mv dir* playground

vagrant@server1:~$ ls

fun  playground

vagrant@server1:~$ mv fun playground/

vagrant@server1:~$ ls

playground

vagrant@server1:~$ cd playground

vagrant@server1:~/playground$ ls

dir1  dir2  fun

vagrant@server1:~/playground$ mv fun dir1

vagrant@server1:~/playground$ mv dir1/fun dir2

vagrant@server1:~/playground$ mv fun dir2/fun .

vagrant@server1:~/playground$ mv fun dir1

vagrant@server1:~/playground$ ls

dir1  dir2

vagrant@server1:~/playground$ mv dir1 dir2

vagrant@server1:~/playground$ ls -l dir2

total 4

drwxrwxr-x 2 vagrant vagrant 4096 Nov  4 12:00 dir1

vagrant@server1:~/playground$ ls -l dir2/dir1

total 4

-rw-r--r-- 1 vagrant vagrant 1457 Nov  4 11:51 fun

vagrant@server1:~/playground$ mv dir2/dir1 .

vagrant@server1:~/playground$ mv dir1/fun .

vagrant@server1:~/playground$ ls

dir1  dir2  fun

## Creating hard links

vagrant@server1:~/playground$ ln fun fun-hard

vagrant@server1:~/playground$ ln fun dir1/fun-hard

vagrant@server1:~/playground$ ln fun dir2/fun-hard

vagrant@server1:~/playground$ ls -l

total 16

drwxrwxr-x 2 vagrant vagrant 4096 Nov  4 12:08 dir1

drwxrwxr-x 2 vagrant vagrant 4096 Nov  4 12:09 dir2

-rw-r--r-- 4 vagrant vagrant 1457 Nov  4 11:51 fun

-rw-r--r-- 4 vagrant vagrant 1457 Nov  4 11:51 fun-hard

Note the second field is how many hard links there are for a file. We created 3 and there is one hard link per file created by default.
