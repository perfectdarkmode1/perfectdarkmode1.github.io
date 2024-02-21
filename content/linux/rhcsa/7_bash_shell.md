# Chapter 7 RHCSA Notes - The Bash Shell

Introduction to the bash shell 
- Understand, set, and unset shell and environment variables 
- Comprehend and use command and variable expansions 
- Grasp and utilize input, output, and error redirections 
- Know and use history substitution, command line editing, tab completion, tilde substitution, and command aliasing Identify and use metacharacters, wildcard characters, pipes, and pipelines Discover the use of quoting mechanisms and regular expressions Run and control jobs in background and foreground Identify and examine shell startup files

RHCSA Objectives:
02. Use input-output redirection (>, >>, |, 2>, etc.) 
03. Use grep and regular expressions to analyze text

Regular expressions are text patterns for matching against an input provided in a search operation.

At login, plenty of system and user startup scripts are executed to set up the user environment.

bash shell is resident in the /usr/bin/bash file.

## Shell and Environment Variables
 
 - current shell 
		- Where a program is executed.
- sub-shell (child shell)
		- created within a shell to run a program.
		
- two types of variables: local (or shell) and environment. 
	local variable 
	- Private to the shell in which it is created.
	- Value cannot be used by programs that are not started in that shell. 
	environment variable
	- inherited from the current shell to the sub-shell during the execution of a program
	- value stored in an environment variable is accessible to the program, as well as any sub-programs that it spawns during its lifecycle. 
	- Any environment variable set in a sub-shell is lost when the sub-shell terminates.
	- env or the printenv command to view predefined environment variables.
	- Common predefined environment variables:
		- DISPLAY 
			- Stores the hostname or IP address for graphical terminal sessions 
		- HISTFILE 
			- Defines the file for storing the history of executed commands 
		- HISTSIZE 
			- Defines the maximum size for the HISTFILE 
		- HOME 
			- Sets the home directory path LOGNAME Retains the login name 
		- MAIL 
			- Contains the path to the user mail directory
		- PATH 
			- Directories to be searched when executing a command. Eliminates the need to specify the absolute path of a command to run it. 
		- PPID 
			- Holds the identifier number for the parent program 
		- PS1 
			- Defines the primary command prompt PS2 Defines the secondary command prompt 
		- PWD 
			- Stores the current directory location 
		- SHELL 
			- Holds the absolute path to the primary primary shell file
		- TERM 
			- Holds the terminal type value 
		- UID 
			- Holds the logged-in user’s UID 
		- USER 
			- Retains the name of the logged-in user

## Setting and unsetting variables
- export, unset, and echo to define and undefine environment variables
- Use uppercase for variables

### echo command
- restricted to showing the value of a specific variable
### env command
- Displays the environment variables only.
### printenv command
- Displays the environment variables only.
### set command
- View both local and environment variables.

## Command and Variable substitutions
- PS1 Environment variable sets what the prompt looks like.
- Default value is \\u@\\h \\W\\$
	- \\u
		- logged-in user name
	- \\h
		- System hostname
	- \\W
		- Working directory
	- \\$
		- End of command prompt
- command whose output you want assigned to a variable must be encapsulated within either backticks `hostname` or parentheses $(hostname).

## Input, Output, and Error Redirections

- Input, output, and error character streams:
	- standard input (or stdin)
		- input redirection
		- <
	- standard output (or stdout)
		- >
		- >>
			- append instead of overwrite
		- $>
			- Redirect standard error and output
	 - standard error (or stderr)
		 - >
- File descriptors:
	- 0, 1, and 2
		- 1
			- represents standard output location
	- Can use these to represent character streams instead of <, and >
- noclobber feature
	- prevent overwriting of the output file
	- set -o noclobber
		- activates the feature
	- set +o noclobber
		- deactivate the feature

