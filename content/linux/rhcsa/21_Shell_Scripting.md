## Chapter 21 {style="text-align: right"}

\

### Shell Scripting {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Overview of shell scripts

\

Write scripts to display basic system information, employ shell and
environment variables, use command substitution, and manipulate special
and positional parameters

\

Execute and debug scripts

\

Know exit codes and test conditions

\

Understand logical constructs: if-then-fi, if-then-else-fi, and
if-then-elif-fi

\

Write scripts using logical statements

\

Know arithmetic test conditions

\

Comprehend looping construct: for-do-done

\

Write scripts using looping statements

\

#### RHCSA Objectives:

\

12\. Conditionally execute code (use of: if, test, \[\], etc.)

13\. Use Looping constructs (for, etc.) to process file, command line
input

14\. Process script inputs (\$1, \$2, etc.)

15\. Processing output of shell commands within a script

::: {style="page-break-before: always;"}
:::

\

Shell scripts are essentially a group of Linux commands along with
control structures and optional comments stored in a text file. Their
primary purpose of creation is the automation of long and repetitive
tasks. Scripts may include any simple to complex command and can be
executed directly at the Linux command prompt. They do not need to be
compiled as they are interpreted by the shell line by line.

\

::: {style="text-align: center;"}
![](image-WHEOUCJN.jpg){height="100%"}
:::

This chapter presents example scripts and analyzes them to solidify the
learning. These scripts begin with simple programs and advance to more
complicated ones. As with any other programming language, the scripting
skill develops over time as more and more scripts are read, written, and
examined. This chapter also discusses a debug technique that may be
helpful in troubleshooting the code.

::: {style="page-break-before: always;"}
:::

