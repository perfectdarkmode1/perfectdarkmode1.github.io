---
title: Shell
date: 2023-11-06T06:20:36-07:00
draft: true
---
Different Linux Shells

- Bourne-again shell (Bash)
- C shell (csh/tcsh)
- Korn Shell (ksh)
- Z shell (zsh)

View your system's hostname by running the hostname command:

```
hostname
```

2 types of commands

\- internal (~30 built in commands) (builtins)

\- External

\- reside in individual files

\- usually binary programs or scripts

\- shellusys PATH variable to find the command (the executable file)

Quoting

Double quotes

\- text in between is regular characters

\- except $ \ `

variables, command substitution and arithmetic still work

\- a space bar loses it's meaning as an argument seperator

Single Quotes

\- revoke special meaning from all characters in quotes

Escape Characters

\- takes special meaning out of characters

$ echo \\$USER

$ USER

\- .\ tells bash to ignore specialness of preceding character

Set a variable

$ $TWOWORDS

2.1

Variables

Local Variable

\- available to the current shell process only

\- Not accessible to other programs

Environment Variables

\- available in shell session and sub processes

\- usually in capital letters

\- all variables are set when shell is started

Config: Local variables

$ greeting=hello

$ echo $greeting

hello

Remove variable

$ unset greeting

Config: Global Variables

$ greeting=hello

$ export greeting

or

$ export greeting=hello

Use variable in front of a command

$ TZ=EST date

$ TZ=GMT date

Display all environment variables

$ env

The PATH Variable

\- stores a list of directories that have executable commands

append new directory to PATH

$ PATH=$PATH:new_directory

append new directory to PATH using another variable

$ mybin=/opt/bin

$ PATH=$PATH:$mybin

which = find out how shell invokes a specific command

$ which nano

Using the command line to get help

/usr/share/doc/

\- stores most documentation

Display quick help options

$ bash --help

Man

categories

1 user command

2 system calls

3 functions to the c library

4 drivers and device files

5 configuration files and file formats

6 games

7 misc

8 system administrator commands

9 kernel

\- Man page belongs to one category

\- Each category can have a man page with the same name

\- call a specific page & category

$ man 5 passwd

\- otherwise man will select 1st available (passwd(1))

\- uses less to display content

\- Search man page (while it is displayed)

\ search_word

\- searching forward

$ search-word

\- searching backward

type N

\- jump to next match

type H

\- see other features

Info pages

$ info mkdir

\- place cursor on hyperlinks & press enter to visit them

/usr/share/doc

\- contains directory for most packages installed on the system

\- each one contains README or readme.txt

\- can also contain changelog, etc.

Locating files

$ locate word

\- searches database for matching string

\- database is managed by updatedb

can run updatedb to manually update the database

The find command

\- searches directory tree recursively

\- requires search path

$ find . -name myfile

Using directories and Listing Files

$ sudo apt install tree

$ tree

Shows current directory and sub directories

File and directory names

Navigating the Filesytem

Special relative paths

$ ls -a

\- also shows hidden files and directories

. indicates current location

.. indicates parent directory

$ cd ../..

\- can be used to navigate up the file tree very quickly

Using directories and Listing Files Part 2

$ tree -L 1 /

\- shows only first column of thre root directory tree

FHS (Filesystem Hierarchy Standard)

\- Defines standards of standard directory locations

\- changes made in root filesystem effect all users

\- will also require admin

$ su - michael

\- switch user

ls ~michael

\- ls the home directory of a user (if you have permissions)

Hidden files

\- begin with .

\- often used to set user-specific configuration settings

Additional ls Options

l: Long

h: Human readable

d: directories without contents

t: modification time

r: reverse sort

X: file eXtension

S: size

R: Recursive (run ls here and then repeat the command in every subdirectory you find)

Recursion in Bash

\- when something is defined in terms of itself

$ du -h

output a list file size of all files, directories, and subdirectories for a certain location

Creating, Moving, and Deleting Files

globbing

\* matches any character including no character

? matches any one character

\[\] matches a class of characters

$ ls file \[1-35-6a-c\]

can use multiple ranges

$ \[1a5\]

match certain characters

$ \[^a\]

match everything but a

Character class

ls file \[\[:digit:\]\]

match everything in the digit class

ls file \[\[:digit:\]a\]

match digit or a

\[:alnum:\]

letters and numbers

\[:alpha:\]

upper or lowercase letters

\[:blank:\]

spaces and tabs

\[:cntrl:\]

control characters (backspace, bell, NAK, escape)

\[:digit:\]

Numerals

\[:graph:\]

Graphic characters (all characters except ctrl and space)

\[:lower:\]

lowercase letters

\[:print:\]

printable characters (alnum, punct, and space)

\[:punct:\]

Punctuation (!, &,")

\[:space:\]

whitespace characters (tabs, spaces, newlines\]

\[:upper:\]

Uppercase letters

\[:xdigit:\]

Hexadecimal numerals
