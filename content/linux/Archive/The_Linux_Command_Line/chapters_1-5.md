What is the shell?

\# prompt = superuser

Display current time/date
```
$ date
```

Calendar
```
$ cal
```

see disk space
```
$ df
```

See free memory

```
$ free
```

Close Terminal
```
$ exit
```
or
```
ctrl+d
```

Navigation

single files tree regardless of drives/ storage devices

## absolute pathnames

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

Exploring the system

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

File Access Rights

\- rw- r-- r--

type of file | file owner | group | everyone else

Determine file type

$ file filename

\- brief description of file's contents

View text files

less

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

Search the next occurance of the previous search

h

Display help screen

q

Quit less

pagers

programs that allow the easy viewing of long text documents in a page-by-page manner

Take a guided tour

\- you can doubleclick a filename to copy it and middle click to paste

\- enter reset to clear a messy terminal

Directories

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

Symbolic Links

soft link (symlink)

file referenced by multiple names

\- used for version change

\- don't have to point programs to new file

\- can revert link if newer version has a bug

Hard Links

\- allow files to have multiple names

Chapter 4: Manipulating Files and Directories

copy only files that do not exist in the destination directory or are newer than the versions in the destination directory.

$ cp -u *.html destination

## Wildcards

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

mkdir

$ mkdir dir1 dir2 dir3

cp

copy files or directories

$ cp item1 item2

$ cp item.. dir

cp options

-a, --archive

copy files and directories and their attributes
