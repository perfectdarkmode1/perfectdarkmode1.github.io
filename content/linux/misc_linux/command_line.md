---
title: Command Line
date: 2023-11-06T06:20:36-07:00
draft: true
---
The Shell

A program that takes your commands from the keyboard and sends them to the operating system to perform.

Almost all Linux distros will default to the bash shell.

Shell prompt , for the most part, adheres to the following format

username@hostname:current_directory

david@David-Thomas:/$

The $ is for a normal user using bash

Some commands: (Case sensitive)

$ echo

Echo Hello World

Output: Hello World

$ date

Output: Mon Nov 30 09:57:25 MST 2020

$ whoami

Output: username

pwd (Print Working Directory)

Everything in linux is a file, all files are organized in a hierarchical directory tree. The first directory in the file system is the root directory

$pwd

Output: current directory

cd (Change Directory)

2 different ways to specify a path

Absolute Path: starts from / (root) directory

Relative path: from where you currently are /pictures etc.

$ cd /home/david/pictures

Output: changes to the above directory

$ cd Hawaii

(ran from directory above)

Output: goes to Hawaii folder in the above directory

$ cd .

(current directory)

$ cd ..

(parent directory)

$ cd ~

(home directory)

$ cd -

(previous directory)

ls (List Directories)

Lists directory contents of the current directory by default but you can specify which path you want to list the directories of.

$ ls

$ ls /home/david

ls also shows detailed information about the files and directories you are looking at.

Not all files in a directory will be visible. Filenames that start with . are hidden, you can view them with ls -a (a is for all)

-l flag will list files in long format (ls -l)

the output starting from the left shows file permissions, number of links, owner name, owner group, file size, timestamp of last modification, and file/ directory name.

$ ls -R

recursively list directory contents

$ ls - r

reverse order while sorting

$ ls -t

sort by modification time, newest first

$ ls -la

uses -l and -a flags together. Use this format to combine flags, the order doesn't usually matter but the flags are ran left to right in order.

Touch (allows you to create new empty files)

$touch mynewfile

creates a file called mynewfile

if you touch an existing file then it will update the timestamp on that file.

file

$file banana.jpg

will show a description of the file's contents.

banana.jpg: empty

mynewfile: ASCII text

cat (concatenate)

$ cat mynewfile

Output: hello

You can also cat multiple files

$cat mynewfile banana.jpg

Output: hello

This only says hello because banana.jpg is empty.

less

opens a page file of a file that you choose

$less scribble.txt

or $less \\home\\david\\scribble.txt

in the page viewer there are commands to help you navigate.

q - quit out of less

page up, page down, up and down - navigate using page and arrow keys

g - moves to the beginning of the text file

G - Moves to the end of a text file

/search - search for words in the document. Prefacing words you want to search with /

h - help with using less

history

$ history - shows previously used commands

$ !! \- runs the last used commands

ctrl-R - reverse search command, start typing the command you want and use ctrl-r to cycle through previous commands based on your search. hit enter once you have found the command you want.

$ clear - clears command prompt to a fresh one.

the history is not cleared though.

tab completion - use tab to auto complete a command.

cp (Copy)

makes a copy of files

$ cp mycoolfile /home/pete/Documents/cooldocs

copies mycoolfile to /home/pete/Documents/cooldocs

$ cp *.jpg /home/pete/Pictures

copies all files with .jpg extension to /home/pete/Pictures

$ cp -r Pumpkin/ /home/peteDocuments

if you copy a file over to a directory that has the same filename, the file will be overwritten with whatever you are copying over. You can use the -i flag to prompt you before overwriting a file.

mv (move)

Used for moving files and renaming them

Similar to cp command in terms of flags and functionality.

You can rename files like this:

$ mv oldfile newfile

move file to a different directory

$ mv file2 /home/david/Documents

move multiple files

$ mv file1 file 2 /somedirectory

rename a directory

$ mv directory1 directory2

if you mv a file or directory  it will overwrite anything in the same directory. You can use -I flag to prompt you before overwriting anything

$ mv -i directory1 directory2

to mv a file to overwrite a previous one and back up the old one use -b. It will rename the old one with a ~.

$ mv -b directory1 directory2

mkdir (make directory)

Will create a directory if it doesn't already exist.

$ mkdir books paintings

Makes multiple directories at the same time

$mkdir -p books/hemmingway/favorites

makes subdirectories with -p (parent flag)

rm (Remove)

used to delete files and directories

$ rm file1

Once files are removed they are gone for good.

Write-protected files will prompt you before deleting them. If a directory is write-protected it will also not easily be removed.

$ rm -f file1

-f flag forces rm to remove all files whether they are write-protected or not, without prompting the user (as long as you have the appropriate permissions.

$ rm -i file

-i flag will prompt you on whether or not you actually want to remove the file.

$ rm -r directory

(recursive) You can't remove a directory by default. You must use the -r flag. this will remove all files and subdirectories within a directory.

$ ir directory

You can delete an empty directory this way.

find

$ find /home -name puppies.jpg

Specify the directory you are searching, what you are searching for. This will search subdirectories as will.

$ find /home -type d -name MyFolder

This is trying to find type d (directory)

help

Used to help you with a command or check what flags are available.

$ help echo

Gives a description and options for the Echo command This format is for built in bash commands.

$ echo --help

Conventional standard if the above option does not work. Used for dev tools.

man (manual)

$ man ls

Manuals built in to most Linux operating systems. They provide documentation about commands and other aspects of the system.

whatis

Provides a brief description on what a command does.

$ whatis cat

Sourced from cat's manual page.

alias

Uses an alias for longer or frequently used commands.

$ alias foobar ='ls -la'

now you can just type foobar instead of typing ls -la

~/.bashrc

./profile in Windows Subsystem Linux

to add a permanent alias

$ unalias foobar

removes an alias

exit

$ exit

exits from the shell (completely closes the window.)

$ logout