## History Substitution
- Command history or history expansion.
- can disable and re-enable if required.
- Values may be altered for individual users by editing .bashrc or .bash_profile in the user's home directory.
- Three variables
	- HISTFILE
		- defines the name and location of the history file to be used to store command history,
		- default is .bash_history in the user’s home directory.
	- HISTSIZE
		- dictates the maximum number of commands commands to be held in memory for the current session.
	- HISTFILESIZE
		- sets the maximum number of commands allowed for storage in the history file at the beginning of the current session and are written to the HISTFILE from memory at the end of the current terminal session.
		- Usually, HISTSIZE and HISTFILESIZE are set to a common value.

### history command
- displays or reruns previously executed commands.
- gets the history data from the system memory as well as from the .bash_history file.
- Shows all entries by default.
- set +0 history
	- disable history expansion
- set -0 history
	- re-enable history expansion

## Editing at the Command line

### Common key combinations:
- Ctrl+a / Home 
	- Moves the cursor to the beginning of the command line 
- Ctrl+e / End 
	- Moves the cursor to the end of the command line 
- Ctrl+u 
	- Erase the entire line 
- Ctrl+k 
	- Erase from the cursor to the end of the command line 
- Alt+f 
	- Moves the cursor to the right one word at a time 
- Alt+b 
	- Moves the cursor to the left one word at a time 
- Ctrl+f / Right arrow 
	- Moves the cursor to the right one character at a time
- Ctrl+b / Left arrow 
	- Moves the cursor to the left one character at a time

### Tab completion
- Hitting the Tab key twice automatically completes the entire name.
- In case of multiple possibilities matching the entered characters, it completes up to the point they have in common and prints the rest of the possibilities on the screen.

### Tilde Substitution (tilde expansion)
- performed on words that begin with the tilde character (~).
- ~ 
	- refers to user's home directory.
- ~+
	- refers to current directory
- ~-
	- Refers to previous working directory.
- ~USER
	- Refers to specific user's home directory.

## Alias Substitution (command aliasing or alias)
- define shortcuts for commands.
- bash shell includes several predefined aliases that are set during user login.
- Shell gives precedent to an alias if an alias matches a command or program.
	- can still run the command without using the alias but preceding command with a backslash. \

### alias command
- set an alias.
- internal shell command.
### unalias command
- unset an alias.
- internal shell command.

## Metacharacters and Wildcard Characters
- Metacharacters
	- special characters that possess special meaning to the shell.
	- used in pattern matching (a.k.a. filename expansion or file globbing) and regular expressions.
	- dollar sign ($) 
		- mark the end of a line
		- Used in regular expressions
	- caret (^)
		- mark the beginning of a line
		- Used in regular expressions
	- period (.)
		- match a single position
		- Used in regular expressions
	- asterisk (\*)
		- used in pattern matching
		- wildcard character
		- matches zero to an unlimited number of characters except for the leading period (.) in a hidden filename.
		- Used in regular expressions
	- question mark (?)
		- used in pattern matching
		- wildcard character
		- matches exactly one character except for the leading period in a hidden filename.
		- Used in regular expressions
	- pipe (|)
		- send the output of one command as input to the next.
		- also used to define alternations in regular expressions.
		- Can use as many times in a command as you need. (pipeline)
		- Can be used as an OR operator (alternation)
			- this|that|other
	- angle brackets (< >)
	- curly brackets ({})
		- Used in regular expressions
	- square brackets ([])
		- used in pattern matching
		- wildcard character
		- match either a set of characters or a range of characters for a single character position.
		- order in which they are listed has no importance.
		- range of characters must be specified in a proper sequence such as [a-z] or [0-9].
		- Used in regular expressions
	- parentheses (())
	- plus (+)
	- exclamation mark (!)
		- inverse matches
	- semicolon (;)
	- backslash (\) 
	
## Quoting Mechanisms
- Disable special meaning of metacharacters
- backslash (\)
	- escape character
	- 
