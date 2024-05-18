---
title: Text Editors
date: 2023-11-06T06:20:36-07:00
draft: true
---
stdout (Standard Out)

I/O (input/output streams)

$ echo Hello World  \> Peanuts.txt

Writes Hello World to a new file called Peanuts.txt

Processes use I/O streams to receive input and return output.

echo takes the input of the keyboard and returns it as output to the screen. > Is an I/O redirection operator that changes where the standard output goes. if the file already exist the contents will be overwritten.

$ echo Hello World >> Peanuts.txt

>\> is used to add the output to the end of the file instead of overwriting it. This will also create Peanuts.txt if it doesn't already exist.

stdin (Standard In) <

cat &lt; peanuts.txt &gt; banana.txt

inputs cat to peanuts.txt and outputs to Banana.txt

stderr (Standard Error)

$ ls /fake/directory > peanuts.txt

trying to ls a directory that doesn't exist

Output: ls: cannot access /fake/directory: No such file or directory

This does not output to peanut.txt because you cannot output a stderror the same way as stdout.

Use a file descriptor to do this. This is a non-negative number that is used to access a file or stream.

The file descriptor for stdin, stdout, and stderr is 0,1, and 2 respectively.

Redirect stderr to a file

$ ls /fake/directory 2> peanuts.txt

To see both stderr and stdout in a file

$ ls /fake/directory > peanuts.txt 2>&1

There is a shorter way to redirect both stdout and stderr to a file

$ ls /fake/directory &> peanuts.txt

To get rid of stderr messages completely

$ ls fake/directory 2> /dev/null

redirects output to /dev/null

pipe and tee

$ ls -la /etc | less

| allows us to take the stdout of a command and make that the stdin to another process.

$ ls | tee peanuts.txt

tee writes the output to two different streams.

env (Environment)

Environment variables store info to variables in your specific user environment.

$ echo $HOME

Shows what is stored in the HOME variable

$ echo $USER

Shows what is stored in the USER variable

$ env

Shows all environment info used by shell and other processes

You can access a variable by placing $ in front of it like the above examples

The system will check the paths in the PATH variable for the command you are trying to run. If it is not in any of those paths then it will not find the command. If you downloaded a tool and place the commands in a path not listed then it will not find the tool when you run the command. You can include other paths in this list.

cut

$ cut -c 5 file.txt

outputs the 5th character in each line of file.txt space also counts as a character.

$ cut -f 2 file.txt

-f flag sorts by fields. Fields are separated by tabs. So this would output the field after the first tab which is the second field.

$ cut -f  1 -d ";" file.txt

Changes tab delimiter to a ; delimiter

paste

$ paste -s file2.txt

combines file2.txt into one line using tabs to separate. -s makes everything go on one line.

$ paste -d ' ' -s file2.txt

changes the delimiter to a space

head

by default, the head command will show you the first 10 lines in a file

$ head /var/log/syslog

shows the first 10 lines in /var/log/syslog

$ head -n 15 /var/log/syslog

-n flag is for number of lines, this would output 15 lines. You can output as many lines as you want.

tail

Shows last 10 lines of file by default

$ tail /var/log/syslog

$ tail -n 15 /var/log/syslog

Shows 15 lines instead of 10

$ tail -f /var/log/syslog

-f will follow the file as it grows

Expand and Unexpand

$ expand sample.txt

converts any tabs in the file to a series of spaces.

$ expand file.txt > spacefile.txt

put that output into a new file

$ unexpand -a result.txt

converts spaces back to tabs

Join and Split

$ join file1.txt file2.txt

Joined via matching list fields

-1 refers to file3.txt -2 refers to list2.txt and specifies the field from each file that you want.

$ split somefile

splits into different files by default it will split them once they reach a 1000 line limit. The files are names x** by default

sort

useful for sorting lines

$ sort file.txt

Sorts file in alphabetical order

$  sort  -r file.txt

-r flag reverses the order of the sort

$ sort -n file.txt

sorts by numerical value

tr (Translate)

allows you to translate a set of characters into another set of characters

$ tr a-z A-Z

hello

HELLO

uniq (Unique)

Useful tool for parsing text.

$ uniq reading.txt

Outputs contents of reading.txt without duplicates.

$ uniq -c reading.txt

Outputs a count of each word

$ unique -u reading.txt

Outputs only unique words

$ unique -d reading.txt

Only outputs duplicate values

This will not detect duplicate lines if they are not adjacent

To overcome this limitation:

$ sort reading.txt | uniq

This will output duplicated because the sort puts all of the duplicates together first.

wc and nl

The wc (word count) command shows the total count of words in a file

$ wc /etc/passwd

Output: 96  265  5925 /etc/passwd

displays number of lines, number of words, and number of bytes respectively

To just see the count of a certain field, use the -l, -w, or -c respectively

$ wc -l /etc/psswd

$ nl file.txt

shows number of lines in the file

grep

Allows you to search files for characters that match a certain pattern. Like if a string is in a certain file or file in a certain directory.

$ grep fox sample.txt

looks for fox

$ grep -i somepattern somefile

looks for patterns that are case insensitive

$ env | grep -i User

Grabs User from env without needing CAPS for USER variable

$ ls /somedir | grep '.txt$'

returns all files ending with .txt in somedi