[]{#chapter0612.html}

## Shell Scripts {.style3}

\

Shell scripts (a.k.a. shell programs or simply scripts) are text files
that contain Linux commands and control structures to automate lengthy,
complex, or repetitive tasks, such as managing packages and users,
administering partitions and file systems, monitoring file system
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

\

Scripts presented in this chapter are written in the bash shell and may
be used in other Linux shells with slight modifications.

\

You can use any available text editor to write the scripts; however, it
is suggested to use the vim editor so that you have an opportunity to
practice it as you learn scripting. To quickly identify where things are
in your scripts, you can use the nl command to enumerate the lines. You
can store your scripts in the /usr/local/bin directory, which is
included in the PATH of all users by default.

::: {style="page-break-before: always;"}
:::

[]{#chapter0613.html}

## Script01: Displaying System Information

\

Let's create the first script called sys_info.sh on server10 in the
/usr/local/bin directory and examine it line by line. Use the vim editor
with sudo to write the script. Type what you see below. Do not enter the
line numbers, as they are used for explanation and reference.

\

<div>

![](image-WBYX6HL9.jpg){height="100%"}

</div>

\

Within vim, press the ESC key and then type :set nu to view line numbers
associated with each line entry.

\

In this script, comments and commands are used as follows:

\

The first line indicates the shell that will run the commands in the
script. This line must start with the "#!" character combination (called
shebang) followed by the full pathname to the shell file.

\

The next three lines contain comments: the script name, author name,
creation time, default directory location for storage, and purpose. The
number sign (#) implies that anything to the right of it is
informational and will be ignored during script execution. Note that the
first line also uses the number character (#), but it is followed by the
exclamation mark (!); that combination has a special meaning to the
shell.

\

The fifth line has the first command of the script. The echo command
prints on the screen whatever follows it ("Display Basic System
Information" in this case). This may include general comments, errors,
or script usage.

\

The sixth line will highlight the text "Display Basic System
Information" by underlining it.

\

The seventh line has the echo command followed by nothing. This will
insert an empty line in the output.

\

The eighth line will print "The hostname, hardware, and OS information
is:".

\

The ninth line will execute the hostnamectl command to display basic
information about the system.

\

The tenth line will insert an empty line.

\

The eleventh line will print "The following users are currently logged
in:" on the screen.

\

The twelfth line will execute the who command to list the logged-in
users.

\

Here is the listing of the sys_info.sh file created in the
/usr/local/bin directory:

\

<div>

![](image-U9347GDR.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0614.html}

## Executing a Script {.style3}

\

The script created above does not have the execute permission bit since
the default umask for the root user is set to 0022, which allows
read/write access to the owner, and read-only access to the rest. You
will need to run the chmod command on the file and add an execute bit
for everyone:

\

<div>

![](image-V96GO5KX.jpg){height="100%"}

</div>

Any user on the system can now run this script using either its name or
the full path.

\

Let's run the script and see what the output will look like:

\

<div>

![](image-HT7WGILI.jpg){height="100%"}

</div>

The output reflects the execution of the commands as scripted.

\

The hostnamectl command displays the hostname of the system, type of
platform (physical, virtual) it is running on, hypervisor vendor name,
operating system name and version, current kernel version, hardware
architecture, and other information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0615.html}

## Debugging a Script {.style3}

\

Before you have a perfectly working script in place, you may have to run
and modify it more than once. You can use a debugging technique that
will help identify where the script might have failed or did not
function as expected. You can either append the -x option to the
"#!/bin/bash" at the beginning of the script to look like "#!/bin/bash
-x", or execute the script as follows:

\

<div>

![](image-S85E88QO.jpg){height="100%"}

</div>

The above output now also includes the actual lines from the script
prefixed by the + sign and followed by the command execution result. It
also shows the line number of the problem line in the output if there is
any. This way you can identify any issues pertaining to the path,
command name, use of special characters, etc., and address it quickly.
Try changing any of the echo commands in the script to "iecho" and
re-run the script in the debug mode to confirm what has just been said.

::: {style="page-break-before: always;"}
:::

[]{#chapter0616.html}

## Script02: Using Local Variables

\

You had worked with variables earlier in the book and seen their usage.
To recap, there are two types of variables: local (also called private
or shell) and environment. Both can be defined and used in scripts and
at the command line.

\

The following script called use_var.sh will define a local variable and
display its value on the screen. You will re-check the value of this
variable after the script execution has completed. The comments have
been excluded for brevity.

\

<div>

![](image-Z5K3LMWN.jpg){height="100%"}

</div>

Add the execute bit to the script. The following output will be
generated when you run it:

\

<div>

![](image-DM2GAYSJ.jpg){height="100%"}

</div>

If you run the echo command to see what is stored in the SYSNAME
variable, you will get nothing:

\

<div>

![](image-2RTUEEJZ.jpg){height="100%"}

</div>

The output is self-explanatory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0617.html}

## Script03: Using Pre-Defined Environment Variables {.style3}

\

The following script called pre_env.sh will display the values of SHELL
and LOGNAME environment variables:

\

<div>

![](image-KXAKOW0I.jpg){height="100%"}

</div>

Add the execute bit to the script, and run to view the result:

\

<div>

![](image-BXTG2UOW.jpg){height="100%"}

</div>

The output is self-explanatory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0618.html}

## Script04: Using Command Substitution

\

During the execution of a script, you can use the command substitution
feature of the bash shell and store the output generated by the command
into a variable. For example, the following script called cmd_out.sh
will run the hostname and uname commands and save their outputs in
variables. This script shows two different ways to use command
substitution. Make sure to use the backticks (normally located with the
\~ character on the keyboard) to enclose the uname command.

\

<div>

![](image-QGX6T5R3.jpg){height="100%"}

</div>

Add the execute bit and run the script:

\

<div>

![](image-831AH0EM.jpg){height="100%"}

</div>

The output is self-explanatory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0619.html}

## Understanding Shell Parameters {.style3}

\

A shell parameter (or simply a parameter) is an entity that holds a
value such as a name, special character, or number. The parameter that
holds a name is referred to as a variable; a special character is
referred to as a special parameter; and one or more digits, except for 0
is referred to as a positional parameter (a.k.a. a command line
argument). A special parameter represents the command or script itself
(\$0), count of supplied arguments (\$\* or \$@), all arguments (\$#),
and PID of the process (\$\$). A positional parameter (\$1, \$2, \$3 . .
.) is an argument supplied to a script at the time of its invocation,
and its position is determined by the shell based on its location with
respect to the calling script. Figure 21-1 gives a pictorial view of the
special and positional parameters.

\

::: {style="text-align: center;"}
![](image-G1VF6C4I.jpg){height="100%"}
:::

Figure 21-1 Shell Parameters

\

[Figure 21-1 also shows that positional parameters beyond 9 are to be
enclosed in curly brackets. Just like the variable and command
substitutions, the shell uses the dollar (\$) sign for special and
positional parameter expansions as well.](#chapter0619.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0620.html}

## Script05: Using Special and Positional Parameters

\

The script com_line_arg.sh below will show the supplied arguments, total
count, value of the first argument, and PID of the script:

\

<div>

![](image-EGIJTGSL.jpg){height="100%"}

</div>

The result will be as follows when the script is executed with four
arguments. Do not forget to add the execute bit prior to running it.

\

<div>

![](image-2PFHP876.jpg){height="100%"}

</div>

The output is self-explanatory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0621.html}

## Script06: Shifting Command Line Arguments

\

The shift command is used to move arguments one position to the left.
During this move, the value of the first argument is lost. The
com_line_arg_shift.sh script below is an extension to the
com_line_arg.sh script. It uses the shift command to show what happens
when arguments are moved.

\

<div>

![](image-ERHNBPKE.jpg){height="100%"}

</div>

Let's execute the script with the same four arguments. Notice that a new
value is assigned to \$1 after each shift.

\

<div>

![](image-IWAN4BI1.jpg){height="100%"}

</div>

Multiple shifts in a single attempt may be performed by furnishing a
count of desired shifts to the shift command as an argument. For
example, "shift 2" will carry out two shifts, "shift 3" will make three
shifts, and so on.

::: {style="page-break-before: always;"}
:::

[]{#chapter0622.html}

## Logical Constructs {.style3}

\

So far, we have talked about simple scripts that run the code line by
line. The shell lets us employ logical constructs to control the flow of
scripts. It does this by allowing us to use test conditions, which
decides what to do next based on the true or false status of the
condition.

\

The shell offers two logical constructs: the if-then-fi construct and
the case construct. The if-then-fi construct has a few variations and
those will be covered as well. A discussion on the case construct is
beyond the scope.

\

Before starting to look at the example scripts and see how logical
constructs are used, let's discuss exit codes and various test
conditions. You will use them later in the example scripts.

::: {style="page-break-before: always;"}
:::

[]{#chapter0623.html}

## Exit Codes {.style3}

\

Exit codes, or exit values, refer to the value returned by a command
when it finishes execution. This value is based on the outcome of the
command. If the command runs successfully, you typically get a zero exit
code, otherwise you get a non-zero value. This code is also referred to
as a return code, and it is stored in a special shell parameter called ?
(question mark). Let's look at the following two examples to understand
their usage:

\

<div>

![](image-IHP0DK8G.jpg){height="100%"}

</div>

In the first example, the pwd command ran successfully and it produced
the desired result, hence a zero exit code was returned and stored in
the ?. In the second example, the man command did not run successfully
because of a missing argument, therefore a non-zero exit code was
returned and stored in the ?.

\

You can define exit codes within a script at different locations to help
debug the script by knowing where exactly it terminated.

::: {style="page-break-before: always;"}
:::

[]{#chapter0624.html}

## Test Conditions {.style3}

\

Test conditions are used in logical constructs to decide what to do
next. They can be set on integer values, string values, or files using
the test command or by enclosing them within the square brackets \[\].
Table 21-1 describes various test condition operators.

\

  ----------------------------------- -----------------------------------
  Operation on Integer Value          Description

  integer1 -eq (-ne) integer2         Integer1 is equal (not equal) to
                                      integer2

  integer1 -lt (-gt) integer2         Integer1 is less (greater) than
                                      integer2

  integer1 -le (-ge) integer2         Integer1 is less (greater) than or
                                      equal to integer2

  Operation on String Value           Description

  string1=(!=)string2                 Tests whether the two strings are
                                      identical (not identical)

  -l string or -z string              Tests whether the string length is
                                      zero

  string or -n string                 Tests whether the string length is
                                      non-zero

  Operation on File                   Description

  -b (-c) file                        Tests whether the file is a block
                                      (character) device file

  -d (-f) file                        Tests whether the file is a
                                      directory (normal file)

  -e (-s) file                        Tests whether the file exists
                                      (non-empty)

  -L file                             Tests whether the file is a symlink

  -r (-w) (-x) file                   Tests whether the file is readable
                                      (writable) (executable)

  -u (-g) (-k) file                   Tests whether the file has the
                                      setuid (setgid) (sticky) bit

  file1 -nt (-ot) file2               Tests whether file1 is newer
                                      (older) than file2

  Logical Operators                   Description

  !                                   The logical NOT operator

  -a or && (two ampersand characters) The logical AND operator. Both
                                      operands must be true for the
                                      condition to be true. Syntax: \[ -b
                                      file1 && -r file1 \]

  -o or \|\| (two pipe characters)    The logical OR operator. Either of
                                      the two or both operands must be
                                      true for the condition to be true.
                                      Syntax: \[ (x == 1 -o y == 2) \]
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 21-1 Test Conditions

\

Having described the exit codes and test conditions, let's look at a few
example scripts and observe their effects.

::: {style="page-break-before: always;"}
:::

[]{#chapter0625.html}

## The if-then-fi Construct {.style3}

\

The if-then-fi statement evaluates the condition for true or false. It
executes the specified action if the condition is true; otherwise, it
exits the construct. The if-then-fi statement begins with an "if" and
ends with a "fi", as depicted in the flow diagram in Figure 21-2:

\

::: {style="text-align: center;"}
![](image-7FX8FVMW.jpg){height="100%"}
:::

Figure 21-2 The if-then-fi Construct

\

The general syntax of this statement is as follows:

\

if condition

then

action

fi

\

This construct is used in the following script.

::: {style="page-break-before: always;"}
:::

[]{#chapter0626.html}

## Script07: The if-then-fi Construct

\

You saw earlier how to check the number of arguments supplied at the
command line. The following script called if_then_fi.sh determines the
number of arguments and prints an error message if there are none
provided:

\

<div>

![](image-8Y1IGGJV.jpg){height="100%"}

</div>

This script will display the following messages on the screen if it is
executed without exactly two arguments specified at the command line:

\

<div>

![](image-NOUL2V6Q.jpg){height="100%"}

</div>

A value of 2 will appear upon examining the return code as follows. This
value reflects the exit code that you defined in the script on line 6.

\

<div>

![](image-CCG46V45.jpg){height="100%"}

</div>

Conversely, the return code will be 0 and the message will be as follows
if you supply a pair of arguments:

\

<div>

![](image-GJ5ZA27Q.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0627.html}

## The if-then-else-fi Construct {.style3}

\

The if-then-fi statement has a limitation and it can execute an action
only if the specified condition is true. It quits the statement if the
condition is untrue. The if-then-else-fi statement, in contrast, is more
advanced in the sense that it can execute an action if the condition is
true and another action if the condition is false. The flow diagram for
this structure is shown in Figure 21-3:

\

::: {style="text-align: center;"}
![](image-CMLV644G.jpg){height="100%"}
:::

Figure 21-3 The if-then-else-fi Construct

\

The general syntax of this statement is as follows:

\

if condition

then

action1

else

action2

fi

\

action1 or action2 is performed based on the true or false evaluation of
the condition.

::: {style="page-break-before: always;"}
:::

[]{#chapter0628.html}

## Script08: The if-then-else-fi Construct

\

The following script called if_then_else_fi.sh will accept an integer
value as an argument and tell if the value is positive or negative:

\

<div>

![](image-3YKJ4725.jpg){height="100%"}

</div>

Run this script one time with a positive integer value and the next time
with a negative value:

\

<div>

![](image-7VU4BPZY.jpg){height="100%"}

</div>

Try the script again but with a non-integer value and see what it does.

::: {style="page-break-before: always;"}
:::

[]{#chapter0629.html}

## The if-then-elif-fi Construct {.style3}

\

The if-then-elif-fi is a more sophisticated construct than the other two
conditional statements. You can define multiple conditions and associate
an action with each one of them. During the evaluation, the action
corresponding to the true condition is performed. The flow diagram for
this structure is shown in Figure 21-4:

\

::: {style="text-align: center;"}
![](image-TNYN7SP2.jpg){height="100%"}
:::

Figure 21-4 The if-then-elif-fi Construct

\

The general syntax of this statement is as follows:

\

  ----------------------------------- -----------------------------------
  if                                  condition1

  then                                action1

  elif                                condition2

  then                                

                                      action2

  elif                                condition3

  then                                

                                      action3

  ............                        

  else                                

                                      action(n)

  fi                                  
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Let's use the if-then-elif-fi construct in the following two example
scripts.

::: {style="page-break-before: always;"}
:::

[]{#chapter0630.html}

## Script09: The if-then-elif-fi Construct (Example 1)

\

The if_then_elif_fi.sh script is an enhanced version of the
if_then_else_fi.sh script. It accepts an integer value as an argument
and tells if it is positive, negative, or zero. If a non-integer value
or no argument is supplied, the script will complain. Notice that the
script employs the exit command after each action to help you identify
where it exited.

\

<div>

![](image-2ZQ5DZAT.jpg){height="100%"}

</div>

Run this script four times: the first time with a positive integer, the
second time with 0, the third time with a negative integer, and the
fourth time with a non-integer value. Check the exit code after each
execution to know where the script exited.

\

<div>

![](image-DE8N5FXR.jpg){height="100%"}

</div>

The outputs and exit values reflect the program code.

::: {style="page-break-before: always;"}
:::

[]{#chapter0631.html}

## Script10: The if-then-elif-fi Construct (Example 2)

\

The script ex200_ex294.sh will display the name of the Red Hat exam
RHCSA or RHCE in the output based on the input argument (ex200 or
ex294). If a random or no argument is provided, it will print "Usage:
Acceptable values are ex200 and ex294". Make sure to add white spaces in
the conditions as shown.

\

<div>

![](image-6L2U92X3.jpg){height="100%"}

</div>

Run this script three times: the first time with argument ex200, the
second time with argument ex294, and the third time with something
random as an argument:

\

<div>

![](image-99I0JRAK.jpg){height="100%"}

</div>

The results are as expected.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: A good understanding of the usage of logical statements is
important.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0632.html}

## Looping Constructs {.style3}

\

As a Linux user and administrator, you often want to perform certain
task on a number of given elements or repeatedly until a specified
condition becomes true or false. For instance, if plenty of disks need
to be initialized for use in LVM, you can either run the pvcreate
command on each disk one at a time manually or employ a loop to do it
for you. Likewise, based on a condition, you may want a program to
continue to run until that condition becomes true or false.

\

There are three constructs---for-do-done, while-do-done, and
until-do-done---that you can use to implement looping.

\

The for loop is also referred to as the foreach loop.

\

The for loop iterates on a list of given values until the list is
exhausted. The while loop runs repeatedly until the specified condition
becomes false. The until loop does just the opposite of the while loop;
it performs an operation repeatedly until the specified condition
becomes true. This chapter will discuss the for loop only; the other two
are out of scope.

::: {style="page-break-before: always;"}
:::

[]{#chapter0633.html}

## Test Conditions {.style3}

\

The let command is used in looping constructs to evaluate a condition at
each iteration. It compares the value stored in a variable against a
pre-defined value. Each time the loop does an iteration, the variable
value is altered. You can enclose the condition for arithmetic
evaluation within a pair of parentheses (( )) or quotation marks (" ")
instead of using the let command explicitly.

\

[Table 21-2 lists operators that can be used in test
conditions.](#chapter0633.html)

\

  ----------------------------------- -----------------------------------
  Operator                            Description

  !                                   Negation

  \+ / -- / \* / /                    Addition / subtraction /
                                      multiplication / division

  \%                                  Remainder

  \< / \<=                            Less than / less than or equal to

  \> / \>=                            Greater than / greater than or
                                      equal to

  =                                   Assignment

  == / !=                             Comparison for equality /
                                      non-equality
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 21-2 Arithmetic Operators

\

Having described various test condition operators, let's look at the
syntax of the for loop and a few example scripts and observe the
implications of some of the test conditions.

::: {style="page-break-before: always;"}
:::

[]{#chapter0634.html}

## The for Loop {.style3}

\

The for loop is executed on an array of elements until all the elements
in the array are consumed. Each element is assigned to a variable one
after the other for processing. The flow diagram for this construct is
displayed in Figure 21-5:

\

::: {style="text-align: center;"}
![](image-BPQ7RWER.jpg){height="100%"}
:::

Figure 21-5 The for Loop

\

The general syntax of this construct is as follows:

\

for VAR in list

do

action

done

::: {style="page-break-before: always;"}
:::

[]{#chapter0635.html}

## Script11: Print Alphabets Using for Loop

\

The for_do_done.sh script initializes the variable COUNT to 0. The for
loop will read each letter sequentially from the range placed within
curly brackets (no spaces before the letter A and after the letter Z),
assign it to another variable LETTER, and display the value on the
screen. The expr command is an arithmetic processor, and it is used here
to increment the COUNT by 1 at each loop iteration.

\

<div>

![](image-SGYVLBJI.jpg){height="100%"}

</div>

The output of the script will be:

\

<div>

![](image-LPILMH3X.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0636.html}

## Script12: Create Users Using for Loop

\

The create_user.sh script can create several Linux user accounts. As
each account is created, the value of the variable ? is checked. If the
value is 0, a message saying the account is created successfully will be
displayed, otherwise the script will terminate. In case of a successful
account creation, the passwd command will be invoked to assign the user
the same password as their username.

\

<div>

![](image-LBKMPM2V.jpg){height="100%"}

</div>

The result of the script execution below confirms the addition of three
new user accounts:

\

<div>

![](image-RX78F6SX.jpg){height="100%"}

</div>

If this script is re-executed without modifying the list of elements
(usernames), the following will appear:

\

<div>

![](image-Y5KNA8OX.jpg){height="100%"}

</div>

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: A good understanding of the looping construct will help on the
exam.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0637.html}

## Chapter Summary {.style3}

\

In this chapter, we learned the basics of bash shell scripting. This
chapter began with an overview of scripting and then demonstrated how to
write and analyze test scripts using various built-in features of the
bash shell. We wrote and examined simple code and gradually advanced to
more advanced scripts, including those that employed logical and looping
constructs. We learned how to identify problem lines in our scripts.
After understanding and practicing the scripts presented in this
chapter, you should be able to write your own programs, debug them, and
examine those authored by others.

::: {style="page-break-before: always;"}
:::

[]{#chapter0638.html}

## Review Questions {.style3}

\

1\. What are the two types of logical constructs mentioned in this
chapter?

2\. What would != imply in a looping condition?

3\. What is the function of the shift command?

4\. You can script the startup and shutdown of a database. True or
False?

5\. What is the difference between a line in a script starting with a
"#" and a "#!"?

6\. What comments may you want to include in a shell script? Write any
six.

7\. What is one benefit of writing shell scripts?

8\. What are the three major components in a shell script?

9\. Which looping construct can be used to perform an action on listed
items?

10\. What does the echo command do without any arguments?

11\. What would the command echo \$? do?

12\. When would you want to use an exit code in your script?

13\. What would you modify in a shell script to run it in the debug
mode?

14\. What would the command bash -x /usr/local/bin/script1.sh do?

::: {style="page-break-before: always;"}
:::

[]{#chapter0639.html}

## Answers to Review Questions {.style3}

\

1\. The if and case constructs.

2\. != would check the value for non-equality.

3\. The shift command moves an argument to the left.

4\. True.

5\. The former is used to include general comments in the script and the
latter combination dictates the full path to the shell file that is to
be used to execute the script.

6\. The author name, creation date, last modification date, location,
purpose, and usage.

7\. One major benefit of writing shell scripts is to automate lengthy
and repetitive tasks.

8\. The three major components in a shell script are commands, control
structures, and comments.

9\. The for loop.

10\. The echo command inserts an empty line in the output when used
without arguments.

11\. This command will display the exit code of the last command
executed.

12\. The purpose of using an exit code is to determine exactly where the
script quits.

13\. We would specify -x as an argument to the shell path.

14\. This command will execute script1.sh in debug mode.

::: {style="page-break-before: always;"}
:::

[]{#chapter0640.html}

## Do-It-Yourself Challenge Labs

\

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the labs have already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

\

Use the lab environment built specifically for end-of-chapter labs. See
sub-section "Lab Environment for End-of-Chapter Labs" in Chapter 01
"Local Installation" for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0641.html}

## Lab 21-1: Write Script to Create Logical Volumes {.style3}

\

For this lab, present 2x1GB virtual disks to server40 in VirtualBox
Manager. As user1 with sudo on server40, write a single bash script to
create 2x800MB partitions on each disk using parted and then bring both
partitions into LVM control with the pvcreate command. Create a volume
group called vgscript and add both physical volumes to it. Create three
logical volumes each of size 500MB and name them lvscript1, lvscript2,
and lvscript3.

::: {style="page-break-before: always;"}
:::

[]{#chapter0642.html}

## Lab 21-2: Write Script to Create File Systems {.style3}

\

This lab is a continuation of Lab 21-1. Write another bash script to
create xfs, ext4, and vfat file system structures in the logical
volumes, respectively. Create mount points /mnt/xfs, /mnt/ext4, and
/mnt/vfat, and mount the file systems. Include the df command with -h in
the script to list the mounted file systems.

::: {style="page-break-before: always;"}
:::

[]{#chapter0643.html}

## Lab 21-3: Write Script to Configure New Network Connection Profile {.style3}

\

For this lab, present a new network interface to server40 in VirtualBox
Manager. As user1 with sudo on server40, write a single bash script to
run the nmcli command to configure custom IP assignments (choose your
own settings) on the new network device. Make a copy of the /etc/hosts
file as part of this script. Choose a hostname of your choice and add a
mapping to the /etc/hosts file without overwriting existing file
content.

::: {style="page-break-before: always;"}
:::

[]{#chapter0644.html}

