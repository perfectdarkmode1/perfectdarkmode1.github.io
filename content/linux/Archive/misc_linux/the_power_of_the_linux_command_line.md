---
title: Symbols in Bash
date: 2023-11-06T06:20:36-07:00
draft: true
---
3.1 Archiving Files on the Command Line

2 types of compression

lossless

\- can be decompressed back to original form

\- bzip2, gzip, and xz

\- file compressed with one tool can't be decompressed by another

lossy

\- cannot be recovered

\- used for images, video, and audio

Archiving

\- tools that are used to bundle files and directories into a single file.

\- can install zip and unzip for working with windows files

bzip2/ bunzip2 (.bz)

gzip/ gunzip (.gz)

gzip -9 bigfile

\- set the level of compression to 9

-

xz/ unxz (.xz)

xz -9 file

\- set the compression level

compression level: the higher the number the more compression and smaller file size

Reading compressed files without uncompressing

tools are prefixed: cat, grep, less, diff, more, etc.

z prefix for gzip

bz prefix for bzip2

xz prefix for xz

Example: zcat file.gz

Archiving tools

TAR (tape archive)

\- files created with TAR are often call tar balls

Options:

c: create a new archive file

f: name of the file to create

v: output names of files operated on

$ tar cf archiving/3.1.tar compression

\- adding the directory “compression” and all of it's contents to the archive

$ tar -tf 3.1.tar

\- view contents of a tar ball

$ tar xf 3.1.tar (you don't need the - with tar options)

\- extract the file

$ tar xvf 3.1.tar compression/hosts.gz

\- select which file to get from the archive

\- files save the path when archived

Compressing tar files at the same time

bzip2; j

xz: J

gzip: z

u: add file to an uncompressed archive

Supporting wildcards

$ tar xf tarfile.tar --wildcards dir/file*

\- when using no dash

or

$ tar --wildcards -xf tarfile.tar dir/file*

Managing ZIP files

$ zip -r zipfile.zip dir

\- zips the directory (makes a zipped copy?)

$ unzip zipfile.zip

\- unzip

Options

r: include directories contents

#: (0-9) Change compression level

Searching and Extracting Data from Files

Standard Input

\- stdin

\- channel 0

\- keyboard

Standard Output

\- stdout

\- channel 1

\- Screen

Error Output

\- stderr

\- Channel 2

I/O redirection

redirecting standard output

Redirecting standar error

\- use 2> because the channel must be specified

$ find /usr games 2> text-error

Bit Bucket

\- file that accepts input and does nothing with it

\- /dev/null

Redirecting Standard Input > <

\- usually used with commands that don't accept file arguments

tr

\- used to translate file contents by modifying the characters in a file in specific ways like deleting a character from a file

$ tr -d “l” < text

\- deletes l from the text

Here Documents

<<

\- represents the block of code or text which can be redirected to the command or the interactive program.

\- bash, sh, and csh are able to take input directly from the command line

I do not get this

Read cat man page

Combinations

&\> and &>>

\- combines channel 1 and 2 (standard output and standard error)

Cut

\- cuts specified fields from the input file by using the -f option,

d: lets the command find the feild using a delimeter

$ cut -f 3 -d “/” newfile

Command Line Pipes

wc options:

w: count the words

l: count the lines

c: count the bytes

3.2 Lesson 2

Grep (global regular expression print)

\- search within files for the specified pattern

\- outputs the line containing the specified pattern highlighted in red

$ grep bash /etc/passwd

or

$ grep “bash” /etc/passwd

Options:

i: search case insensitive

r: recursive

c: counts number of matches

v: invert, lines that do not match search term

E: extended regular expressions (needed for advanced meta-characters like |, + and ?)

Regular expressions

\- every character counts

\- string: specific sequence of characters

\- matches ASCII symbols (letters, digits, punctuation, etc.)

\- Matches Unicode characters for any other type of text.

.

match any single character except newline

\[abcABC\]

match any one character within the brackets

\[^abcABC\]

match any one character except the ones in the brackets

\[a-z\]

Match any character in the range

\[^a-z\]

Match any character

sun|moon

Find either of the listed strings

^

Start of a line

$

End of a line

$ grep “ab” text.txt

\- searches for exact string, anywhere in the line

$ grep “\[ab\]” text.txt

\- searches for sets of characters that contain any of the characters between the brackets

\- any line that has an a or ‘a’ 'b' in it

$ grep “^a” text.txt

\- searches for any line that begins with 'a'

$ grep "2$" text.txt

\- searches for any line that ends with a “2”

Meta characters (enables multiplication of the previously specified pattern) (Extended expressions?)

*

\- Zero or more of the preceding pattern

+

\- one or more of the proceding pattern

?

\- Zero or one of the preceding pattern

|

\- match one of the following “tree|bark|bowl”

$ grep -E “ab.+” text.txt

\- searches for a string that contains 'ab', a single character and one or more of the characters previously found

\- E option used because of the extended regular expression “+”

sed

\- command to find and replace characters or sets of characters within a file.

3.3 Turning Commands into a script

Commands and PATH

$ which ls

\- find location of ls

$echo $PATH

\- show PATH ariable

\- shows all the directories in PATH

Two ways to use a script file as a command

1\. Add the directory and to PATH

2\. Add the file to PATH

3\. specify current location with ./ in front of the command

You must also give the command executable permissions

$ chmod +x new_script

\- gives file executable permissions for all users

bang line (shebanhg)

\- specifies the type of interpreter to use in the first line of a script

$which bash

/bin/bash

#!/bin/bash

\- tells system to use bash

#

\- used to write a comment

Labeling

\- included at the end of bash scripts to identify them easily

\- this does not effect functtionality in any way

.sh for bash

.bash for bash

.py for python

Vi

\- vim adds some functionality to Vi but the interface is the same

3 different modes

Navigation Mode

H,J,K and L to navigate

press esc from insert mode to return to navigation mode

Insert mode

\- press "I" from navigation mode to enter insert mode

\- type normally

Command mode

\- press : from navigation mode to enter command mode

\- Save, delete, quit or change options

nano

\- does not have different modes

\- can begin typing on startup

\- use “ctrl” to acces tools printed at bottom of screen

Variables

\- You can modify and add environment variables

\- Variable names must contain only alphanumeric

\- case sensitive

\- variable can also be put in brackets ${username}

\- implicit type

\- considered strings

Use " to put spaces in variable value

username="carol smith"

" (weak)

allows interpreter to perform substitution inside the quotes

' (strong)

prevent any substitution from occuring

Arguments

$1

\- first argument

$ ./new_script.sh Carol

\- assigns Carol as the first argument

\- can go up to $9
