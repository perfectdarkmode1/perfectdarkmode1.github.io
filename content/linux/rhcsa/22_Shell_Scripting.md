
This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Overview of shell scripts

[![](images/00001.jpeg){.c37}]{.c36}Write scripts to display basic
system information, employ shell and environment variables, use command
substitution, and manipulate special and positional parameters

[![](images/00001.jpeg){.c37}]{.c36}Execute and debug scripts

[![](images/00001.jpeg){.c37}]{.c36}Know exit codes and test conditions

[![](images/00001.jpeg){.c37}]{.c36}Understand logical constructs:
if-then-fi, if-then-else-fi, and if-then-elif-fi

[![](images/00001.jpeg){.c37}]{.c36}Write scripts using logical
statements

[![](images/00001.jpeg){.c37}]{.c36}Know arithmetic test conditions

[![](images/00001.jpeg){.c37}]{.c36}Comprehend looping construct:
for-do-done

[![](images/00001.jpeg){.c37}]{.c36}Write scripts using looping
statements

[RHCSA Objectives:]{.c39}

[12]{#part0034_split_000.html#id_778 .calibre10}. Conditionally execute
code (use of: if, test, \[\], etc.)

[13]{#part0034_split_000.html#id_779 .calibre10}. Use Looping constructs
(for, etc.) to process file, command line input

[14]{#part0034_split_000.html#id_780 .calibre10}. Process script inputs
(\$1, \$2, etc.)

[15]{#part0034_split_000.html#id_781 .calibre10}. Processing output of
shell commands within a script

[16]{#part0034_split_000.html#id_782 .calibre10}. Processing shell
command exit codes

::: {#part0034_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0034_split_001.html}

[ S]{.c42}[hell]{.c43} scripts are essentially a group of Linux commands
along with control structures and optional comments stored in a text
file. Their primary purpose of creation is the automation of long and
repetitive tasks. Scripts may include any simple to complex command and
can be executed directly at the Linux command prompt. They do not need
to be compiled as they are interpreted by the shell line by line. This
chapter presents example scripts and analyzes them to solidify the
learning. These scripts begin with simple programs and advance to more
complicated ones. As with any other programming language, the scripting
skill develops over time as more and more scripts are read, written, and
examined. This chapter also discusses a debug technique that may be
helpful in troubleshooting the code.

**[Shell]{#part0034_split_001.html#id_565 .calibre10} Scripts**

Shell scripts (a.k.a. *shell programs* or simply *scripts*) are text
files that contain Linux commands and control structures to automate
lengthy, complex, or repetitive tasks, such as managing packages and
users, administering partitions and file systems, monitoring file system
utilization, trimming log files, archiving and compressing files,
finding and removing unnecessary files, starting and stopping database
services and applications, and producing reports. Commands in a script
are interpreted and run by the shell one at a time in the order in which
they are listed. Each line is executed as if it is typed and run at the
command prompt. Control structures are utilized for creating and
managing conditional and looping constructs. Comments are also generally
included to add information about the script such as the author name,
creation date, previous modification dates, purpose, and usage. If the
script encounters an error during execution, the error message is
printed on the screen.

Scripts presented in this chapter are written in the bash shell and may
be used in other Linux shells with slight modifications.

You can use any available text editor to write the scripts; however, it
is suggested to use the *vim* editor so that you have an opportunity to
practice it as you learn scripting. To quickly identify where things are
in your scripts, you can use the *nl* command to enumerate the lines.
You can store your scripts in the **usr*local/bin* directory, which is
included in the PATH of all users by default.

**[Script]{#part0034_split_001.html#id_566 .calibre10}01: Displaying
System Information**

Let's create the first script called *sys_info.sh* on *server10* in the
**usr*local/bin* directory and examine it line by line. Use the *vim*
editor with *sudo* to write the script. Type what you see below. Do not
enter the line numbers, as they are used for explanation and reference.

![](images/01012.jpeg){.image2}

![](images/00002.jpeg){.image} Within vim, press the ESC key and then
type :set nu to view line numbers associated with each line entry.

In this script, comments and commands are used as follows:

The first line indicates the shell that will run the commands in the
script. This line must start with the "#!" character combination (called
*shebang*) followed by the full pathname to the shell file.

The next three lines contain comments: the script name, author name,
creation time, default directory location for storage, and purpose. The
number sign (#) implies that anything to the right of it is
informational and will be ignored during script execution. Note that the
first line also uses the number character (#), but it is followed by the
exclamation mark (!); that combination has a special meaning to the
shell.

The fifth line has the first command of the script. The *echo* command
prints on the screen whatever follows it ("Display Basic System
Information" in this case). This may include general comments, errors,
or script usage.

The sixth line will highlight the text "Display Basic System
Information" by underlining it.

The seventh line has the *echo* command followed by nothing. This will
insert an empty line in the output.

The eighth line will print "The hostname, hardware, and OS information
is:".

The ninth line will execute the *hostnamectl* command to display basic
information about the system.

The tenth line will insert an empty line.

The eleventh line will print "The following users are currently logged
in:" on the screen.

The twelfth line will execute the *who* command to list the logged-in
users.

Here is the listing of the *sys_info.sh* file created in the
**usr*local/bin* directory:

![](images/01013.jpeg){.image2}

**[Executing]{#part0034_split_001.html#id_567 .calibre10} a Script**

The script created above does not have the execute permission bit since
the default umask for the *root* user is set to 0022, which allows
read/write access to the owner, and read-only access to the rest. You
will need to run the *chmod* command on the file and add an execute bit
for everyone:

![](images/01014.jpeg){.image2}

Any user on the system can now run this script using either its name or
the full path.

Let's run the script and see what the output will look like:

![](images/01015.jpeg){.image2}

The output reflects the execution of the commands as scripted.

The *hostnamectl* command displays the hostname of the system, type of
platform (physical, virtual) it is running on, hypervisor vendor name,
operating system name and version, current kernel version, hardware
architecture, and other information.

**[Debugging]{#part0034_split_001.html#id_568 .calibre10} a Script**

Before you have a perfectly working script in place, you may have to run
and modify it more than once. You can use a debugging technique that
will help identify where the script might have failed or did not
function as expected. You can either append the -x option to the
"#!/bin/bash" at the beginning of the script to look like "#!/bin/bash
-x", or execute the script as follows:

![](images/01016.jpeg){.image2}

The above output now also includes the actual lines from the script
prefixed by the + sign and followed by the command execution result. It
also shows the line number of the problem line in the output if there is
any. This way you can identify any issues pertaining to the path,
command name, use of special characters, etc., and address it quickly.
Try changing any of the *echo* commands in the script to "iecho" and
re-run the script in the debug mode to confirm what has just been said.

**[Script]{#part0034_split_001.html#id_569 .calibre10}02: Using Local
Variables**

You had worked with variables earlier in the book and seen their usage.
To recap, there are two types of variables: *local* (also called
*private* or *shell*) and *environment*. Both can be defined and used in
scripts and at the command line.

The following script called *use_var.sh* will define a local variable
and display its value on the screen. You will re-check the value of this
variable after the script execution has completed. The comments have
been excluded for brevity.

![](images/01017.jpeg){.image2}

Add the execute bit to the script. The following output will be
generated when you run it:

![](images/01018.jpeg){.image2}

If you run the *echo* command to see what is stored in the SYSNAME
variable, you will get nothing:

![](images/01019.jpeg){.image2}

The output is self-explanatory.

**[Script]{#part0034_split_001.html#id_570 .calibre10}03: Using
Pre-Defined Environment Variables**

The following script called *pre_env.sh* will display the values of
SHELL and LOGNAME environment variables:

![](images/01020.jpeg){.image2}

Add the execute bit to the script, and run to view the result:

![](images/01021.jpeg){.image2}

The output is self-explanatory.

**[Script]{#part0034_split_001.html#id_571 .calibre10}04: Using Command
Substitution**

During the execution of a script, you can use the command substitution
feature of the bash shell and store the output generated by the command
into a variable. For example, the following script called *cmd_out.sh*
will run the *hostname* and *uname* commands and save their outputs in
variables. This script shows two different ways to use command
substitution. Make sure to use the backticks (normally located with the
\~ character on the keyboard) to enclose the *uname* command.

![](images/01022.jpeg){.image2}

Add the execute bit and run the script:

![](images/01023.jpeg){.image2}

The output is self-explanatory.

**[Understanding]{#part0034_split_001.html#id_572 .calibre10} Shell
Parameters**

A *shell parameter* (or simply a *parameter*) is an entity that holds a
value such as a name, special character, or number. The parameter that
holds a name is referred to as a variable; a special character is
referred to as a *special parameter*; and one or more digits, except for
0 is referred to as a *positional parameter* (a.k.a. a *command line
argument*). A special parameter represents the command or script itself
(\$0), count of supplied arguments (\$\* or \$@), all arguments (\$#),
and PID of the process (\$\$). A positional parameter (\$1, \$2, \$3 . .
.) is an argument supplied to a script at the time of its invocation,
and its position is determined by the shell based on its location with
respect to the calling script. [Figure
22-1](#part0034_split_001.html#page_487){.calibre5} gives a pictorial
view of the special and positional parameters.

::: c49
::: width_
![](images/01024.jpeg){.calibre13}
:::

**Figure 22-1 Shell Parameters**
:::

[Figure 22-1](#part0034_split_001.html#page_487){.calibre5} also shows
that positional parameters beyond 9 are to be enclosed in curly
brackets. Just like the variable and command substitutions, the shell
uses the dollar (\$) sign for special and positional parameter
expansions as well.

**[Script]{#part0034_split_001.html#id_573 .calibre10}05: Using Special
and Positional Parameters**

The script *com_line_arg.sh* below will show the supplied arguments,
total count, value of the first argument, and PID of the script:

![](images/01025.jpeg){.image2}

The result will be as follows when the script is executed with four
arguments. Do not forget to add the execute bit prior to running it.

![](images/01026.jpeg){.image2}

The output is self-explanatory.

**[Script]{#part0034_split_001.html#id_574 .calibre10}06: Shifting
Command Line Arguments**

The *shift* command is used to move arguments one position to the left.
During this move, the value of the first argument is lost. The
*com_line_arg_shift.sh* script below is an extension to the
*com_line_arg.sh* script. It uses the *shift* command to show what
happens when arguments are moved.

![](images/01027.jpeg){.image2}

Let's execute the script with the same four arguments. Notice that a new
value is assigned to \$1 after each shift.

![](images/01028.jpeg){.image2}

Multiple shifts in a single attempt may be performed by furnishing a
count of desired shifts to the *shift* command as an argument. For
example, "*shift* 2" will carry out two shifts, "*shift* 3" will make
three shifts, and so on.

**[Logical]{#part0034_split_001.html#id_575 .calibre10} Constructs**

So far, we have talked about simple scripts that run the code line by
line. The shell lets us employ logical constructs to control the flow of
scripts. It does this by allowing us to use test conditions, which
decides what to do next based on the true or false status of the
condition.

The shell offers two logical constructs: the *if-then-fi* construct and
the *case* construct. The if-then-fi construct has a few variations and
those will be covered as well. A discussion on the case construct is
beyond the scope.

Before starting to look at the example scripts and see how logical
constructs are used, let's discuss exit codes and various test
conditions. You will use them later in the example scripts.

**[Exit]{#part0034_split_001.html#id_576 .calibre10} Codes**

*Exit codes*, or *exit values*, refer to the value returned by a command
when it finishes execution. This value is based on the outcome of the
command. If the command runs successfully, you typically get a zero exit
code, otherwise you get a non-zero value. This code is also referred to
as a *return code,* and it is stored in a special shell parameter called
*?* (question mark). Let's look at the following two examples to
understand their usage:

![](images/01029.jpeg){.image2}

In the first example, the *pwd* command ran successfully and it produced
the desired result, hence a zero exit code was returned and stored in
the ?. In the second example, the *man* command did not run successfully
because of a missing argument, therefore a non-zero exit code was
returned and stored in the ?.

You can define exit codes within a script at different locations to help
debug the script by knowing where exactly it terminated.

**[Test]{#part0034_split_001.html#id_577 .calibre10} Conditions**

Test conditions are used in logical constructs to decide what to do
next. They can be set on integer values, string values, or files using
the *test* command or by enclosing them within the square brackets \[\].
[Table 22-1](#part0034_split_001.html#id_760){.calibre5} describes
various test condition operators.

::: c49
  ---------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------
  **Operation on Integer Value**     **Description**
  integer1 -eq (-ne) integer2        Integer1 is equal (not equal) to integer2
  integer1 -lt (-gt) integer2        Integer1 is less (greater) than integer2
  integer1 -le (-ge) integer2        Integer1 is less (greater) than or equal to integer2
  **Operation on String Value**      **Description**
  string1=(!=)string2                Tests whether the two strings are identical (not identical)
  -l string or -z string             Tests whether the string length is zero
  string or -n string                Tests whether the string length is non-zero
  **Operation on File**              **Description**
  -b (-c) file                       Tests whether the file is a block (character) device file
  -d (-f) file                       Tests whether the file is a directory (normal file)
  -e (-s) file                       Tests whether the file exists (non-empty)
  -L file                            Tests whether the file is a symlink
  -r (-w) (-x) file                  Tests whether the file is readable (writable) (executable)
  -u (-g) (-k) file                  Tests whether the file has the setuid (setgid) (sticky) bit
  file1 -nt (-ot) file2              Tests whether file1 is newer (older) than file2
  **Logical Operators**              **Description**
  !                                  The logical NOT operator
  -a or && (two ampersand            The logical AND operator. Both operands must be true for
  characters)                        the condition to be true. Syntax: \[ -b file1 && -r file1 \]
  -o or \|\| (two pipe characters)   The logical OR operator. Either of the two or both operands must be true for the condition to be true. Syntax: \[ (x == 1 -o y == 2) \]
  ---------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0034_split_001.html#id_760} 22-1 Test Conditions**
:::

Having described the exit codes and test conditions, let's look at a few
example scripts and observe their effects.

**[The]{#part0034_split_001.html#id_578 .calibre10} if-then-fi
Construct**

The if-then-fi statement evaluates the condition for true or false. It
executes the specified action if the condition is true; otherwise, it
exits the construct. The if-then-fi statement begins with an "if" and
ends with a "fi", as depicted in the flow diagram in [Figure
22-2](#part0034_split_001.html#id_681){.calibre5}:

::: c49
::: width_
![](images/01030.jpeg){.calibre14}
:::

**Figure 22-2 The if-then-fi Construct**
:::

The general syntax of this statement is as follows:

  ------ -----------
  if     condition
  then   
         action
  fi     
  ------ -----------

This construct is used in the following script.

**[Script]{#part0034_split_001.html#id_579 .calibre10}07: The if-then-fi
Construct**

You saw earlier how to check the number of arguments supplied at the
command line. The following script called *if_then_fi.sh* determines the
number of arguments and prints an error message if there are none
provided:

![](images/01031.jpeg){.image2}

This script will display the following messages on the screen if it is
executed without exactly two arguments specified at the command line:

![](images/01032.jpeg){.image2}

A value of 2 will appear upon examining the return code as follows. This
value reflects the exit code that you defined in the script on line 6.

![](images/01033.jpeg){.image2}

Conversely, the return code will be 0 and the message will be as follows
if you supply a pair of arguments:

![](images/01034.jpeg){.image2}

**[The]{#part0034_split_001.html#id_580 .calibre10} if-then-else-fi
Construct**

The if-then-fi statement has a limitation and it can execute an action
only if the specified condition is true. It quits the statement if the
condition is untrue. The if-then-else-fi statement, in contrast, is more
advanced in the sense that it can execute an action if the condition is
true and another action if the condition is false. The flow diagram for
this structure is shown in [Figure
22-3](#part0034_split_001.html#page_492){.calibre5}:

::: c49
::: width_
![](images/01035.jpeg){.calibre14}
:::

**Figure 22-3 The if-then-else-fi Construct**
:::

The general syntax of this statement is as follows:

  ------ -----------
  if     condition
  then   
         action1
  else   
         action2
  fi     
  ------ -----------

action1 or action2 is performed based on the true or false evaluation of
the condition.

**[Script]{#part0034_split_001.html#id_581 .calibre10}08: The
if-then-else-fi Construct**

The following script called *if_then_else_fi.sh* will accept an integer
value as an argument and tell if the value is positive or negative:

![](images/01036.jpeg){.image2}

Run this script one time with a positive integer value and the next time
with a negative value:

![](images/01037.jpeg){.image2}

Try the script again but with a non-integer value and see what it does.

**[The]{#part0034_split_001.html#id_582 .calibre10} if-then-elif-fi
Construct**

The if-then-elif-fi is a more sophisticated construct than the other two
conditional statements. You can define multiple conditions and associate
an action with each one of them. During the evaluation, the action
corresponding to the true condition is performed. The flow diagram for
this structure is shown in [Figure
22-4](#part0034_split_001.html#id_682){.calibre5}:

::: c49
::: width_
![](images/01038.jpeg){.calibre13}
:::

**Figure 22-4 The if-then-elif-fi Construct**
:::

The general syntax of this statement is as follows:

  -------------- ------------
  if             condition1
  then           
                 action1
  elif           condition2
  then           
                 action2
  elif           condition3
  then           
                 action3
  ............   
  else           
                 action(n)
  fi             
  -------------- ------------

Let's use the if-then-elif-fi construct in the following two example
scripts.

**[Script]{#part0034_split_001.html#id_583 .calibre10}09: The
if-then-elif-fi Construct (Example 1)**

The *if_then_elif_fi.sh* script is an enhanced version of the
*if_then_else_fi.sh* script. It accepts an integer value as an argument
and tells if it is positive, negative, or zero. If a non-integer value
or no argument is supplied, the script will complaint. Notice that the
script employs the *exit* command after each action to help you identify
where it exited.

![](images/01039.jpeg){.image2}

Run this script four times: the first time with a positive integer, the
second time with 0, the third time with a negative integer, and the
fourth time with a non-integer value. Check the exit code after each
execution to know where the script exited.

![](images/01040.jpeg){.image2}

The outputs and exit values reflect the program code.

**[Script]{#part0034_split_001.html#id_584 .calibre10}10: The
if-then-elif-fi Construct (Example 2)**

The script *ex200_ex294.sh* will display the name of the Red Hat exam
RHCSA or RHCE in the output based on the input argument (ex200 or
ex294). If a random or no argument is provided, it will print "Usage:
Acceptable values are ex200 and ex294". Make sure to add white spaces in
the conditions as shown.

![](images/01041.jpeg){.image2}

Run this script three times: the first time with argument ex200, the
second time with argument ex294, and the third time with something
random as an argument:

![](images/01042.jpeg){.image2}

The results are as expected.

[**EXAM TIP:**]{.c56} A good understanding of the usage of logical
statements is important.

**[Looping]{#part0034_split_001.html#id_585 .calibre10} Constructs**

As a Linux user and administrator, you often want to perform certain
task on a number of given elements or repeatedly until a specified
condition becomes true or false. For instance, if plenty of disks need
to be initialized for use in LVM, you can either run the *pvcreate*
command on each disk one at a time manually or employ a loop to do it
for you. Likewise, based on a condition, you may want a program to
continue to run until that condition becomes true or false.

There are three constructs---*for-do-done*, *while-do-done*, and
*until-do-done*---that you can use to implement looping.

![](images/00002.jpeg){.image} The for loop is also referred to as the
foreach loop.

The for loop iterates on a list of given values until the list is
exhausted. The while loop runs repeatedly until the specified condition
becomes false. The until loop does just the opposite of the while loop;
it performs an operation repeatedly until the specified condition
becomes true. This chapter will discuss the for loop only; the other two
are out of scope.

**[Test]{#part0034_split_001.html#id_586 .calibre10} Conditions**

The *let* command is used in looping constructs to evaluate a condition
at each iteration. It compares the value stored in a variable against a
pre-defined value. Each time the loop does an iteration, the variable
value is altered. You can enclose the condition for arithmetic
evaluation within a pair of parentheses (( )) or quotation marks (" ")
instead of using the *let* command explicitly.

[Table 22-2](#part0034_split_001.html#id_761){.calibre5} lists operators
that can be used in test conditions.

  -------------- --------------------------------------------------
  **Operator**   **Description**
  !              Negation
  \+ *--* \*     Addition *subtraction* multiplication / division
  \%             Remainder
  \< / \<=       Less than / less than or equal to
  \> / \>=       Greater than / greater than or equal to
  =              Assignment
  == / !=        Comparison for equality / non-equality
  -------------- --------------------------------------------------

**[Table]{#part0034_split_001.html#id_761} 22-2 Arithmetic Operators**

Having described various test condition operators, let's look at the
syntax of the for loop and a few example scripts and observe the
implications of some of the test conditions.

**[The]{#part0034_split_001.html#id_587 .calibre10} for Loop**

The for loop is executed on an array of elements until all the elements
in the array are consumed. Each element is assigned to a variable one
after the other for processing. The flow diagram for this construct is
displayed in [Figure 22-5](#part0034_split_001.html#id_683){.calibre5}:

::: c49
::: width_
![](images/01043.jpeg){.calibre14}
:::

**Figure 22-5 The for Loop** The general syntax of this construct is as
follows:
:::

  ----------------- --------
  for VAR in list   
  do                
                    action
  done              
  ----------------- --------

**[Script]{#part0034_split_001.html#id_588 .calibre10}11: Print
Alphabets Using for Loop**

The *for_do_done.sh* script initializes the variable COUNT to 0. The for
loop will read each letter sequentially from the range placed within
curly brackets (no spaces before the letter A and after the letter Z),
assign it to another variable LETTER, and display the value on the
screen. The *expr* command is an arithmetic processor and it is used
here to increment the COUNT by 1 at each loop iteration.

![](images/01044.jpeg){.image2}

The output of the script will be:

![](images/01045.jpeg){.image2}

**[Script]{#part0034_split_001.html#id_589 .calibre10}12: Create Users
Using for Loop**

The *create_user.sh* script can create several Linux user accounts. As
each account is created, the value of the variable ? is checked. If the
value is 0, a message saying the account is created successfully will be
displayed, otherwise the script will terminate. In case of a successful
account creation, the *passwd* command will be invoked to assign the
user the same password as their username.

![](images/01046.jpeg){.image2}

The result of the script execution below confirms the addition of three
new user accounts:

![](images/01047.jpeg){.image2}

If this script is re-executed without modifying the list of elements
(user names), the following will appear:

![](images/01048.jpeg){.image2}

[**EXAM TIP:**]{.c56} A good understanding of the looping construct will
help on the exam.

**[Chapter]{#part0034_split_001.html#id_590 .calibre10} Summary**

In this chapter, we learned the basics of bash shell scripting. This
chapter began with an overview of scripting and then demonstrated how to
write and analyze test scripts using various built-in features of the
bash shell. We wrote and examined simple code and gradually advanced to
more advanced scripts, including those that employed logical and looping
constructs. We learned how to identify problem lines in our scripts.
After understanding and practicing the scripts presented in this
chapter, you should be able to write your own programs, debug them, and
examine those authored by others.

**[Review]{#part0034_split_001.html#id_591 .calibre10} Questions**

1[.]{.c19}What are the three major components in a shell script?

2[.]{.c19}Which looping construct can be used to perform an action on
listed items?

3[.]{.c19}What is the function of the *shift* command?

4[.]{.c19}You can script the startup and shutdown of a database. True or
False?

5[.]{.c19}What does the *echo* command do without any arguments?

6[.]{.c19}What would the command *echo \$?* do?

7[.]{.c19}When would you want to use an exit code in your script?

8[.]{.c19}What would you modify in a shell script to run it in the debug
mode?

9[.]{.c19}What are the two types of logical constructs mentioned in this
chapter?

10[.]{.c23}What would != imply in a looping condition?

11[.]{.c23}What is the difference between a line in a script starting
with a "#" and a "#!"?

12[.]{.c23}What comments may you want to include in a shell script?
Write any six.

13[.]{.c23}What is one benefit of writing shell scripts?

14[.]{.c23}What would the command *bash -x *usr*local/bin/script1.sh*
do?

**[Answers]{#part0034_split_001.html#id_592 .calibre10} to Review
Questions**

1[.]{.c19}The three major components in a shell script are commands,
control structures, and comments.

2[.]{.c19}The for loop.

3[.]{.c19}The *shift* command moves an argument to the left.

4[.]{.c19}True.

5[.]{.c19}The *echo* command inserts an empty line in the output when
used without arguments.

6[.]{.c19}This command will display the exit code of the last command
executed.

7[.]{.c19}The purpose of using an exit code is to determine exactly
where the script quits.

8[.]{.c19}We would specify -x as an argument to the shell path.

9[.]{.c19}The if and case constructs.

10[.]{.c23}!= would check the value for non-equality.

11[.]{.c23}The former is used to include general comments in the script
and the latter combination dictates the full path to the shell file that
is to be used to execute the script.

12[.]{.c23}The author name, creation date, last modification date,
location, purpose, and usage.

13[.]{.c23}One major benefit of writing shell scripts is to automate
lengthy and repetitive tasks.

14[.]{.c23}This command will execute *script1.sh* in debug mode.

**[DIY]{#part0034_split_001.html#id_593 .calibre10} Challenge Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform these
labs without any additional help. A step-by-step guide is not provided,
as the implementation of these labs requires the knowledge that has been
presented in this chapter. Use defaults or your own thinking for missing
information.

**[Lab]{#part0034_split_001.html#id_594 .calibre10} 22-1: Write a Script
to Create Logical Volumes**

For this lab, present 2x1GB virtual disks to your system in VirtualBox
VM Manager. Write a single bash shell script to create 2x800MB
partitions on each disk using *parted* and then bring both partitions
into LVM control with the *pvcreate* command. Create a volume group
called *vgscript* and add both PVs to it. Create three logical volumes
each of size 500MB and name them *lvscript1*, *lvscript2*, and
*lvscript3*.

**[Lab]{#part0034_split_001.html#id_595 .calibre10} 22-2: Write a Script
to Create File Systems**

This lab is a continuation of Lab 22-1. Write another bash shell script
to create xfs, ext4, and vfat file system structures in each logical
volume, respectively. Create mount points **mnt*xfs*, **mnt*ext4*, and
**mnt*vfat*, and mount the file systems. Include the *df* command with
-h to list the mounted file systems.

**[Lab]{#part0034_split_001.html#id_596 .calibre10} 22-3: Write a Script
to Configure a New Network Profile**

For this lab, present a new network interface to your system in
VirtualBox VM Manager. Write a single bash shell script to run the
*nmcli* command to configure custom IP assignments (choose your own
settings) on the new network device and ensure that they are
automatically applied to it on future system reboots. Make a copy of the
**etc*hosts* file as part of this script. Choose a hostname of your
choice and add a mapping to the **etc*hosts* file without overwriting
existing file content.

[]{#part0035_split_000.html}