- single quotation (‘’)
	- mask the meaning of all encapsulated special characters.
- double quotation (“”)
	- mask the meaning of all but the backslash (\), dollar sign ($), and single quotes (‘’).

## Regular expressions (regexp or regex)
- text pattern or an expression that is matched against a string of characters in a file or supplied input in a search operation
- pattern may include a single character, multiple random characters, a range of characters, word, phrase, or an entire sentence.
- Any pattern containing one or more white spaces must be surrounded by quotation marks.

### grep command
- searches the contents of one or more text files or input supplied for a match.
- Flags
	- -i
		- case insensitive search
	- -n
		- number the lines
	- -v
		- exclude these lines
	- -w
		- find an exact match for a word
	- -E
		- match one or the other
	- -e 

## Running and Controlling Jobs in Foreground and Background
- job
	- process that is started in the background and controlled by the terminal where it is spawned.
	- assigned a PID (process identifier) by the kernel and, additionally, a job ID by the shell.
	- does not hold the terminal window where it is initiated.
	- Can run multiple job simultaneously.
	- can be brought to foreground, returned to the background, suspended, or stopped.
- job control
	- management of multiple jobs within a shell environment

commands and control sequences for administering the jobs.
- jobs 
	- Shell built-in command
	- display jobs.
- bg 
	- Shell built-in command 
	- move a job to the background or restart a job in the background that was suspended with Ctrl+z.
- fg 
	- Shell built-in command 
	- move a job to the foreground 
- Ctrl+z 
	- Suspends a foreground job and allows the terminal window to be used for other purposes

### jobs command
output
	plus sign (+) 
		- indicates the current background job and the 
	minus sign (-) 
		- signifies the previous job.
	Stopped
		- currently suspended
		- can be signaled to continue their execution with bg or fg

## Shell Startup Files
- Sourced by the shell following user authentication at the time of logging in and before the command prompt appears.
- Aliases, functions, and scripts can be added to these files as well.
- two types of startup files: 
	- 1. system-wide
		- set the general environment for all users at the time of their login to the system.
		- \located in the /etc directory
		- maintained by the Linux admin.
		- system-wide startup files for bash shell users:
			- /etc/bashrc 
				- Defines functions and aliases, sets umask for user accounts with a non-login shell, establishes the command prompt, etc.
				- may include settings from the shell scripts located in the /etc/profile.d directory. 
			- /etc/profile 
				- Sets common environment variables such as PATH, USER, LOGNAME, MAIL, HOSTNAME, HISTSIZE, and HISTCONTROL for all users, establishes umask for user accounts with a login shell, processes the shell scripts located in the /etc/profile.d directory, and so on.
			- /etc/profile.d 
				- Contains scripts for bash shell users that are executed by the /etc/profile file.
				- Files can be edited and updated.
	- 2. per-user.
		- override or modify system default definitions set by the system-wide startup files.
		- By default, two files, in addition to the .bash_logout file, are located in the skeleton directory /etc/skel and are copied into user home directories at the time of user creation.
		- .bashrc 
			- Defines functions and aliases. This file sources global definitions from the /etc/bashrc file. 
		- .bash_profile 
			- Sets environment variables and sources the .bashrc file to set functions and aliases. 
		- .gnome2/ 
			- Directory that holds environment settings when GNOME desktop is started. Only available if GNOME is installed.
		- .bash_logout
			- Executed when the user leaves the shell or logs off. 
			- May be customized
- Startup file order:
	- /etc/profile > .bash_profile > .bashrc > /etc/bashrc
- Per user settings must be added to the appropriate file for persistence.
## Labs

### Lab: View environment variables
```
env
printenv
```



### Lab: Viewing Environment variable values
1. View the value for the PATH variable
```
echo $PATH
```

2. View the value for the HOME variable
```
echo $HOME
```

3. View the value for the SHELL variable
```
echo $SHELL
```

