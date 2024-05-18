---
title: ls
date: 2023-11-06T06:20:36-07:00
draft: true
---
Options
- -l long listing
	- file type, permissions, link count, owner, group, size, date and time of last modification, and name of the file
- -a Include hidden files and directories  
- -d listing of the specified directory but hides its contents
- -h file sizes shown in human-friendly format
- -t sorted by date and time with the newest file first
- -r oldest file first (reverse)
- -R Lists contents of the specified directory and all its subdirectories (recursive listing)

Column 1: 
	The first character (hyphen or d) divulges the file type, and the next nine characters (rw-rw-r--) indicate permissions.
Column 2: 
	number of links
Column 3: 
	owner name
Column 4: 
	owning group
Column 5: 
	file size in bytes. For directories, this number reflects the number of blocks being used by the directory to hold information about its contents.
Columns 6, 7, and 8: 
	month, day, and time of creation or last modification
Column 9: 
	name of the file or directory