4. View the value for the TERM variable
```
echo $TERM
```

5. View the value for the PPID variable
```
echo $PPID
```

6. View the value for the PS1 variable
```
echo $PS1
```

7. View the value for the USER variable
```
echo $USER
```

### Lab: Setting and Unsetting Variables
1. Define a local variable called VR1:
```
VR1=RHEL8
```

2. View the value of VR1:
```
echo $VR1
```

3. Type bash at the command prompt to enter a sub-shell and then run echo $VR1 to check whether the variable is visible in the sub-shell.
```
echo $VR1
```

4. Exit out of the subshell:
```
exit
```

5. Turn VR1 into an environment variable:
```
export VR1
```

6. Type bash at the command prompt to enter a sub-shell and then run echo $VR1 to check whether the variable is visible in the sub-shell.
```
echo $VR1
```

7. Undefine this variable and erase it from the shell environment:
```
unset VR1
```

8. Define a local variable that contains a value with one or more white spaces:
```
VR2="I love RHEL 8"
```

9. Define and make the variable an environment variable at the same time:
```
export VR3="I love RHEL 8"
```

10. View local and environment variables:
```
set
```



### Lab: Modify Primary Command Prompt
1. Change the value of the variable PS1 to reflect the desired information:
```
export PS1="< $LOGNAME on $HOSTNAME in \$PWD > " 
```

2. Edit the .bash_profile file for user1 and define the value exactly as it was run in Step 1.
```
vim .bash_profile
```

3. Test by logging off as user1 and logging back in. The new command prompt will be displayed.

### Lab: Redirecting Standard Input
1. have the cat command read the /etc/redhat-release file and display its content on the standard output (terminal screen):
```
cat < /etc/redhat-release
```

### Lab: Redirecting Standard Output
1. Direct the ls command output to a file called ls.out:
```
ls > ls.out
```

2. Do the same thing but using file descriptors:
```
ls 1> ls.out
```

3. Activate the noclobber feature then try the redirect feature again:
```
set -o noclobber
ls > ls.out
```

4. Deactivate noclobber
```
set +o noclobber
```

5. Direct the ls command to append the output to the ls.out file instead of overwriting it:
```
ls >> ls.out
or
ls 1>> ls.out
```


### Lab: Redirecting Standard Error
1. Direct the find command issued as a normal user to search for all occurrences of files by the name core in the entire directory tree and sends any error messages produced to /dev/null
```
find / -name core -print 2> /dev/null
```

2. Redirect both standard output and error:
```
ls /usr /cdr &> outerr.out
or
ls /usr /cdr 1> outerr.out 2>&1
# means to redirect file descriptor 1 to file outerr.out as well as to file descriptor 2.
```

3. Same as above but append to file:
```
ls /usr/cdr &>> outerr.out
```

### Lab: Show History Variables
1. View HISTFILE Variable:
```
echo $HISTFILE
```

2. View HISTSIZE variable:
```
echo $HISTSIZE
```

3. View HISTFILESIZE variable:
```
echo $HISTFILESIZE
```

### Lab: History command
1. Rune history without any options:
```
history
```

2. Display 10 entries:
```
history 10
```

3. Run the 15th command in history:
```
!15
```

4. re-execute the most recent occurrence of a command that started with a particular letter or series of letters (ch for example):
```
!ch
```

5. Issue the most recent command that contained “grep”:
```
!?grep?
```

6. Remove entry 24 from history:
```
history -d 24
```

7. Repeat the last command executed:
```
!!
```

### Lab: Tilde expansion
1. Display user's home directory:
```
echo ~
```

2. Display the current directory:
```
echo ~+
```


3. Display the previous working directory:
```
echo ~-
```

4. Display user1's home directory:
```
echo ~user1
```

5. cd into the home directory of user1 and confirm:
```
cd ~user1
pwd
```

6. cd into a subdirectory:
```
cd ~/Documents/
```

7. view directory information of the root user's desktop:
```
ls -ld ~root/Desktop
```



### Lab: Command Aliasing
1. shows all aliases that are currently set for user1:
```
su - user1
alias
```

2. Run alias as root:
```
alias
```

3. Create an alias “search” to abbreviate the find command with several switches and arguments. Enclose the entire command within single quotation marks (‘’) to ensure white spaces are taken care of. Do not leave any spaces before and after the equal sign (=).
```
alias search='find / -name core -exec ls -l {} \;'
```

4. Search with the new alias:
```
search
```

5.  create and alias by the same name as rm command but adding the -i flag:
```
alias rm='rm -i'
```

6. Run rm without using the alias:
```
\rm file1
```

7. Remove the two aliases we just created:
```
unalias search rm
```

### Lab: Wildcards and Metacharacters
1. List all files in the /etc directory that begin with letters “ma” and followed by any characters:
```
ls /etc/ma*
```

2. List all hidden files and directories in /home/user1:
```
ls -d .*
```

3. List all files in the /var/log directory that end in “.log”:
```
ls /ver/log/*.log
```

4. list all files and directories under /var/log with exactly four characters in their names:
```
ls -d /var/log/????
```

5. Include all files and directories that begin with either of the two characters and followed by any number of characters.
```
ls /usr/bin/[yw]*
```

6. Match all directory names that begin with any letter between “m” and “o” in the /etc/systemd/system directory:
```
ls -d /etc/systemd/system/[m-o]*
```

6. Inverse results of the previous:
```
ls -d /etc/systemd/system/[!m-o]*
```

### Lab: Piping
1. pipe the output to the less command in order to view the directory listing one screenful at a time:
```
ls -l /etc | less
```

2. Run the last command and pipe the output to nl to number each line:
```
last | nl
```

3. Send the output of ls to grep for the lines that do not contain the pattern “root”.  Piped again for a case-insensitive selection of all lines that exclude the pattern “dec”. Number the output, and show the last four lines on the display:
```
ls -l /proc | grep -v root | grep -iv dec | nl | tail -4
```

### Lab: Quoting Mechanisms
1. Remove a file called * without deleting everything in the directory:
```
rm \*
```

2. Display $LOGNAME without expanding the LOGNAME variable:
```
echo '$LOGNAME'
```

3. Run the following with double quotes and without:
```
echo "$SHELL"
echo "\$PWD"
echo "'\'"
```



### Lab: grep and regex
1. Search for the pattern “operator” in the /etc/passwd file:
```
grep operator /etc/passwd
```

2. Search for the space-separated pattern “aliases and functions” in the $HOME/.bashrc file:
```
grep 'aliases and functions' .bashrc
```

3. Search for the pattern “nologin” in the passwd file and exclude (-v) the lines in the output that contain this pattern. Add the -n switch to show the line numbers associated with the matched lines.
```
grep -nv nologin /etc/passwd
```

4. Find any duplicate entries for the root user in the passwd file. Prepend the caret sign (^) to the pattern “root” to mark the beginning of a line.
```
grep ^root /etc/passwd
```

5. Identify all users in the passwd file with bash as their primary shell.
```
grep bash$ /etc/passwd
```

6. show the entire login.defs file but exclude all the empty lines:
```
grep -v ^$ /etc/login.defs
```

7. Perform a case-insensitive search (-i) for all the lines in the /etc/bashrc file that match the pattern “path.”
```
grep -i path /etc/bashrc
```

8. Print all the lines from the /etc/lvm/lvm.conf file that contain an exact match for a word (-w) “acce” followed by exactly two characters:
```
grep -w acce.. /etc/lvm/lvm.conf
```

9. Print all the lines from the ls command output that include either (-E) the pattern “cron” or “ly”.
```
ls -l /etc | grep -E 'cron|ly'
```

10. Show all the lines from the /etc/ssh/sshd_config file but exclude (-v) the empty lines and commented lines. Use the -e flag multiple times instead of | for either or.
```
sudo grep -ve ^$ -ve ^# /etc/ssh/sshd_config
```

11. Learn more about regex:
```
man 7 regex
```

12. Consult the grep man pages:
```
man grep
```

### Lab: Managing jobs
1. Issue the jobs command with the -l switch to view all the jobs running in the background:
```
jobs -l
```

2. bring job ID 1 to the foreground and start running it:
```
fg %1
```

3. Suspend job 1 with ctrl+z and then let it run in the background:
```
bg %1
```

4. Terminate job ID 1, supply its PID (31726) to the kill command:
```
kill 31726
```



### Lab: Shell Startup Files
1. View the first 10 lines of /etc/bashrc:
```
head /etc/bashrc
```

2. View the first 10 lines of /etc/profile:
```
head /etc/profile
```

3. View the directory /etc/profile.d:L
```
ls -l /etc/profile.d/
```

4. View .bashrc
```
cat ~/.bashrc
```

5. View .bash_profile
```
cat ~/.bash_profile
```






### Lab:  Customize the Command Prompt (user1)
1. Permanently customize the primary shell prompt to display “<user1@server1 in /etc >:” when this user switches into the /etc directory. The prompt should always reflect the current directory directory path. 
```
vim ~/.bash_profile
export PS1='$USERNAME $PWD
```

### Lab 7-2: Redirect the Standard Input, Output, and Error (user1)
1. Run the ls command on /etc, /dvd, and /var. Have the output printed on the screen and the errors forwarded to file /tmp/ioerror. 
```
ls /etc /dvd /var 2> /tmp/ioerror
```

2. Check the file after the command execution and analyze the results:
```
cat /tmp/ioerror
```

## Review Questions

Q. You want to change the command prompt for yourself. Where (the bash shell file) would you define it so that you get the custom command prompt whenever you log in? 
A. You can define it in the ~/.bash_profile file. 

Q. What is the other name for the command line completion feature? 
A. The other name for the command line completion feature is tab completion. 

Q. What is a common use of the pipe symbol? 
A. A common use of the pipe character is to receive the output of one command and pass it along to the next command as an input. 

Q. Which directory location stores most, if not all, privileged commands? 
A. Privileged commands are stored in /usr/sbin directory. 

Q. You have a file called “?” in your home directory along with other one-letter files. What would you run to delete the “?” file only? 
A. rm \\? to remove the file. 

Q. What would the command ls /cdr /usr > output do? Assume /cdr does not exist. 
A. The command provided will redirect ls /usr output to the specified file and ls /cdr (error) to the terminal. 

Q. What is the name of the command that allows a user to define shortcuts to lengthy commands? 
A. The alias command. 

Q. Which file typically defines the history variables for all users? 
A. /etc/profile is the file where the history variables are defined for all users. 

Q. You have a command running that is tied to your terminal window. You want to get the command prompt back without terminating the running command. Which key combination would you press to return to the command prompt? 
A. The Ctrl+z key combination will suspend the running program and give you access to the command prompt. 

Q. Name the three quoting mechanisms? 
A. The three quoting mechanisms are backslash, single quotation mark, and double quotation mark. 

Q. What would the command export VAR1=”I passed RHCSA” do? 
A. The command provided will set an environment variable with the quoted string as its value. 

Q. Name the default filename and location where user command history is stored? 
A. The user command history is stored in ~/.bash_history file. 

Q. What is the primary function of the shell in Linux? 
A. The shell acts as an interface between a user and the system. 

Q. What would the command cd ~user20 do if executed as user10? 
A. The command provided will allow user10 to cd into user20’s home directory provided user10 has proper access permissions. 

Q. Which command would you use to display all matching lines from a text file? 
A. The grep command. 

Q. What would the command ls > ls.out do?
A. The command provided will redirect the ls command output to the specified file.

