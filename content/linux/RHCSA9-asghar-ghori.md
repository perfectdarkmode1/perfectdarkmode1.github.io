[]{#coverpage.xhtml}

::: {style="text-align: center;"}
![cover](image-DGP9LAHI.jpg){height="100%"}
:::

[]{#chapter0000.html}

::: {style="text-align: center;"}
![cover](image-DGP9LAHI.jpg){height="100%"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0001.html}

\

::: {style="text-align: center;"}
![](image-5WA0VWRC.jpg){height="100%"}
:::

[www.ingramspark.com](http://www.ingramspark.com)

::: {style="page-break-before: always;"}
:::

[]{#chapter0002.html}

Technical Reviewers: Many of author's students and peers

Editors: FirstEditing.com and Zainab Ghori

Cover Design: Nid n Nad Graphics Printing Inc. (www.nidnnad.ca)

Printers and Distributors: IngramSpark Inc.

\

Copyright © 2023 Asghar Ghori

All rights reserved.

No portion of this book may be stored in a retrieval system,
transmitted, or reproduced in any form, including but not limited to
photocopying or other recording, without the express written consent of
the author.

\

Printed in the USA, Canada, UK, France, Germany, Italy, Spain, and
Australia.

\

ISBN-13: 978-1-7750621-6-5

ISBN-10: 1-7750621-6-3

ISBN-13: 978-1-7750621-7-2 (e-book)

\

To order in bulk at special quantity discounts for sales promotions or
training programs, please contact the author directly at
asghar_ghori2002@yahoo.com

\

The following are registered trademarks in the U.S. and other countries:

\

Red Hat® is a registered trademark of Red Hat, Inc.

\

RHCSA® is a registered trademark of Red Hat, Inc.

\

Linux® is a registered trademark of Linus Torvalds.

\

Oracle® and VirtualBox® are registered trademarks of Oracle Corporation,
Inc.

\

UNIX® is a registered trademark of The Open Group.

\

Microsoft® and Windows® are US registered trademarks of Microsoft
Corporation.

\

Docker and the Docker logo are trademarks or registered trademarks of
Docker, Inc.

\

Intel® is the trademark or registered trademark of Intel Corporation or
its subsidiaries.

\

All other trademarks, registered trademarks, or logos used in this book
are the property of their respective owners.

\

The author has made his best efforts to prepare this book. The contents
are based on Red Hat® Enterprise Linux® version 9.1. The author makes no
representation or warranties of any kind with regard to the completeness
or accuracy of the contents herein and accepts no liability whatsoever
including but not limited to merchantability, fitness for any particular
purpose, or any losses or damages of any kind caused or allegedly caused
directly or indirectly from this material.

\

This book is not a replacement for the official Red Hat RH124 and RH134
training courses offered by Red Hat, Inc. for the preparation of the Red
Hat Certified System Administrator (RHCSA) exam, EX200. However, it may
be used to get ready for this exam based on the latest version of the
exam objectives available on Red Hat's training and certification
website. Neither author nor publisher warrants that use of this
publication will ensure passing the relevant exam or that the
information contained herein is endorsed by Red Hat, Inc.

::: {style="page-break-before: always;"}
:::

[]{#chapter0003.html}

## Preface {.style3}

\

Red Hat Enterprise Linux 9 was released on May 18, 2022. The official
objectives for the Red Hat Certified System Administrator (RHCSA)
certification exam were updated for the public shortly thereafter. There
were no major enhancements or changes introduced; however, a few minor
updates made to the exam objectives resulted in this publication: RHCSA
Red Hat Enterprise Linux 9: Training and Exam Preparation Guide. This
book presents a single, definitive resource to self-learners,
instructor-led learners, and Linux instructors.

The RHCSA exam is performance-based and presents several tasks that are
to be completed on virtual machines within a stipulated time. This book
provides the necessary coverage from both theoretical and practical
standpoints to assist learners in passing the exam. Moreover, this book
may be used for in-class and live virtual trainings, and as an
on-the-job deskside reference.

Keeping in mind the hands-on nature of the exam, I have included a
multitude of step-by-step exercises and Do-It-Yourself (DIY) challenge
labs throughout this publication. Chapter 01 describes how to obtain
copies of VirtualBox Manager and RHEL 9 software, and the steps for
building a lab environment to practice the procedures and perform labs.

I suggest that you study the material presented in each chapter
thoroughly before proceeding to the relevant hands-on exercise(s). I
have provided several review questions with answers at the end of each
chapter. Take the quiz and then attempt the DIY challenge labs offered
thereafter. I have not furnished solutions to these labs intentionally,
as I am confident that the knowledge and skills you will have gained by
that time will be sufficient to accomplish the labs on your own; and, in
essence, this is what I want you to eventually get at. After you have
read and understood the material, performed the exercises, completed
review questions, and accomplished DIY challenge labs fully, take time
to attempt the sample RHCSA exams provided in Appendices.

While performing exercises and labs, if a command does not produce the
published result, I advise you to check the message the command has
generated and browse through relevant log files. Minor issues such as a
wrong path, typing error, or an incorrect option prevent commands from
running. Sometimes, syntax errors in command constructs could result in
execution failures. You will have to address the issue with the command
to run it as expected. RHEL manual pages prove useful in comprehending
commands and their syntaxes.

There are four areas I suggest you focus on to develop expertise with
RHEL, as well as to prepare for the exam: 1) grasping concepts; 2)
mastering implementation procedures, exercises, and labs; 3) learning
commands, understanding configuration files, and knowing service
processes; and 4) being able to analyze logs, and troubleshoot and
resolve issues. An advanced knowledge of commands and key options, and
the files they update should also be developed along with what processes
handle which corresponding services, and so on. This will help you
obtain a greater overall understanding of what exactly happens behind
the scenes when a command runs. Debugging becomes easier when concepts
are clear and working knowledge is solid.

I maintain www.nixeducation.com where I add errata, additional
certification information, helpful videos on Linux concepts and
administration topics, and links to other useful resources. I encourage
you to visit this website.

To conclude, I would like to request your constructive feedback be sent
to my personal email asghar_ghori2002@yahoo.com regarding any
grammatical or technical errors or mistakes in the book, as well as any
suggestions. Please be specific in your description. Improvement is a
continuous process, and I believe your feedback will help me to continue
delivering quality books.

\

Good luck in your endeavors.

\

Asghar Ghori \| February 2023 \| Toronto, Canada

::: {style="page-break-before: always;"}
:::

[]{#chapter0004.html}

## Acknowledgments {.style3}

\

As always, I am grateful to God who enabled me to write this book
successfully.

\

I would like to acknowledge the valuable feedback my students, friends,
and colleagues provided on my previous publications on RHCSA, RHCE,
CompTIA Linux+, and HP-UX. I am thankful for their help in making this
book better in all respects.

\

I recognize the constructive feedback I had received from the readers of
my previous publications. I have used their comments toward the
improvement of this edition.

\

I would like to express my special thanks to my wife, daughters, and
sons, who endured my mental absence while writing this book. I could not
have accomplished this project without their continuous support and
encouragement.

\

Lastly, I would like to offer my very special tributes to my deceased
parents and sisters.

\

Asghar Ghori

::: {style="page-break-before: always;"}
:::

[]{#chapter0005.html}

## About the Author {.style3}

\

Asghar Ghori is a seasoned Linux \| Cloud \| DevOps consultant, trainer,
curriculum developer, and author. As a consultant with 30+ years of
experience, he has architected, implemented, and administered complex
technology solutions for both private and public sector organizations.
As a trainer and curriculum developer with 20+ years of experience, he
has designed, developed, and delivered numerous training programs on
Linux/UNIX fundamentals, RHCSA, RHCE, Microsoft Azure (Fundamentals,
Administrator, and Solution Architect), AWS (Practitioner and Solution
Architect), Automation (Terraform and Ansible), UNIX administration and
networking, high-availability clusters, and backup and recovery. As a
published author with 20+ years of writing experience, he has 11 books
on Linux (Red Hat Enterprise Linux and CompTIA Linux+) and UNIX to his
credit.

\

Asghar is an engineer by education. He holds several technical
certifications including RHCSA, RHCE, HPCSA, HPCSE, SCSA, IBM Certified
Specialist for AIX, and CNE, as well as IT Infrastructure Library (ITIL)
Foundation and Project Management Professional (PMP) certifications. He
is 5x Azure Certified, 4x AWS Certified, MCP, and HashiCorp Certified
Terraform Associate (HCTA). Asghar is Microsoft Certified Trainer (MCT)
and a big advocate of cloud adoption.

\

Asghar lives in Toronto, Canada with his wife and children, and can be
reached via email asghar_ghori2002@yahoo.com or LinkedIn
https://www.linkedin.com/in/asghar-ghori-0315632/.

\

Publications of Asghar Ghori including this are:

\

1\. RHCSA Red Hat Enterprise Linux 9: Training and Exam Preparation
Guide (EX200) (ISBN: 978-1775062165) (RHEL version 9), published
February 2023

\

2\. RHCSA Red Hat Enterprise Linux 8 (UPDATED): Training and Exam
Preparation Guide (EX200) (ISBN: 978-1775062141) (RHEL version 8),
published November 2020

\

3\. RHCSA Red Hat Enterprise Linux 8: Training and Exam Preparation
Guide (EX200) (ISBN: 978-1775062127) (RHEL version 8), published January
2020

\

4\. CompTIA Linux+/LPIC-1: Training and Exam Preparation Guide (Exam
Codes: LX0-103/101-400 and LX0-104/102-400) (ISBN: 978-1775062103),
published 2017

\

5\. RHCSA & RHCE Red Hat Enterprise Linux 7: Training and Exam
Preparation Guide (EX200 and EX300) (ISBN: 978-1495148200) (RHEL version
7), published 2015

\

6\. Red Hat Certified System Administrator & Engineer: Training Guide
and a Quick Deskside Reference (ISBN: 978-1467549400) (RHEL version 6),
published 2012

\

7\. Red Hat Certified Technician & Engineer (RHCT and RHCE) Training
Guide and Administrator's Reference (ISBN: 978-1615844302) (RHEL version
5), published 2009

\

8\. HP-UX: HP Certified Systems Administrator, Exam HP0-A01, Training
Guide and Administrator's Reference (ISBN: 978-1606436547) (HP-UX
11iv3), published 2008

\

9\. HP Certified Systems Administrator, Exam HP0-095, Training Guide and
Administrator's Reference (ISBN: 978-1424342310) (HP-UX 11iv2 and
11iv3), published 2007

\

10\. Certified System Administrator for HP-UX: Study Guide and
Administrator's Reference (ISBN: 978-1419645938) (HP-UX 11iv1),
published 2006

\

11\. Fundamentals of UNIX: published 2002

::: {style="page-break-before: always;"}
:::

[]{#chapter0006.html}

## Conventions Used in this Book {.style3}

\

The following typographic and other conventions are used in this book:

\

Book Antiqua Italic 10 pt. is used in text paragraphs to introduce new
terms. For example:

\

"Red Hat renamed the Red Hat Linux operating system series Red Hat
Enterprise Linux (RHEL) in 2003."

\

Times Roman Italic 10 pt. is used in text paragraphs to highlight names
of files, directories, commands, daemons, users, groups, hosts, domains,
and URLs. This font also highlights file and directory paths. For
example:

\

"To go directly from /etc to a subdirectory dir1 under user1's home
directory, create dir1, as . . . ."

\

Times New Roman 9 pt. is used to segregate command output, script/file
contents, and information expected to be entered in configuration files
from the surrounding text. It is also used in tables, index, and side
notes.

\

Times Roman Bold 10 pt. is used to highlight commands and command line
arguments that the user is expected to type and execute at the command
prompt. For example:

\

\[user1@server1 \~\]\$ ls -lt

\

Two white spaces (cp -p file1 /tmp) are employed between parts of a
typed command for the sake of clarity in text.

\

Hundreds of screenshots taken directly from the Linux terminal screens
showing commands and output are included. These screenshots will give
the readers of this book an idea of what they should expect to see in
their own lab environments.

\

All headings and sub-headings are in California FB font, and are bolded.

\

Ctrl+x key sequence implies that you hold down the Ctrl key and then
press the other key. Courier New font is used to highlight such
combinations. This font is also used to identify keystrokes, such as
Enter and Esc.

\

. . . . . . . . Dotted lines represent truncated command output.

\

Pictures at chapter start are the property of their respective owners or
taken from public domain.

\

Times Roman 8 pt. is used for notes.

\

Times Roman 8 pt. is used for warning messages.

\

Exam Tip surrounded by a solid box is included where necessary.

::: {style="page-break-before: always;"}
:::

[]{#chapter0007.html}

## The RHCSA 9 Exam and Exam Objectives {.style3}

\

The Red Hat Certified System Administrator (RHCSA) certification exam is
a performance-based hands-on exam designed for certification aspirants.
This exam is presented on a live server running Red Hat Enterprise Linux
9. This server has two RHEL 9-based virtual machines to accomplish the
exam tasks. During the exam, the candidates do not have access to any
external resources such as the internet, printed material, electronic
content, and mobile devices, except for the manuals and other
documentation that is installed on the exam virtual machines.

\

The official exam objectives (68 in total as of February 21, 2023) are
available for reference at
http://www.redhat.com/training/courses/ex200/examobjective. Visit the
URL for up-to-date information.

\

There are no pre-requisites to earn this certification.

\

The exam objectives are covered in detail in the chapters throughout
this book. An enumerated list of the objectives are presented below
along with the chapter number where each objective is discussed.

\

### Understand and Use Essential Tools {.style3}

1.Access a shell prompt and issue commands with correct syntax (chapter
2)

2.Use input-output redirection (\>, \>\>, \|, 2\>, etc) (chapter 7)

3.Use grep and regular expressions to analyze text (chapter 7)

4.Access remote systems using ssh (chapters 01 and 18)

5.Log in and switch users in multi-user targets (chapter 6)

6.Archive, compress, unpack, and uncompress files using tar, star, gzip,
and bzip2 (chapter 3)

7.Create and edit text files (chapter 3)

8.Create, delete, copy, and move files and directories (chapter 3)

9.Create hard and soft links (chapter 3)

10.List, set, and change standard ugo/rwx permissions (chapter 4)

11.Locate, read, and use system documentation including man, info, and
files in /usr/share/doc (chapter 2)

\

### Create Simple Shell Scripts {.style3}

12\. Conditionally execute code (use of: if, test, \[\], etc.) (chapter
21)

13\. Use Looping constructs (for, etc.) to process file, command line
input (chapter 21)

14\. Process script inputs (\$1, \$2, etc.) (chapter 21)

15\. Processing output of shell commands within a script (chapter 21)

\

### Operate Running Systems {.style3}

16\. Boot, reboot, and shut down a system normally (chapter 12)

17\. Boot systems into different targets manually (chapter 12)

18\. Interrupt the boot process in order to gain access to a system
(chapter 11)

19\. Identify CPU/memory intensive processes and kill processes (chapter
8)

20\. Adjust process scheduling (chapter 8)

21\. Manage tuning profiles (chapter 12)

22\. Locate and interpret system log files and journals (chapter 12)

23\. Preserve system journals (chapter 12)

24\. Start, stop, and check the status of network services (chapter 12)

25\. Securely transfer files between systems (chapter 18)

\

### Configure Local Storage {.style3}

26\. List, create, and delete partitions on MBR and GPT disks (chapter
13)

27\. Create and remove physical volumes (chapter 13)

28\. Assign physical volumes to volume groups (chapter 13)

29\. Create and delete logical volumes (chapter 13)

30\. Configure systems to mount file systems at boot by Universally
Unique ID (UUID) or label (chapter 14)

31\. Add new partitions and logical volumes, and swap to a system
non-destructively (chapters 13 and 14)

\

### Create and Configure File Systems {.style3}

32\. Create, mount, unmount, and use vfat, ext4, and xfs file systems
(chapter 14)

33\. Mount and unmount network file systems using NFS (chapter 16)

34\. Configure autofs (chapter 16)

35\. Extend existing logical volumes (chapters 13 and 14)

36\. Create and configure set-GID directories for collaboration (chapter
4)

37\. Diagnose and correct file permission problems (chapter 4)

\

### Deploy, Configure, and Maintain Systems {.style3}

38\. Schedule tasks using at and cron (chapter 8)

39\. Start and stop services and configure services to start
automatically at boot (chapter 12)

40\. Configure systems to boot into a specific target automatically
(chapter 12)

41\. Configure time service clients (chapter 17)

42\. Install and update software packages from Red Hat Network, a remote
repository, or from the local file system (chapter 9 and 10)

43\. Modify the system bootloader (chapter 11)

\

### Manage Basic Networking {.style3}

44\. Configure IPv4 and IPv6 addresses (chapter 15)

45\. Configure hostname resolution (chapter 17)

46\. Configure network services to start automatically at boot (chapter
12)

47\. Restrict network access using firewall-cmd/firewall (chapter 19)

\

### Manage Users and Groups {.style3}

48\. Create, delete, and modify local user accounts (chapter 5)

49\. Change passwords and adjust password aging for local user accounts
(chapter 5 and 6)

50\. Create, delete, and modify local groups and group memberships
(chapter 6)

51\. Configure superuser access (chapter 6)

\

### Manage Security {.style3}

52\. Configure firewall settings using firewall-cmd/firewalld (chapter
19)

53\. Manage default file permissions (chapter 04)

54\. Configure key-based authentication for SSH (chapter 18)

55\. Set enforcing and permissive modes for SELinux (chapter 20)

56\. List and identify SELinux file and process context (chapter 20)

57\. Restore default file contexts (chapter 20)

58\. Manage SELinux port labels (chapter 20)

59\. Use Boolean settings to modify system SELinux settings (chapter 20)

60\. Diagnose and address routine SELinux policy violations (chapter 20)

\

### Manage Containers {.style3}

61\. Find and retrieve container images from a remote registry (chapter
22)

62\. Inspect container images (chapter 22)

63\. Perform container management using commands such as podman and
skopeo (chapter 22)

64\. Build a container from a Containerfile (chapter 22)

65\. Perform basic container management such as running, starting,
stopping, and listing running containers (chapter 22)

66\. Run a service inside a container (chapter 22)

67\. Configure a container to start automatically as a systemd service
(chapter 22)

68\. Attach persistent storage to a container (chapter 22)

::: {style="page-break-before: always;"}
:::

[]{#chapter0008.html}

## Taking the Exam {.style3}

\

1\. Save time wherever possible, as time is of the essence during the
exam

2\. Make certain that any changes you make must survive system reboots

3\. Use any available text editor you feel comfortable with to modify
text configuration files

4\. Exam tasks are split into two groups and each group must be
performed in its own assigned virtual machine

5\. Inform the proctor right away if you encounter any issues with your
exam system or the virtual machines

6\. The exam is administered with no access to the Internet, electronic
devices, or written material

7\. Read each exam task fully and understand it thoroughly before
attempting it

8\. Read all storage tasks carefully and use the lsblk command as
explained in the book to identify the right disk to perform each task
on.

\

## Exam Fee and Registration Procedure {.style3}

\

The fee for the RHCSA exam is US\$400 (plus any applicable taxes), or
equivalent in local currencies. To register, visit
http://www.redhat.com/training/courses/ex200/examobjective, select your
location, and click Get Started to log in with your Red Hat credentials
to continue through the registration process. The RHCSA exam is based on
version 9, and it lasts for 3 hours.

::: {style="page-break-before: always;"}
:::

[]{#chapter0009.html}

## About this Book {.style3}

\

RHCSA Red Hat Enterprise Linux 9: Training and Exam Preparation Guide,
Third Edition provides an in-depth coverage of the latest RHCSA (version
9) EX200 exam objectives. The most definitive guide available on the
subject, this book explains concepts, analyzes configuration files,
describes command outputs, provides step-by-step procedures (includes
screenshots of actual commands executed and outputs they produced), and
challenges the readers' comprehension of the concepts and procedures by
presenting plenty of supplementary labs and sample realistic exam tasks
to perform on their own.

\

This book has 22 chapters that are organized logically, from building a
lab environment to the fundamentals of Linux to sophisticated Linux
administration topics. The book covers the topics on local RHEL 9
installation; initial interaction with the system; essential Linux
commands; file compression and archiving; file editing and manipulation;
standard and special permissions; file searching and access controls;
user monitoring and authentication files; users, groups, and password
aging; bash shell features and startup files; processes and job
scheduling; basic and advanced software administration techniques;
system boot process and bootloader; kernel management and system
initialization; logging and system tuning; basic and advanced storage
management tools and solutions; local file systems and swap regions;
network device and connection configuration; hostname resolution and
time synchronization; remote file systems and automounting; the secure
shell service; firewall and SELinux controls; bash shell scripting; and
operating system virtualization using containers.

\

Each chapter highlights the major topics and relevant exam objectives at
the beginning and ends with several review questions & answers and
Do-It-Yourself challenge labs. Throughout the book, figures, tables,
screenshots, examples, warnings, notes, and exam tips are furnished to
support explanation and exam preparation. There are four sample RHCSA
exams that are expected to be performed using the knowledge and skills
attained from reading the material, following the in-chapter exercises,
and completing the end-of-chapter challenge labs. The labs and the
sample exams include hints to relevant topics and/or exercises.

\

This book may be used as a self-learning guide by RHCSA 9 exam
aspirants, a resource by instructors and students to follow in physical
and virtual training sessions, an on-the-job resource for reference, and
an easy-to-understand guide by novice and non-RHEL administrators.

::: {style="page-break-before: always;"}
:::

[]{#chapter0010.html}

### TABLE OF CONTENTS {.style3 style="text-align: center"}

\

[Preface](#chapter0003.html)

[Acknowledgments](#chapter0004.html)

[About the Author](#chapter0005.html)

[Conventions Used in this Book](#chapter0006.html)

[About this Book](#chapter0009.html)

\

[01. Local Installation](#chapter0013.html)

[A Quick Look at Linux Development](#chapter0014.html)

[Linux History in a Nutshell](#chapter0015.html)

[Linux from Red Hat](#chapter0016.html)

[Lab Environment for Practice](#chapter0017.html)

[Lab Environment for In-Chapter Exercises](#chapter0018.html)

[Lab Environment for End-of-Chapter Labs](#chapter0019.html)

[The RHEL Installer Program](#chapter0020.html)

[Installation Logs](#chapter0021.html)

[Virtual Console Screens](#chapter0022.html)

[Exercise 1-1: Download and Install VirtualBox Software, and Create a
Virtual Machine](#chapter0023.html)

[Downloading and Installing VirtualBox](#chapter0024.html)

[Creating a Virtual Machine](#chapter0025.html)

[Exercise 1-2: Download and Install RHEL](#chapter0026.html)

[Downloading RHEL 9 ISO Image](#chapter0027.html)

[Attaching RHEL 9 ISO Image to the Virtual Machine](#chapter0028.html)

[Launching the Installer](#chapter0029.html)

[Adding Support for Keyboards and Languages](#chapter0030.html)

[Configuring Time & Date](#chapter0031.html)

[Choosing an Installation Source](#chapter0032.html)

[Selecting Software to be Installed](#chapter0033.html)

[Configuring Installation Destination](#chapter0034.html)

[Configuring Network and Hostname](#chapter0035.html)

[Configuring User Settings](#chapter0036.html)

[Beginning Installation](#chapter0037.html)

[Concluding Installation](#chapter0038.html)

[Changing Default Boot Order](#chapter0039.html)

[Logging In and Out at the Graphical Console](#chapter0040.html)

[Logging In for the First Time](#chapter0041.html)

[Logging Out](#chapter0042.html)

[Exercise 1-3: Logging In from Windows](#chapter0043.html)

[Chapter Summary](#chapter0044.html)

[Review Questions](#chapter0045.html)

[Answers to Review Questions](#chapter0046.html)

[Do-It-Yourself Challenge Labs](#chapter0047.html)

[Lab 1-1: Build RHEL9-VM2 (server2)](#chapter0048.html)

\

[02. Initial Interaction with the System](#chapter0049.html)

[Linux Graphical Environment](#chapter0050.html)

[Display/Login Manager](#chapter0051.html)

[Desktop Environment](#chapter0052.html)

[Linux Directory Structure and File Systems](#chapter0053.html)

[Top-Level Directories](#chapter0054.html)

[File System Categories](#chapter0055.html)

[The Root File System (/), Disk-Based](#chapter0056.html)

[The Boot File System (/boot), Disk-Based](#chapter0057.html)

[The Home Directory (/home)](#chapter0058.html)

[The Optional Directory (/opt)](#chapter0059.html)

[The UNIX System Resources Directory (/usr)](#chapter0060.html)

[The Variable Directory (/var)](#chapter0061.html)

[The Temporary Directory (/tmp)](#chapter0062.html)

[The Devices File System (/dev), Virtual](#chapter0063.html)

[The Procfs File System (/proc), Virtual](#chapter0064.html)

[The Runtime File System (/run), Virtual](#chapter0065.html)

[The System File System (/sys), Virtual](#chapter0066.html)

[Essential System Commands](#chapter0067.html)

[Starting a Remote Terminal Session](#chapter0068.html)

[Understanding the Command Mechanics](#chapter0069.html)

[Listing Files and Directories](#chapter0070.html)

[Printing Working Directory](#chapter0071.html)

[Navigating Directories](#chapter0072.html)

[Viewing Directory Hierarchy](#chapter0073.html)

[Identifying Terminal Device File](#chapter0074.html)

[Inspecting System's Uptime and Processor Load](#chapter0075.html)

[Clearing the Screen](#chapter0076.html)

[Determining Command Path](#chapter0077.html)

[Viewing System Information](#chapter0078.html)

[Viewing CPU Specs](#chapter0079.html)

[Getting Help](#chapter0080.html)

[Accessing Manual Pages](#chapter0081.html)

[Headings in the Manual](#chapter0082.html)

[Manual Sections](#chapter0083.html)

[Searching by Keyword](#chapter0084.html)

[Exposing Short Description](#chapter0085.html)

[Documentation in the /usr/share/doc Directory](#chapter0086.html)

[Red Hat Enterprise Linux 9 Documentation](#chapter0087.html)

[Chapter Summary](#chapter0088.html)

[Review Questions](#chapter0089.html)

[Answers to Review Questions](#chapter0090.html)

[Do-It-Yourself Challenge Labs](#chapter0091.html)

[Lab 2-1: Navigate Linux Directory Tree](#chapter0092.html)

[Lab 2-2: Miscellaneous Tasks](#chapter0093.html)

[Lab 2-3: Identify System and Kernel Information](#chapter0094.html)

[Lab 2-4: Use Help](#chapter0095.html)

\

[03. Basic File Management](#chapter0096.html)

[Common File Types](#chapter0097.html)

[Regular Files](#chapter0098.html)

[Directory Files](#chapter0099.html)

[Block and Character Special Device Files](#chapter0100.html)

[Symbolic Links](#chapter0101.html)

[Compression and Archiving](#chapter0102.html)

[Using gzip and gunzip](#chapter0103.html)

[Using bzip2 and bunzip2](#chapter0104.html)

[Differences between gzip and bzip2](#chapter0105.html)

[Using tar](#chapter0106.html)

[Exercise 3-1: Create Compressed Archives](#chapter0107.html)

[File Editing](#chapter0108.html)

[Modes of Operation](#chapter0109.html)

[Starting vim](#chapter0110.html)

[Inserting text](#chapter0111.html)

[Navigating within vim](#chapter0112.html)

[Revealing Line Numbering](#chapter0113.html)

[Deleting Text](#chapter0114.html)

[Undoing and Repeating](#chapter0115.html)

[Searching for Text](#chapter0116.html)

[Replacing Text](#chapter0117.html)

[Copying, Moving, and Pasting Text](#chapter0118.html)

[Changing Text](#chapter0119.html)

[Saving and Quitting vim](#chapter0120.html)

[File and Directory Operations](#chapter0121.html)

[Creating Files and Directories](#chapter0122.html)

[Displaying File Contents](#chapter0123.html)

[Counting Words, Lines, and Characters in Text Files](#chapter0124.html)

[Copying Files and Directories](#chapter0125.html)

[Moving and Renaming Files and Directories](#chapter0126.html)

[Removing Files and Directories](#chapter0127.html)

[File Linking](#chapter0128.html)

[Hard Link](#chapter0129.html)

[Soft Link](#chapter0130.html)

[Differences between Copying and Linking](#chapter0131.html)

[Exercise 3-2: Create and Manage Hard Links](#chapter0132.html)

[Exercise 3-3: Create and Manage Soft Links](#chapter0133.html)

[Chapter Summary](#chapter0134.html)

[Review Questions](#chapter0135.html)

[Answers to Review Questions](#chapter0136.html)

[Do-It-Yourself Challenge Labs](#chapter0137.html)

[Lab 3-1: Archive, List, and Restore Files](#chapter0138.html)

[Lab 3-2: Practice the vim Editor](#chapter0139.html)

[Lab 3-3: File and Directory Operations](#chapter0140.html)

\

[04. Advanced File Management](#chapter0141.html)

[File and Directory Access Permissions](#chapter0142.html)

[Determining Access Permissions](#chapter0143.html)

[Permission Classes](#chapter0144.html)

[Permission Types](#chapter0145.html)

[Permission Modes](#chapter0146.html)

[Modifying Access Permission Bits](#chapter0147.html)

[Exercise 4-1: Modify Permission Bits Using Symbolic
Form](#chapter0148.html)

[Exercise 4-2: Modify Permission Bits Using Octal
Form](#chapter0149.html)

[Default Permissions](#chapter0150.html)

[Calculating Default Permissions](#chapter0151.html)

[Special File Permissions](#chapter0152.html)

[The setuid Bit on Binary Executable Files](#chapter0153.html)

[Exercise 4-3: Test the Effect of setuid Bit on Executable
Files](#chapter0154.html)

[The setgid Bit on Binary Executable Files](#chapter0155.html)

[Exercise 4-4: Test the Effect of setgid Bit on Executable
Files](#chapter0156.html)

[The setgid Bit on Shared Directories](#chapter0157.html)

[Exercise 4-5: Set up Shared Directory for Group
Collaboration](#chapter0158.html)

[The Sticky Bit on Public and Shared Writable
Directories](#chapter0159.html)

[Exercise 4-6: Test the Effect of Sticky Bit](#chapter0160.html)

[File Searching](#chapter0161.html)

[Using the find Command](#chapter0162.html)

[Using find with -exec and -ok Flags](#chapter0163.html)

[Chapter Summary](#chapter0164.html)

[Review Questions](#chapter0165.html)

[Answers to Review Questions](#chapter0166.html)

[Do-It-Yourself Challenge Labs](#chapter0167.html)

[Lab 4-1: Manipulate File Permissions](#chapter0168.html)

[Lab 4-2: Configure Group Collaboration and Prevent File
Deletion](#chapter0169.html)

[Lab 4-3: Find Files](#chapter0170.html)

[Lab 4-4: Find Files Using Different Criteria](#chapter0171.html)

\

[05. Basic User Management](#chapter0172.html)

[User Login Activity and Information](#chapter0173.html)

[Listing Logged-In Users](#chapter0174.html)

[Inspecting History of Successful Login Attempts and System
Reboots](#chapter0175.html)

[Viewing History of Failed User Login Attempts](#chapter0176.html)

[Reporting Recent User Login Attempts](#chapter0177.html)

[Examining User and Group Information](#chapter0178.html)

[Local User Authentication Files](#chapter0179.html)

[The passwd File](#chapter0180.html)

[The shadow File](#chapter0181.html)

[The group File](#chapter0182.html)

[The gshadow File](#chapter0183.html)

[The useradd and login.defs Configuration Files](#chapter0184.html)

[User Account Management](#chapter0185.html)

[The useradd, usermod, and userdel Commands](#chapter0186.html)

[Exercise 5-1: Create a User Account with Default
Attributes](#chapter0187.html)

[Exercise 5-2: Create a User Account with Custom
Values](#chapter0188.html)

[Exercise 5-3: Modify and Delete a User Account](#chapter0189.html)

[No-Login (Non-Interactive) User Account](#chapter0190.html)

[Exercise 5-4: Create a User Account with No-Login
Access](#chapter0191.html)

[Chapter Summary](#chapter0192.html)

[Review Questions](#chapter0193.html)

[Answers to Review Questions](#chapter0194.html)

[Do-It-Yourself Challenge Labs](#chapter0195.html)

[Lab 5-1: Check User Login Attempts](#chapter0196.html)

[Lab 5-2: Verify User and Group Identity](#chapter0197.html)

[Lab 5-3: Create Users](#chapter0198.html)

[Lab 5-4: Create User with Non-Interactive Shell](#chapter0199.html)

\

[06. Advanced User Management](#chapter0200.html)

[Password Aging and its Management](#chapter0201.html)

[The chage Command](#chapter0202.html)

[Exercise 6-1: Set and Confirm Password Aging with
chage](#chapter0203.html)

[The passwd Command](#chapter0204.html)

[Exercise 6-2: Set and Confirm Password Aging with
passwd](#chapter0205.html)

[The usermod Command](#chapter0206.html)

[Exercise 6-3: Lock and Unlock a User Account with usermod and
passwd](#chapter0207.html)

[Linux Groups and their Management](#chapter0208.html)

[The groupadd, groupmod, and groupdel Commands](#chapter0209.html)

[Exercise 6-4: Create a Group and Add Members](#chapter0210.html)

[Exercise 6-5: Modify and Delete a Group Account](#chapter0211.html)

[Substituting Users and Doing as Superuser](#chapter0212.html)

[Substituting (or Switching) Users](#chapter0213.html)

[Doing as Superuser (or Doing as Substitute User)](#chapter0214.html)

[Owning User and Owning Group](#chapter0215.html)

[Exercise 6-6: Modify File Owner and Owning Group](#chapter0216.html)

[Chapter Summary](#chapter0217.html)

[Review Questions](#chapter0218.html)

[Answers to Review Questions](#chapter0219.html)

[Do-It-Yourself Challenge Labs](#chapter0220.html)

[Lab 6-1: Create User and Configure Password Aging](#chapter0221.html)

[Lab 6-2: Lock and Unlock User](#chapter0222.html)

[Lab 6-3: Modify Group](#chapter0223.html)

[Lab 6-4: Configure sudo Access](#chapter0224.html)

[Lab 6-5: Modify Owning User and Group](#chapter0225.html)

\

[07. The Bash Shell](#chapter0226.html)

[The Bourne-Again Shell](#chapter0227.html)

[Shell and Environment Variables](#chapter0228.html)

[Setting and Unsetting Variables](#chapter0229.html)

[Command and Variable Substitutions](#chapter0230.html)

[Exercise 7-1: Modify Primary Command Prompt](#chapter0231.html)

[Input, Output, and Error Redirections](#chapter0232.html)

[History Substitution](#chapter0233.html)

[Editing at the Command Line](#chapter0234.html)

[Tab Completion](#chapter0235.html)

[Tilde Substitution](#chapter0236.html)

[Alias Substitution](#chapter0237.html)

[Metacharacters and Wildcard Characters](#chapter0238.html)

[Piping Output of One Command as Input to Another](#chapter0239.html)

[Quoting Mechanisms](#chapter0240.html)

[Regular Expressions](#chapter0241.html)

[Shell Startup Files](#chapter0242.html)

[System-wide Shell Startup Files](#chapter0243.html)

[Per-user Shell Startup Files](#chapter0244.html)

[Chapter Summary](#chapter0245.html)

[Review Questions](#chapter0246.html)

[Answers to Review Questions](#chapter0247.html)

[Do-It-Yourself Challenge Labs](#chapter0248.html)

[Lab 7-1: Customize the Command Prompt](#chapter0249.html)

[Lab 7-2: Redirect the Standard Input, Output, and
Error](#chapter0250.html)

\

[08. Linux Processes and Job Scheduling](#chapter0251.html)

[Processes and Priorities](#chapter0252.html)

[Process States](#chapter0253.html)

[Viewing and Monitoring Processes with ps](#chapter0254.html)

[Viewing and Monitoring Processes with top](#chapter0255.html)

[Listing a Specific Process](#chapter0256.html)

[Listing Processes by User and Group Ownership](#chapter0257.html)

[Understanding Process Niceness and Priority](#chapter0258.html)

[Exercise 8-1: Start Processes at Non-Default
Priorities](#chapter0259.html)

[Exercise 8-2: Alter Process Priorities](#chapter0260.html)

[Controlling Processes with Signals](#chapter0261.html)

[Job Scheduling](#chapter0262.html)

[Controlling User Access](#chapter0263.html)

[Scheduler Log File](#chapter0264.html)

[Using at](#chapter0265.html)

[Exercise 8-3: Submit, View, List, and Erase an at
Job](#chapter0266.html)

[Using crontab](#chapter0267.html)

[Syntax of User Crontables](#chapter0268.html)

[Exercise 8-4: Add, List, and Erase a Cron Job](#chapter0269.html)

[Chapter Summary](#chapter0270.html)

[Review Questions](#chapter0271.html)

[Answers to Review Questions](#chapter0272.html)

[Do-It-Yourself Challenge Labs](#chapter0273.html)

[Lab 8-1: Nice and Renice a Process](#chapter0274.html)

[Lab 8-2: Configure a User Crontab File](#chapter0275.html)

\

[09. Basic Package Management](#chapter0276.html)

[Package Overview](#chapter0277.html)

[Packages and Packaging](#chapter0278.html)

[Package Naming](#chapter0279.html)

[Package Dependency](#chapter0280.html)

[Package Database](#chapter0281.html)

[Package Management Tools](#chapter0282.html)

[Package Management with rpm](#chapter0283.html)

[The rpm Command](#chapter0284.html)

[Exercise 9-1: Mount RHEL 9 ISO Persistently](#chapter0285.html)

[Querying Packages](#chapter0286.html)

[Installing a Package](#chapter0287.html)

[Upgrading a Package](#chapter0288.html)

[Freshening a Package](#chapter0289.html)

[Overwriting a Package](#chapter0290.html)

[Removing a Package](#chapter0291.html)

[Extracting Files from an Installable Package](#chapter0292.html)

[Validating Package Integrity and Credibility](#chapter0293.html)

[Viewing GPG Keys](#chapter0294.html)

[Verifying Package Attributes](#chapter0295.html)

[Exercise 9-2: Perform Package Management Using rpm](#chapter0296.html)

[Chapter Summary](#chapter0297.html)

[Review Questions](#chapter0298.html)

[Answers to Review Questions](#chapter0299.html)

[Do-It-Yourself Challenge Labs](#chapter0300.html)

[Lab 9-1: Install and Verify Packages](#chapter0301.html)

[Lab 9-2: Query and Erase Packages](#chapter0302.html)

\

[10. Advanced Package Management](#chapter0303.html)

[Advanced Package Management Concepts](#chapter0304.html)

[Package Groups](#chapter0305.html)

[BaseOS Repository](#chapter0306.html)

[AppStream Repository](#chapter0307.html)

[Benefits of Segregation](#chapter0308.html)

[dnf Repository](#chapter0309.html)

[Software Management with dnf](#chapter0310.html)

[dnf Configuration File](#chapter0311.html)

[The dnf Command](#chapter0312.html)

[Exercise 10-1: Configure Access to Pre-Built
Repositories](#chapter0313.html)

[Individual Package Management](#chapter0314.html)

[Listing Available and Installed Packages](#chapter0315.html)

[Installing and Updating Packages](#chapter0316.html)

[Exhibiting Package Information](#chapter0317.html)

[Removing Packages](#chapter0318.html)

[Exercise 10-2: Manipulate Individual Packages](#chapter0319.html)

[Determining Provider and Searching Package Metadata](#chapter0320.html)

[Package Group Management](#chapter0321.html)

[Listing Available and Installed Package Groups](#chapter0322.html)

[Installing and Updating Package Groups](#chapter0323.html)

[Removing Package Groups](#chapter0324.html)

[Exercise 10-3: Manipulate Package Groups](#chapter0325.html)

[Chapter Summary](#chapter0326.html)

[Review Questions](#chapter0327.html)

[Answers to Review Questions](#chapter0328.html)

[Do-It-Yourself Challenge Labs](#chapter0329.html)

[Lab 10-1: Configure Access to RHEL 9 Repositories](#chapter0330.html)

[Lab 10-2: Install and Manage Individual Packages](#chapter0331.html)

[Lab 10-3: Install and Manage Package Groups](#chapter0332.html)

\

[11. Boot Process, GRUB2, and the Linux Kernel](#chapter0333.html)

[Linux Boot Process](#chapter0334.html)

[The Firmware Phase (BIOS and UEFI)](#chapter0335.html)

[The Bootloader Phase](#chapter0336.html)

[The Kernel Phase](#chapter0337.html)

[The Initialization Phase](#chapter0338.html)

[The GRUB2 Bootloader](#chapter0339.html)

[Interacting with GRUB2](#chapter0340.html)

[Understanding GRUB2 Configuration Files](#chapter0341.html)

[Exercise 11-1: Change Default System Boot Timeout](#chapter0342.html)

[Booting into Specific Targets](#chapter0342.html)

[Exercise 11-2: Reset the root User Password](#chapter0343.html)

[The Linux Kernel](#chapter0344.html)

[Kernel Packages](#chapter0345.html)

[Analyzing Kernel Version](#chapter0346.html)

[Understanding Kernel Directory Structure](#chapter0347.html)

[Installing the Kernel](#chapter0348.html)

[Exercise 11-3: Download and Install a New Kernel](#chapter0349.html)

[Chapter Summary](#chapter0350.html)

[Review Questions](#chapter0351.html)

[Answers to Review Questions](#chapter0352.html)

[Do-It-Yourself Challenge Labs](#chapter0353.html)

[Lab 11-1: Enable Verbose System Boot](#chapter0354.html)

[Lab 11-2: Reset root User Password](#chapter0355.html)

[Lab 11-3: Install New Kernel](#chapter0356.html)

\

[12. System Initialization, Message Logging, and System
Tuning](#chapter0357.html)

[System Initialization and Service Management](#chapter0358.html)

[Units](#chapter0359.html)

[Targets](#chapter0360.html)

[The systemctl Command](#chapter0361.html)

[Listing and Viewing Units](#chapter0362.html)

[Managing Service Units](#chapter0363.html)

[Managing Target Units](#chapter0364.html)

[System Logging](#chapter0365.html)

[The Syslog Configuration File](#chapter0366.html)

[Rotating Log Files](#chapter0367.html)

[The Boot Log File](#chapter0368.html)

[The System Log File](#chapter0369.html)

[Logging Custom Messages](#chapter0370.html)

[The systemd Journal](#chapter0371.html)

[Retrieving and Viewing Messages](#chapter0372.html)

[Preserving Journal Information](#chapter0373.html)

[Exercise 12-1: Configure Persistent Storage for Journal
Information](#chapter0374.html)

[System Tuning](#chapter0375.html)

[Tuning Profiles](#chapter0376.html)

[The tuned-adm Command](#chapter0377.html)

[Exercise 12-2: Manage Tuning Profiles](#chapter0378.html)

[Chapter Summary](#chapter0379.html)

[Review Questions](#chapter0380.html)

[Answers to Review Questions](#chapter0381.html)

[Do-It-Yourself Challenge Labs](#chapter0382.html)

[Lab 12-1: Modify Default Boot Target](#chapter0383.html)

[Lab 12-2: Record Custom Alerts](#chapter0384.html)

[Lab 12-3: Apply Tuning Profile](#chapter0385.html)

\

[13. Storage Management](#chapter0386.html)

[Storage Management Overview](#chapter0387.html)

[Master Boot Record (MBR)](#chapter0388.html)

[GUID Partition Table (GPT)](#chapter0389.html)

[Disk Partitions](#chapter0390.html)

[Storage Management Tools](#chapter0391.html)

[Thin Provisioning](#chapter0392.html)

[Adding Storage for Practice](#chapter0393.html)

[Exercise 13-1: Add Required Storage to server2](#chapter0394.html)

[MBR Storage Management with parted](#chapter0395.html)

[Exercise 13-2: Create an MBR Partition](#chapter0396.html)

[Exercise 13-3: Delete an MBR Partition](#chapter0397.html)

[GPT Storage Management with gdisk](#chapter0398.html)

[Exercise 13-4: Create a GPT Partition](#chapter0399.html)

[Exercise 13-5: Delete a GPT Partition](#chapter0400.html)

[Logical Volume Manager (LVM)](#chapter0401.html)

[Physical Volume](#chapter0402.html)

[Volume Group](#chapter0403.html)

[Physical Extent](#chapter0404.html)

[Logical Volume](#chapter0405.html)

[Logical Extent](#chapter0406.html)

[LVM Operations and Commands](#chapter0407.html)

[Exercise 13-6: Create Physical Volume and Volume
Group](#chapter0408.html)

[Exercise 13-7: Create Logical Volumes](#chapter0409.html)

[Exercise 13-8: Extend a Volume Group and a Logical
Volume](#chapter0410.html)

[Exercise 13-9: Rename, Reduce, Extend, and Remove Logical
Volumes](#chapter0411.html)

[Exercise 13-10: Reduce and Remove a Volume Group](#chapter0412.html)

[Exercise 13-11: Uninitialize Physical Volumes](#chapter0413.html)

[Storage Optimization with Virtual Data Optimizer
(VDO)](#chapter0414.html)

[How VDO Conserves Storage](#chapter0415.html)

[VDO Integration with LVM](#chapter0416.html)

[VDO Components](#chapter0417.html)

[Exercise 13-12: Create an LVM VDO Volume](#chapter0418.html)

[Exercise 13-13: Remove a Volume Group and Uninitialize Physical
Volume](#chapter0419.html)

[Chapter Summary](#chapter0420.html)

[Review Questions](#chapter0421.html)

[Answers to Review Questions](#chapter0422.html)

[Do-It-Yourself Challenge Labs](#chapter0423.html)

[Lab 13-1: Create and Remove Partitions with parted](#chapter0424.html)

[Lab 13-2: Create and Remove Partitions with gdisk](#chapter0425.html)

[Lab 13-3: Create Volume Group and Logical Volumes](#chapter0426.html)

[Lab 13-4: Expand Volume Group and Logical Volume](#chapter0427.html)

[Lab 13-5: Add a VDO Logical Volume](#chapter0428.html)

[Lab 13-6: Reduce and Remove Logical Volumes](#chapter0429.html)

[Lab 13-7: Remove Volume Group and Physical Volumes](#chapter0430.html)

\

[14. Local File Systems and Swap](#chapter0431.html)

[File Systems and File System Types](#chapter0432.html)

[Extended File Systems](#chapter0433.html)

[XFS File System](#chapter0434.html)

[VFAT File System](#chapter0435.html)

[ISO9660 File System](#chapter0436.html)

[File System Management](#chapter0437.html)

[File System Administration Commands](#chapter0438.html)

[Mounting and Unmounting File Systems](#chapter0439.html)

[Determining the UUID of a File System](#chapter0440.html)

[Labeling a File System](#chapter0441.html)

[Automatically Mounting a File System at Reboots](#chapter0442.html)

[Monitoring File System Usage](#chapter0443.html)

[Calculating Disk Usage](#chapter0444.html)

[Exercise 14-1: Create and Mount Ext4, VFAT, and XFS File Systems in
Partitions](#chapter0445.html)

[Exercise 14-2: Create and Mount Ext4 and XFS File Systems in LVM
Logical Volumes](#chapter0446.html)

[Exercise 14-3: Resize Ext4 and XFS File Systems in LVM Logical
Volumes](#chapter0447.html)

[Exercise 14-4: Create and Mount XFS File System in LVM VDO
Volume](#chapter0448.html)

[Swap and its Management](#chapter0449.html)

[Determining Current Swap Usage](#chapter0450.html)

[Prioritizing Swap Spaces](#chapter0451.html)

[Swap Administration Commands](#chapter0452.html)

[Exercise 14-5: Create and Activate Swap in Partition and Logical
Volume](#chapter0453.html)

[Chapter Summary](#chapter0454.html)

[Review Questions](#chapter0455.html)

[Answers to Review Questions](#chapter0456.html)

[Do-It-Yourself Challenge Labs](#chapter0457.html)

[Lab 14-1: Create VFAT, Ext4, and XFS File Systems in Partitions and
Mount Persistently](#chapter0458.html)

[Lab 14-2: Create XFS File System in LVM VDO Volume and Mount
Persistently](#chapter0459.html)

[Lab 14-3: Create Ext4 and XFS File Systems in LVM Volumes and Mount
Persistently](#chapter0460.html)

[Lab 14-4: Extend Ext4 and XFS File Systems in LVM
Volumes](#chapter0461.html)

[Lab 14-5: Create Swap in Partition and LVM Volume and Activate
Persistently](#chapter0462.html)

\

[15. Networking, Network Devices, and Network
Connections](#chapter0463.html)

[Networking Fundamentals](#chapter0464.html)

[Hostname](#chapter0465.html)

[Exercise 15-1: Change System Hostname](#chapter0466.html)

[IPv4 Address](#chapter0467.html)

[Classful Network Addressing](#chapter0468.html)

[Subnetting](#chapter0469.html)

[Subnet Mask](#chapter0470.html)

[Classless Network Addressing](#chapter0471.html)

[Protocol](#chapter0472.html)

[TCP and UDP Protocols](#chapter0473.html)

[Well-Known Ports](#chapter0474.html)

[ICMP Protocol](#chapter0475.html)

[Ethernet Address](#chapter0476.html)

[IPv6 Address](#chapter0477.html)

[Major Differences between IPv4 and IPv6](#chapter0478.html)

[Network Devices and Connections](#chapter0479.html)

[Consistent Network Device Naming](#chapter0480.html)

[Exercise 15-2: Add Network Devices to server10 and
server20](#chapter0481.html)

[The NetworkManager Service](#chapter0482.html)

[Understanding Interface Connection Profile](#chapter0483.html)

[Network Device and Connection Administration Tools](#chapter0484.html)

[The nmcli Command](#chapter0485.html)

[Exercise 15-3: Configure New Network Connection
Manually](#chapter0486.html)

[Exercise 15-4: Configure New Network Connection Using
nmcli](#chapter0487.html)

[Understanding Hosts Table](#chapter0488.html)

[Testing Network Connectivity](#chapter0489.html)

[Exercise 15-5: Update Hosts Table and Test
Connectivity](#chapter0490.html)

[Chapter Summary](#chapter0491.html)

[Review Questions](#chapter0492.html)

[Answers to Review Questions](#chapter0493.html)

[Do-It-Yourself Challenge Labs](#chapter0494.html)

[Lab 15-1: Add New Interface and Configure Connection Profile with
nmcli](#chapter0495.html)

[Lab 15-2: Add New Interface and Configure Connection Profile
Manually](#chapter0496.html)

\

[16. Network File System](#chapter0497.html)

[Network File System](#chapter0498.html)

[Benefits of Using NFS](#chapter0499.html)

[NFS Versions](#chapter0500.html)

[NFS Server and Client Configuration](#chapter0501.html)

[Exercise 16-1: Export Share on NFS Server](#chapter0502.html)

[Exercise 16-2: Mount Share on NFS Client](#chapter0503.html)

[Auto File System (AutoFS)](#chapter0504.html)

[Benefits of Using AutoFS](#chapter0505.html)

[How AutoFS Works](#chapter0506.html)

[AutoFS Configuration File](#chapter0507.html)

[AutoFS Maps](#chapter0508.html)

[Exercise 16-3: Access NFS Share Using Direct Map](#chapter0509.html)

[Exercise 16-4: Access NFS Share Using Indirect Map](#chapter0510.html)

[Automounting User Home Directories](#chapter0511.html)

[Exercise 16-5: Automount User Home Directories Using Indirect
Map](#chapter0512.html)

[Chapter Summary](#chapter0513.html)

[Review Questions](#chapter0514.html)

[Answers to Review Questions](#chapter0515.html)

[Do-It-Yourself Challenge Labs](#chapter0516.html)

[Lab 16-1: Configure NFS Share and Automount with Direct
Map](#chapter0517.html)

[Lab 16-2: Automount NFS Share with Indirect Map](#chapter0518.html)

\

[17. Hostname Resolution and Time Synchronization](#chapter0519.html)

[DNS and Name Resolution](#chapter0520.html)

[DNS Name Space and Domains](#chapter0521.html)

[DNS Roles](#chapter0522.html)

[Understanding Resolver Configuration File](#chapter0523.html)

[Viewing and Adjusting Name Resolution Sources and
Order](#chapter0524.html)

[Performing Name Resolution with dig](#chapter0525.html)

[Performing Name Resolution with host](#chapter0526.html)

[Performing Name Resolution with nslookup](#chapter0527.html)

[Performing Name Resolution with getent](#chapter0528.html)

[Time Synchronization](#chapter0529.html)

[Time Sources](#chapter0530.html)

[NTP Roles](#chapter0531.html)

[Stratum Levels](#chapter0532.html)

[Chrony Configuration File](#chapter0533.html)

[Chrony Daemon and Command](#chapter0534.html)

[Exercise 17-1: Configure NTP Client](#chapter0535.html)

[Displaying and Setting System Date and Time](#chapter0536.html)

[Chapter Summary](#chapter0537.html)

[Review Questions](#chapter0538.html)

[Answers to Review Questions](#chapter0539.html)

[Do-It-Yourself Challenge Labs](#chapter0540.html)

[Lab 17-1: Configure Chrony](#chapter0541.html)

[Lab 17-2: Modify System Date and Time](#chapter0542.html)

\

[18. The Secure Shell Service](#chapter0543.html)

[The OpenSSH Service](#chapter0544.html)

[Common Encryption Techniques](#chapter0545.html)

[Authentication Methods](#chapter0546.html)

[OpenSSH Protocol Version and Algorithms](#chapter0547.html)

[OpenSSH Packages](#chapter0548.html)

[OpenSSH Server Daemon and Client Commands](#chapter0549.html)

[Server Configuration File](#chapter0550.html)

[Client Configuration File](#chapter0551.html)

[System Access and File Transfer](#chapter0552.html)

[Exercise 18-1: Access RHEL System from Another RHEL
System](#chapter0553.html)

[Exercise 18-2: Generate, Distribute, and Use SSH
Keys](#chapter0554.html)

[Executing Commands Remotely Using ssh](#chapter0555.html)

[Transferring Files Remotely Using sftp](#chapter0556.html)

[Chapter Summary](#chapter0557.html)

[Review Questions](#chapter0558.html)

[Answers to Review Questions](#chapter0559.html)

[Do-It-Yourself Challenge Labs](#chapter0560.html)

[Lab 18-1: Establish Key-Based Authentication](#chapter0561.html)

[Lab 18-2: Test the Effect of PermitRootLogin
Directive](#chapter0562.html)

\

[19. The Linux Firewall](#chapter0563.html)

[Firewall Overview](#chapter0564.html)

[Overview of the firewalld Service](#chapter0565.html)

[firewalld Zones](#chapter0566.html)

[Zone Configuration Files](#chapter0567.html)

[firewalld Services](#chapter0568.html)

[Service Configuration Files](#chapter0569.html)

[Firewalld Management](#chapter0570.html)

[The firewall-cmd Command](#chapter0571.html)

[Querying the Operational Status of firewalld](#chapter0572.html)

[Exercise 19-1: Add Services and Ports, and Manage
Zones](#chapter0573.html)

[Exercise 19-2: Remove Services and Ports, and Manage
Zones](#chapter0574.html)

[Exercise 19-3: Test the Effect of Firewall Rule](#chapter0575.html)

[Chapter Summary](#chapter0576.html)

[Review Questions](#chapter0577.html)

[Answers to Review Questions](#chapter0578.html)

[Do-It-Yourself Challenge Labs](#chapter0579.html)

[Lab 19-1: Add Service to Firewall](#chapter0580.html)

[Lab 19-2: Add Port Range to Firewall](#chapter0581.html)

\

[20. Security Enhanced Linux](#chapter0582.html)

[Security Enhanced Linux](#chapter0583.html)

[Terminology](#chapter0584.html)

[SELinux Contexts for Users](#chapter0585.html)

[SELinux Contexts for Processes](#chapter0586.html)

[SELinux Contexts for Files](#chapter0587.html)

[Copying, Moving, and Archiving Files with SELinux
Contexts](#chapter0588.html)

[SELinux Contexts for Ports](#chapter0589.html)

[Domain Transitioning](#chapter0590.html)

[SELinux Booleans](#chapter0591.html)

[SELinux Administration](#chapter0592.html)

[Management Commands](#chapter0593.html)

[Viewing and Controlling SELinux Operational State](#chapter0594.html)

[Querying Status](#chapter0595.html)

[Exercise 20-1: Modify SELinux File Context](#chapter0596.html)

[Exercise 20-2: Add and Apply File Context](#chapter0597.html)

[Exercise 20-3: Add and Delete Network Ports](#chapter0598.html)

[Exercise 20-4: Copy Files with and without Context](#chapter0599.html)

[Exercise 20-5: View and Toggle SELinux Boolean
Values](#chapter0600.html)

[Monitoring and Analyzing SELinux Violations](#chapter0601.html)

[Chapter Summary](#chapter0602.html)

[Review Questions](#chapter0603.html)

[Answers to Review Questions](#chapter0604.html)

[Do-It-Yourself Challenge Labs](#chapter0605.html)

[Lab 20-1: Disable and Enable the SELinux Operating
Mode](#chapter0606.html)

[Lab 20-2: Modify Context on Files](#chapter0607.html)

[Lab 20-3: Add Network Port to Policy Database](#chapter0608.html)

[Lab 20-4: Copy Files with and without Context](#chapter0609.html)

[Lab 20-5: Flip SELinux Booleans](#chapter0610.html)

\

[21. Shell Scripting](#chapter0611.html)

[Shell Scripts](#chapter0612.html)

[Script01: Displaying System Information](#chapter0613.html)

[Executing a Script](#chapter0614.html)

[Debugging a Script](#chapter0615.html)

[Script02: Using Local Variables](#chapter0616.html)

[Script03: Using Pre-Defined Environment Variables](#chapter0617.html)

[Script04: Using Command Substitution](#chapter0618.html)

[Understanding Shell Parameters](#chapter0619.html)

[Script05: Using Special and Positional Parameters](#chapter0620.html)

[Script06: Shifting Command Line Arguments](#chapter0621.html)

[Logical Constructs](#chapter0622.html)

[Exit Codes](#chapter0623.html)

[Test Conditions](#chapter0624.html)

[The if-then-fi Construct](#chapter0625.html)

[Script07: The if-then-fi Construct](#chapter0626.html)

[The if-then-else-fi Construct](#chapter0627.html)

[Script08: The if-then-else-fi Construct](#chapter0628.html)

[The if-then-elif-fi Construct](#chapter0629.html)

[Script09: The if-then-elif-fi Construct (Example 1)](#chapter0630.html)

[Script10: The if-then-elif-fi Construct (Example 2)](#chapter0631.html)

[Looping Constructs](#chapter0632.html)

[Test Conditions](#chapter0633.html)

[The for Loop](#chapter0634.html)

[Script11: Print Alphabets Using for Loop](#chapter0635.html)

[Script12: Create Users Using for Loop](#chapter0636.html)

[Chapter Summary](#chapter0637.html)

[Review Questions](#chapter0638.html)

[Answers to Review Questions](#chapter0639.html)

[Do-It-Yourself Challenge Labs](#chapter0640.html)

[Lab 21-1: Write Script to Create Logical Volumes](#chapter0641.html)

[Lab 21-2: Write Script to Create File Systems](#chapter0642.html)

[Lab 21-3: Write Script to Configure New Network Connection
Profile](#chapter0643.html)

\

[22. Containers](#chapter0644.html)

[Introduction to Containers](#chapter0645.html)

[Containers and the Linux Features](#chapter0646.html)

[Benefits of Using Containers](#chapter0647.html)

[Container Home: Bare Metal or Virtual Machine](#chapter0648.html)

[Container Images and Container Registries](#chapter0649.html)

[Rootful vs. Rootless Containers](#chapter0650.html)

[Working with Images and Containers](#chapter0651.html)

[Exercise 22-1: Install Necessary Container Support](#chapter0652.html)

[The podman Command](#chapter0653.html)

[The skopeo Command](#chapter0654.html)

[The registries.conf File](#chapter0655.html)

[Viewing Podman Configuration and Version](#chapter0656.html)

[Image Management](#chapter0657.html)

[Exercise 22-2: Search, Examine, Download, and Remove an
Image](#chapter0658.html)

[Containerfile](#chapter0659.html)

[Exercise 22-3: Use Containerfile to Build Image](#chapter0660.html)

[Basic Container Management](#chapter0661.html)

[Exercise 22-4: Run, Interact with, and Remove a Named
Container](#chapter0662.html)

[Exercise 22-5: Run a Nameless Container and Auto-Remove it After Entry
Point Command Execution](#chapter0663.html)

[Advanced Container Management](#chapter0664.html)

[Containers and Port Mapping](#chapter0665.html)

[Exercise 22-6: Configure Port Mapping](#chapter0666.html)

[Exercise 22-7: Stop, Restart, and Remove a
Container](#chapter0667.html)

[Containers and Environment Variables](#chapter0668.html)

[Exercise 22-8: Pass and Set Environment Variables](#chapter0669.html)

[Containers and Persistent Storage](#chapter0670.html)

[Exercise 22-9: Attach Persistent Storage and Access Data Across
Containers](#chapter0671.html)

[Container State Management with systemd](#chapter0672.html)

[Exercise 22-10: Configure a Rootful Container as a systemd
Service](#chapter0673.html)

[Exercise 22-11: Configure Rootless Container as a systemd
Service](#chapter0674.html)

[Chapter Summary](#chapter0675.html)

[Review Questions](#chapter0676.html)

[Answers to Review Questions](#chapter0677.html)

[DIY Challenge Labs](#chapter0678.html)

[Lab 22-1: Launch Named Root Container with Port
Mapping](#chapter0679.html)

[Lab 22-2: Launch Nameless Rootless Container with Two
Variables](#chapter0680.html)

[Lab 22-3: Launch Named Rootless Container with Persistent
Storage](#chapter0681.html)

[Lab 22-4: Launch Named Rootless Container with Port Mapping,
Environment Variables, and Persistent Storage](#chapter0682.html)

[Lab 22-5: Control Rootless Container States via
systemd](#chapter0683.html)

[Lab 22-6: Control Rootful Container States via
systemd](#chapter0684.html)

[Lab 22-7: Build Custom Image Using Containerfile](#chapter0685.html)

\

[Appendix A: Sample RHCSA Exam 1](#chapter0686.html)

\

[Appendix B: Sample RHCSA Exam 2](#chapter0687.html)

\

[Appendix C: Sample RHCSA Exam 3](#chapter0688.html)

\

[Appendix D: Sample RHCSA Exam 4](#chapter0689.html)

\

[Bibliography](#chapter0690.html)

\

[Glossary](#chapter0691.html)

\

[Index](#chapter0692.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0011.html}

## List of Figures {.style3 style="text-align: center"}

\

[Figure 1-1 Lab Setup for Exercises](#chapter0018.html)

[Figure 1-2 VirtualBox Website](#chapter0024.html)

[Figure 1-3 VirtualBox Download](#chapter0024.html)

[Figure 1-4 VirtualBox Installation 1](#chapter0024.html)

[Figure 1-5 VirtualBox Installation 2](#chapter0024.html)

[Figure 1-6 VirtualBox Installation 3](#chapter0024.html)

[Figure 1-7 VirtualBox Installation 4](#chapter0024.html)

[Figure 1-8 VirtualBox Installation 5](#chapter0024.html)

[Figure 1-9 VirtualBox Installation 6](#chapter0024.html)

[Figure 1-10 Virtual Machine Creation 1](#chapter0025.html)

[Figure 1-11 Virtual Machine Creation 2](#chapter0025.html)

[Figure 1-12 Virtual Machine Creation 3](#chapter0025.html)

[Figure 1-13 Virtual Machine Creation 4](#chapter0025.html)

[Figure 1-14 Virtual Machine Creation 5](#chapter0025.html)

[Figure 1-15 Virtual Machine Configuration Summary](#chapter0025.html)

[Figure 1-16 Virtual Machine Network Configuration](#chapter0025.html)

[Figure 1-17 Red Hat User Account Creation 1](#chapter0027.html)

[Figure 1-18 Red Hat User Account Creation 2](#chapter0027.html)

[Figure 1-19 Red Hat Developer Login](#chapter0027.html)

[Figure 1-20 ISO Image Attached to VM](#chapter0028.html)

[Figure 1-21 Boot Menu](#chapter0029.html)

[Figure 1-22 Language Selection](#chapter0029.html)

[Figure 1-23 Installation Summary \| Main](#chapter0029.html)

[Figure 1-24 Installation Summary \| Time & Date](#chapter0031.html)

[Figure 1-25 Installation Summary \| Installation
Source](#chapter0032.html)

[Figure 1-26 Installation Summary \| Software
Selection](#chapter0033.html)

[Figure 1-27 Installation Summary \| Installation
Destination](#chapter0034.html)

[Figure 1-28 Installation Summary \| Network &
Hostname](#chapter0035.html)

[Figure 1-29 Installation Summary \| Network & Hostname \|
Configure](#chapter0035.html)

[Figure 1-30 Installation Summary \| Network &
Hostname](#chapter0035.html)

[Figure 1-31 Installation Summary \| Root Password](#chapter0036.html)

[Figure 1-32 Installation Summary \| User Creation](#chapter0036.html)

[Figure 1-33 Configuration \| Finishing Installation](#chapter0038.html)

[Figure 1-34 VirtualBox Manager \| System \| Boot
Order](#chapter0039.html)

[Figure 1-35 VirtualBox Manager \| System \| Boot Order \|
Alter](#chapter0039.html)

[Figure 1-36 Graphical Desktop \| Sign-in Screen](#chapter0041.html)

[Figure 1-37 GNOME Desktop Environment](#chapter0041.html)

[Figure 1-38 GNOME Desktop Environment\| Log Out](#chapter0042.html)

[Figure 1-39 PuTTY Interface](#chapter0043.html)

[Figure 2-1 GNOME Display Manager](#chapter0051.html)

[Figure 2-2 GNOME Desktop Environment](#chapter0052.html)

[Figure 2-3 GNOME Desktop Environment \| Activities](#chapter0052.html)

[Figure 2-4 Linux Directory Structure](#chapter0054.html)

[Figure 2-5 Remote Terminal Session](#chapter0068.html)

[Figure 2-6 Red Hat's Webpage for RHEL 9
Documentation](#chapter0087.html)

[Figure 3-1 Hard Link](#chapter0129.html)

[Figure 3-2 Soft Link](#chapter0130.html)

[Figure 4-1 Permission Weights](#chapter0147.html)

[Figure 4-2 find Command Syntax](#chapter0162.html)

[Figure 5-1 The passwd File](#chapter0180.html)

[Figure 5-2 The shadow File](#chapter0181.html)

[Figure 5-3 The group File](#chapter0182.html)

[Figure 5-4 The gshadow File](#chapter0183.html)

[Figure 8-1 Process State Transition](#chapter0253.html)

[Figure 8-2 Syntax of Crontables](#chapter0268.html)

[Figure 11-1 GRUB2 Menu](#chapter0339.html)

[Figure 11-2 GRUB2 Kernel Entry Edit](#chapter0340.html)

[Figure 11-3 GRUB2 Commands](#chapter0340.html)

[Figure 11-4 Anatomy of a Kernel Version](#chapter0346.html)

[Figure 13-1 VirtualBox Manager \| RHEL9-VM2
Selected](#chapter0394.html)

[Figure 13-2 VirtualBox Manager \| Add Storage](#chapter0394.html)

[Figure 13-3 VirtualBox Manager \| Medium Selector
Screen](#chapter0394.html)

[Figure 13-4 VirtualBox Manager \| Create a Disk](#chapter0394.html)

[Figure 13-5 VirtualBox Manager \| 5 New Disks
Created](#chapter0394.html)

[Figure 13-6 VirtualBox Manager \| 5 New Disks Added](#chapter0394.html)

[Figure 13-7 LVM Structure](#chapter0401.html)

[Figure 13-8 Storage Optimization with VDO](#chapter0415.html)

[Figure 15-1 VirtualBox Manager \| Add Network
Interface](#chapter0481.html)

[Figure 16-1 NFS Server/Client](#chapter0498.html)

[Figure 17-1 Sample DNS Hierarchy](#chapter0521.html)

[Figure 17-2 NTP Stratum Levels](#chapter0532.html)

[Figure 20-1 SELinux Allow/Deny Process](#chapter0601.html)

[Figure 21-1 Shell Parameters](#chapter0619.html)

[Figure 21-2 The if-then-fi Construct](#chapter0625.html)

[Figure 21-3 The if-then-else-fi Construct](#chapter0627.html)

[Figure 21-4 The if-then-elif-fi Construct](#chapter0629.html)

[Figure 21-5 The for Loop](#chapter0634.html)

[Figure 22-1 Container Home: Bare Metal or Virtual
Machine](#chapter0648.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0012.html}

## List of Tables {.style3 style="text-align: center"}

\

[Table 1-1 Installation Logs](#chapter0021.html)

[Table 1-2 Installation Summary \| Software Selection \| Base
Environments](#chapter0033.html)

[Table 2-1 ls Command Options](#chapter0070.html)

[Table 2-2 tree Command Options](#chapter0073.html)

[Table 2-3 Navigating within Manual Pages](#chapter0081.html)

[Table 3-1 tar Command Options](#chapter0106.html)

[Table 3-2 tar with Compression Options](#chapter0106.html)

[Table 3-3 vim Editor \| Inserting Text](#chapter0111.html)

[Table 3-4 vim Editor \| Navigating](#chapter0112.html)

[Table 3-5 vim Editor \| Revealing Line Numbering](#chapter0113.html)

[Table 3-6 vim Editor \| Deleting Text](#chapter0114.html)

[Table 3-7 vim Editor \| Undoing and Repeating](#chapter0115.html)

[Table 3-8 vim Editor \| Searching for Text](#chapter0116.html)

[Table 3-9 vim Editor \| Replacing Text](#chapter0117.html)

[Table 3-10 vim Editor \| Copying, Moving, and Pasting
Text](#chapter0118.html)

[Table 3-11 vim Editor \| Changing Text](#chapter0119.html)

[Table 3-12 vim Editor \| Saving and Quitting](#chapter0120.html)

[Table 3-13 Navigating with less and more](#chapter0123.html)

[Table 3-14 wc Command Options](#chapter0124.html)

[Table 3-15 Copying vs. Linking](#chapter0131.html)

[Table 4-1 Octal Permission Notation](#chapter0147.html)

[Table 5-1 login.defs File Directives](#chapter0184.html)

[Table 5-2 useradd Command Options](#chapter0186.html)

[Table 5-3 usermod Command Options](#chapter0186.html)

[Table 6-1 chage Command Options](#chapter0202.html)

[Table 6-2 passwd Command Options](#chapter0204.html)

[Table 6-3 usermod Command Options for User
Lock/Unlock](#chapter0206.html)

[Table 6-4 groupadd Command Options](#chapter0209.html)

[Table 7-1 Common Predefined Environment Variables](#chapter0228.html)

[Table 7-2 Helpful Command Line Editing Shortcuts](#chapter0234.html)

[Table 7-3 Predefined Aliases](#chapter0237.html)

[Table 7-4 System-wide Startup Files](#chapter0243.html)

[Table 7-5 Per-user Startup Files](#chapter0244.html)

[Table 8-1 ps Command Output Description](#chapter0254.html)

[Table 8-2 Control Signals](#chapter0261.html)

[Table 8-3 User Access Restrictions to Scheduling
Tools](#chapter0263.html)

[Table 8-4 Crontable Syntax Explained](#chapter0268.html)

[Table 9-1 rpm Command Query Options](#chapter0284.html)

[Table 9-2 rpm Command Install/Remove/Verify Options](#chapter0284.html)

[Table 9-3 Red Hat GPG Key Files](#chapter0293.html)

[Table 9-4 Package Verification Codes](#chapter0295.html)

[Table 9-5 File Type Codes](#chapter0295.html)

[Table 10-1 Directive Settings in dnf.conf File](#chapter0311.html)

[Table 10-2 dnf Subcommands for Package and Repository
Manipulation](#chapter0312.html)

[Table 10-3 dnf Subcommands for Package Group
Manipulation](#chapter0312.html)

[Table 11-1 GRUB2 Default Settings](#chapter0341.html)

[Table 11-2 Kernel Packages](#chapter0345.html)

[Table 12-1 systemd Unit Types](#chapter0359.html)

[Table 12-2 systemd Targets](#chapter0360.html)

[Table 12-3 systemctl Subcommands](#chapter0361.html)

[Table 12-4 Journal Data Storage Options](#chapter0373.html)

[Table 12-5 Tuning Profiles](#chapter0376.html)

[Table 13-1 Common parted Subcommands](#chapter0395.html)

[Table 13-2 Common LVM Operations and Commands](#chapter0407.html)

[Table 14-1 File System Types](#chapter0432.html)

[Table 14-2 File System Management Commands](#chapter0438.html)

[Table 14-3 Common mount Command Options](#chapter0439.html)

[Table 15-1 IPv4 vs IPv6](#chapter0478.html)

[Table 15-2 Network Connection Configuration
Directives](#chapter0484.html)

[Table 15-3 Network Interface Management Tools](#chapter0484.html)

[Table 15-4 Network Connection and Device Administration
Tools](#chapter0485.html)

[Table 16-1 AutoFS Directives](#chapter0507.html)

[Table 17-1 The Resolver Configuration File](#chapter0523.html)

[Table 17-2 Name Service Source and Order
Determination](#chapter0524.html)

[Table 17-3 Chrony Directives](#chapter0533.html)

[Table 18-1 OpenSSH Client Tools](#chapter0549.html)

[Table 18-2 OpenSSH Server Configuration File](#chapter0550.html)

[Table 18-3 OpenSSH Client Configuration File](#chapter0551.html)

[Table 19-1 firewalld Default Zones](#chapter0566.html)

[Table 19-2 Common firewall-cmd Options](#chapter0571.html)

[Table 20-1 SELinux Management Commands](#chapter0593.html)

[Table 21-1 Test Conditions](#chapter0624.html)

[Table 21-2 Arithmetic Operators](#chapter0633.html)

[Table 22-1 Common podman Subcommands](#chapter0653.html)

[Table 22-2 Common Containerfile Instructions](#chapter0659.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0013.html}

## Chapter 01 {style="text-align: right"}

\

### Local Installation {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

A quick look at Linux and Open Source

\

Linux distribution from Red Hat

\

Recommended lab setup for RHCSA exam preparation

\

Overview of the installer program

\

Where are installation messages stored?

\

What are virtual console screens?

\

Download and install VirtualBox

\

Create virtual machine

\

Download and install Red Hat Enterprise Linux in virtual machine

\

Log in and out at the graphical console

\

Log in and out over the network

\

#### RHCSA Objectives:

\

04\. Access remote systems using ssh

This chapter sets up the foundation for learning and practicing the exam
objectives for RHCSA

::: {style="page-break-before: always;"}
:::

\

Linux is a free operating system that has been in existence and use for
just over three decades. Its source code is available to developers,
amateurs, and the general public for enhancements and customization. Red
Hat Inc. modifies a copy of a selected version of Linux source code and
introduces features, adds improvements, and fixes bugs. The company
packages the updated version as a Linux distribution of their own for
commercial purposes. This distribution is thoroughly tested to run
smoothly and perform well on a wide range of computer hardware
platforms. It is stable, robust, feature-rich, and ready to host a
workload of any size.

\

::: {style="text-align: center;"}
![](image-4XEV7K1H.jpg){height="100%"}
:::

Red Hat Enterprise Linux may be downloaded for learning, practicing, and
preparing for the RHCSA exam. It is available as a single installable
image file. A lab environment is necessary to practice the procedures to
solidify the understanding of the concepts and tools learned. The
installation process requires careful planning to identify critical
system configuration pieces prior to launching the installer program.
Once the operating system is installed, users can log in at the console
or over the network.

::: {style="page-break-before: always;"}
:::

[]{#chapter0014.html}

## A Quick Look at Linux Development {.style3}

\

Linux is a free computer operating system (OS) that is similar to the
UNIX OS in terms of concepts, features, functionality, and stability. It
is referred to as a UNIX-like operating system.

\

Linux powers an extensive range of computer hardware platforms, from
laptop and desktop computers to massive mainframes and supercomputers.
Linux also runs as the base OS on networking, storage, gaming, smart
television, and mobile devices. Numerous vendors, including Red Hat,
IBM, Canonical, Oracle, Microsoft, DXC Technology, Novell, and Dell,
offer commercial support to Linux users worldwide.

\

Linux is the main alternative to proprietary UNIX and Windows operating
systems because of its functionality, adaptability, portability, and
cost-effectiveness. Currently, over one hundred different Linux
distributions are circulating from various vendors, organizations,
non-profit groups, and individuals, though only a few are popular and
widely recognized.

\

Linux is largely used in government agencies, corporate businesses,
academic institutions, scientific organizations, as well as in home
computers. Linux development, adoption, and usage are constantly on the
rise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0015.html}

## Linux History in a Nutshell {.style3}

\

In 1984, Richard Stallman, an American software engineer, had a goal to
create a completely free UNIX-compatible open-source (non-proprietary)
operating system. The initiative was called the GNU Project (GNU's Not
Unix) and by 1991, significant software had been developed. The only
critical piece missing was a core software component called kernel to
drive and control the GNU software and to regulate its communication
with the hardware.

\

Around the same time, Finnish computer science student Linus Torvalds
developed a kernel and proclaimed its availability. The new kernel was
named Linux, and it was gradually integrated with the GNU software to
form what is now referred to as GNU/Linux, Linux operating system, or
simply Linux.

\

Linux was released under the GNU General Public License (GPL). Initially
written to run on Intel x86-based computers, the first version (0.01)
was released in September 1991 with little more than 10,000 lines of
code. In 1994, the first major release (1.0.0) was introduced, followed
by a series of successive major and minor versions until the release of
version 5.0 in 2019. At the time of this writing, version 5.10 with
millions of lines of code, is the latest long-term stable kernel.

\

The Linux kernel, and the operating system in general, has been enhanced
with contributions from tens of thousands of software programmers,
amateurs, and organizations around the world into a large and complex
system under GNU GPL, which provides public access to its source code
free of charge and with full consent to amend, package, and
redistribute.

::: {style="page-break-before: always;"}
:::

[]{#chapter0016.html}

## Linux from Red Hat {.style3}

\

Red Hat, Inc. used the available Linux source code and created one of
the first commercial Linux operating system distribution called Red Hat
Linux (RHL). The company released the first version 1.0 in November
1994. Several versions followed until the last version in the series,
Red Hat Linux 9 (later referred to as RHEL 3), based on kernel 2.4.20,
was released in March 2003. Red Hat renamed their Red Hat Linux brand as
Red Hat Enterprise Linux (RHEL) commencing 2003.

\

RHL was originally assembled and enhanced within the Red Hat company. In
2003, Red Hat sponsored and facilitated the Fedora Project and invited
the user community to join hands in enhancing and updating the source
code. This project served as the test bed for developing and testing new
features and enabled Red Hat to include the improved code in successive
versions of RHEL.

\

The Fedora distribution is completely free, while RHEL is commercial.
RHEL 4 was based on kernel 2.6.9 and released in February 2005, RHEL 5
on kernel 2.6.18 with release date in March 2007, RHEL 6 on kernel
2.6.32 and released in November 2010, RHEL 7 on kernel 3.10 and released
in June 2014, RHEL 8 on kernel 4.18 and released in May 2019, and RHEL 9
was based on kernel 5.14 with release date in May 2022). These RHEL
releases were built using Fedora distributions 3, 6, 13, 20, 28, and 34
respectively.

\

RHEL 9 has been tested to run on bare-metal computer hardware,
virtualized platforms, cloud-based virtual machines, high-end graphics
workstations, IBM Power servers, IBM System Z, etc.

::: {style="page-break-before: always;"}
:::

[]{#chapter0017.html}

## Lab Environment for Practice {.style3}

\

RHEL 9 is available as a free download from Red Hat for Intel and AMD
processor machines. You will need to create a free Red Hat user account
in order to download it. The downloaded image file can then be attached
to a Virtual Machine (VM) as an ISO image, burned to a DVD to support
installation on a physical computer, or placed on a remote server for
network-based installations via HTTP, FTP, or NFS protocol.

\

An ISO image is a single file that represents the content of an entire
DVD or CD.

\

Burning the image to a DVD and configuring a server for network-based
installations are beyond the scope of this book. This chapter will focus
on local installation of the operating system with an ISO image.

::: {style="page-break-before: always;"}
:::

[]{#chapter0018.html}

## Lab Environment for In-Chapter Exercises {.style3}

\

Throughout this book, there will be several discussions around system,
network, and security, along with examples on how to implement and
administer them. Each chapter will contain a number of exercises that
will help you perform certain tasks and execute commands.

\

You'll need a laptop or a desktop computer with at least a dual-core
processor, 8GB of physical memory (16GB preferred), and 50GB of free
storage space to run two virtual machines with required storage. If you
want to use the static IP addresses on your home router, make sure that
you keep a mapping between them, and the ones provided below to avoid
any confusion. The computer must have hardware virtualization support
enabled in the BIOS/firmware to allow for 64-bit OS installation. Here
is a summary of what is needed and how it will be configured:

\

  ----------------------------------- -----------------------------------
  Base/Host Operating System:         Windows 10/11 or MacOS 10.12 or
                                      higher

  Hypervisor Software:                Oracle VM VirtualBox Manager
                                      (VirtualBox or VB in short) 7.0 or
                                      higher

  Number of VMs:                      2

  vCPUs in each VM:                   2

  OS in each VM:                      RHEL 9.1

  VM1 (RHEL9-VM1):                    server1.example.com with static IP
                                      192.168.0.110/24, 2048MB memory,
                                      1x20GB virtual disk for OS, and one
                                      virtual network device. This VM
                                      will be built using the RHEL 9.1
                                      ISO image. Exercises 1-1 and 1-2
                                      will walk through the process of
                                      installation. In Chapter 15,
                                      "Networking, Network Devices, and
                                      Network Connections", you will add
                                      another virtual network device and
                                      will rename this server to
                                      server10.example.com.

  VM2 (RHEL9-VM2):                    server2.example.com with static IP
                                      192.168.0.120/24, 2048MB memory,
                                      1x20GB virtual disk for OS, and one
                                      virtual network device. In Chapter
                                      13, "Storage Management", you will
                                      add 4x250MB and 1x5GB data disks
                                      for numerous upcoming exercises.
                                      You will build this VM using the
                                      RHEL 9.1 ISO image by referencing
                                      the steps outlined in Exercise 1-1
                                      and Exercise 1-2. In Chapter 15,
                                      "Networking, Network Devices, and
                                      Network Connections", you will add
                                      another virtual network device and
                                      will rename this server to
                                      server20.example.com.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Check your Windows/MacOS IP assignments and make sure to use the same
network subnet for your RHEL VMs. For instance, use 172.16.3.110/24 and
172.16.3.120/24 for your VMs if your Windows/MacOS is on the
172.16.3.0/24 subnet.

\

The setup for the lab is shown in Figure 1-1.

\

::: {style="text-align: center;"}
![](image-SVDMQYV3.jpg){height="100%"}
:::

Figure 1-1 Lab Setup for Exercises

\

You will install VirtualBox 7.0 (or higher) on Windows 10/11 or MacOS
10.12 (or higher). You may use VMware or other virtualization software
as an alternative; however, all exercises and examples in this book
reference VirtualBox.

::: {style="page-break-before: always;"}
:::

[]{#chapter0019.html}

## Lab Environment for End-of-Chapter Labs {.style3}

\

For the end-of-chapter labs, I recommend you build a new environment
with two virtual machines with the exact same specifications in terms of
CPU, memory, network interface, and storage as RHEL-VM1 (server1) and
RHEL-VM2 (server2). You may name the new systems RHEL-VM3 (server3) and
RHEL-VM4 (server4). This new environment may be created after you have
completed all in-chapter exercises and you are ready to perform the labs
with minimal assistance (hints included but no solutions provided).

::: {style="page-break-before: always;"}
:::

[]{#chapter0020.html}

## The RHEL Installer Program {.style3}

\

The RHEL installer program is called Anaconda. There are several
configuration options on the main screen that require modification
before the installation process begins. Some of the questions are
compulsory and must be answered appropriately while others are optional
and may be skipped for post-installation setup.

\

The configuration can be done in any sequence. You should have the
minimum mandatory configuration data handy and be ready to enter it.
Some of the key configuration items are language, keyboard type, time
zone, disk partitioning, hostname/IP, software selection, root password,
and user information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0021.html}

## Installation Logs {.style3}

\

There are plenty of log files created and updated as the installation
progresses. These files record configuration and status information. You
can view their contents after the installation has been completed to
check how the installation proceeded. Most of these files are described
in Table 1-1.

\

  ----------------------------------- -----------------------------------
  File                                Description

  /root/anaconda-ks.cfg               Records the configuration entered

  /var/log/anaconda/anaconda.log      Contains informational, debug, and
                                      other general messages

  /var/log/anaconda/journal.log       Stores messages generated by many
                                      services and components during
                                      system installation

  /var/log/anaconda/packaging.log     Records messages generated by the
                                      dnf and rpm commands during
                                      software installation

  /var/log/anaconda/program.log       Captures messages generated by
                                      external programs

  /var/log/anaconda/storage.log       Records messages generated by
                                      storage modules

  /var/log/anaconda/syslog            Records messages related to the
                                      kernel

  /var/log/anaconda/X.log             Stores X Window System information
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 1-1 Installation Logs

\

Files in the /var/log/anaconda directory are actually created and
resided in the /tmp directory during the installation; however, they are
moved over once the installation is complete.

::: {style="page-break-before: always;"}
:::

[]{#chapter0022.html}

## Virtual Console Screens {.style3}

\

During the installation, there are six text-based virtual console
screens available to monitor the process, view diagnostic messages, and
discover and fix any issues encountered. The information displayed on
the console screens is captured in the installation log files (Table
1-1). You can switch between screens by pressing a combination of keys
as described below.

\

Console 1 (Ctrl+Alt+F1): This is the main screen. Before Anaconda
begins, you will select a language to use during installation, and then
it will switch the default console to the sixth screen (Console 6).

\

Console 2 (Ctrl+Alt+F2): Presents the shell interface to run commands as
the root user.

\

Console 3 (Ctrl+Alt+F3): Displays installation messages and stores them
in /tmp/anaconda.log file. This file also captures information on
detected hardware, in addition to other data.

\

Console 4 (Ctrl+Alt+F4): Shows storage messages and records them in
/tmp/storage.log file.

\

Console 5 (Ctrl+Alt+F5): Exhibits program messages and logs them to
/tmp/program.log file.

\

Console 6 (Ctrl+Alt+F6): Default graphical configuration and
installation console screen.

::: {style="page-break-before: always;"}
:::

[]{#chapter0023.html}

Exercise 1-1: Download and Install VirtualBox Software, and Create a
Virtual Machine

\

In this exercise, you will download and install VirtualBox software. You
will create a virtual machine to set up the foundation to install RHEL 9
for the next exercise.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Downloading and installing VirtualBox software and creating a
virtual machine are not part of the exam objectives. These tasks have
been included here only to support readers with building their own lab
environment for practice.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0024.html}

## Downloading and Installing VirtualBox {.style3}

\

VirtualBox is available for free download and use. At the time of this
writing, the latest version is 7.0; however, you can use any previous
6.x or a future version. Here is a quick guide on how to download and
install the current version of VirtualBox on a Windows 11 (works on
Windows 10 as well) computer.

\

1\. Go to www.virtualbox.org (Figure 1-2) and click "Download VirtualBox
7.0".

\

::: {style="text-align: center;"}
![](image-RYEUPN4F.jpg){height="100%"}
:::

Figure 1-2 VirtualBox Website

\

2\. On the next screen, click on "Windows hosts". This will start a
download to your computer.

\

::: {style="text-align: center;"}
![](image-1DYZ3Q1X.jpg){height="100%"}
:::

Figure 1-3 VirtualBox Download

\

The software is now available on your computer.

\

3\. Double-click on the VirtualBox binary to start the installation.
Click Next to proceed on the first screen that appears.

\

::: {style="text-align: center;"}
![](image-N71B6T0L.jpg){height="100%"}
:::

Figure 1-4 VirtualBox Installation 1

\

4\. If needed, choose a different location on the disk for installation.
Click Next to continue.

\

::: {style="text-align: center;"}
![](image-1DXVB8DX.jpg){height="100%"}
:::

Figure 1-5 VirtualBox Installation 2

\

5\. Accept the warning and continue by pressing Yes.

\

::: {style="text-align: center;"}
![](image-0TSWNWTK.jpg){height="100%"}
:::

Figure 1-6 VirtualBox Installation 3

\

6\. The installation process will report if any Python Core and/or
win32api dependencies are missing. Click Yes to proceed.

\

::: {style="text-align: center;"}
![](image-X38P0TXD.jpg){height="100%"}
:::

Figure 1-7 VirtualBox Installation 4

\

7\. The setup wizard is now ready to begin the installation. Click
Install to proceed.

\

::: {style="text-align: center;"}
![](image-D4879HVC.jpg){height="100%"}
:::

Figure 1-8 VirtualBox Installation 5

\

8\. Click Finish to continue.

\

::: {style="text-align: center;"}
![](image-J1K9ZPIT.jpg){height="100%"}
:::

Figure 1-9 VirtualBox Installation 6

\

This brings the installation of VirtualBox to a successful completion.
It will also launch the application when you click Finish.

::: {style="page-break-before: always;"}
:::

[]{#chapter0025.html}

## Creating a Virtual Machine {.style3}

\

Use VirtualBox to create the first virtual machine called RHEL9-VM1 with
specifications described earlier in this chapter. Here are the steps for
the creation.

\

1\. Launch VirtualBox if it is not already running. The interface looks
similar to what is shown in Figure 1-10.

\

::: {style="text-align: center;"}
![](image-L7VES11A.jpg){height="100%"}
:::

Figure 1-10 Virtual Machine Creation 1

\

2\. Click on New on the top menu bar to start the virtual machine
creation wizard as shown in Figure 1-11. Enter the name RHEL9-VM1,
select Linux as the operating system type, and Red Hat (64-bit) as the
version. For this demonstration, accept the default location to store
the VM files on the C drive. Click Next to continue.

\

::: {style="text-align: center;"}
![](image-JRKIAXWL.jpg){height="100%"}
:::

Figure 1-11 Virtual Machine Creation 2

\

3\. In the next window, specify the memory size and number of processors
you want allocated to the VM. Accept the recommended 2GB for memory and
move the slider to the right to select 2 vCPUs and click Next.

\

::: {style="text-align: center;"}
![](image-DXGFJAD7.jpg){height="100%"}
:::

Figure 1-12 Virtual Machine Creation 3

\

4\. The VM will need a virtual hard disk to store RHEL 9 operating
system. For this demonstration, choose the creation of a virtual hard
disk now with a size of 20GB. Both are also the defaults.

\

::: {style="text-align: center;"}
![](image-EA79AA6L.jpg){height="100%"}
:::

Figure 1-13 Virtual Machine Creation 4

\

5\. Clicking Next on the previous window completes the VM creation
process and displays a summary of the selections. Click Finish to end
the wizard.

\

::: {style="text-align: center;"}
![](image-ZJGX9SWI.jpg){height="100%"}
:::

Figure 1-14 Virtual Machine Creation 5

\

6\. VirtualBox will have the VM listed along with its configuration. See
Figure 1-15.

\

::: {style="text-align: center;"}
![](image-N7UY11R9.jpg){height="100%"}
:::

Figure 1-15 Virtual Machine Configuration Summary

\

7\. On the VM configuration page above (Figure 1-15), click Network and
choose Bridged Adapter from the dropdown and ensure that the right
network connection name is selected. See Figure 1-16. This will allow
the RHEL VM to communicate with the hosting Windows computer as well as
the internet in both directions.

\

::: {style="text-align: center;"}
![](image-Q2H5IDDW.jpg){height="100%"}
:::

Figure 1-16 Virtual Machine Network Configuration

\

There are other configurable items as depicted in Figure 1-15. You will
be attaching a bootable RHEL 9 OS image to the VM under Storage (Optical
Drive Empty) shortly and may be making additional changes later.

::: {style="page-break-before: always;"}
:::

[]{#chapter0026.html}

## Exercise 1-2: Download and Install RHEL {.style3}

\

This exercise will build server1 in RHEL9-VM1.

\

In this exercise, you will download RHEL 9 and install it in RHEL9-VM1
that you created in Exercise 1-1. You will attach the RHEL 9 ISO image
to the VM, name the Linux system server1.example.com, and configure IP
192.168.0.110/24. Additional configuration will be supplied as the
installation advances.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Downloading and installing RHEL 9 are beyond the scope of the
exam. They have been included here only to support the readers with
building their own lab environment for practice.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The user creation, base environments, storage management, network device
and connection configuration, time synchronization, and other topics are
not explained as part of this exercise; however, they will be discussed
in later chapters.

::: {style="page-break-before: always;"}
:::

[]{#chapter0027.html}

## Downloading RHEL 9 ISO Image {.style3}

\

RHEL 9 image is available for a free download from Red Hat Developer's
website. You need to create a user account in order to log in and obtain
a copy for yourself. Alternatively, you can use your credentials on
Facebook, Google, LinkedIn, Microsoft, Twitter, etc. for login. For this
demonstration, you will find instructions on how to open a new account
and download the software.

\

1\. Visit https://developers.redhat.com/login and click "Register for a
Red Hat Account".

\

::: {style="text-align: center;"}
![](image-NTU4J16N.jpg){height="100%"}
:::

Figure 1-17 Red Hat User Account Creation 1

\

2\. Fill out the form by providing a unique username, email address, and
password. Make sure to checkmark the boxes to accept terms and
conditions. Click "Create My Account" at the bottom of the screen to
continue.

\

::: {style="text-align: center;"}
![](image-RX7LMWSU.jpg){height="100%"}
:::

Figure 1-18 Red Hat User Account Creation 2

\

3\. After an account has been created, go back to the login page
https://developers.redhat.com/login and submit the credentials to log
in.

4\. Click on "Explore Products" and then "Red Hat Enterprise Linux"
under Featured Downloads.

5\. Click "Download RHEL at no-cost". An ISO file of the latest version
of RHEL will begin downloading for x86_64 computer. The latest version
of RHEL available at the time of this writing is 9.1.

\

::: {style="text-align: center;"}
![](image-59IRNLF8.jpg){height="100%"}
:::

Figure 1-19 Red Hat Developer Login

\

The filename of the downloaded image for RHEL version 9.1 will be
rhel-baseos-9.1-x86_64-dvd.iso and it will be around 8.4GB in size. You
can move the file to a disk location on your computer where you want it
stored.

::: {style="page-break-before: always;"}
:::

[]{#chapter0028.html}

## Attaching RHEL 9 ISO Image to the Virtual Machine {.style3}

\

We now attach the RHEL 9 ISO image to RHEL9-VM1 to boot and install the
OS in the VM. Click "\[Optical Drive\] Empty" under Storage in
VirtualBox for this VM and select Choose Disk File. Navigate to where
you have the ISO image stored. Highlight the image and click Open to
attach it to the VM. After the image has been attached, the VirtualBox
Storage configuration will look like as depicted in Figure 1-20.

\

::: {style="text-align: center;"}
![](image-7GQXKE38.jpg){height="100%"}
:::

Figure 1-20 ISO Image Attached to VM

\

Leave the rest of the settings to their default values.

::: {style="page-break-before: always;"}
:::

[]{#chapter0029.html}

## Launching the Installer {.style3}

\

6\. While the VM is highlighted in VirtualBox, click the Start button at
the top to power up the VM.

7\. A console screen pops up displaying the boot menu (Figure 1-21) with
three options. Press the Spacebar key to halt the autoboot process.

\

::: {style="text-align: center;"}
![](image-HSGQHQB3.jpg){height="100%"}
:::

Figure 1-21 Boot Menu

\

The first option, "Install Red Hat Enterprise Linux 9.1", is used for
installing the highlighted RHEL version unless you want the installation
media tested for integrity before continuing, in which case you will
select the second option. Anaconda awaits 60 seconds for you to alter
the selection, or it proceeds and autoboots using the second option on
the list, which is also the default. The third option,
"Troubleshooting", allows you to address some boot-related issues that
might occur during installation.

\

Use the Up or Down arrow key to select the "Install Red Hat Enterprise
Linux 9.1" entry and press Enter. The installer is launched in graphical
mode.

\

8\. The installer program shows a welcome screen with a long list of
supported languages that you could use during installation. The default
is set to English. Click Continue to accept the default and move on.

\

::: {style="text-align: center;"}
![](image-3ZOAO9D3.jpg){height="100%"}
:::

Figure 1-22 Language Selection

\

If all the content does not fit on the console screen, try changing the
Graphics Controller to VMSVGA under Settings \| Display in the
VirtualBox Manager for the VM. You will need to power off the VM to make
this change.

\

9\. The "Installation Summary" screen appears next, as shown in Figure
1-23. You have the opportunity to make all necessary configuration
changes prior to starting the installation. This screen presents a
unified interface to configure localization (keyboard, language, date,
time, and time zone), software (installation source and software
selection), system (disk partitioning, network assignments, hostname
setting, etc.), and user settings (root password and user creation).

\

::: {style="text-align: center;"}
![](image-94XH47BJ.jpg){height="100%"}
:::

Figure 1-23 Installation Summary \| Main

\

Any items highlighted in red and with a warning sign must be configured
before the Begin Installation button at the bottom right of the screen
is enabled.

\

There is no particular sequence to configure these items. If you do not
wish to change a non-highlighted item, simply leave it intact and the
installation program will apply the default settings for it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0030.html}

## Adding Support for Keyboards and Languages {.style3}

\

10\. Anaconda presents additional choices for keyboard layouts and
languages for use during and after the installation. The default is the
US English for the keyboard and Canadian English as the language (for my
location). Go ahead and change them as required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0031.html}

## Configuring Time & Date {.style3}

\

11\. Click Time & Date to set the time zone (region and city), date, and
time for the system. See Figure 1-24. Click Done in the upper left
corner to save the changes and return to the Installation Summary
screen.

\

::: {style="text-align: center;"}
![](image-HRSI2BJZ.jpg){height="100%"}
:::

Figure 1-24 Installation Summary \| Time & Date

\

[Figure 1-24 reflects three adjustments from the default. The city is
changed to Toronto, the clock format is switched to AM/PM, and the
network time is turned off.](#chapter0031.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0032.html}

## Choosing an Installation Source {.style3}

\

12\. You can set the installation source for RHEL 9. By default,
Anaconda chooses the auto-detected installation media (DVD, USB flash
drive, or ISO image) that was used to start this installation. For this
demonstration, leave the installation source to the default. Click Done
to return to the Installation Summary page.

\

::: {style="text-align: center;"}
![](image-QYL8NB4M.jpg){height="100%"}
:::

Figure 1-25 Installation Summary \| Installation Source

::: {style="page-break-before: always;"}
:::

[]{#chapter0033.html}

## Selecting Software to be Installed {.style3}

\

13\. You can choose the base operating environment that you want
installed. Base environments are predefined groups of software packages
designed for specific use cases. The six available base environments are
described in Table 1-2.

\

  ----------------------------------- -----------------------------------
  Base Environment                    Description

  Server with GUI                     Infrastructure server with graphics
                                      support

  Server                              Infrastructure server without
                                      graphics support

  Minimal Install                     Installs a minimum number of
                                      packages for basic system use

  Workstation                         Ideal for desktop and laptop users
                                      who require graphical support and
                                      with a minimal set of services

  Custom Operating System             Gives you a set of basic building
                                      blocks for custom installations

  Virtualization Host                 Infrastructure plus virtualization
                                      support to host virtual machines
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 1-2 Installation Summary \| Software Selection \| Base
Environments

\

Choosing a base environment in the left pane reveals additional
components on the right that may be ticked for installation along with
the selected base environment. See Figure 1-26.

\

::: {style="text-align: center;"}
![](image-Q7PTJJFK.jpg){height="100%"}
:::

Figure 1-26 Installation Summary \| Software Selection

\

The installer automatically picks and installs prerequisite software
components to fulfill dependency requirements for a successful
installation. The default base environment is "Server with GUI" for this
demonstration. Leave add-ons to the default as well. Click Done to
return to the Installation Summary page.

::: {style="page-break-before: always;"}
:::

[]{#chapter0034.html}

## Configuring Installation Destination {.style3}

\

14\. The Installation Destination allows you to choose an available
local or remote disk for partitioning and installing the OS on. Anaconda
selects "Automatic partitioning selected" (highlighted in red) on the
Installation Summary page (Figure 1-23), which you can change on
Installation Destination (Figure 1-27). By default, the 20GB virtual
disk you assigned to the VM is automatically picked up by the installer
as the target and it is represented as sda. The "Encrypt my data"
checkbox under Encryption (scroll down to see it) encrypts all
partitions on the disk. If you choose this option, you will be prompted
to enter a passphrase to access the partitions later. The "Full disk
summary and bootloader" link at the bottom left allows you to choose a
disk to place the bootloader program on. This does not need to be
modified on a single disk system. The default and the only bootloader
program available in RHEL 9 is called GRUB2, and it is explained at
length in Chapter 11, "Boot Process, GRUB2, and the Linux Kernel".

\

::: {style="text-align: center;"}
![](image-IO9H4D76.jpg){height="100%"}
:::

Figure 1-27 Installation Summary \| Installation Destination

\

For this demonstration, stick to the default automatic partitioning
scheme. Simply click Done to return to the previous screen. This scheme
will create three partitions---/boot, /, and swap---and together they
will consume the entire selected disk space.

::: {style="page-break-before: always;"}
:::

[]{#chapter0035.html}

## Configuring Network and Hostname {.style3}

\

15\. Assigning appropriate IP and hostname are essential for system
functionality in a network environment. Click Network & Hostname on the
Installation Summary page and a window similar to the one shown in
Figure 1-28 will appear. Anaconda detects all attached network
interfaces, but it does not automatically assign them IPs. Also, the
default hostname field is empty. You need to modify these assignments so
that your system can communicate with other systems on the network.
Currently, there is one network device assigned to the system, which is
represented as enp0s3.

\

The terms "network interface" and "network device" refer to the same
network hardware component. These terms are used interchangeably
throughout this book. These terms are different from the term "network
connection", which is the software configuration applied to a network
interface/device.

\

The default naming convention for network devices vary based on the
underlying virtualization software being used.

\

Enter the hostname server1.example.com in the Hostname field and click
Apply next to the field to activate it. For IP assignments, click
Configure at the bottom right and enter IP information manually. You
also need to ensure that the network connection is set to autostart.

\

::: {style="text-align: center;"}
![](image-KJ3OEFEP.jpg){height="100%"}
:::

Figure 1-28 Installation Summary \| Network & Hostname

\

There are multiple tabs available on the network connection
configuration screen, as depicted in Figure 1-29. Go to IPv4 Settings
and choose Manual from the drop-down list against Method. Click Add and
enter address 192.168.0.110, netmask 24, and gateway 192.168.0.1. Click
Save to save the configuration and return to the Network & Hostname
window.

\

Check your Windows/MacOS host computer IP assignments and make sure to
use the same subnet for your RHEL VMs. For instance, use
172.16.3.110/120 for your VMs if your host system is on the 172.16.3
subnet.

\

::: {style="text-align: center;"}
![](image-U88JN5XT.jpg){height="100%"}
:::

Figure 1-29 Installation Summary \| Network & Hostname \| Configure

\

On the Network & Hostname window, slide the ON/OFF switch to the ON
position so that the new assignments take effect right away. This will
also ensure that the assignments are applied automatically on subsequent
system reboots.

\

::: {style="text-align: center;"}
![](image-73JSEC0L.jpg){height="100%"}
:::

Figure 1-30 Installation Summary \| Network & Hostname

\

Now click Done to return to the Installation Summary page. Chapter 16
"Networking, Network Devices, and Network Connections" discusses
configuring hostnames, network interfaces, and network connections in
detail.

::: {style="page-break-before: always;"}
:::

[]{#chapter0036.html}

## Configuring User Settings {.style3}

\

16\. Setting the root user password is essential on a Linux system.
Click Root Password on the Installation Summary page and a window
similar to the one shown in Figure 1-31 will appear. Enter a password
twice. Also tick the box "Allow root SSH login with password" to enable
direct root login access to the VM. Click Done to return to the previous
page.

\

::: {style="text-align: center;"}
![](image-IMMYGUZG.jpg){height="100%"}
:::

Figure 1-31 Installation Summary \| Root Password

\

You will need to click Done twice if the password you entered is weak or
too short.

\

17\. Next, click User Creation (not shown earlier on the Installation
Summary page image) under User Settings and create a user account called
user1 and assign it a password. Click Done (two clicks if the password
entered is too short or simple) to return to the previous screen.

\

::: {style="text-align: center;"}
![](image-Y7F3JQTE.jpg){height="100%"}
:::

Figure 1-32 Installation Summary \| User Creation

\

Anaconda will set the root user password and create the user account
during the configuration part of the installation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0037.html}

## Beginning Installation {.style3}

\

18\. You're now on the Installation Summary page. You still have the
opportunity to go back and configure or reconfigure any items you've
missed. Once you are satisfied, click Begin Installation at the bottom
right to initiate the installation based on the configuration entered in
the previous steps. Anaconda will partition the selected disk, install
the software, and perform all the configuration. Any data previously
stored on the disk will be erased and unrecoverable.

\

The Begin Installation button remains inactive until all the items
highlighted in red and with a warning sign are configured.

\

The configuration and software copy will take some time to complete. The
progress will depend on the system performance and resources allocated
to the VM.

::: {style="page-break-before: always;"}
:::

[]{#chapter0038.html}

## Concluding Installation {.style3}

\

19\. When the required setup is complete and all software packages are
installed, the Reboot System button at the bottom right on the
Installation Progress screen (Figure 1-33) will become active. Click
this button to reboot the new system.

\

::: {style="text-align: center;"}
![](image-75HNP06Y.jpg){height="100%"}
:::

Figure 1-33 Configuration \| Finishing Installation

\

By default, VirtualBox does not automatically change the default boot
order for the VM. This may result in rebooting the VM from the ISO image
again and restarting the installation. To avoid this situation, power
off the virtual machine from VirtualBox Manager and alter the boot
sequence.

::: {style="page-break-before: always;"}
:::

[]{#chapter0039.html}

## Changing Default Boot Order {.style3}

\

20\. Power off the VM from VirtualBox Manager.

21\. The current boot sequence, as shown in Figure 1-34, is set to boot
with floppy first and then optical (DVD/CD) followed by hard disk.

\

::: {style="text-align: center;"}
![](image-VR2X26SS.jpg){height="100%"}
:::

Figure 1-34 VirtualBox Manager \| System \| Boot Order

\

22\. Change this sequence to hard disk first and optical next. See
Figure 1-35. Untick Floppy, as it is not needed.

\

::: {style="text-align: center;"}
![](image-LDV9IOW7.jpg){height="100%"}
:::

Figure 1-35 VirtualBox Manager \| System \| Boot Order \| Alter

\

Power on the VM from the VirtualBox Manager. It will boot the installed
OS.

::: {style="page-break-before: always;"}
:::

[]{#chapter0040.html}

## Logging In and Out at the Graphical Console {.style3}

\

Now that the installation is complete, you can log on to the system. You
selected the Server with GUI base environment, which includes graphical
desktop support to interact with the system. You also entered
credentials for a user account, user1, during installation. You can now
use this account to log in.

::: {style="page-break-before: always;"}
:::

[]{#chapter0041.html}

## Logging In for the First Time {.style3}

\

1\. On the graphical logon screen, click user1 and enter the password
when prompted.

\

::: {style="text-align: center;"}
![](image-Z346KSK3.jpg){height="100%"}
:::

Figure 1-36 Graphical Desktop \| Sign-in Screen

\

2\. Select "No Thanks" when prompted for a tour.

3\. The default graphical desktop included in RHEL 9 is the GNOME
desktop environment (Figure 1-37). You should now be able to start using
the system as user1.

\

::: {style="text-align: center;"}
![](image-CFLLTST6.jpg){height="100%"}
:::

Figure 1-37 GNOME Desktop Environment

\

Close the System Not Registered message as you skipped Connect to Red
Hat under Installation Summary \| Software during configuration.

\

GNOME stands for GNU Network Object Model Environment. It is the default
graphical display manager and desktop environment for users in RHEL 9.
Chapter 02 "Initial Interaction with the System" provides more details
on this topic.

::: {style="page-break-before: always;"}
:::

[]{#chapter0042.html}

## Logging Out {.style3}

\

4\. Logging out of the system is easy. Click on any icon in the top
right corner, expand Power Off/Log Out, and click Log Out. See Figure
1-38. The user will be signed out and the main login screen will
reappear.

\

::: {style="text-align: center;"}
![](image-LVZMTSPF.jpg){height="100%"}
:::

Figure 1-38 GNOME Desktop Environment\| Log Out

\

Now, let's look at how to connect and log in to the system remotely from
over the network.

::: {style="page-break-before: always;"}
:::

[]{#chapter0043.html}

## Exercise 1-3: Logging In from Windows {.style3}

\

This exercise should be done on the Windows computer hosting the virtual
machine for server1.

\

In this exercise, you will use a program called PuTTY to access server1
using its IP address and as user1. You will run some basic commands on
the server for validation. You will log off to terminate the session.

\

1\. On Windows desktop, download PuTTY free of charge from the Internet.
Launch this program and enter the target host's IP address. Leave the
rest of the settings to their defaults.

\

::: {style="text-align: center;"}
![](image-7XUS3MGQ.jpg){height="100%"}
:::

Figure 1-39 PuTTY Interface

\

You may assign a name to this session (typically the hostname is used as
the session name) in the Saved Sessions field and click Save to store
this information so as to avoid retyping in the future.

\

2\. Click on the "Open" button at the bottom of the screen to try a
connection.

3\. Click Yes to accept a potential security breach warning. This alert
only appears once.

4\. Enter user1 and password at the "login as" prompt to log in:

\

<div>

![](image-NCGS2C6Y.jpg){height="100%"}

</div>

5\. Issue the basic Linux commands whoami, hostname, and pwd to confirm
that you are logged in as user1 on server1 and placed in the correct
home directory:

\

<div>

![](image-K9PFSVHH.jpg){height="100%"}

</div>

6\. Run the logout or the exit command or press the key combination
Ctrl+d to log off server1 and terminate the login session:

\

<div>

![](image-9SJC3DR2.jpg){height="100%"}

</div>

This concludes the exercise. Going forward, you should be doing all the
exercises and labs presented in this book in PuTTY (ssh) terminal
sessions.

\

[Chapter 02 will explore how to navigate within the GNOME desktop
environment, execute basic Linux commands at the command prompt, and
obtain necessary help.](#chapter0049.html)

::: {style="page-break-before: always;"}
:::

[]{#chapter0044.html}

## Chapter Summary {.style3}

\

In this chapter, we started by looking at Linux history and exploring
available versions of Linux from Red Hat. We examined various
pre-installation items for our lab environment to prepare for a smooth
installation in order to practice the exercises and labs presented in
this book. We demonstrated downloading the images for VirtualBox Manager
software and RHEL 9. We built a virtual machine and installed RHEL 9 in
it. Finally, we logged in to the new system at the console and over the
network via PuTTY to verify the installation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0045.html}

## Review Questions {.style3}

\

1\. RHEL 9 cannot be installed over the network. True or False?

2\. Can you install RHEL 9 in text mode?

3\. You can use the /boot partition within LVM to boot RHEL. True or
False?

4\. Which kernel version is the initial release of RHEL 9 based on?

5\. Several log files are created and updated in the /tmp directory
during the installation process. Where are these files moved to after
the completion of installation?

6\. The Minimal Install base environment includes the graphical support.
True or False?

7\. Name the RHEL installer program.

8\. How many console screens do you have access to during the
installation process?

9\. RHEL 9 may be downloaded from Red Hat's developer site. True or
False?

10\. What is the name of the default graphical user desktop if Server
with GUI is installed?

::: {style="page-break-before: always;"}
:::

[]{#chapter0046.html}

## Answers to Review Questions {.style3}

\

1\. False. RHEL 9 can be installed with installation files located on a
network server.

2\. Yes, RHEL 9 can be installed using text mode.

3\. False. /boot cannot reside within LVM.

4\. The initial release of RHEL 9 is based on kernel version 5.14.

5\. These files are moved to the /var/log directory.

6\. False. Minimal Install base environment does not include graphics
support.

7\. The name of the RHEL installer program is Anaconda.

8\. There are six console screens available to you during the
installation process.

9\. True. RHEL 9 may be downloaded from developers.redhat.com. You need
to open a new account or use an existing before you can download it.

10\. The default graphical desktop is called GNOME desktop environment.

::: {style="page-break-before: always;"}
:::

[]{#chapter0047.html}

## Do-It-Yourself Challenge Labs

\

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab have already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

::: {style="page-break-before: always;"}
:::

[]{#chapter0048.html}

## Lab 1-1: Build RHEL9-VM2 (server2) {.style3}

\

Create another virtual machine called RHEL9-VM2 in VirtualBox, attach
the ISO image to it, and install RHEL 9.1. Use the configuration
provided in "Lab Environment for Practice" and follow the procedures
outlined in Exercise 1-1 and Exercise 1-2. Use PuTTY with the IP address
of the new server to connect to it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0049.html}

## Chapter 02 {style="text-align: right"}

\

### Initial Interaction with the System {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Interact with display manager and understand graphical interface

\

Overview of Linux directory structure

\

Recognize top-level directories

\

Understand command construct

\

Describe and run basic Linux commands

\

Obtain help using multiple native tools and RHEL documentation

\

#### RHCSA Objectives:

\

##### 01. Access a shell prompt and issue commands with correct syntax

##### 11. Locate, read, and use system documentation including man, info, and files in /usr/share/doc

::: {style="page-break-before: always;"}
:::

\

Wayland is an advanced display protocol that sets up the foundation for
running graphical applications in RHEL, which includes system
administration tools, user applications, as well as graphical display
and desktop manager programs. Working in a graphical environment to
interact with the system is convenient for users with limited command
line knowledge or specific requirements.

\

Linux files are organized logically for ease of administration. This
file organization is maintained in hundreds of directories located in
larger containers called file systems. Red Hat Enterprise Linux follows
the File system Hierarchy Standard for file organization, which
describes names, locations, and permissions for many file types and
directories.

\

Linux offers a variety of commands for users and system managers. User
commands are general purpose that are intended for execution by any user
on the system. However, system management commands require elevated
privileges of the superuser. Knowledge of these tools is essential for
productive usage and efficient administration of the system. This
chapter provides an analysis of command components and how to construct
a command. Following that, it introduces a few basic user-level
commands.

\

::: {style="text-align: center;"}
![](image-EIGCXOY4.jpg){height="100%"}
:::

The availability of native help on the system simplifies task execution
for Linux users and system administrators alike. This assistance is
available on commands and configuration files via locally installed
searchable manual pages and documentation for installed packages. In
addition, Red Hat documentation website provides a wealth of information
on various topics, procedures, and command usage.

::: {style="page-break-before: always;"}
:::

[]{#chapter0050.html}

## Linux Graphical Environment {.style3}

\

RHEL allows users to work in both text and graphical environments. Text
interface might be cumbersome, but it is the preferred choice for
administrators and developers. Nevertheless, a graphical environment
provides easier and convenient interaction with the OS by hiding the
challenges that users may otherwise experience when working in
text-mode.

\

Wayland is a client/server display protocol that sets up the foundation
for running graphical programs and applications in RHEL 9. It is
available alongside the legacy X Window System, which has been around in
RHEL for decades. Wayland provides superior graphics capabilities,
features, and performance than X. There are two components that are
critical to the functionality of a graphical environment: a display
manager (a.k.a. login manager) and a desktop environment. Both are
launched following the completion of the groundwork established by
Wayland.

::: {style="page-break-before: always;"}
:::

[]{#chapter0051.html}

## Display/Login Manager

\

A display/login manager handles the presentation of graphical login
screen. It allows users to enter credentials to log on to the system. A
preconfigured graphical desktop manager appears after the credentials
are verified. In RHEL 9, the default display manager is called GNOME
Display Manager (GDM). Figure 2-1 provides an image of GDM.

\

::: {style="text-align: center;"}
![](image-EOVDRFYH.jpg){height="100%"}
:::

Figure 2-1 GNOME Display Manager

\

The login screen presents a list of all normal user accounts that exist
on the system. You can log in as any one of them by selecting the
desired account. If you wish to sign in as an unlisted user or the root
user, click "Not Listed?" and enter the username and password for the
desired account. The current system date and time also appear at the top
of the login screen.

\

There are two downward arrowheads at the top right of the login screen.
The arrowhead on the left is to enable or disable an accessibility
feature. The arrowhead on the right allows you to power off or reboot
the system and change the system volume. More controls become available
after you have logged in. There are three additional icons at the top
right that show the network connectivity, sound level, and battery/power
status.

::: {style="page-break-before: always;"}
:::

[]{#chapter0052.html}

## Desktop Environment {.style3}

\

Once the credentials are validated for a user, the display/login manager
establishes a Desktop Environment (DE) to work in. RHEL 9 comes with
several graphical desktop software with GNOME desktop environment set as
the default. It provides an easy and point-and-click GUI for users to
run programs and operating system tools. Figure 2-2 is an image of the
default GNOME desktop environment for root.

\

::: {style="text-align: center;"}
![](image-0DGMOFPB.jpg){height="100%"}
:::

Figure 2-2 GNOME Desktop Environment

\

If you have worked with Microsoft Windows or MacOS, you should have no
difficulty using this desktop environment. The default screen has an
Activities icon at the top left, which allows you to search and access
programs. Figure 2-3 depicts a list of application icons at the bottom
when you click on Activities.

\

::: {style="text-align: center;"}
![](image-YUOF8FBN.jpg){height="100%"}
:::

Figure 2-3 GNOME Desktop Environment \| Activities

\

These application icons represent (from the left) the Firefox web
browser, file manager, software updates, GNOME help, and shell terminal.
The icon with nine dots displays all available programs, including
Settings. The Settings application includes administrative and
user-level controls to view or modify configuration for Wi-Fi,
Bluetooth, desktop background, notifications, regional settings,
privacy, sound, power, screensaver, network, and more.

::: {style="page-break-before: always;"}
:::

[]{#chapter0053.html}

## Linux Directory Structure and File Systems {.style3}

\

Linux files are organized logically in a hierarchy for ease of
administration and recognition. This organization is maintained in
hundreds of directories located in larger containers called file
systems. Red Hat Enterprise Linux follows the Filesystem Hierarchy
Standard (FHS) for file organization, which describes names, locations,
and permissions for many file types and directories.

\

Linux file systems contain files and subdirectories. A subdirectory,
also referred to as a child directory, is located under a parent
directory. The parent directory is a subdirectory of a higher-level
directory. The Linux directory structure is analogous to an inverted
tree, where the top of the tree is the root of the directory, tree
branches are subdirectories, and leaves are files. The root of the
directory is represented by the forward slash character (/), and this is
where the entire directory structure is ultimately connected. The
forward slash is also used as a directory separator in a path, such as
/etc/rc.d/init.d/README.

\

In this example, the etc subdirectory is located under /, making root
the parent of etc (which is a child), rc.d (child) is located under etc
(parent), init.d (child) is located under rc.d (parent), and README
(leaf) is located under init.d (parent) at the bottom.

\

The term subdirectory is used for a directory that has a parent
directory.

\

Each directory has a parent directory and a child directory, with the
exception of the root and the lowest level subdirectories. The root
directory has no parent, and the lowest level subdirectory has no child.

::: {style="page-break-before: always;"}
:::

[]{#chapter0054.html}

## Top-Level Directories

\

The key top-level directories under the / are shown in Figure 2-4. Some
of these hold static data while others contain dynamic or variable
information. Static data refers to file content that remains unchanged
unless modified explicitly. Dynamic or variable data, in contrast,
refers to file content that is modified and updated as required by
system processes. Static directories normally contain commands,
configuration files, library routines, kernel files, device files, etc.,
and dynamic directories contain log files, status files, temporary
files, etc.

\

::: {style="text-align: center;"}
![](image-0Y6JGBPH.jpg){height="100%"}
:::

Figure 2-4 Linux Directory Structure

\

The hierarchical directory structure keeps related information together
in a logical fashion. Compare this concept with a file cabinet
containing several drawers, with each drawer storing multiple file
folders.

::: {style="page-break-before: always;"}
:::

[]{#chapter0055.html}

## File System Categories {.style3}

\

There are a variety of file system types supported in RHEL that can be
categorized in three basic groups: disk-based, network-based, and
memory-based. Disk-based file systems are typically created on physical
media such as a hard drive or a USB flash drive. Network-based file
systems are essentially disk-based file systems that are shared over the
network for remote access. Memory-based file systems are virtual; they
are created automatically at system startup and destroyed when the
system goes down. The first two types of file systems store information
persistently, while any data saved in virtual file systems is lost at
system reboots.

\

During RHEL installation, two disk-based file systems are created when
you select the default partitioning. These file systems are referred to
as the root and boot file systems. Furthermore, several memory-based
file systems are vital to the operation of a RHEL system.

::: {style="page-break-before: always;"}
:::

[]{#chapter0056.html}

## The Root File System (/), Disk-Based {.style3}

\

The root directory is the top-level file system in the FHS and contains
many higher-level directories that store specific information. Some of
the key directories are:

\

/etc: The etcetera (or extended text configuration) directory holds
system configuration files. Some common subdirectories are systemd,
sysconfig, lvm, and skel, which comprise configuration files for
systemd, most system services, the Logical Volume Manager, and per-user
shell startup template files, respectively.

\

/root: This is the default home directory location for the root user.

\

/mnt: This directory is used to mount a file system temporarily.

\

The size of the root file system is automatically determined by the
installer program based on the available disk space when you select the
default partitioning; however, it may be altered at the time of
installation if required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0057.html}

## The Boot File System (/boot), Disk-Based {.style3}

\

The boot file system contains the Linux kernel, boot support files, and
boot configuration files. Just like the root file system, the size of
this file system is also automatically determined by the installer
program based on the available disk space when you select the default
partitioning; however, it may be set to a different size during or after
the installation if required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0058.html}

## The Home Directory (/home) {.style3}

\

The /home directory is designed to store user home directories and other
user contents. Each user is assigned a home directory to save personal
files, and the user can block access to other users.

::: {style="page-break-before: always;"}
:::

[]{#chapter0059.html}

## The Optional Directory (/opt) {.style3}

\

This directory can be used to hold additional software that may need to
be installed on the system. A subdirectory is created for each installed
software.

::: {style="page-break-before: always;"}
:::

[]{#chapter0060.html}

## The UNIX System Resources Directory (/usr) {.style3}

\

This directory contains most of the system files. Some of the important
subdirectories are:

\

/usr/bin: The binary directory contains crucial user executable
commands.

\

/usr/sbin: Most commands are required at system boot, and those that
require the root user privileges in order to run are located in this
system binary directory. In other words, this directory contains crucial
system administration commands that are not intended for execution by
normal users (although they can still run a few of them). This directory
is not included in the default search path for normal users because of
the nature of data it holds.

\

/usr/lib and /usr/lib64: The library directories contain shared library
routines required by many commands and programs located in the /usr/bin
and /usr/sbin directories, as well as by the kernel and other
applications and programs for their successful installation and
operation. The /usr/lib directory also stores system initialization and
service management programs. The subdirectory /usr/lib64 contains 64-bit
shared library routines.

\

/usr/include: This directory contains header files for C language.

\

/usr/local: This directory serves as a system administrator repository
for storing commands and tools downloaded from the web, developed
in-house, or obtained elsewhere. These commands and tools are not
generally included with the original Linux distribution. In particular,
/usr/local/bin holds executables, /usr/local/etc holds configuration
files, and /usr/local/lib and /usr/local/lib64 holds library routines.

\

/usr/share: This is the directory location for manual pages,
documentation, sample templates, configuration files, etc., that may be
shared with other Linux platforms.

\

/usr/src: This directory is used to store source code.

::: {style="page-break-before: always;"}
:::

[]{#chapter0061.html}

## The Variable Directory (/var) {.style3}

\

The /var directory contains data that frequently changes while the
system is operational. Files in this directory contain log, status,
spool, lock, and other dynamic data. Some common subdirectories under
/var are:

\

/var/log: This is the storage for most system log files, such as system
logs, boot logs, user logs, failed user logs, installation logs, cron
logs, mail logs, etc.

\

/var/opt: This directory stores log, status, and other variable data
files for additional software installed in /opt.

\

/var/spool: Directories that hold print jobs, cron jobs, mail messages,
and other queued items before being sent out to their intended
destinations are located here.

\

/var/tmp: Large temporary files or temporary files that need to exist
for longer periods of time than what is typically allowed in another
temporary directory, /tmp, are stored here. These files survive system
reboots and are automatically deleted if they are not accessed or
modified for a period of 30 days.

::: {style="page-break-before: always;"}
:::

[]{#chapter0062.html}

## The Temporary Directory (/tmp) {.style3}

\

This directory is a repository for temporary files. Many programs create
temporary files here during runtime or installation. These files survive
system reboots and are automatically removed if they are not accessed or
modified for a period of 10 days.

::: {style="page-break-before: always;"}
:::

[]{#chapter0063.html}

## The Devices File System (/dev), Virtual {.style3}

\

The Devices (dev file system) file system is accessible via the /dev
directory, and it is used to store device nodes for physical hardware
and virtual devices. The Linux kernel communicates with these devices
through corresponding device nodes located here. These device nodes are
automatically created and deleted by the udevd service (a Linux service
for dynamic device management) as necessary.

\

There are two types of device files: character (or raw) device files,
and block device files. The kernel accesses devices using one of these
files or both.

\

Character devices are accessed serially with streams of bits transferred
during kernel and device communication. Examples of such devices are
console, serial printers, mice, keyboards, terminals, etc.

\

Block devices are accessed in a parallel fashion with data exchanged in
blocks (parallel) during kernel and device communication. Data on block
devices is accessed randomly. Examples of block devices are hard disk
drives, optical drives, parallel printers, etc.

::: {style="page-break-before: always;"}
:::

[]{#chapter0064.html}

## The Procfs File System (/proc), Virtual {.style3}

\

The Procfs (process file system) file system is accessible via the /proc
directory, and it is used to maintain information about the current
state of the running kernel. This includes the details for current
hardware configuration and status information on CPU, memory, disks,
partitioning, file systems, networking, running processes, and so on.
This information is stored in a hierarchy of subdirectories that contain
thousands of zero-length pseudo files. These files point to relevant
data maintained by the kernel in the memory. This virtual directory
structure simply provides an easy interface to interact with
kernel-maintained information. The Procfs file system is dynamically
managed by the system.

\

The contents in /proc are created in memory at system boot time, updated
during runtime, and destroyed at system shutdown.

::: {style="page-break-before: always;"}
:::

[]{#chapter0065.html}

## The Runtime File System (/run), Virtual {.style3}

\

This virtual file system is a repository of data for processes running
on the system. One of its subdirectories, /run/media, is also used to
automatically mount external file systems such as those that are on
optical (CD and DVD) and flash USB.

\

The contents of this file system are automatically deleted at system
shutdown.

::: {style="page-break-before: always;"}
:::

[]{#chapter0066.html}

## The System File System (/sys), Virtual {.style3}

\

Information about hardware devices, drivers, and some kernel features is
stored and maintained in the /sys file system. This information is used
by the kernel to load necessary support for the devices, create device
nodes in /dev, and configure the devices. This file system is
auto-maintained as well.

::: {style="page-break-before: always;"}
:::

[]{#chapter0067.html}

## Essential System Commands {.style3}

\

There are hundreds of commands available in RHEL that range from simple
to complex in terms of their construct and usage. Commands can be
combined to build complex structures for innovative use cases. Some
commands offer a few options, while others have as many as 70 or more.
This section furnishes an understanding of how commands are formed and
demonstrates the use of some of the basic, common Linux commands. You
will learn more commands and their advanced usages throughout this book.

::: {style="page-break-before: always;"}
:::

[]{#chapter0068.html}

## Starting a Remote Terminal Session {.style3}

\

In order to issue commands and run programs at the command prompt, you
need access to a terminal session. Follow the steps identified in
Exercise 1-3 to log in to the system remotely as the root user. Figure
2-5 below shows a session with root user logged in.

\

::: {style="text-align: center;"}
![](image-VBWMF02L.jpg){height="100%"}
:::

Figure 2-5 Remote Terminal Session

\

The header bar displays the logged-in username, hostname, and your
current directory location.

\

The "\[root@server1 \~\]#" is the default representation of the command
prompt. It reflects the logged-in username (root, user1, etc.), hostname
of the system (server1, server2, etc.), and your current directory
location, all enclosed within square brackets \[\]. The command prompt
ends with the hash sign (#) for the root user or the dollar sign (\$)
for normal users outside of the closing square bracket. Commands are
typed at the cursor position and executed by pressing the Enter key.

::: {style="page-break-before: always;"}
:::

[]{#chapter0069.html}

## Understanding the Command Mechanics {.style3}

\

To practice the commands provided in this chapter, you can log in as
user1, run the commands, and observe their outputs. However, as you are
learning Linux system administration, it's important to feel comfortable
working as root in the beginning. If something breaks, server1 and
server2 are lab servers and they can be rebuilt.

\

The basic syntax of a Linux command is:

\

command option(s) argument(s)

\

Options (a.k.a. a switch of flag) are optional. You can specify zero or
more options with a command. Arguments, in contrast, may be optional or
mandatory depending on the command and its usage. Many commands have
preconfigured default options and arguments. You are not required to
specify them. Other commands do require at least one option or argument
in order to work. An option modifies the behavior of the command. An
argument supplies a target on which to perform the command action.

\

An option may start with a single hyphen character (-la, for instance),
and it is referred to as the short-option format. Each individual letter
in this depiction represents a separate option (l and a are two options
in -la). This is a frequent format throughout this book.

\

An option may also begin with two hyphen characters (\--all, for
instance), and it is referred to as the long-option format. All letters
in this representation are collectively identified as a single option
(-all is one option).

\

The following examples express some command structures with a
description on the right that states the number of options and arguments
supplied:

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

  ----------------------------------- -----------------------------------
  \# ls                               No option, no explicit argument;
                                      the default argument is the current
                                      directory name

  \# ls -l                            One option, no explicit argument;
                                      the default argument is the current
                                      directory name

  \# ls -al                           Two options, no explicit argument;
                                      the default argument is the current
                                      directory name

  \# ls \--all                        One option, no explicit argument;
                                      the default argument is the current
                                      directory name

  \# ls -l directory_name             One option, one explicit argument
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Use online help on the usage of a command if needed. Refer to
"Getting Help" later in this chapter for details on how to access and
use help.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Now let's take a look at some essential Linux commands and understand
their usage.

::: {style="page-break-before: always;"}
:::

[]{#chapter0070.html}

## Listing Files and Directories {.style3}

\

One of the most rudimentary commands in Linux is the ls (list) command.
It is used to show the list of files and directories. This command
supports a multitude of options, some of which are listed in Table 2-1
along with a short explanation.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -a                                  Includes hidden files and
                                      directories in the output. A file
                                      or directory name that begins with
                                      the period character (.) is
                                      considered hidden.

  -l                                  Displays long listing with detailed
                                      file information including the file
                                      type, permissions, link count,
                                      owner, group, size, date and time
                                      of last modification, and name of
                                      the file

  -ld                                 Displays long listing of the
                                      specified directory but hides its
                                      contents

  -lh                                 Displays long listing with file
                                      sizes shown in human-friendly
                                      format

  -lt                                 Lists all files sorted by date and
                                      time with the newest file first

  -ltr                                Lists all files sorted by date and
                                      time with the oldest file first
                                      (reverse)

  -R                                  Lists contents of the specified
                                      directory and all its
                                      subdirectories (recursive listing)
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 2-1 ls Command Options

\

A grasp of the usage of this command and the output it produces is
important. The following examples will illustrate the impact of options
used with the ls command.

\

To list files in the current directory with the assumption that you are
in the /root directory:

\

<div>

![](image-PHLYAZVF.jpg){height="100%"}

</div>

To list files in the current directory with detailed information:

\

<div>

![](image-BOX5Z77F.jpg){height="100%"}

</div>

The long listing in the output above furnishes a unique piece of
information about the file or directory in nine discrete columns:

\

Column 1: The first character (hyphen or d) divulges the file type, and
the next nine characters (rw-rw-r\--) indicate permissions.

Column 2: Displays the number of links (links are explained later in
this chapter)

### Column 3: Shows the owner name {.style3}

### Column 4: Exhibits the owning group name {.style3}

Column 5: Identifies the file size in bytes. For directories, this
number reflects the number of blocks being used by the directory to hold
information about its contents.

### Columns 6, 7, and 8: Displays the month, day, and time of creation or last modification {.style3}

Column 9: Indicates the name of the file or directory

\

As an alternative to ls -l, you may use its shortcut ll for brevity and
convenience unless there is a specific need to use the former.

\

To show the long listing of only the specified directory without showing
its contents:

\

<div>

![](image-0O8WG75W.jpg){height="100%"}

</div>

To display all files in the current directory with their sizes in
human-friendly format:

\

<div>

![](image-QFQ50CUV.jpg){height="100%"}

</div>

To list all files, including the hidden files, in the current directory
with detailed information:

\

<div>

![](image-IQP067S8.jpg){height="100%"}

</div>

To repeat the previous example with the output sorted by date and time
and with the newest file first:

\

<div>

![](image-8E6BPMM9.jpg){height="100%"}

</div>

To list contents of the /etc directory recursively:

\

<div>

![](image-R45WLN04.jpg){height="100%"}

</div>

Run man ls at the command prompt to view the manual pages of the ls
command with all the options it supports and how to use them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0071.html}

## Printing Working Directory {.style3}

\

The pwd (print working directory or present working directory) command
displays a user's current location in the directory tree. The following
example shows that root is currently in the /root directory:

\

<div>

![](image-RSZ89C0C.jpg){height="100%"}

</div>

/root is the home directory for the root user. The pwd command always
returns the absolute path to a file or directory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0072.html}

## Navigating Directories {.style3}

\

Files are placed in various directories in Linux, and there are tens of
thousands of them. Each file and directory is recognized by a unique
path in the directory tree. A path (or pathname) is like a road map that
shows you how to get from one place in the directory hierarchy to
another. It uniquely identifies a particular file or directory by its
absolute or relative location in the directory structure.

\

An absolute path (a.k.a. a full path or a fully qualified pathname)
points to a file or directory in relation to the top of the directory
tree. It always starts with the forward slash (/). You can use the pwd
command to view your current absolute path in the tree:

\

<div>

![](image-AJL9FOAO.jpg){height="100%"}

</div>

The output indicates that /root is the current location for the root
user in the directory hierarchy, and the leading / identifies this
location as a full path.

\

A relative path, on the other hand, points to a file or directory in
relation to your current location. This file path never begins with the
forward slash (/). It may begin with two period characters (..) or with
a subdirectory name without a leading /, such as etc/sysconfig.

\

It's easy to navigate in the directory hierarchy if you have a good
understanding of the absolute and relative paths and the key difference
between them. Let's run a couple of examples using the cd (change
directory) command, which is used to switch between directories, and
verify the result with the pwd command.

\

To determine the current location and then go one level up into the
parent directory using the relative path:

\

<div>

![](image-F50DK2QV.jpg){height="100%"}

</div>

The above sequence of commands display the current location (/root
output of pwd), then move one level up (cd .. is relative to the current
location), and finally verify the new location (/ output of pwd). You
may want to use the absolute path (cd /) instead of (cd ..) to go to the
top of the directory tree (parent directory of /root).

\

Now, let's switch to the directory sysconfig, which is located under
/etc. There are two options: the absolute path (/etc/sysconfig), or the
relative path (etc/sysconfig):

\

<div>

![](image-KG8A2UB7.jpg){height="100%"}

</div>

To change into the /usr/bin directory, for instance, you can run either
of the following:

\

<div>

![](image-S1GJXJW7.jpg){height="100%"}

</div>

The above example indicates that the absolute path can be used to switch
into a target directory regardless of your current location in the
hierarchy. However, a relative path must be entered based on your
current location in order to move to a target directory.

\

At this point, if you want to return to your home directory, you can
simply run the cd command without inputting a path or by supplying the
tilde character (\~) with it. Either of the two will produce the desired
result.

\

<div>

![](image-PHCHRAPP.jpg){height="100%"}

</div>

In the above example, you could also use the absolute path (cd /root) or
a relative path (cd ../../root) instead.

\

To switch between the current and previous directories, issue the cd
command with the hyphen character (-). See the following example and
observe the output:

\

<div>

![](image-KVGSWNYH.jpg){height="100%"}

</div>

The example shows the use of the hyphen character (-) with the cd
command to switch between the current and previous directories.

::: {style="page-break-before: always;"}
:::

[]{#chapter0073.html}

## Viewing Directory Hierarchy {.style3}

\

The tree command lists a hierarchy of directories and files. There are a
number of options with this command that can be specified to include
additional information. Table 2-2 describes some common options.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -a                                  Includes hidden files in the output

  -d                                  Excludes files from the output

  -h                                  Displays file sizes in
                                      human-friendly format

  -f                                  Prints the full path for each file

  -p                                  Includes file permissions in the
                                      output
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 2-2 tree Command Options

\

To list only the directories in the root user home directory (/root):

\

<div>

![](image-6C8003QO.jpg){height="100%"}

</div>

The output indicates that there are eight directories under /root.

\

To list files in the /etc/sysconfig directory along with their sizes in
human-readable format, permissions, and full path:

\

<div>

![](image-ZZQ5KI48.jpg){height="100%"}

</div>

The output shows permissions in column 1, sizes in column 2, and full
path of the files in column 3.

::: {style="page-break-before: always;"}
:::

[]{#chapter0074.html}

Run man tree at the command prompt to view the manual pages of this
command for additional options and their usage.

\

## Identifying Terminal Device File {.style3}

\

Linux allocates unique pseudo (or virtual) numbered device files to
represent terminal sessions opened by users on the system. It uses these
files to communicate with individual sessions. By default, these files
are stored in the /dev/pts (pseudo terminal session) directory. These
files are created by the system when a user opens a new terminal session
and they are removed on its closure. The destroyed files are recreated
and reused for new terminal sessions.

\

Linux provides a command called tty (teletype) to identify your current
active terminal session. Here is an example:

\

<div>

![](image-OARQ88HS.jpg){height="100%"}

</div>

The output discloses the filename "0" and its location (/dev/pts
directory).

::: {style="page-break-before: always;"}
:::

[]{#chapter0075.html}

## Inspecting System's Uptime and Processor Load {.style3}

\

The uptime command is used to display the system's current time, length
of time it has been up for, number of users currently logged in, and the
average CPU (processing) load over the past 1, 5, and 15 minutes. See
the following output:

\

<div>

![](image-53B9PR0U.jpg){height="100%"}

</div>

The output shows the current system time (14:49:51), up duration (21
hours and 48 minutes), number of logged-in users (2), and the CPU load
averages over the past 1, 5, and 15 minutes (0.00, 0.00, and 0.00),
respectively.

\

The load average numbers correspond to the percentage of CPU load with
0.00 and 1.00 represent no load and full load, and a number greater than
1.00 signifies excess load (over 100%).

::: {style="page-break-before: always;"}
:::

[]{#chapter0076.html}

## Clearing the Screen {.style3}

\

The clear command clears the terminal screen and places the cursor at
the top left of the screen. This command is useful to clear the screen
of any distractive content and run new commands on a clean slate.

\

<div>

![](image-O228U47E.jpg){height="100%"}

</div>

You can also use Ctrl+l for this command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0077.html}

## Determining Command Path {.style3}

\

RHEL provides a set of tools that can be used to identify the absolute
path of the command that will be executed when you run it without
specifying its full path. These tools are the which, whereis, and type
commands. The following examples show the full location of the uptime
command:

\

<div>

![](image-Q7UY9UP5.jpg){height="100%"}

</div>

As shown above, all three commands responded with an identical path
location for the uptime command, which is /usr/bin/uptime. This implies
that there is no need to type the entire path /usr/bin/uptime to run
uptime, as the system will automatically determine its location based on
some predefined settings. Refer to Chapter 07 "The Bash Shell" for more
guidance.

::: {style="page-break-before: always;"}
:::

[]{#chapter0078.html}

## Viewing System Information {.style3}

\

There are several elements in the RHEL system that identify various
information regarding the operating system, hardware, kernel, storage,
networking, and so on. The uname command identifies elementary
information about the system including its hostname. Without any
options, the output of this command is restricted to displaying the
operating system name only; however, it reports other details by adding
the -a option.

\

<div>

![](image-A7ODXPK9.jpg){height="100%"}

</div>

The data returned by the second command above is elaborated below:

\

  ----------------------------------- -----------------------------------
  Linux                               Kernel name

  server1.example.com                 Hostname of the system

  5.14.0-162.6.1.el9_1.x86_64         Kernel release

  #1 SMP PREEMPT_DYNAMIC Fri Sep 30   Date and time of the kernel built
  07:36:03 EDT 2022                   

  x86_64                              Machine hardware name

  x86_64                              Processor type

  x86_64                              Hardware platform

  GNU/Linux                           Operating system name
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Try running the uname command with the -s (kernel name), -n (node name),
-r (kernel release), -v (kernel build date), -m (hardware name), -p
(processor type), -i (hardware platform), and -o (OS name) options
separately to view specific information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0079.html}

## Viewing CPU Specs {.style3}

\

A CPU has many architectural pieces that can be looked at using the
lscpu command. These pieces include the CPU architecture, its operating
modes, vendor, family, model, speed, cache memory, and whether it
supports virtualization. The following example shows the CPU information
from server1:

\

<div>

![](image-3RZ4PAD4.jpg){height="100%"}

</div>

The output indicates the architecture of the CPU (x86_64), supported
modes of operation (32-bit and 64-bit), number of CPUs (2), vendor ID
(GenuineIntel), model name (Intel ...), threads per core (1), cores per
socket (2), number of sockets (1), the amount and levels of cache memory
(L1d, L1i, L2, and L3), and other information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0080.html}

## Getting Help {.style3}

\

While working on the system, you may require help to obtain information
about a command or a configuration file. RHEL offers online help via
manual pages. Manual pages are online documentation that provides
details on commands, configuration files, etc. They are installed under
the /usr/share/man directory when associated software packages are
installed.

\

In addition to the manual pages, apropos and whatis commands as well as
documentation located in the /usr/share/doc directory are also available
on the system.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: If you need help with a command or configuration file, do not
hesitate to use the man pages, refer to the documentation available in
the /usr/share/doc directory, or employ one of the other help tools.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0081.html}

## Accessing Manual Pages {.style3}

\

Use the man command to view manual pages. The following example shows
how to check manual pages for the passwd command:

\

<div>

![](image-LAIVUJED.jpg){height="100%"}

</div>

The output returns the name of the command, the section of the manual
pages it is documented in within the parentheses, and the type (User
utilities) of the command on line 1. It then shows a short description
(NAME), the command's usage (SYNOPSIS), and a long description
(DESCRIPTION), followed by a detailed explanation of each option
(OPTIONS) that the command supports and other relevant data. The
highlighted line at the bottom indicates the line number of the manual
page. Press h to get help on navigation, press q to quit and return to
the command prompt, use the Up and Down arrow keys to scroll up and
down, and the PgUp and PgDn keys to scroll one page at a time.

\

[Table 2-3 summarizes the six keys described above and introduces more
to assist in navigation.](#chapter0081.html)

\

  ----------------------------------- -----------------------------------
  Key                                 Action

  Enter / Down arrow                  Moves forward one line

  Up arrow                            Moves backward one line

  f / Spacebar / Page down            Moves forward one page

  b / Page up                         Moves backward one page

  d / u                               Moves down / up half a page

  g / G                               Moves to the beginning / end of the
                                      man pages

  :f                                  Displays the line number and bytes
                                      being viewed

  q                                   Quits the man pages

  /pattern                            Searches forward for the specified
                                      pattern

  ?pattern                            Searches backward for the specified
                                      pattern

  n / N                               Finds the next / previous
                                      occurrence of a pattern

  h                                   Gives help on navigational keys
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 2-3 Navigating within Manual Pages

\

Run man on any of the commands that you have reviewed so far and
navigate using the keys provided in Table 2-3 for practice.

::: {style="page-break-before: always;"}
:::

[]{#chapter0082.html}

## Headings in the Manual {.style3}

\

Each page in the manual organizes information under several headings.
Some common headings are NAME of the command or file with a short
description, SYNOPSIS (syntax summary), long DESCRIPTION, available
OPTIONS, EXAMPLES to explain the usage, a list of related FILES, SEE
ALSO (reference) to other manual pages or topics, any reported BUGS or
issues, and AUTHOR information. You may find a subset of these headings
or additional headings depending on what information is documented for
that command or file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0083.html}

## Manual Sections {.style3}

\

Depending on the type of information, the manual information is split
into nine sections for organization and clarity. For instance, section 1
refers to user commands (see "NAME" for an example of the passwd
command), section 4 contains special files, section 5 describes file
formats for many system configuration files, and section 8 documents
system administration and privileged commands that are designed for
execution by the root user.

\

The default behavior of the man command is to search through section 1
and each successive section until it finds a match. There are a few
commands in Linux that also have a configuration file with an identical
name. One instance is the passwd command and the passwd file. The former
is located in the /usr/bin directory and the latter in the /etc
directory.

\

When you run man passwd, the man command scans through the manual pages
and the first occurrence it finds is of the passwd command that's stored
in section 1. If you want to consult the manual pages of the passwd
configuration file, you will need to specify the section number with the
command (man 5 passwd) to instruct it to scan that particular section
only.

\

<div>

![](image-2KYYXF5Y.jpg){height="100%"}

</div>

The header at the top in the above output is an indication that this
help is for the passwd file and it is documented in section 5.

::: {style="page-break-before: always;"}
:::

[]{#chapter0084.html}

## Searching by Keyword {.style3}

\

Sometimes you need to use a command, but you can't recall its name.
Linux allows you to perform a keyword search on manual pages using the
man command with the -k (lowercase) flag, or the apropos command. These
commands search all sections of the manual pages and show a list of all
entries matching the specified keyword in their names or descriptions.

\

Before you can perform keyword searches on a new Linux installation,
you'll need to run the mandb command in order to build an indexed
database of the manual pages. This activity depends on the speed and the
number of RHEL packages installed on the system, and it should not take
long to perform. Simply type the command at the prompt and press the
Enter key as follows:

\

<div>

![](image-CTK4D6LS.jpg){height="100%"}

</div>

Now you are ready to run keyword lookups. As an example, to find a
forgotten XFS administration command, search for a string "xfs" by
running either man -k xfs or apropos xfs. Both will produce an identical
result.

\

<div>

![](image-ZS97GPLO.jpg){height="100%"}

</div>

Once you have identified the command you were looking for, you can check
that command's manual pages for usage.

\

Some commands also support the use of the \--help and -? parameters.
These parameters provide a brief list of options and a description
without going through the manual pages. For example, to get quick help
on the passwd command, run either passwd \--help or passwd -?:

\

<div>

![](image-UZRFBCBC.jpg){height="100%"}

</div>

\

Not all commands support the \--help and -? parameters.

::: {style="page-break-before: always;"}
:::

[]{#chapter0085.html}

## Exposing Short Description {.style3}

\

The whatis command searches for a short description of the specified
command or file in the manual database. It quickly scans through the
installed manual pages for the specified string and displays all
matching entries. For instance, the following shows outputs of the
command when run on yum.conf and passwd files:

\

<div>

![](image-SBGS7UQ8.jpg){height="100%"}

</div>

The first output indicates that the specified file is a configuration
file associated with the yum command, and the second output points to
three entries for the passwd file (one configuration file and two
commands).

\

You may alternatively run man -f yum.conf and man -f passwd for the
exact same results. Both man -f and whatis produce identical output.

::: {style="page-break-before: always;"}
:::

[]{#chapter0086.html}

## Documentation in the /usr/share/doc Directory {.style3}

\

The /usr/share/doc directory stores general documentation for installed
packages under subdirectories that match their names. For example, the
documentation for the gzip package includes the following files:

\

<div>

![](image-P52C8YQ1.jpg){height="100%"}

</div>

These text files contain general information about the gzip package.
However, the manual pages and the info documentation prove to be more
resourceful to Linux users and administrators.

::: {style="page-break-before: always;"}
:::

[]{#chapter0087.html}

## Red Hat Enterprise Linux 9 Documentation {.style3}

\

The website at docs.redhat.com hosts documentation for Red Hat's various
products including RHEL 9 in HTML, PDF, and EPUB formats. See Figure
2-6.

\

::: {style="text-align: center;"}
![](image-RLHIS7S9.jpg){height="100%"}
:::

Figure 2-6 Red Hat's Webpage for RHEL 9 Documentation

\

This set of documentation includes release notes, as well as guides on
planning, installation, administration, security, storage management,
virtualization, and so on. For reference, you can download any of these
guides for free in a format of your choice.

::: {style="page-break-before: always;"}
:::

[]{#chapter0088.html}

## Chapter Summary {.style3}

\

This chapter touched upon a few basic topics. We started by looking at a
new display protocol that has replaced the legacy X Window System in
RHEL 9. We interacted with the operating system at the graphical console
screen and examined various settings.

\

Next, we reviewed the Linux file system structure standard and
significant higher-level subdirectories that consisted of static and
variable files, and were grouped logically into lower-level
subdirectories.

\

We analyzed command construct, and learned and run selected user level
commands for familiarity. These tools included listing, viewing, and
identifying basic information, and navigating in the directory
hierarchy.

\

Finally, we learned how to access online help for commands and
configuration files. We saw how to search through manual pages for
desired text. Explanations regarding what commands to use were offered
for additional help.

::: {style="page-break-before: always;"}
:::

[]{#chapter0089.html}

## Review Questions {.style3}

\

1\. What type of information does section 5 in manual pages contain?

2\. Which protocol is used as the default display protocol in RHEL 9?

3\. Which command can be used to determine the time the kernel was
build?

4\. RHEL follows the Filesystem Hierarchy Standard. True or False?

5\. Consider a Linux system with six processor cores. How many times do
you have to run the lscpu command to pull information for all the cores?

6\. Which three categories can Linux file systems be divided into?

7\. Which three commands may be used to identify the full path of a
command?

8\. Which Linux command displays the hierarchy of a directory?

9\. Linux commands may be categorized into two groups: privileged and
non-privileged. True or False?

10\. What is the name of the default display manager in RHEL 9?

11\. What is the use of the apropos command?

12\. Which Linux service creates device nodes at system startup?

13\. What is the function of the pwd command?

14\. Which three formats RHEL 9 documentation is available in at
docs.redhat.com?

15\. What are the -R and -a options used for with the ls command?

16\. What is the default number of days files in /tmp are kept before
they are automatically deleted if not accessed or modified.

::: {style="page-break-before: always;"}
:::

[]{#chapter0090.html}

## Answers to Review Questions {.style3}

\

1\. Section 5 of the manual pages contain information on configuration
files.

2\. Wayland is the default display protocol in RHEL 9.

3\. The uname command shows the kernel build time.

4\. True.

5\. Only one time.

6\. Linux file systems may be divided into disk-based, network-based,
and memory-based file systems.

7\. The which, whereis, and type commands may be used to determine the
full path for a specified command.

8\. The tree command shows the hierarchy of a directory.

9\. True.

10\. GNOME Display Manager is the default display manager in RHEL 9.

11\. The apropos command can be used to perform a keyword search in the
manual pages.

12\. The udevd service.

13\. The pwd command shows the absolute path of the current working
directory.

14\. The RHEL 9 documentation is available in PDF, EPUB, and HTML
formats.

15\. The -R option is used for recursive directory listing and the -a
option for listing hidden files.

16\. Ten days.

::: {style="page-break-before: always;"}
:::

[]{#chapter0091.html}

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

[]{#chapter0092.html}

## Lab 2-1: Navigate Linux Directory Tree {.style3}

\

As user1 on server3, execute the pwd command to check your location in
the directory tree. Run the ls command with appropriate switches to show
files in the current directory including the hidden files. Change
directory into /etc and run pwd again to confirm the directory change.
Switch back to the directory where you were before and run pwd again to
verify. (Hint: Essential System Commands).

::: {style="page-break-before: always;"}
:::

[]{#chapter0093.html}

## Lab 2-2: Miscellaneous Tasks {.style3}

\

As user1 on server3, execute the tty command to identify the terminal
device file. Observe the terminal number reported. Open a couple of more
terminal sessions, and run the tty command and compare the terminal
numbers. Execute the uptime command and analyze the system uptime and
processor load information. Use the three commands---which, whereis, and
type---and identify the location of the vgs command. (Hint: Essential
System Commands).

::: {style="page-break-before: always;"}
:::

[]{#chapter0094.html}

Lab 2-3: Identify System and Kernel Information

\

As user1 on server3, issue uname -a. Analyze the basic information about
the system and kernel reported. Run the lscpu command and examine the
key items relevant to the processor. (Hint: Essential System Commands).

::: {style="page-break-before: always;"}
:::

[]{#chapter0095.html}

## Lab 2-4: Use Help {.style3}

\

As user1 on server3, run man uname and man 5 shadow, and browse various
headings and understand what they contain. Try apropos ext4 and man -k
ext4, whatis group, and observe their outputs. (Hint: Getting Help).

::: {style="page-break-before: always;"}
:::

[]{#chapter0096.html}

## Chapter 03 {style="text-align: right"}

\

### Basic File Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Common types of file in Linux

\

Compress and uncompress files

\

Archive and compress files and directories

\

Edit files with the vim editor

\

Create, list, display, copy, move, rename, and remove files and
directories

\

Create file and directory links

\

Identify differences between copying and linking

\

#### RHCSA Objectives:

\

06\. Archive, compress, unpack, and uncompress files using tar, star,
gzip, and bzip2

07\. Create and edit text files

08\. Create, delete, copy, and move files and directories

09\. Create hard and soft links

::: {style="page-break-before: always;"}
:::

\

Linux supports different file types that are identified based on the
kind of data they store. There are files that save information in plain
text or binary format. This file type is very common. There are other
files that store device information or simply point to the same data on
the disk. A good comprehension of Linux file types is important for both
Linux users, developers, and administrators.

\

Compressing and archiving one or more large files or an entire directory
hierarchy allows users to conserve disk space or remote copy them at a
faster pace. The resulting compressed archive can be easily uncompressed
and unarchived whenever and wherever needed. RHEL offers native tools to
support both user needs.

\

Normal and application users and database and system administrators all
need to edit text files on a regular basis as part of their job. Linux
delivers several text editors for this purpose, including the vim
editor, which is popular within the Linux community. A sound, working
knowledge of this tool is essential for all these roles.

\

::: {style="text-align: center;"}
![](image-8FMHO049.jpg){height="100%"}
:::

There are a number of common operations that can be performed on files
and directories in addition to viewing their contents. These operations
include creating, listing, copying, moving, renaming, and removing both
files and directories. Normal users will require higher privilege in
order to perform these operations outside of their realm.

\

There is a tool available in the operating system that helps in linking
files and directories for various use cases. An understanding of when to
link files or directories versus when to copy them is important.

::: {style="page-break-before: always;"}
:::

[]{#chapter0097.html}

## Common File Types {.style3}

\

RHEL supports seven types of files: regular, directory, block special
device, character special device, symbolic link, named pipe, and socket.
The first two are the most common. The two types of device files are
used by the operating system to communicate with peripheral devices.
There are many instances of symbolic links as well. The last two
types---named pipes and sockets---are used in inter-process
communication.

\

Linux does not require an extension to a file to identify its type. It
provides two elementary commands called file and stat, in addition to
the ls command, to ascertain the type of data that a file may contain.
This chapter discusses the first five file types and skips the last two
(named pipes and sockets), as they are beyond the scope of this book.

::: {style="page-break-before: always;"}
:::

[]{#chapter0098.html}

## Regular Files {.style3}

\

Regular files may contain text or binary data. These files may be shell
scripts or commands in the binary form. When you list a directory, all
line entries for files in the output that begin with the hyphen
character (-) represent regular files. The following truncated output is
of the /root directory:

\

<div>

![](image-THICZHLY.jpg){height="100%"}

</div>

Notice the hyphen in field 1 of column 1 before rw. This character
indicates that the listed file is a regular file. Now, let's run the
file and stat commands on this file and see what they report:

\

<div>

![](image-MZ5FQW79.jpg){height="100%"}

</div>

The two commands report the file type differently. The first command
returns the specific type of data that the file contains (ASCII text),
and the latter simply states that it is a regular file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0099.html}

## Directory Files {.style3}

\

Directories are logical containers that hold files and subdirectories.
The following ls command output shows a few directories from /usr/bin:

\

<div>

![](image-8XHJ7XCB.jpg){height="100%"}

</div>

The letter "d" at the beginning of each line entry identifies the file
as a directory. Try running the file and stat commands on /usr and see
what they report.

::: {style="page-break-before: always;"}
:::

[]{#chapter0100.html}

## Block and Character Special Device Files {.style3}

\

Each piece of hardware in the system has an associated file in the /dev
directory that is used by the system to communicate with that device.
This type of file is called a device file. There are two types of device
files: character (or raw) and block. In the example below, the ls
command in field 1 of column 1 distinguishes between the two with a "c"
for character and a "b" for block:

\

<div>

![](image-4PM49963.jpg){height="100%"}

</div>

Use the file and stat commands on /dev/console and /dev/sda files for
additional verification.

\

Every hardware device such as a disk, CD/DVD, printer, and terminal has
an associated device driver loaded in the kernel. The kernel
communicates with hardware devices through their respective device
drivers. Each device driver is assigned a unique number called the major
number, which the kernel uses to recognize its type.

\

Furthermore, there may be more than one instance of the same device type
in the system. In that case, the same driver is used to control all
those instances. For example, SATA device driver controls all SATA hard
disks and CD/DVD drives. The kernel in this situation allots a minor
number to each individual device within that device driver category to
identify it as a unique device. This scheme applies to disk partitions
as well. In short, a major number points to the device driver, and a
minor number points to a unique device or partition that the device
driver controls.

\

In the above long listing, columns 5 and 6 depict the major and minor
number association for each device instance. Major number 8 represents
the block device driver for SATA disks. Similarly (not shown in the
above output), major number 253 denotes the driver for device mapper
(VDO volumes, LVM logical volumes, etc.), and 11 signifies optical
devices. VDO and LVM volumes are discussed in Chapter 13 "Storage
Management".

::: {style="page-break-before: always;"}
:::

[]{#chapter0101.html}

## Symbolic Links {.style3}

\

A symbolic link (a.k.a. a soft link or a symlink) may be considered a
shortcut to another file or directory. If you issue ls -l on a
symbolically linked file or directory, the line entry will begin with
the letter "l", and an arrow will be pointing to the target link. For
example:

\

<div>

![](image-5OQYCSMU.jpg){height="100%"}

</div>

Run the file and stat commands on /usr/sbin/vigr for additional
confirmation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0102.html}

## Compression and Archiving {.style3}

\

Compression tools are used to compress one or more files to conserve
space. They may be used with archive commands, such as tar or star, to
create a single compressed archive of hundreds of files and directories.
A compressed archive can then be copied to a remote system faster than a
non-compressed archive or stored at a backup location. RHEL offers a
multitude of compression tools such as gzip (gunzip) and bzip2
(bunzip2).

\

The tar and star commands have the ability to preserve general file
attributes such as ownership, owning group, and timestamp as well as
extended attributes such as SELinux contexts.

\

SELinux context is set on files and directories to provide an enhanced
level of protection from unauthorized users and processes. Refer to
Chapter 20 "Security Enhanced Linux" for details around SELinux.

\

The syntax and usage of tar and star commands are similar, and most of
the common options are identical. We discuss only the tar command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0103.html}

## Using gzip and gunzip {.style3}

\

The gzip/gunzip compression utility pair has been available in Linux for
over two decades. The gzip command is used to create a compressed file
of each of the specified files and it adds the .gz extension to each
file for identification. This tool can be used with the -r option to
compress an entire directory tree, and with the -l option to display
compression information about a gzipped file. The -l option also
instructs the command to display the filename that will be given to the
file when it is uncompressed.

\

To compress the file fstab located in the /etc directory, copy this file
in the root user's home directory /root using the cp command and confirm
with ls:

\

<div>

![](image-AIU4IYX1.jpg){height="100%"}

</div>

Now use the gzip command to compress this file and ls to confirm:

\

<div>

![](image-6TGQPI7P.jpg){height="100%"}

</div>

Notice that the original file is compressed, and it now has the .gz
extension added to it. If you wish to view compression information for
the file, run the gzip command again with the -l option:

\

<div>

![](image-5FUKWTU1.jpg){height="100%"}

</div>

To decompress this file, use the gunzip command:

\

<div>

![](image-B4HIG7RG.jpg){height="100%"}

</div>

Check the file after the decompression with the ls command. It will be
the same file with the same size, timestamp, and other attributes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0104.html}

## Using bzip2 and bunzip2 {.style3}

\

The bzip2/bunzip2 is another compression pair that has been available in
Linux for a long time. The bzip2 command creates a compressed file of
each of the specified files and it adds the .bz2 extension to each file
for identification.

\

Let's compress the fstab file again, but this time with bzip2 and
confirm with ls:

\

<div>

![](image-J0QK1M5F.jpg){height="100%"}

</div>

Notice that the original file is compressed, and it now has the .bz2
extension. To decompress this file, use the bunzip2 command:

\

<div>

![](image-VI9VT4E9.jpg){height="100%"}

</div>

Check the file after the decompression with the ls command. It will be
the same file with the same size, timestamp, and other attributes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0105.html}

## Differences between gzip and bzip2 {.style3}

\

The function of both gzip and bzip2 is the same: to compress and
decompress files. However, in terms of the compression and decompression
rate, bzip2 has a better compression ratio (smaller target file size),
but it is slower. These differences are evident on fairly large files.
On small files, you can use either of the two. Both commands support
several identical options.

::: {style="page-break-before: always;"}
:::

[]{#chapter0106.html}

## Using tar {.style3}

\

The tar (tape archive) command is used to create, append, update, list,
and extract files or an entire directory tree to and from a single file,
which is called a tarball or tarfile. This command can be instructed to
also compress the tarball after it has been created.

\

tar supports a multitude of options such as those described in Table
3-1.

\

  ----------------------------------- -----------------------------------
  Option                              Definition

  -c                                  Creates a tarball.

  -f                                  Specifies a tarball name.

  -p                                  Preserve file permissions. Default
                                      for the root user. Specify this
                                      option if you create an archive as
                                      a normal user.

  -r                                  Appends files to the end of an
                                      extant uncompressed tarball.

  -t                                  Lists contents of a tarball.

  -u                                  Appends files to the end of an
                                      extant uncompressed tarball
                                      provided the specified files being
                                      added are newer.

  -v                                  Verbose mode.

  -x                                  Extracts or restores from a
                                      tarball.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-1 tar Command Options

\

The -r and -u options do not support adding files to an existing
compressed tarball.

\

A few examples are provided below to elucidate the use of tar. Pay
special attention to the syntax and options used in each command and
observe the output.

\

To create a tarball called /tmp/home.tar of the entire /home directory,
use the -v option for verbosity and the -f option to specify the name of
the archive file with the command. The following is a truncated output
of the command:

\

<div>

![](image-SUE044AM.jpg){height="100%"}

</div>

The resulting tarball will not include the leading forward slash (/) in
the file paths as indicated on line 1 of the output even though the full
path of /home is supplied. This is the default behavior of the tar
command, which gives you the flexibility to restore the files at any
location of your choice without having to worry about the full
pathnames. Use the -P option at the creation time to override this
behavior.

\

To create a tarball called /tmp/files.tar containing only a select few
files (two files in this example) from the /etc directory:

\

<div>

![](image-VMLD26KX.jpg){height="100%"}

</div>

To append files located in the /etc/yum.repos.d directory to the
existing tarball /tmp/files.tar:

\

<div>

![](image-CX1NZ1NN.jpg){height="100%"}

</div>

To list what files are included in the files.tar tarball:

\

<div>

![](image-X4F6HAVE.jpg){height="100%"}

</div>

To restore a single file, etc/yum.conf, from /tmp/files.tar under /root
and confirm the output with ls:

\

<div>

![](image-KEHMD5TJ.jpg){height="100%"}

</div>

To restore all files from /tmp/files.tar under /root and confirm the
output with ls:

\

<div>

![](image-GI6Q97O0.jpg){height="100%"}

</div>

tar also supports options to directly compress the target file while
being archived using the gzip or bzip2 command. These options are
described in Table 3-2.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -j                                  Compresses a tarball with bzip2

  -z                                  Compresses a tarball with gzip
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-2 tar with Compression Options

\

You will use the options in Table 3-2 to create compressed archives in
Exercise 3-1.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Archiving and compression are tasks usually done together to
produce smaller archive files.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0107.html}

## Exercise 3-1: Create Compressed Archives {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create a tarball called home.tar.gz of the
/home directory under /tmp and compress it with gzip. You will create
another tarball called home.tar.bz2 of the /home directory under /tmp
and compress it with bzip2. You will list the content of home.tar.gz
without uncompressing it and then extract all the files in the current
directory. Finally, you will extract the bzip2-compressed archive in the
/tmp directory.

\

1\. Create (-c) a gzip-compressed (-z) tarball under /tmp (-f) for
/home:

\

<div>

![](image-N71YHO6R.jpg){height="100%"}

</div>

2\. Create (-c) a bzip2-compressed (-j) tarball under /tmp (-f) for
/home:

\

<div>

![](image-2B5JU6VF.jpg){height="100%"}

</div>

3\. List (-t) the content of the gzip-compressed archive (-f) without
uncompressing it:

\

<div>

![](image-QJHCZUCC.jpg){height="100%"}

</div>

4\. Extract (-x) files from the gzip-compressed tarball (-f) in the
current directory:

\

<div>

![](image-KGN0U946.jpg){height="100%"}

</div>

5\. Extract (-x) files from the bzip2-compressed (-f) tarball under /tmp
(a different directory location than the current directory) (-C):

\

<div>

![](image-06CIKGK6.jpg){height="100%"}

</div>

Run ls /tmp to view the list of extracted files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0108.html}

## File Editing {.style3}

\

The vim editor is an interactive, full-screen visual text-editing tool
that allows you to create and modify text files. This tool is available
as a standard editor in all vendor UNIX versions and Linux
distributions. It does not require the graphical capability and it is
not heavy on compute resources. All text editing within vim takes place
in a buffer (a small chunk of memory used to hold file updates). Changes
can either be written to the disk or discarded.

\

It is essential for you as a system administrator to master the vim
editor skills. The best way to learn vim is to practice by opening or
creating a file and run the vim commands. See the manual pages of vim
for details. Alternatively, you can run the vimtutor command to view the
tutorial.

::: {style="page-break-before: always;"}
:::

[]{#chapter0109.html}

## Modes of Operation {.style3}

\

The vim editor has three modes of operation: the command mode, the input
mode, and the last line mode. The fourth mode is referred to as the
visual mode, but it is not discussed in the book.

\

The command mode is the default mode of vim. The vim editor places you
into this mode when you start it. While in the command mode, you can
carry out tasks such as copy, cut, paste, move, remove, replace, change,
and search on text, in addition to performing navigational operations.
This mode is also known as the escape mode because the Esc key is used
to enter the mode.

\

In the input mode, anything that is typed on the keyboard is entered
into the file as text. Commands cannot be run in this mode. The input
mode is also called the edit mode or the insert mode. You need to press
the Esc key to return to the command mode.

\

While in the command mode, you may carry out advanced editing tasks on
text by pressing the colon character (:), which places the cursor at the
beginning of the last line of the screen, and hence it is referred to as
the last line or extended mode. This mode is considered a special type
of command mode.

::: {style="page-break-before: always;"}
:::

[]{#chapter0110.html}

## Starting vim {.style3}

\

The vim editor may be started by typing the command vim at the command
prompt, and it may follow an existing or a new filename as an argument.
Without a specified filename, it simply opens an empty screen where you
can enter text. You can save the text in a file or discard using
commands provided in subsequent subsections.

\

<div>

![](image-82ERBIU1.jpg){height="100%"}

</div>

Alternatively, you can supply a filename as an argument. This way, vim
will open the specified file for editing if the file exists, or it will
create a file by that name if it does not exist.

\

\[root@server1 \~\]# vim \<filename\>

\

There are options available that you may specify at the time of starting
this editing tool. Refer to the manual pages for more information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0111.html}

## Inserting text {.style3}

\

Once vim is started, there are six commands that can switch into the
edit mode. These commands are simple lower and uppercase i, a, and o,
and are described in Table 3-3.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  i                                   Inserts text before the current
                                      cursor position

  I                                   Inserts text at the beginning of
                                      the current line

  a                                   Appends text after the current
                                      cursor position

  A                                   Appends text to the end of the
                                      current line

  o                                   Opens a new line below the current
                                      line

  O                                   Opens a new line above the current
                                      line
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-3 vim Editor \| Inserting Text

\

Press the Esc key when you've finished entering text in the edit mode to
return to the command mode.

::: {style="page-break-before: always;"}
:::

[]{#chapter0112.html}

## Navigating within vim {.style3}

\

Navigation keys are helpful in editing small and large files. They allow
you to make rapid moves in the file. There are multiple key sequences
available within vim to control the cursor movement. Some of the
elementary keystrokes are elaborated in Table 3-4.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  h                                   Moves backward one character

  j                                   Moves downward one line

  k                                   Moves upward one line

  l                                   Moves forward one character

  w                                   Moves to the start of the next word

  b                                   Moves backward to the start of the
                                      preceding word

  e                                   Moves to the ending character of
                                      the next word

  \$                                  Moves to the end of the current
                                      line

  Enter                               Moves to the beginning of the next
                                      line

  Ctrl+f                              Scrolls down to the next page

  Ctrl+b                              Scrolls up to the previous page
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-4 vim Editor \| Navigating

\

You can precede any of the commands listed in Table 3-4 by a numeral to
repeat the command action that many times. For instance, 3h would move
the cursor three places to the left, 5Enter would move the cursor five
lines below, and 2Ctrl+f would move the cursor two screens down.

\

In addition, you can use 0 (zero) to move to the beginning of the
current line, \[\[ to move to the first line of the file, and \]\] to
move to the last line of the file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0113.html}

## Revealing Line Numbering {.style3}

\

While working with large files in the vim editor, you deal with hundreds
or even thousands of lines. You may need to delete, copy, paste, or move
one or more lines within the file. To perform these operations with
accuracy, vim offers a way to enable line numbering within the editor.
Table 3-5 describes the command.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  :set nu                             Shows line numbering

  :set nonu                           Hides line numbering
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-5 vim Editor \| Revealing Line Numbering

\

Line numbers are not recorded when you save the file. They are for a
reference purpose only.

::: {style="page-break-before: always;"}
:::

[]{#chapter0114.html}

## Deleting Text {.style3}

\

vim provides several commands to carry out delete operations. Some of
the commands are described in Table 3-6.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  x                                   Deletes the character at the cursor
                                      position

  X                                   Deletes the character before the
                                      cursor location

  dw                                  Deletes the word or part of the
                                      word to the right of the cursor
                                      location

  dd                                  Deletes the current line

  D                                   Deletes at the cursor position to
                                      the end of the current line

  :6,12d                              Deletes lines 6 through 12
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-6 vim Editor \| Deleting Text

\

You can precede any of the commands listed in Table 3-6, except for the
last line mode command, by a numeral to repeat the command action that
many times. For instance, 2X would delete two characters before the
cursor position, and 3dd would delete the current line and the two lines
below it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0115.html}

## Undoing and Repeating {.style3}

\

[Table 3-7 explicates the commands that undo the last change made and
repeat the last command run.](#chapter0115.html)

\

  ----------------------------------- -----------------------------------
  Command                             Action

  u                                   Undoes the previous command

  U                                   Undoes all the changes done on the
                                      current line

  :u                                  Undoes the previous last line mode
                                      command

  . (dot)                             Repeats the last command run
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-7 vim Editor \| Undoing and Repeating

\

You can precede any of the commands listed in Table 3-7, except for the
U and :u commands, by a numeral to repeat the command action that many
times. For instance, 2u would undo the previous two changes, and 2U
would undo all the changes done on the current and the previous lines.

::: {style="page-break-before: always;"}
:::

[]{#chapter0116.html}

## Searching for Text {.style3}

\

You can perform forward and reverse searches while in the command mode
by using the / and ? characters followed by the string to be searched.
For instance, in a file with numerous occurrences of the string
"profile," you can run /profile or ?profile for a forward or reverse
search.

\

[Table 3-8 summarizes these actions.](#chapter0116.html)

\

  ----------------------------------- -----------------------------------
  Command                             Action

  /string                             Searches forward for a string

  ?string                             Searches backward for a string

  n                                   Finds the next occurrence of a
                                      string

  N                                   Finds the previous occurrence of a
                                      string
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-8 vim Editor \| Searching for Text

\

For forward searches, repeating "n" takes the cursor to the previous
occurrences of the searched string, and repeating "N" moves the cursor
to the next occurrences.

\

The behavior is reversed for backward searches. Repeating "n" takes the
cursor to the next occurrences of the searched string, and repeating "N"
moves the cursor to the previous occurrences.

::: {style="page-break-before: always;"}
:::

[]{#chapter0117.html}

## Replacing Text {.style3}

\

[Table 3-9 describes two last line mode commands that are used to
perform a search and replace operation.](#chapter0117.html)

\

  ----------------------------------- -----------------------------------
  Command                             Action

  :%s/old/new                         Replaces the first occurrence of
                                      old with new in a file. For
                                      example, to replace the first
                                      occurrence of profile with Profile,
                                      use :%s/profile/Profile.

  :%s/old/new/g                       Replaces all occurrences of old
                                      with new in a file. For example, to
                                      replace all the occurrences of
                                      profile with Profile in a file, use
                                      :%s/profile/Profile/g.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-9 vim Editor \| Replacing Text

\

If you have used either of these and would like to undo it, use the last
line mode command :u.

::: {style="page-break-before: always;"}
:::

[]{#chapter0118.html}

## Copying, Moving, and Pasting Text {.style3}

\

vim allows you to copy some text and paste it to the desired location
within the file. You can copy (yank) a single character, a single word,
or an entire line, and then paste it wherever you need it. The copy
function can be performed on multiple characters, words, or lines
simultaneously. Table 3-10 describes the copy, move, and paste commands.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  yl                                  Yanks the current letter into
                                      buffer

  yw                                  Yanks the current word into buffer

  yy                                  Yanks the current line into buffer

  p                                   Pastes yanked data below the
                                      current line

  P                                   Pastes yanked data above the
                                      current line

  :1,3co6                             Copies lines 1 through 3 and pastes
                                      them after line 6

  :4,6m9                              Moves lines 4 through 6 after line
                                      9
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-10 vim Editor \| Copying, Moving, and Pasting Text

\

You can precede any of the commands listed in Table 3-10, except for the
last line mode commands, by a numeral to repeat the command action that
many times. For instance, 2yw would yank two words, 2yy would yank two
lines, and 2p would paste two times.

::: {style="page-break-before: always;"}
:::

[]{#chapter0119.html}

## Changing Text {.style3}

\

There are numerous commands available within vim to change and modify
text as summarized in Table 3-11. Most of these commands switch into the
edit mode, so you will have to press the Esc key to return to the
command mode.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  cl                                  Changes the letter at the cursor
                                      location

  cw                                  Changes the word (or part of the
                                      word) at the cursor location to the
                                      end of the word

  cc                                  Changes the entire line

  C                                   Changes text at the cursor position
                                      to the end of the line

  r                                   Replaces the character at the
                                      cursor location with the character
                                      entered following this command

  R                                   Overwrites or replaces the text on
                                      the current line

  J                                   Joins the next line with the
                                      current line

  xp                                  Switches the position of the
                                      character at the cursor position
                                      with the character to the right of
                                      it

  \~                                  Changes the letter case (uppercase
                                      to lowercase, and vice versa) at
                                      the cursor location
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-11 vim Editor \| Changing Text

\

You can precede any of the commands listed in Table 3-11 by a numeral to
repeat the command action that many times. For instance, 2cc would
change the entire current and the next line, and 2r would replace the
current character and the next character.

::: {style="page-break-before: always;"}
:::

[]{#chapter0120.html}

## Saving and Quitting vim {.style3}

\

When you are done with modifications, you can save or discard them. Use
one of the commands listed in Table 3-12 as required.

\

  ----------------------------------- -----------------------------------
  Command                             Action

  :w                                  Writes changes into the file
                                      without quitting vim

  :w file2                            Writes changes into a new file
                                      called file2 without quitting vim

  :w!                                 Writes changes to the file even if
                                      the file owner does not have write
                                      permission on the file

  :wq                                 Writes changes to the file and
                                      quits vim

  :wq!                                Writes changes to the file and
                                      quits vim even if the file owner
                                      does not have write permission on
                                      the file

  :q                                  Quits vim if no modifications were
                                      made

  :q!                                 Quits vim if modifications were
                                      made, but we do not wish to save
                                      them
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-12 vim Editor \| Saving and Quitting

\

The exclamation mark (!) can be used to override the write protection
placed on the file for the owner.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You may be required to edit configuration files or write
scripts. Working knowledge of the vim editor is crucial.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0121.html}

## File and Directory Operations {.style3}

\

This section elaborates on various management operations that can be
performed on files and directories. These operations include creating,
displaying contents, copying, moving, renaming, and deleting files and
directories. These common operations can be performed by normal users
who own or have appropriate permissions. The root user can accomplish
these tasks on any file or directory on the system, regardless of who
owns it. In case there's a lack of user permissions, an error message is
generated.

::: {style="page-break-before: always;"}
:::

[]{#chapter0122.html}

## Creating Files and Directories {.style3}

\

Files can be created in multiple ways using different commands; however,
there is only one command to create directories.

\

### Creating Empty Files Using touch {.style3}

The touch command creates an empty file. If the file already exists, it
simply updates the timestamp on it to match the current system date and
time. Execute the following as root in the root user's home directory to
create file1 and then run ls to verify:

\

<div>

![](image-O78BDF0T.jpg){height="100%"}

</div>

As expected, column 5 (the size column) in the output is 0, meaning that
file1 is created with zero bytes in size. If you rerun the touch command
on this file after a minute or so, a new timestamp is placed on it:

\

<div>

![](image-CIOVUAMS.jpg){height="100%"}

</div>

The touch command has a few interesting options. The -d and -t options
set a specific date and time on a file; the -a and -m options enable you
to change only the access or the modification time on a file to the
current system time; and the -r option sets the modification time on a
file to that of a reference file's. Let's use a couple of these options
in the examples below:

\

To set the date on file1 to January 31, 2023:

\

<div>

![](image-DQRG2FE4.jpg){height="100%"}

</div>

To change the modification time on file1 to the current system time:

\

<div>

![](image-84UO6LD7.jpg){height="100%"}

</div>

Try the rest of the options for practice.

\

### Creating Short Files Using cat {.style3}

The cat command allows you to create short text files. The ending angle
bracket "\>" must be used to redirect the output to the specified file
(catfile1 in this example):

\

<div>

![](image-RMUFFKPP.jpg){height="100%"}

</div>

Nothing is displayed when you execute the above, as the system is
waiting for you to input something. Type some text. Press the Enter key
to open a new line and continue typing. When you are done, press Ctrl+d
to save the text in catfile1 and return to the command prompt. You can
verify the file creation with the ls command.

\

### Creating Files Using vim {.style3}

You can use the vim editor to create and modify text files of any size.
Refer to the previous section in this chapter on how to use vim.

\

### Making Directories Using mkdir {.style3}

The mkdir command is used to create directories. This command shows an
output if you run it with the -v option. The following example
demonstrates the creation of a directory called dir1 in the root user's
home directory:

\

<div>

![](image-05TTIW83.jpg){height="100%"}

</div>

You can create a hierarchy of subdirectories by specifying the -p
(parent) option with mkdir. In the following example, mkdir is used to
create the hierarchy dir2/perl/perl5:

\

<div>

![](image-OKFHWA19.jpg){height="100%"}

</div>

Notice the placement of options in the two examples. Many commands in
Linux accept either format.

::: {style="page-break-before: always;"}
:::

[]{#chapter0123.html}

## Displaying File Contents {.style3}

\

RHEL offers a variety of tools for showing file contents. Directory
contents are simply the files and subdirectories that it contains. Use
the ls command as explained earlier to view directory contents.

\

For viewing files, you can use the cat, more, less, head, and tail
commands. These tools are explained below.

\

### Using cat {.style3}

cat displays the contents of a text file. It is typically used to view
short files. It shows the entire file on the screen. The following
example shows the .bash_profile file in the root user's home directory
with the cat command:

\

<div>

![](image-EXQ3VH47.jpg){height="100%"}

</div>

You can add the -n option to the cat command to view the output in
numbered format.

\

### Using less and more {.style3}

Both less and more are text filters that are used for viewing long text
files one page at a time, starting at the beginning. The less command is
more capable than the more command. less does not need to read the
entire file before it starts to display its contents, thus making it
faster. The more command is limited to forward text searching only,
whereas less is able to perform both forward and backward searches. Run
the less and more commands one at a time and observe the visual
difference in the outputs:

\

<div>

![](image-TQORVOPT.jpg){height="100%"}

</div>

You can navigate with the keys described in Table 3-13 while viewing the
files with either tool.

\

  ----------------------------------- -----------------------------------
  Key                                 Purpose

  Spacebar / f                        Scrolls forward one screen

  Enter                               Scrolls forward one line

  b                                   Scrolls backward one screen

  d                                   Scrolls forward half a screen

  h                                   Displays help

  q                                   Quits and returns to the command
                                      prompt

  /string                             Searches forward for a string

  ?string                             Searches backward for a string;
                                      only applies to the less command

  n                                   Finds the next occurrence of a
                                      string

  N                                   Finds the previous occurrence of a
                                      string; only applies to the less
                                      command
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-13 Navigating with less and more

\

If the /usr/bin/znew file is unavailable, use /etc/profile instead.

\

### Using head and tail {.style3}

head displays the starting few lines of the specified text file. By
default, it returns the first ten lines. See the example below:

\

<div>

![](image-EU3N9K6J.jpg){height="100%"}

</div>

The above output includes three empty lines as well. You can pass a
numeral to the command as an argument to limit the number of lines in
the output. For example, run the following to view only the top three
lines from /etc/profile:

\

<div>

![](image-ELEC9F1W.jpg){height="100%"}

</div>

On the other hand, the tail command displays the ending ten lines from
the specified file by default unless a numeral is passed as an argument
to alter the behavior. Issue the following two commands on your terminal
to witness the difference:

\

<div>

![](image-SE6FLHZI.jpg){height="100%"}

</div>

The tail command is particularly useful when watching a log file while
it is being updated. The -f (follow) option enables this function. The
following example enables us to view the updates to the system log file
/var/log/messages in real time:

\

<div>

![](image-KFPLVXHY.jpg){height="100%"}

</div>

You may have to wait for some time before you see an update. Press
Ctrl+c to quit when you are done.

::: {style="page-break-before: always;"}
:::

[]{#chapter0124.html}

## Counting Words, Lines, and Characters in Text Files {.style3}

\

The wc (word count) command displays the number of lines, words, and
characters (or bytes) contained in a text file or input supplied. For
example, when you run this command on the /etc/profile file, you will
see output similar to the following:

\

<div>

![](image-3RW9955G.jpg){height="100%"}

</div>

Column 1 in the output discloses the number of lines (78) in the file
followed by the number of words (247), the number of characters (or
bytes) (1899), and the filename (/etc/profile).

\

You can use the options listed in Table 3-14 to restrict the output as
desired.

\

  ----------------------------------- -----------------------------------
  Option                              Action

  -l                                  Prints a count of lines

  -w                                  Prints a count of words

  -c                                  Prints a count of bytes

  -m                                  Prints a count of characters
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-14 wc Command Options

\

The following example displays only the count of characters in
/etc/profile:

\

<div>

![](image-NFVHNCR4.jpg){height="100%"}

</div>

Try running wc with the other options and observe the outcomes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0125.html}

## Copying Files and Directories {.style3}

\

The copy operation duplicates a file or directory. RHEL provides the cp
command for this purpose, and it has a variety of options.

\

### Copying Files {.style3}

The cp command copies one or more files within a directory or to another
directory. To duplicate a file in the same directory, you must give a
different name to the target file. However, if the copy is being made to
a different directory, you can use either the same filename or assign a
different one. Consider the following examples:

\

To copy file1 as newfile1 within the same directory:

\

<div>

![](image-CVJ5NU3B.jpg){height="100%"}

</div>

To copy file1 by the same name to another existing directory dir1:

\

<div>

![](image-X0QITJ8I.jpg){height="100%"}

</div>

By default, the copy operation overwrites the destination file if it
exists without presenting a warning. To alter this behavior, use the -i
(interactive) option to instruct cp to prompt for confirmation before
overwriting:

\

<div>

![](image-YJD07GBI.jpg){height="100%"}

</div>

Press Enter after keying in a "y" for yes or an "n" for no to proceed.

\

By default, you do not need to specify the -i option for yes/no
confirmation if you attempt to copy a file to overwrite the destination
file as root. The predefined alias---"alias cp='cp -i'"---in the .bashrc
file in the root user's home directory takes care of that.

\

### Copying Directories {.style3}

The cp command with the -r (recursive) option copies an entire directory
tree to another location. In the following example, dir1 is copied to
dir2 and then the directory contents of dir2 are listed for validation:

\

<div>

![](image-C1NALXYV.jpg){height="100%"}

</div>

You may use the -i option for overwrite confirmation if the destination
already has a matching file or directory.

\

Try running ls -l dir2 -R to view the entire dir2 hierarchy.

\

The cp command can also use -p, which can provide the ability to
preserve the attributes (timestamp, permissions, ownership, etc.) of a
file or directory being copied. Try running cp -p file1 /tmp and then
use ls -l to compare the attributes for both files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0126.html}

## Moving and Renaming Files and Directories {.style3}

\

A file or directory can be moved within the same file system or to
another. Within the file system move, an entry is added to the target
directory and the source entry is removed, which leaves the actual data
intact. On the other hand, a move to a different file system physically
moves the file or directory content to the new location and deletes the
source.

\

A rename simply changes the name of a file or directory; data is not
touched.

\

### Moving and Renaming Files {.style3}

The mv command is used to move or rename files. The -i option can be
specified for user confirmation if a file by that name already exists.
The following example moves file1 to dir1 and prompts for confirmation:

\

<div>

![](image-XKQ27QUD.jpg){height="100%"}

</div>

By default, you do not need to specify the -i option for yes/no
confirmation if you attempt to move a file to overwrite the destination
file as root. The predefined alias---"alias mv='mv -i'"---in the .bashrc
file in the root user's home directory takes care of that.

\

To rename newfile1 as newfile2:

\

<div>

![](image-K7ZF5ENF.jpg){height="100%"}

</div>

Verify the above operations with ls -l.

\

### Moving and Renaming Directories {.style3}

Use the mv command to move a directory and its contents to somewhere
else or to change the name of the directory. For example, you can move
dir1 into dir2 (dir2 must exist, otherwise it will be a simple rename
operation):

\

<div>

![](image-AIC4GCS3.jpg){height="100%"}

</div>

To rename dir2 as dir20:

\

<div>

![](image-FDORIWVP.jpg){height="100%"}

</div>

Verify the above operations with ls -l.

::: {style="page-break-before: always;"}
:::

[]{#chapter0127.html}

## Removing Files and Directories {.style3}

\

The remove operation deletes a file entry from the directory structure
and marks its data space as free. For a directory, the remove operation
weeds corresponding entries out from the file system structure.

\

### Removing Files {.style3}

You can remove a file using the rm command, which deletes one or more
specified files. For example, issue the following command to erase
newfile2:

\

<div>

![](image-I62ESX2X.jpg){height="100%"}

</div>

By default, you do not need to specify the -i option for yes/no
confirmation if you attempt to remove a file as root. The predefined
alias---"alias rm='rm -i'"---in the .bashrc file in the root user's home
directory takes care of that.

\

The rm command can also be used to erase a file that has a wildcard
character, such as an asterisk (\*) or a question mark (?), embedded in
its name. These characters have special meaning to the shell, and
filenames containing them must be prepended with the backslash character
(\\) to instruct the shell to treat them as regular characters.

\

A careful use of the rm command is particularly important when you have
administrative rights on the system.

\

For example, if a file exists by the name \* under the /tmp directory
(use touch /tmp/\\\* to create it), you can remove it by executing rm
/tmp/\\\*. If you mistakenly run rm /tmp/\* instead, all files under
/tmp will be deleted.

\

Wildcard characters are used in filename globbing and in commands where
an action needs to occur on multiple files matching certain criteria.
They are discussed in Chapter 07 "The Bash Shell".

\

### Removing Directories {.style3}

The rmdir and rm commands erase directories. The rmdir command is used
to delete empty directories, while rm requires the -d option to
accomplish the same. In addition, the -r or -R (recursive) flag with rm
will remove a directory and all of its contents. Both commands support
the -v switch for reporting what they are doing. Let's look at a few
examples.

\

To erase an empty directory called emptydir (assuming emptydir exists),
use either of the following:

\

<div>

![](image-63ALKUMM.jpg){height="100%"}

</div>

To remove dir20 and all its contents recursively, use either -r or -R
with the command:

\

<div>

![](image-3KZV2R4T.jpg){height="100%"}

</div>

The rm command supports the -i flag for interactive deletions.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Manipulating files and directories is one of the most common
tasks performed in any operating system. Working knowledge of the tools
learned in this section is crucial.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The same rules that apply on filenames with wildcard characters in their
names, apply on directory names as well. See the previous topic for
details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0128.html}

## File Linking {.style3}

\

Each file within a file system has a multitude of attributes assigned to
it at the time of its creation. These attributes are collectively
referred to as the file's metadata, and they change when the file is
accessed or modified. A file's metadata includes several pieces of
information, such as the file type, size, permissions, owner's name,
owning group name, last access/modification times, link count, number of
allocated blocks, and pointers to the data storage location. This
metadata takes 128 bytes of space for each file. This tiny storage space
is referred to as the file's inode (index node).

\

An inode is assigned a unique numeric identifier that is used by the
kernel for accessing, tracking, and managing the file. In order to
access the inode and the data it points to, a filename is assigned to
recognize it and access it. This mapping between an inode and a filename
is referred to as a link. It is important to note that the inode does
not store the filename in its metadata; the filename and corresponding
inode number mapping is maintained in the directory's metadata where the
file resides.

\

Linking files or directories creates additional instances of them, but
all of them eventually point to the same physical data location in the
directory tree. Linked files may or may not have identical inode numbers
and metadata depending on how they are linked.

\

There are two ways to create file and directory links in RHEL, and they
are referred to as hard links and soft links. Links are created between
files or between directories, but not between a file and a directory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0129.html}

## Hard Link {.style3}

\

A hard link is a mapping between one or more filenames and an inode
number, making all hard-linked files indistinguishable from one another.
This implies that all hard-linked files will have identical metadata.
Changes to the file metadata and content can be made by accessing any of
the filenames.

\

[Figure 3-1 shows two filenames---file10 and file20---both sharing the
same inode number 10176147. Here, each filename is essentially a hard
link pointing to the same inode.](#chapter0129.html)

\

::: {style="text-align: center;"}
![](image-C0T2UN4H.jpg){height="100%"}
:::

Figure 3-1 Hard Link

\

A hard link cannot cross a file system boundary, and it cannot be used
to link directories because of the restrictions placed within Linux
designed to avoid potential issues with some commands.

\

The following example creates an empty file called file10 and then uses
the ln command to create a hard link called file20 in the same
directory:

\

<div>

![](image-EK765B6W.jpg){height="100%"}

</div>

After creating the link, run ls with the -li flags as follows:

\

<div>

![](image-JT0N82H0.jpg){height="100%"}

</div>

Look at columns 1 and 3. Column 1 shows the shared inode number
(10176147), and column 3 provides a link count of the hard links that
each file has (file10 points to file20, and vice versa). If you remove
the original file (file10), you will still have access to the data
through file20. Each time you add a hard link to an extant file, the
link count will increase by 1. Similarly, if you delete a hard link, the
link count will go down by 1. When all the hard links (files) are
erased, the link count will set to 0. The increase and decrease in the
number of links is reflected on all hard-linked files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0130.html}

## Soft Link {.style3}

\

A soft link (a.k.a. a symbolic link or a symlink) makes it possible to
associate one file with another. The concept is analogous to that of a
shortcut in Microsoft Windows where the actual file is resident
somewhere in the directory structure, but there can be one or more
shortcuts with different names pointing to it. With a soft link, you can
access the file directly via the actual filename as well as any of the
shortcuts. Each soft link has a unique inode number that stores the
pathname to the file it is linked with. For a symlink, the link count
does not increase or decrease, rather each symlinked file receives a new
inode number. The pathname can be absolute or relative depending on what
was specified at the time of its creation. The size of the soft link is
the number of characters in the pathname to the target.

\

[Figure 3-2 shows the file file10 with a soft link called soft10
pointing to it.](#chapter0130.html)

\

::: {style="text-align: center;"}
![](image-Z1PUZVFR.jpg){height="100%"}
:::

Figure 3-2 Soft Link

\

A soft link can cross a file system boundary and it can be used to link
directories, as it simply uses the pathname of the destination object.

\

To create a soft link for file10 as soft10 in the same directory, use
the ln command with the -s switch:

\

<div>

![](image-OOCFIMA5.jpg){height="100%"}

</div>

After you have created the link, issue ls -l and notice the letter "l"
as the first character in column 2 of the output. Also notice the arrow
that is pointing from the linked file to the original file. Both of
these indicate that soft10 is merely a pointer to file10. The -i option
displays the associated inode numbers in the first column. See the
output of ls -il below:

\

<div>

![](image-D1NQ338T.jpg){height="100%"}

</div>

If you remove the original file (file10 in this case), the link soft10
will stay but points to something that does not exist.

\

RHEL 9 has four soft-linked directories under /. They are:

\

<div>

![](image-1H0Q5MIJ.jpg){height="100%"}

</div>

The syntax for creating soft-linked directories is exactly the same as
that for soft-linked files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0131.html}

## Differences between Copying and Linking {.style3}

\

There are key differences between copying and linking operations. This
subsection will discuss when to use copy and when to opt for a soft or
hard link. Table 3-15 highlights the main differences between the two:

\

  ----------------------------------- -----------------------------------
  Copying                             Linking

  Creates a duplicate of the source   Creates a shortcut that points to
  file. If either file is modified,   the source file. The source can be
  the other file will remain intact.  accessed or modified using either
                                      the source file or the link.

  Each copied file stores its own     All linked files point to the same
  data at a unique location.          data.

  Each copied file has a unique inode Hard Link: All hard-linked files
  number with its unique metadata.    share the same inode number, and
                                      hence the metadata. Symlink: Each
                                      symlinked file has a unique inode
                                      number, but the inode number stores
                                      only the pathname to the source.

  If a copy is moved, erased, or      Hard Link: If the hard link is
  renamed, the source file will have  weeded out, the other file and the
  no impact, and vice versa.          data will remain untouched.
                                      Symlink: If the source is deleted,
                                      the soft link will be broken and
                                      become meaningless. If the soft
                                      link is removed, the source will
                                      have no impact.

  Copy is used when the data needs to Links are used when access to the
  be edited independent of the other. same source is required from
                                      multiple locations.

  Permissions on the source and the   Permissions are managed on the
  copy are managed independent of     source file.
  each other.                         
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 3-15 Copying vs. Linking

\

Keep these differences in mind when you need to decide whether to use
copy or a link.

::: {style="page-break-before: always;"}
:::

[]{#chapter0132.html}

## Exercise 3-2: Create and Manage Hard Links {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create an empty file hard1 under /tmp and
display its attributes (the inode number, permissions, number of links,
owning user, owning group, size, and timestamp). You will create two
hard links hard2 and hard3 for it and list the attributes for all three
files. You will edit hard2 and add some text. You will list the
attributes for all three files again and observe identicalness in all
attributes except for the names of files. You will remove hard1 and
hard3 and list the attributes again for the remaining file. You will
notice a decrease in the link count by 2.

\

1\. Create an empty file /tmp/hard1, and display the long file listing
including the inode number:

\

<div>

![](image-M1Z9VT3J.jpg){height="100%"}

</div>

The file listing indicates the inode number in column 1, followed by
permissions (column 2), number of links (column 3), owning user and
group (columns 4 and 5), size (column 6), timestamp (columns 7, 8, and
9), and filename (column 10).

\

2\. Create two hard links called hard2 and hard3 under /tmp, and display
the long listing:

\

<div>

![](image-9FQWQNDN.jpg){height="100%"}

</div>

Observe the file listing. All attributes are identical.

\

3\. Edit file hard2 and add some random text. Display the long listing
for all three files again:

\

<div>

![](image-N3EG7QQC.jpg){height="100%"}

</div>

Observe the size and timestamp columns for all three files. They are
identical.

\

4\. Erase file hard1 and hard3, and display the long listing for the
remaining file:

\

<div>

![](image-6AZAA0TO.jpg){height="100%"}

</div>

The number of links reduced to 1, all other attributes are the same. You
can still access the same data through this last file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0133.html}

## Exercise 3-3: Create and Manage Soft Links {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create a soft link soft1 under /root pointing
to /tmp/hard2. You will display the attributes (the inode number,
permissions, number of links, owning user, owning group, size, and
timestamp) for both files. You will open soft1 for edit and list the
attributes after editing. You will remove hard2 and then list soft1. You
will notice that soft1 becomes invalid, pointing to something that does
not exist. Remove soft1 to complete the exercise.

\

1\. Create soft link /root/soft1 pointing to /tmp/hard2, and display the
long file listing for both:

\

<div>

![](image-SZ2DMAAY.jpg){height="100%"}

</div>

The file listing indicates the inode number in column 1, followed by
permissions (column 2), number of links (column 3), owning user and
group (columns 4 and 5), size (column 6), timestamp (columns 7, 8, and
9), and filename (column 10). The soft link file has an "l" prefixed to
column 2 and an arrow pointing to the actual file after column 10. Both
are indications of a soft link. Notice the file size (10 bytes for the
full path /tmp/hard2) for soft1. Observe similarities and other
differences.

\

2\. Edit soft1 and display the long listing again:

\

<div>

![](image-C5PFENJ2.jpg){height="100%"}

</div>

The number of bytes for hard1 and the timestamp reflects the editing.
The rest of the attributes are the same.

\

3\. Remove hard2 and display the long listing:

\

<div>

![](image-94K3927V.jpg){height="100%"}

</div>

The actual file, hard2, is gone and the soft link is now invalid. You
can remove it with rm -f /root/soft1.

::: {style="page-break-before: always;"}
:::

[]{#chapter0134.html}

## Chapter Summary {.style3}

\

This chapter started with an introduction of common file types that are
available in RHEL. A file's type is determined by the type of data it
stores. Regular is the most common type of file that stores plain text
or binary information. Directories are also very common and there are
thousands of them on a typical RHEL system. Other file types include
device files and linked files.

\

We looked at creating and manipulating compressed files and compressed
archives. This is a common practice among Linux users for storing old
files and transferring a large amount of data to remote systems.

\

We learned about the vim editor, which is a favorite text file creation
and editing tool. We looked at its various modes of operations and
switching between them. The basics of vim were discussed, including how
to start and insert text, navigate and search for text, copy and paste
text, modify and delete text, save edits, and quit with or without
saving the changes.

\

Next, we described file and directory manipulation tools for operations
such as creating, listing, displaying, copying, moving, renaming, and
removing them. Normal and super users perform these tasks on Linux
systems very often.

\

We examined soft and hard links, and their advantages and limitations.
Based on the knowledge gained, we can identify and create the type of
link we need for a particular use case.

\

Finally, we explored the differences between file copying and file
linking.

::: {style="page-break-before: always;"}
:::

[]{#chapter0135.html}

## Review Questions {.style3}

\

1\. A file compressed with bzip2 can be uncompressed with the gunzip
command. True or False?

2\. The tar command can be used to archive files with their SELinux
contexts. True or False?

3\. Which numeric identifier does the kernel use to determine the
uniqueness of a device within a device driver type?

4\. What are the two indications in the output of ls -l that tells us if
the file is a symlink?

5\. The rmdir command without any switches can be used to erase an
entire directory structure. True or False?

6\. What would the command tar pczf output.file /usr/local do if it is
executed by a normal user?

7\. The ls -l command produces 9 columns in the output by default. True
or False?

8\. Which three Linux utilities can be used to determine a file's type?

9\. There are two hard linked files in a directory. How would you
identify them?

10\. Which vim mode allows to execute advanced copy and move functions?

11\. What would the command wc -c file1 show?

12\. What does the kernel use the major number for?

13\. The tail command can be used to view a file while it is being
updated. True or False?

14\. Soft linked directories cannot cross file system boundaries, but
hard linked directories can. True or False?

15\. A file must have the .exe extension in order to run. True or False?

16\. What would the command touch file1 do on an existing file1 file?

::: {style="page-break-before: always;"}
:::

[]{#chapter0136.html}

## Answers to Review Questions {.style3}

\

1\. False. The file will have to be uncompressed with either bzip2 or
bunzip2.

2\. True. The tar command has the \--selinux switch that provides this
support.

3\. The kernel uses the minor number to identify the uniqueness of a
device within a particular device category.

4\. A symlink file line entry in the ls -l command output begins with
the letter l and has an arrow pointing to the source file.

5\. False. The rmdir command is used to erase empty directories.

6\. This command will create a gzip'ed tar archive called output.file of
the /usr/local directory with file permissions preserved.

7\. True.

8\. The stat, file, and ls commands can be used to determine a file's
type.

9\. You can identify them by running ls -li.

10\. The last line mode (extended mode) allows users to copy or move
lines.

11\. This command will show the number of bytes in file1.

12\. The kernel employs the major number to identify the device type.

13\. True. You need to include the -f switch in the command.

14\. False. Soft linked directories can cross file system boundaries but
hard linked directories cannot.

15\. False.

16\. This command will update the access time on file1.

::: {style="page-break-before: always;"}
:::

[]{#chapter0137.html}

## Do-It-Yourself Challenge Labs {.style3}

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

[]{#chapter0138.html}

## Lab 3-1: Archive, List, and Restore Files {.style3}

\

As root on server3, execute the tar command to create a gzip-compressed
archive of the /etc directory. Run the tar command again to create a
bzip2-compressed archive of the /etc directory. Compare the file sizes
of the two archives. Run the tar command and uncompress and restore both
archives without specifying the compression tool used. (Hint:
Compression and Archiving).

::: {style="page-break-before: always;"}
:::

[]{#chapter0139.html}

## Lab 3-2: Practice the vim Editor {.style3}

\

As user1 on server3, create a file called vipractice in the home
directory using vim. Type (do not copy and paste) each sentence from Lab
3-1 on a separate line (do not worry about line wrapping). Save the file
and quit the editor. Open vipractice in vim again and copy lines 2 and 3
to the end of the file to make the total number of lines in the file to
6. Move line 3 to make it line 1. Go to the last line and append the
contents of the .bash_profile. Substitute all occurrences of the string
"Profile" with "Pro File", and all occurrences of the string "profile"
with "pro file". Erase lines 5 to 8. Save the file and quit vim. Provide
a count of lines, words, and characters in the vipractice file using the
wc command. (Hint: File Editing).

::: {style="page-break-before: always;"}
:::

[]{#chapter0140.html}

## Lab 3-3: File and Directory Operations {.style3}

\

As user1 on server3, create one file and one directory in the home
directory. List the file and directory and observe the permissions,
ownership, and owning group. Try to move the file and the directory to
the /var/log directory and notice what happens. Try again to move them
to the /tmp directory. Duplicate the file with the cp command, and then
rename the duplicated file using any name. Erase the file and directory
created for this lab. (Hint: File and Directory Operations).

::: {style="page-break-before: always;"}
:::

[]{#chapter0141.html}

## Chapter 04 {style="text-align: right"}

\

### Advanced File Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Understand ugo/rwx access permissions on files and directories

\

Know symbolic and octal notations of permission allocation

\

Modify permissions for file owner, owning group, and others

\

Calculate and set default permissions on new files and directories

\

Comprehend and configure special permission bits: setuid, setgid, and
sticky

\

Use setgid bit for group collaboration

\

Apply sticky bit on public and shared writable directories

\

Search for files in a variety of different ways

\

#### RHCSA Objectives:

\

10\. List, set, and change standard ugo/rwx permissions

36\. Create and configure set-GID directories for collaboration

37\. Diagnose and correct file permission problems

53\. Manage default file permissions

::: {style="page-break-before: always;"}
:::

\

Permissions are set on files and directories to prevent access from
unauthorized users. Users are grouped into three distinct categories.
Each user category is then assigned required permissions. Permissions
may be modified using one of two available methods. The user mask may be
defined for individual users so new files and directories they create
always get preset permissions. Every file in Linux has an owner and a
group.

\

RHEL offers three additional permission bits to control user access to
certain executable files and shared directories. A directory with one of
these bits can be used for group collaboration. A public or group
writable directory may also be configured with one of these bits to
prevent file deletion by non-owners.

\

::: {style="text-align: center;"}
![](image-5AS1F2J2.jpg){height="100%"}
:::

There is a tool available in RHEL that proves to be very helpful in
searching for files at the specified location using a range of options
to specify the search criteria. This tool may be set to execute an
action on the output files as they are found.

::: {style="page-break-before: always;"}
:::

[]{#chapter0142.html}

## File and Directory Access Permissions {.style3}

\

Linux is a multi-user operating system that allows hundreds of users the
ability to log in and work concurrently. In addition, the OS has
hundreds of thousands of files and directories that it must maintain
securely to warrant a successful system and application operation from a
security standpoint. Given these factors, it is imperative to regulate
user access to files and directories and grant them appropriate rights
to carry out their designated functions without jeopardizing system
security. This control of permissions on files and directories may also
be referred to as user access rights.

::: {style="page-break-before: always;"}
:::

[]{#chapter0143.html}

## Determining Access Permissions {.style3}

\

Access permissions on files and directories allow administrative control
over which users (permission classes) can access them and to what level
(permission types). File and directory permissions discussed in this
section are referred to as standard ugo/rwx permissions.

::: {style="page-break-before: always;"}
:::

[]{#chapter0144.html}

## Permission Classes {.style3}

\

Users are categorized into three unique classes for maintaining file
security through access rights. These classes are user (u), group (g),
and other (o, also referred to as public). These permission classes
represent the owner, the set of users with identical access
requirements, and everyone else on the system, respectively. There is
another special user class called all (a) that represents the three user
classes combined.

::: {style="page-break-before: always;"}
:::

[]{#chapter0145.html}

## Permission Types {.style3}

\

Permissions control what actions can be performed on a file or directory
and by whom. There are three types of permissions bits---read (r), write
(w), and execute (x)---and they behave differently for files and
directories. For files, the permissions allow viewing and copying
(read), modifying (write), and running (execute). And in the case of
directories, they allow listing contents with ls (read); creating,
erasing, and renaming files and subdirectories (write); and enter (with
the cd command) into it (execute).

\

If a read, write, or execute permission bit is not desired, the hyphen
character (-) is used to represent its absence.

::: {style="page-break-before: always;"}
:::

[]{#chapter0146.html}

## Permission Modes {.style3}

\

A permission mode is used to add (+), revoke (-), or assign (=) a
permission type to a permission class. You can view the permission
settings on files and directories in the long listing of the ls command.
This information is encapsulated in column 1 of the output, a sample of
which is shown below:

\

\- rwx rw- r\--

\

The first character indicates the type of file: - for regular file, d
for directory, l for symbolic link, c for character device file, b for
block device file, p for named pipe, s for socket, and so on.

\

The next nine characters---three groups of three characters---show the
read (r), write (w), and execute (x) permissions for the three user
classes: user (owner), group, and other (public), respectively. The
hyphen character (-) represents a permission denial for that level.

::: {style="page-break-before: always;"}
:::

[]{#chapter0147.html}

## Modifying Access Permission Bits {.style3}

\

The chmod command modifies access rights. It works identically on files
and directories. chmod can be used by root or the file owner, and can
modify permissions specified in one of two ways: symbolic or octal.
Symbolic notation uses a combination of letters (ugo/rwx) and symbols
(+, -, =) to add, revoke, or assign permission bits. The octal notation
(a.k.a. the absolute representation) uses a three-digit numbering system
ranging from 0 to 7 to express permissions for the three user classes.
Octal values are given in Table 4-1.

\

::: {style="text-align: center;"}
![](image-GNDDMZTD.jpg){height="100%"}
:::

Table 4-1 Octal Permission Notation

\

In Table 4-1, each "1" corresponds to an r, w, or x, and each "0"
corresponds to the hyphen character (-) for no permission at that level.
Figure 4-1 shows weights associated with each digit position in the
3-digit octal numbering model.

\

::: {style="text-align: center;"}
![](image-OB461QQ8.jpg){height="100%"}
:::

Figure 4-1 Permission Weights

\

The position to the right is weight 1, the middle position is weight 2,
and the left position is weight 4. If we assign a permission of 6, for
example, it will correspond to the left and middle positions. Similarly,
a permission of 2 would point to the middle position only.

::: {style="page-break-before: always;"}
:::

[]{#chapter0148.html}

## Exercise 4-1: Modify Permission Bits Using Symbolic Form {.style3}

\

This exercise should be done on server1 as user1.

\

For this exercise, presume that a file called permfile1 exists with read
permission for the owner (user1), owning group (user1), and other, as
shown below. If the permissions vary, bring them to the desired state by
executing chmod 444 permfile1 prior to starting the exercise.

\

<div>

![](image-4VM5MRTR.jpg){height="100%"}

</div>

In this exercise, you will add an execute bit for the owner and a write
bit for group and public. You will then revoke the write bit from public
and assign read, write, and execute bits to the three user categories at
the same time. Finally, you will revoke write from the owning group and
write and execute bits from public. The chmod command accepts the -v
switch to display what it has changed. You may alternatively view the
long listing after each command execution for verification.

\

1\. Add an execute bit for the owner:

\

<div>

![](image-U3PFQS1A.jpg){height="100%"}

</div>

2\. Add a write bit for group members and public:

\

<div>

![](image-D3ST00WO.jpg){height="100%"}

</div>

3\. Remove the write permission for public:

\

<div>

![](image-MO6J3LHA.jpg){height="100%"}

</div>

4\. Assign read, write, and execute permission bits to all three user
categories:

\

<div>

![](image-RWFI1BJU.jpg){height="100%"}

</div>

5\. Revoke write bit from the group members and write and execute bits
from public:

\

<div>

![](image-YH0LN3ZE.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0149.html}

## Exercise 4-2: Modify Permission Bits Using Octal Form {.style3}

\

This exercise should be done on server1 as user1.

\

For this exercise, a file called permfile2 exists with read permission
for the owner (user1), owning group (user1), and other, as shown below.
If the permissions vary, bring them to the desired state by executing
chmod 444 permfile2 prior to starting the exercise.

\

<div>

![](image-CKNIBC96.jpg){height="100%"}

</div>

In this exercise, you will add an execute bit for the owner and a write
permission bit for group and public. You will then revoke the write bit
from public and assign read, write, and execute permissions to the three
user categories at the same time. The chmod command accepts the -v flag
to display what it has changed. You may alternatively view the long
listing after each command execution for verification.

\

1\. Add an execute bit for the owner:

\

<div>

![](image-6AYVCXAE.jpg){height="100%"}

</div>

2\. Add a write permission bit for group and public:

\

<div>

![](image-ULO67WW3.jpg){height="100%"}

</div>

3\. Revoke the write bit for public:

\

<div>

![](image-HIROAEOW.jpg){height="100%"}

</div>

4\. Assign read, write, and execute permission bits to all three user
categories:

\

<div>

![](image-VF9KNXH7.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0150.html}

## Default Permissions {.style3}

\

Linux assigns default permissions to a file or directory at the time of
its creation. Default permissions are calculated based on the umask
(user mask) permission value subtracted from a preset initial
permissions value.

\

The umask is a three-digit octal value (also represented in symbolic
notation) that refers to read, write, and execute permissions for owner,
group, and public. Its purpose is to set default permissions on new
files and directories without touching the permissions on existing files
and directories. The default umask value is set to 0022 for all users
including the root user. Note that the left-most 0 bit has no
significance. Run the umask command without any options and it will
display the current umask value in octal notation:

\

<div>

![](image-YU4SMQ5E.jpg){height="100%"}

</div>

Run the command again but with the -S option to display the umask in
symbolic form:

\

<div>

![](image-J3BU1BL2.jpg){height="100%"}

</div>

The predefined initial permission values are 666 (rw-rw-rw-) for files
and 777 (rwxrwxrwx) for directories. Even if the umask is set to 000,
the new files will always get a maximum of 666 permissions; however, you
can add the executable bits explicitly with the chmod command if
desired.

::: {style="page-break-before: always;"}
:::

[]{#chapter0151.html}

## Calculating Default Permissions {.style3}

\

Consider the following example to calculate the default permission
values on files:

\

<div>

![](image-LJMOLT0U.jpg){height="100%"}

</div>

This is an indication that every new file will have read and write
permissions assigned to the owner, and a read-only permission to the
owning group and others.

\

To calculate the default permission values on directories:

\

<div>

![](image-K1337OSM.jpg){height="100%"}

</div>

This indicates that every new directory created will have read, write,
and execute permissions assigned to the owner, and read and execute
permissions to the owning group and everyone else.

\

If you want different default permissions set on new files and
directories, you will need to modify the umask. You first need to
ascertain the desired default values. For instance, if you want all new
files and directories to get 640 and 750 permissions, you can set umask
to 027 by running either of the following:

\

<div>

![](image-J3UDG7Y1.jpg){height="100%"}

</div>

The new value becomes effective right away, and it will only be applied
to files and directories created thereafter. The existing files and
directories will remain intact. Now create tempfile1 and tempdir1 as
user1 under /home/user1 to test the effect of the new umask:

\

<div>

![](image-ABCHQBHQ.jpg){height="100%"}

</div>

The above examples show that the new file and directory were created
with different permissions. The file got (666 -- 027 = 640) and the
directory got (777 -- 027 = 750) permissions.

\

The umask value set at the command line will be lost as soon as you log
off. In order to retain the new setting, place it in an appropriate
shell startup file discussed in Chapter 07 "The Bash Shell".

::: {style="page-break-before: always;"}
:::

[]{#chapter0152.html}

## Special File Permissions {.style3}

\

Linux offers three types of special permission bits that may be set on
binary executable files or directories that respond differently to
non-root users for certain operations. These permission bits are set
user identifier bit (commonly referred to as setuid or suid), set group
identifier bit (a.k.a. setgid or sgid), and sticky bit.

\

The setuid and setgid bits may be defined on binary executable files to
provide non-owners and non-group members the ability to run them with
the privileges of the owner or the owning group, respectively. The
setgid bit may also be set on shared directories for group
collaboration. The sticky bit may be set on public directories for
inhibiting file erasures by non-owners.

\

The setuid and sticky bits may be set on directories and files; however,
they will have no effect.

\

The use of the special bits should be regulated and monitored to evade
potential security issues to system operation and applications.

::: {style="page-break-before: always;"}
:::

[]{#chapter0153.html}

## The setuid Bit on Binary Executable Files {.style3}

\

The setuid flag is set on binary executable files at the file owner
level. With this bit set, the file is executed by non-owners with the
same privileges as that of the file owner. A common example is the su
command that is owned by the root user. This command has the setuid bit
enabled on it by default. See the underlined "s" in the owner's
permission class below:

\

<div>

![](image-QX73HI69.jpg){height="100%"}

</div>

The su (switch user) command allows a user to switch to a different user
account with the password for the target user. However, the root user
can switch into any other user account without being prompted for a
password. When a normal user executes this command, it will run as if
root (the owner) is running it and, therefore, the user is able to run
it successfully and gets the desired result.

::: {style="page-break-before: always;"}
:::

[]{#chapter0154.html}

## Exercise 4-3: Test the Effect of setuid Bit on Executable Files {.style3}

\

This exercise should be done on server1 as root and user1.

\

In this exercise, you will need two terminal windows, one with a root
session running and another with user1 on it. As user1, you will switch
into root and observe what happens. As root, you will then revoke the
setuid bit from the /usr/bin/su file and retry switching into root
again. After the completion of the exercise, you will restore the setuid
bit on /usr/bin/su.

\

1\. Log in as root and have a terminal window open (let's call it
Terminal 1). Open another terminal (let's name it Terminal 2) and run
the following to switch into user1:

\

<div>

![](image-C0K3YX0W.jpg){height="100%"}

</div>

2\. On Terminal 2, run the su command to switch into root:

\

<div>

![](image-E4SO64XC.jpg){height="100%"}

</div>

The output confirms the switch.

\

3\. On Terminal 1, revoke the setuid bit from /usr/bin/su:

\

<div>

![](image-XQI52YDH.jpg){height="100%"}

</div>

The file is still executable by everyone as indicated by the execute
flag; however, it will prevent regular non-owning users from switching
accounts, as they have lost that special elevated privilege.

\

4\. On Terminal 2, press Ctrl+d to log off as root.

5\. On Terminal 2, switch back into root and see what happens:

\

<div>

![](image-HHF4OSV2.jpg){height="100%"}

</div>

user1 gets an "authentication failure" message even though they entered
the correct password.

\

6\. On Terminal 1, restore the setuid bit on /usr/bin/su:

\

<div>

![](image-SOIPED2M.jpg){height="100%"}

</div>

With the argument +4000, the chmod command enables setuid on the
specified file without altering any existing underlying permissions.
Alternatively, you can use the symbolic notation as follows:

\

<div>

![](image-Z9J44HKZ.jpg){height="100%"}

</div>

\

If the file already has the "x" bit set for the user (owner), the long
listing will show a lowercase "s", otherwise it will list it with an
uppercase "S".

\

The setuid bit has no effect on directories.

::: {style="page-break-before: always;"}
:::

[]{#chapter0155.html}

## The setgid Bit on Binary Executable Files {.style3}

\

The setgid attribute is set on binary executable files at the group
level. With this bit set, the file is executed by non-owners with the
exact same privileges as that of the group members. A common example is
the write command that is owned by the root user with tty as the owning
group. This command has the setgid bit enabled on it by default. See the
"s" in the group's permission class below:

\

<div>

![](image-9ZIWIVI1.jpg){height="100%"}

</div>

<div>

![](image-78DFVT8H.jpg){height="100%"}

</div>

\

The write command allows users to write a message on another logged-in
user's terminal. By default, normal users are allowed this special
elevated privilege because of the presence of the setgid flag on the
file. When a normal user executes this command to write to the terminal
of another user, the command will run as if a member of the tty group is
running it, and the user is able to execute it successfully.

::: {style="page-break-before: always;"}
:::

[]{#chapter0156.html}

## Exercise 4-4: Test the Effect of setgid Bit on Executable Files {.style3}

\

This exercise should be done on server1 as root and user1.

\

In this exercise, you will need two terminal windows, one with a root
session running and the other with user1 on it. Both terminal sessions
must be opened with ssh. As user1, you will produce a list of logged-in
users; try to send the root user a message and observe what happens. As
root, you will then revoke the setgid bit from the /usr/bin/write file
and retry sending another message to root as user1. After the completion
of the exercise, you will restore the setgid bit on /usr/bin/write.

\

1\. Open a terminal window (let's call it Terminal 1) and log in as
root. Open another terminal (let's name it Terminal 2) and log in as
user1.

2\. On Terminal 2, run the who command to list users who are currently
logged on:

\

<div>

![](image-MELJE5LX.jpg){height="100%"}

</div>

The output discloses that there are two users---root and
user1---currently signed in.

\

3\. On Terminal 2, execute the write command as follows to send a
message to root:

\

<div>

![](image-DUJJ6CIH.jpg){height="100%"}

</div>

4\. On Terminal 1, you will see the following message from user1:

\

<div>

![](image-MF8G8N3H.jpg){height="100%"}

</div>

Any text you type on Terminal 2 will appear on Terminal 1. Press Ctrl+d
on Terminal 2 to end the write session.

\

5\. On Terminal 1, press Enter to get the command prompt back

6\. Revoke the setgid bit from /usr/bin/write:

\

<div>

![](image-ZPBTA9RV.jpg){height="100%"}

</div>

The file is still executable by everyone as indicated by the execute
flag; however, it will prevent them from writing to the terminals of
other users, as they have lost that special elevated privilege.

\

7\. On Terminal 2, rewrite to root and see what happens:

\

<div>

![](image-87MPG0R9.jpg){height="100%"}

</div>

user1 gets an error as indicated in the above output.

\

8\. On Terminal 1, restore the setgid bit on /usr/bin/write:

\

<div>

![](image-5BPF8CFC.jpg){height="100%"}

</div>

With the argument +2000, the chmod command enables setgid on the
specified file without altering any existing underlying permissions.
Alternatively, you can use the symbolic form as follows:

\

<div>

![](image-5ZJMTCVN.jpg){height="100%"}

</div>

\

If the file already has the "x" bit set for the group, the long listing
will show a lowercase "s", otherwise it will list it with an uppercase
"S".

\

The setgid bit has an impact on shared (and public) directories (next
subsection).

::: {style="page-break-before: always;"}
:::

[]{#chapter0157.html}

## The setgid Bit on Shared Directories {.style3}

\

The setgid bit can also be set on group-shared directories to allow
files and subdirectories created underneath to automatically inherit the
directory's owning group. This saves group members who are sharing the
directory contents from changing the group ID for every new file and
subdirectory that they add. The standard behavior for new files and
subdirectories is to always receive the creator's group.

::: {style="page-break-before: always;"}
:::

[]{#chapter0158.html}

## Exercise 4-5: Set up Shared Directory for Group Collaboration {.style3}

\

This exercise should be done on server1 as root and two test users
user100 and user200. Create the user accounts by running useradd user100
and useradd user200 (if they don't already exist) as root. Assign both
user accounts passwords by running passwd user100 and passwd user200 and
entering a password twice.

\

In this exercise, you will create a group called sgrp with GID 9999, and
add user100 and user200 to this group as members with shared data needs.
You will create a directory called /sdir with ownership and owning group
belonging to root and sgrp, then set the setgid bit on /sdir and test.
For details on managing users and groups, consult Chapter 05 "Basic User
Management" and Chapter 06 "Advanced User Management".

\

1\. Add group sgrp with GID 9999 with the groupadd command:

\

<div>

![](image-WO146GCR.jpg){height="100%"}

</div>

2\. Add user100 and user200 as members to sgrp using the usermod
command:

\

<div>

![](image-Q9RQ45Q3.jpg){height="100%"}

</div>

3\. Create /sdir directory:

\

<div>

![](image-J381JYK8.jpg){height="100%"}

</div>

4\. Set ownership and owning group on /sdir to root and sgrp, using the
chown command:

\

<div>

![](image-CNLYPY61.jpg){height="100%"}

</div>

5\. Set the setgid bit on /sdir using the chmod command:

\

<div>

![](image-QP60YKVY.jpg){height="100%"}

</div>

6\. Add write permission to the group members on /sdir and revoke all
permissions from public:

\

<div>

![](image-X4GXOZJ5.jpg){height="100%"}

</div>

7\. Verify the attributes set in the previous three steps using the ls
command on /sdir:

\

<div>

![](image-UPLAT439.jpg){height="100%"}

</div>

8\. Switch or log in as user100 and change to the /sdir directory:

\

<div>

![](image-5TO9AKS9.jpg){height="100%"}

</div>

9\. Create a file and check the owner and owning group on it:

\

<div>

![](image-E9K5IOUA.jpg){height="100%"}

</div>

10\. Log out as user100, and switch or log in as user200 and change to
the /sdir directory:

\

<div>

![](image-JPF5W0YO.jpg){height="100%"}

</div>

11\. Create a file and check the owner and owning group on it:

\

<div>

![](image-COJMXNX1.jpg){height="100%"}

</div>

As shown above, the owning group for each file is the same, sgrp, and
the group members have identical rights (read and write). Both can
modify or delete each other's file. The group members own the files, but
the owning group will always be sgrp to which they both belong.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Some of the steps provided above for setting up a directory
for group collaboration may not have to be run in that order.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0159.html}

## The Sticky Bit on Public and Shared Writable Directories {.style3}

\

The sticky bit is set on public and shared writable directories to
protect files and subdirectories owned by normal users from being
deleted or moved by other normal users. This attribute is set on the
/tmp and /var/tmp directories by default as depicted below; however, it
can be applied to any writable directory:

\

<div>

![](image-GDP3WQ4B.jpg){height="100%"}

</div>

Notice the underlined letter "t" in other's permission fields. This
indicates the presence of this attribute on the two directories.

::: {style="page-break-before: always;"}
:::

[]{#chapter0160.html}

## Exercise 4-6: Test the Effect of Sticky Bit {.style3}

\

This exercise should be done on server1 as root and two test users
user100 and user200 that were created in the previous exercise.

\

In this exercise, you will create a file under /tmp as user100 and then
try to delete it as user200. You will unset the sticky bit on /tmp and
try to erase the file again. After the completion of the exercise, you
will restore the sticky bit on /tmp. For details on managing users and
groups, consult Chapter 05 "Basic User Management" and Chapter 06
"Advanced User Management".

\

1\. Switch or log in as user100 and change to the /tmp directory:

\

<div>

![](image-UME67W2D.jpg){height="100%"}

</div>

2\. Create a file called stickyfile:

\

<div>

![](image-RPX4A30T.jpg){height="100%"}

</div>

3\. Log out as user100 and switch or log in as user200 and change to the
/tmp directory:

\

<div>

![](image-663CNOJW.jpg){height="100%"}

</div>

4\. Try to erase the file and observe the system reaction:

\

<div>

![](image-UADMO0S8.jpg){height="100%"}

</div>

It says, "Operation not permitted". The user cannot remove the file
owned by another user.

\

5\. Log out as user200 and revoke the sticky bit from /tmp as root and
confirm:

\

<div>

![](image-0Q7K0KTO.jpg){height="100%"}

</div>

6\. Switch or log back in as user200 and retry the removal:

\

<div>

![](image-R5D02U7W.jpg){height="100%"}

</div>

The file is gone. A normal user, user200, was able to successfully
delete a file, stickyfile, that was owned by a different normal user,
user100, in a public writable directory, /tmp.

\

7\. Log out as user200 and restore the sticky bit back on /tmp:

\

<div>

![](image-09FZUCZZ.jpg){height="100%"}

</div>

With the argument +1000, the chmod command sets the sticky bit on the
specified directory without altering any existing underlying
permissions. Alternatively, you can use the symbolic notation as
follows:

\

<div>

![](image-APN04HFX.jpg){height="100%"}

</div>

\

If the directory already has the "x" bit set for public, the long
listing will show a lowercase "t", otherwise it will list it with an
uppercase "T".

\

The sticky bit can also be set on group writable directories such as
/sdir that you created in the previous exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0161.html}

## File Searching {.style3}

\

A typical running RHEL system has a few hundred thousand files
distributed across several file systems. At times, it is imperative to
look for one or more files based on certain criteria. One example would
be to find all files owned by employees who left the company over a year
ago. Another example would be to search for all the files that have been
modified in the past 20 days by a specific user. For such situations,
RHEL offers a command called find. You supply your search criteria and
this command gets you the result. You can also instruct this utility to
execute a command on the files as they are found.

::: {style="page-break-before: always;"}
:::

[]{#chapter0162.html}

## Using the find Command {.style3}

\

The find command recursively searches the directory tree, finds files
that match the specified criteria, and optionally performs an action on
the files as they are discovered. This powerful tool can be tailored to
look for files in a number of ways. The search criteria may include
tracking files by name or part of the name, ownership, owning group,
permissions, inode number, last access or modification time in days or
minutes, size, and file type. Figure 4-2 shows the command syntax.

\

::: {style="text-align: center;"}
![](image-0XQKWV1K.jpg){height="100%"}
:::

Figure 4-2 find Command Syntax

\

With find, files that match the criteria are located and their full
paths are displayed.

\

To search for a file called file10 (execute touch file10 if it does not
already exist) by its name (name) in root's home directory, run the find
command as follows. The period character (.) represents the current
directory, which is /root in this example.

\

<div>

![](image-1AB87PPU.jpg){height="100%"}

</div>

\

-print is optional. The find command, by default, displays the results
on the screen. You do not need to specify this option.

\

To perform a case-insensitive (-iname) search for files and directories
in /dev that begin with the string "usb" followed by any characters:

\

<div>

![](image-SFGZWNPR.jpg){height="100%"}

</div>

To find files smaller than 1MB (-1M) in size (-size) in the root user's
home directory (\~). You do not need to issue the command from this
user's home directory. In fact, you can be anywhere in the directory
tree.

\

<div>

![](image-X8W6K725.jpg){height="100%"}

</div>

\

The tilde character (\~) represents a user's home directory.

\

To search for files larger than 40MB (+40M) in size (-size) in the /usr
directory:

\

<div>

![](image-ZSGHJTY9.jpg){height="100%"}

</div>

To find files in the entire root file system (/) with ownership (-user)
set to user daemon and owning group (-group) set to any group other than
(-not or ! for negation) user1:

\

<div>

![](image-UG0DZ3VR.jpg){height="100%"}

</div>

To search for directories (-type) by the name "src" (-name) in /usr at a
maximum of two subdirectory levels below (-maxdepth):

\

<div>

![](image-VQPI8PM0.jpg){height="100%"}

</div>

To run the above search but at least three subdirectory levels beneath
/usr, substitute -maxdepth 2 with -mindepth 3.

\

To find files in the /etc directory that were modified (-mtime) more
than (the + sign) 2000 days ago:

\

<div>

![](image-UQ3J024P.jpg){height="100%"}

</div>

To run the above search for files that were modified exactly 12 days
ago, replace "+2000" with "12".

\

To find files in the /var/log directory that have been modified (-mmin)
in the past (the - sign) 100 minutes:

\

<div>

![](image-EUFH0UP5.jpg){height="100%"}

</div>

To run the above search for files that have been modified exactly 25
minutes ago, replace "-100" with "25".

\

To search for block device files (-type) in the /dev directory with
permissions (-perm) set to exactly 660:

\

<div>

![](image-YBCRRUJS.jpg){height="100%"}

</div>

To search for character device files (-type) in the /dev directory with
at least (-222) world writable permissions (this example would ignore
checking the write and execute permissions):

\

<div>

![](image-WFEWOCR7.jpg){height="100%"}

</div>

To find files in the /etc/systemd directory that are executable by at
least their owner or group members:

\

<div>

![](image-2970SGDH.jpg){height="100%"}

</div>

To search for symlinked files (-type) in /usr with permissions (-perm)
set to read and write for the owner and owning group:

\

<div>

![](image-IKIM1TTX.jpg){height="100%"}

</div>

find is a very useful and powerful file-searching tool with numerous
other options available to use. Refer to its manual pages, as there are
a ton of examples there. Try some of them out for additional practice.

::: {style="page-break-before: always;"}
:::

[]{#chapter0163.html}

## Using find with -exec and -ok Flags {.style3}

\

An advanced use of the find command is to perform an action on the files
as they are found based on any criteria outlined in the previous
subsection and in the command's manual pages. The action may include
performing basic file management operations such as copying, erasing,
renaming, changing ownership, or modifying permissions on each file
found. This is done with the -exec switch. An equivalent option -ok may
be used instead, which requires user confirmation before taking an
action.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: The find command is very flexible and has a ton of options
available to search for files. You should know the use of the exec
option well.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

To search for directories in the entire directory tree (/) by the name
"core" (-name) and list them (ls -ld) as they are discovered without
prompting for user confirmation (-exec):

\

<div>

![](image-5NUHXM0S.jpg){height="100%"}

</div>

\

The find command replaces {} for each filename as it is found. The
semicolon character (;) marks the termination of the command and it is
escaped with the backslash character (\\).

\

In the next example, the find command uses the -ok switch to prompt for
confirmation (you need to enter a y) before it copies each matched file
(-name) in /etc/sysconfig to /tmp:

\

<div>

![](image-OWQZAT42.jpg){height="100%"}

</div>

The destination directory (/tmp) is specified between {} and \\;. There
are many advanced examples provided in the find command's manual pages.
I suggest trying a few of them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0164.html}

## Chapter Summary {.style3}

\

This chapter covered four topics: file and directory permissions,
default permissions, special permissions, and file searching.

\

We learned classes, types, and modes of permissions, looked at octal and
symbolic notations of changing permissions, and applied the knowledge to
modify user access on files and directories. We examined the concept of
default permissions and how they could be employed on parent directories
to enable files and subdirectories created underneath to automatically
get the desired permissions. We analyzed the role of the umask value in
determining the new default permissions.

\

We looked at special permission bits that could be set on executable
files to gain privileged access, applied on shared directories for
content sharing, and enabled on shared and public writable directories
to prevent file deletion by non-owning users.

\

Finally, we explored the criteria and the tool to search for files at
the specified directory location. We also employed an extended flag for
optional execution of an action on the outcome of the search command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0165.html}

## Review Questions {.style3}

\

1\. What would the find / -name core -ok rm {} \\; command do?

2\. Default permissions are calculated by subtracting the initial
permissions from the umask value. True or False?

3\. What would be the effect of the sticky bit on an executable file?

4\. Name the permission classes, types, and modes.

5\. The default umask for a normal user in bash shell is 0027. True or
False?

6\. What digit represents the setuid bit in the chmod command?

7\. The output generated by the umask command shows the current user
mask in four digits. What is the significance of the left-most digit?

8\. What would the command find /dev -type c -perm 660 do?

9\. What would the command chmod g-s file1 do?

10\. The sticky bit is recommended for every system directory. True or
False?

11\. The setgid bit enables group members to run a command at a higher
priority. True or False?

12\. What is the equivalent symbolic value for permissions 751?

13\. What permissions would the owner of the file get if the chmod
command is executed with 555?

14\. Which special permission bit is set on a directory for team
sharing?

::: {style="page-break-before: always;"}
:::

[]{#chapter0166.html}

## Answers to Review Questions {.style3}

\

1\. The find command provided will display all files by the name core in
the entire directory hierarchy and ask for removal confirmation as it
finds them.

2\. permissions of 660.

3\. False. Default permissions are calculated by subtracting the umask
value from the initial permission values.

4\. Nothing. The sticky bit is meant for directories only.

5\. Permission classes are user, group, and public; permission types are
read, write, and execute; and permission modes are add, revoke, and
assign.

6\. False. The default umask for bash shell users is 0022.

7\. The left-most digit has no significance in the umask value.

8\. The find command provided will find all character device files under
/dev with exact The digit 4 represents the setuid bit.

9\. It would erase the setgid bit from file1.

10\. False.

11\. False.

12\. The equivalent for octal 751 is rwxr-x\--x.

13\. The owner will get read and execute permissions.

14\. The setgid bit is set for team sharing.

::: {style="page-break-before: always;"}
:::

[]{#chapter0167.html}

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

[]{#chapter0168.html}

## Lab 4-1: Manipulate File Permissions {.style3}

\

As user1 on server3, create file file11 and directory dir11 in the home
directory. Make a note of the permissions on them. Run the umask command
to determine the current umask. Change the umask value to 0035 using
symbolic notation. Create file22 and directory dir22 in the home
directory. Observe the permissions on file22 and dir22, and compare them
with the permissions on file11 and dir11. Use the chmod command and
modify the permissions on file11 to match those on file22. Use the chmod
command and modify the permissions on dir22 to match those on dir11. Do
not remove file11, file22, dir11, and dir22 yet. (Hint: File and
Directory Access Permissions).

::: {style="page-break-before: always;"}
:::

[]{#chapter0169.html}

## Lab 4-2: Configure Group Collaboration and Prevent File Deletion {.style3}

\

As root on server3, create directory /sdir. Create group sgrp and add
user1000 and user2000 (create the users). Set up appropriate ownership
(root), owning group (sgrp), and permissions (rwx for group, \-\-- for
public, s for group, and t for public) on the directory to support group
collaboration and ensure non-owners cannot delete files. Log on as
user1000 and create a file under /sdir. Log on as user2000 and try to
edit that file. You should be able to edit the file successfully. As
user2000 try to delete the file. You should not be able to. (Hint:
Special File Permissions).

::: {style="page-break-before: always;"}
:::

[]{#chapter0170.html}

## Lab 4-3: Find Files {.style3}

\

As root on server3, execute the find command to search for all files in
the entire directory structure that have been modified in the last 300
minutes and display their type. Use the find command again and search
for named pipe and socket files. (Hint: File Searching).

::: {style="page-break-before: always;"}
:::

[]{#chapter0171.html}

## Lab 4-4: Find Files Using Different Criteria {.style3}

\

As root on server3, issue the find command to search for regular files
under /usr that were accessed more than 100 days ago, are not bigger
than 5MB in size, and are owned by the user root. (Hint: File
Searching).

::: {style="page-break-before: always;"}
:::

[]{#chapter0172.html}

## Chapter 05 {style="text-align: right"}

\

### Basic User Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Show who is currently logged in

\

Review history of successful user login attempts and system reboots

\

Report history of failed user log in attempts

\

View recent user login attempts

\

Examine user and group information

\

Understand the content and syntax of local user authentication files

\

Analyze user configuration files

\

Add, modify, and delete local user accounts with default and custom
values

\

Set and modify user passwords

\

Add user account with nologin access

\

#### RHCSA Objectives:

\

48\. Create, delete, and modify local user accounts

49\. Change passwords and adjust password aging for local user accounts
(only the first part of this objective "change passwords for local user
accounts" is covered in this chapter; the second part is in Chapter 06)

::: {style="page-break-before: always;"}
:::

\

User login activities are monitored and recorded in various files. RHEL
offers a set of tools that read the activity data from these files and
display the results. In addition to user activities, a history of system
reboots is also maintained, and it may be viewed with one of the tools.
This information may be useful in debugging, testing, or auditing
purposes.

\

In order for an authorized person to gain access to the system, a unique
username must be designated, and a user account must be created for
them. This user is assigned a password and is allowed to change it
themselves. User account information is recorded in several files. These
files may be edited manually if necessary; however, this practice is
discouraged. A good knowledge and grasp of the syntax and the type of
information these files store is paramount for Linux administrators.
User attributes may be modified later, or the account may be removed
from the system altogether if not required anymore.

\

::: {style="text-align: center;"}
![](image-MU2EFWWJ.jpg){height="100%"}
:::

Though service user accounts are added to the system when a
corresponding service is installed, there may be situations when they
need to be added manually. These accounts do not require login access;
their presence is needed to support an installed application.

::: {style="page-break-before: always;"}
:::

[]{#chapter0173.html}

## User Login Activity and Information {.style3}

\

On a busy RHEL system, many users sign in and run jobs as themselves, or
they switch into the root or another user account to run tasks that only
those users have the privilege to execute. As an administrator, it is
one of your responsibilities to ensure that only authorized users are
able to log in to the system. You can keep track of user logins, such as
who is currently logged in and their previous and recent successful and
unsuccessful login attempts. This information can be of immense help in
determining any suspicious login activity. For instance, multiple failed
attempts of logging in by an authorized user could be due to a forgotten
or lost password, or it might be a result of an unauthorized individual
trying to hack in.

\

There are many log files in RHEL that various services running on the
system update automatically and instantly as activities occur. These
logs capture user login activities among many others. This section will
focus on the log files and tools that are relevant to user logins only.
Others will be discussed in later chapters.

::: {style="page-break-before: always;"}
:::

[]{#chapter0174.html}

## Listing Logged-In Users {.style3}

\

A list of the users who have successfully signed on to the system with
valid credentials can be printed using one of the two basic Linux tools:
who and w. These commands show various pieces of information separated
in multiple columns.

\

The who command references the /run/utmp file and displays the
information. Here is a sample from server1:

\

<div>

![](image-HGQYUTVT.jpg){height="100%"}

</div>

Column 1 displays the login name of the user. Column 2 shows the
terminal session device filename (pts stands for pseudo terminal
session, and tty identifies a terminal window on the console). Columns 3
and 4 show the date and time of the user login, and column 5 indicates
if the terminal session is graphical (:0), remote (IP address), or
textual on the console.

\

The w (what) command displays information in a similar format as the who
command, but it also tells the length of time the user has been idle for
(IDLE), along with the CPU time used by all processes attached to this
terminal (JCPU), the CPU time used by the current process (PCPU), and
current activity (WHAT). In the following example, line 1 displays the
current system time (22:29:41), the system up duration (2 days, 5 hours,
and 28 minutes), number of users currently logged in (2), and the CPU
load averages over the past 1, 5, and 15 minutes (0.00, 0.00, and 0.00),
respectively. This is exactly what the uptime command shows, which was
also discussed in Chapter 02 "Initial Interaction with the System".

\

<div>

![](image-1O1MPOQG.jpg){height="100%"}

</div>

The load average numbers represent the percentage of CPU load with 0.00
and 1.00 correspond to no load and full load, and a number greater than
1.00 signifies excess load (over 100%).

::: {style="page-break-before: always;"}
:::

[]{#chapter0175.html}

## Inspecting History of Successful Login Attempts and System Reboots {.style3}

\

The last command reports the history of successful user login attempts
and system reboots by consulting the wtmp file located in the /var/log
directory. This file keeps a record of all login and logout activities,
including the login time, duration a user stayed logged in, and tty
(where the user session took place). Consider the following two
examples.

\

To list all user login, logout, and system reboot occurrences, issue the
last command without any arguments:

\

<div>

![](image-FDTE1LO5.jpg){height="100%"}

</div>

The output has information that is distributed across eight to nine
columns. Here is the description for each column for user history:

\

Column 1: Login name of the user

Column 2: Terminal name assigned upon logging in

Column 3: Terminal name or IP address from where the connection was
established

Column 4 to 7: Day, month, date, and time when the connection was
established

Column 8: Log out time. If the user is still logged on, it will say
"still logged in"

Column 9: Duration of the login session

\

For system reboots, this is what it shows:

\

Column 1: Action name (reboot)

Column 2: Activity name (system boot)

Column 3: Linux kernel version

Column 4 to 7: Day, month, date, and time when the reboot command was
issued

Column 8: System restart time

Column 9: Duration the system remained down. If the system is running,
it will say "still running".

\

The last line in the output indicates the log filename (wtmp) being used
to record this information and the time when it started to log events.

\

To list system reboot details only, you can issue the last command and
specify reboot as an argument:

\

<div>

![](image-JE4QBL3J.jpg){height="100%"}

</div>

The output includes the same information that it depicts with the last
command executed without any argument.

::: {style="page-break-before: always;"}
:::

[]{#chapter0176.html}

## Viewing History of Failed User Login Attempts {.style3}

\

The lastb command reports the history of unsuccessful user login
attempts by reading the btmp file located in the /var/log directory.
This file keeps a record of all unsuccessful login attempts, including
the login name, time, and tty (where the attempt was made). Consider the
following example.

\

To list all unsuccessful login attempts, type the lastb command without
any arguments. You must be root in order to run this command.

\

<div>

![](image-KP2DXNYU.jpg){height="100%"}

</div>

The output has information that is presented in nine columns. Here is
the description for each column:

\

Column 1: Name of the user who made the login attempt

Column 2: Name of the protocol used. No tty was assigned as the attempt
failed

Column 3: Terminal name or IP address from where the connection attempt
was launched

Column 4 to 7: Day, month, date, and time of the attempt

Column 8: Duration the login attempt was tried

Column 9: Duration the login attempt lasted for

\

The last line in the output discloses the log filename (btmp) being used
to record this information and the time when it started to log events.

::: {style="page-break-before: always;"}
:::

[]{#chapter0177.html}

## Reporting Recent User Login Attempts {.style3}

\

The lastlog command reports the most recent login evidence information
for every user account that exists on the system. This information is
captured in the lastlog file located in the /var/log directory. This
file keeps a record of the most recent user login attempts, including
the login name, time, and port (or tty). Consider the following example.

\

<div>

![](image-9KWOLBLG.jpg){height="100%"}

</div>

\

<div>

![](image-7TI5W6WP.jpg){height="100%"}

</div>

The output displays the information across four columns. Here is the
description for each column:

\

Column 1: Login name of the user

Column 2: Terminal name assigned upon logging in

Column 3: Terminal name or IP address from where the session was
initiated

Column 4: Timestamp for the latest login or "Never logged in" if the
user never signed in

\

Note that service accounts are used by their respective services, and
they are not meant for logging. More information on service accounts is
discussed in the next section.

::: {style="page-break-before: always;"}
:::

[]{#chapter0178.html}

## Examining User and Group Information {.style3}

\

The id (identifier) command displays the calling user's UID (User
IDentifier), username, GID (Group IDentifier), group name, all secondary
groups the user is a member of, and SELinux security context. Here is a
sample output for the root user when this command is executed without an
option or argument:

\

<div>

![](image-GAHZ30B2.jpg){height="100%"}

</div>

\

Each user and group has a corresponding number (called UID and GID) for
identification purposes. These will be discussed in subsequent sections
of this chapter. For SELinux, see Chapter 20 "Security Enhanced Linux".

\

The id command can be executed by a user to view other users'
identification information. The following example shows an instance with
the root user viewing another user's id:

\

<div>

![](image-SILBJXEG.jpg){height="100%"}

</div>

The groups command, in contrast, lists all groups the calling user is a
member of:

\

<div>

![](image-HPBQSCQV.jpg){height="100%"}

</div>

The first group listed is the primary group for the user who executed
this command; all other groups are secondary (or supplementary). The
groups command can also be used to view group membership information for
a different user. Try running it as groups user1 and observe the
outcome.

::: {style="page-break-before: always;"}
:::

[]{#chapter0179.html}

## Local User Authentication Files {.style3}

\

RHEL supports three fundamental user account types: root, normal, and
service. The root user (a.k.a. the superuser or the administrator), has
full access to all services and administrative functions on the system.
This user is created by default during installation. Normal users have
user-level privileges; they cannot perform any administrative functions
but can run applications and programs that have been authorized. Service
accounts take care of their respective services, which include apache,
ftp, mail, and chrony.

\

User account information for local users is stored in four files that
are located in the /etc directory. These files---passwd, shadow, group,
and gshadow---are updated when a user or group account is created,
modified, or deleted. The same files are referenced to check and
validate the credentials for a user at the time of their login attempt,
and hence the files are referred to as user authentication files. These
files are so critical to the operation of the system that the system
creates their automatic backups by default as passwd-, shadow-, group-,
and gshadow- in the /etc directory.

\

Here is the list of the four files and their backups from the /etc
directory:

\

<div>

![](image-A4Z5S61Y.jpg){height="100%"}

</div>

All files are short in size, but they grow bigger as new users are
added. Two of the files---gshadow and shadow---along with their backups
have no access permissions for any user, not even for root. Let's
analyze these files and see what information they store and how.

::: {style="page-break-before: always;"}
:::

[]{#chapter0180.html}

## The passwd File {.style3}

\

The passwd file is a simple plaintext file but it contains vital user
login data. Each row in the file holds information for one user account.
There are seven colon-separated fields per line entry. A sample row from
the file is displayed in Figure 5-1.

\

::: {style="text-align: center;"}
![](image-GHNAJE2S.jpg){height="100%"}
:::

Figure 5-1 The passwd File

\

Here is a description for each field:

\

Field 1 (Login Name): Contains the login name for signing in. Login
names with up to 255 characters, including the underscore (\_) and
hyphen (-) characters, are supported. It is not recommended to include
special characters and uppercase letters in login names.

Field 2 (Password): Can contain an "x" (points to the /etc/shadow file
for the actual password), an asterisk \* to identify a disabled account,
or a hashed password.

\

A hashed password---a combination of random letters, numbers, and
special characters---is an irreversible, unique, and scrambled string of
characters to safeguard a clear text password. It is generated as a
result of a conversion process of a password using one of the available
hashing algorithms. By default, RHEL uses the SHA-512 algorithm for this
purpose.

\

An algorithm is a set of well-defined but complex mathematical
instructions used in data encryption and decryption techniques.

\

Field 3 (UID): Comprises a numeric UID between 0 and approximately 4.2
billion. UID 0 is reserved for the root account, UIDs between 1 and 200
are used by Red Hat to statically assign them to core service accounts,
UIDs between 201 and 999 are reserved for non-core service accounts, and
UIDs 1000 and beyond are employed for normal user accounts. By default,
RHEL begins assigning UIDs to new users at 1000.

Field 4 (GID): Holds a GID that corresponds with a group entry in the
/etc/group file. By default, RHEL creates a group for every new user
matching their login name and the same GID as their UID. The GID defined
in this field represents the user's primary group.

Field 5 (Comments): Called GECOS (General Electric Comprehensive
Operating System and later changed to GCOS), optionally stores general
comments about the user that may include the user's name, phone number,
location, or other useful information to help identify the person for
whom the account is set up.

Field 6 (Home Directory): Defines the absolute path to the user home
directory. A home directory is the location where a user is placed after
signing in and it is used for personal storage. The default location for
user home directories is /home.

Field 7 (Shell): Consists of the absolute path of the shell file that
the user will be using as their primary shell after logging in. The
default shell used in RHEL is the Bash shell (/bin/bash). Consult
Chapter 07 "The Bash Shell" for details on the Bash shell.

\

A head and tail from the passwd file for the first and last three lines
is shown below:

\

<div>

![](image-V9XGPG6E.jpg){height="100%"}

</div>

The output indicates the root user with UID 0 followed by two service
accounts (bin and daemon). The last three lines display the three user
accounts that were created earlier as part of some of the exercises.

\

Let's verify the permissions and ownership on the passwd file:

\

<div>

![](image-68DXSWIU.jpg){height="100%"}

</div>

The access permissions on the file are 644 (world-readable and
owner-writable), and it is owned by the root user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0181.html}

## The shadow File {.style3}

\

RHEL has a secure password control mechanism in place that provides an
advanced level of password security for local users. This control is
referred to as the shadow password. With this control mechanism in
place, user passwords are hashed and stored in a more secure file
/etc/shadow, but there are certain limits on user passwords in terms of
expiration, warning period, etc., that can also be applied on a per-user
basis. These limits and other settings are defined in the
/etc/login.defsfile, which the shadow password mechanism enforces on
user accounts. This is called password aging. Unlike the passwd file,
which is world-readable and owner-writable, the shadow file has no
access permissions at all. This is done to safeguard the file's content.

\

With the shadow password mechanism active, a user is initially checked
in the passwd file for existence and then in the shadow file for
authenticity.

\

The shadow file contains user authentication and password aging
information. Each row in the file corresponds to one entry in the passwd
file. There are nine colon-separated fields per line entry. A sample row
from this file is showcased in Figure 5-2.

\

::: {style="text-align: center;"}
![](image-9OZF1NYR.jpg){height="100%"}
:::

Figure 5-2 The shadow File

\

Here is a description for each field:

\

Field 1 (Login Name): Contains the login name as appears in the passwd
file.

Field 2 (Encrypted Password): Consists of a hashed password. A single
exclamation mark (!) at the beginning of this field implies that the
user account is locked. If this field is empty, the user will have
passwordless entry into the system.

Field 3 (Last Change): Sets the number of days (lastchg) since the UNIX
epoch, a.k.a. UNIX time (January 01, 1970 00:00:00 UTC) when the
password was last modified. An empty field represents the passiveness of
password aging features, and a 0 forces the user to change their
password upon next login.

Field 4 (Minimum): Expresses the minimum number of days (mindays) that
must elapse before the user is allowed to change their password. This
field can be altered using the chage command with the -m option or the
passwd command with the -n option. A 0 or null in this field disables
this feature.

Field 5 (Maximum): Defines the maximum number of days (maxdays) of
password validity before the user password expires and it must be
changed. This field may be altered using the chage command with the -M
option or the passwd command with the -x option. A null value here
disables this feature along with other features such as the maximum
password age, warning alerts, and the user inactivity period.

Field 6 (Warning): Denotes the number of days (warndays) for which the
user gets warnings for changing their password before it actually
expires. This field may be altered using the chage command with the -W
option or the passwd command with the -w option. A 0 or null in this
field disables this feature.

Field 7 (Password Expiry): Contains the maximum allowable number of days
for the user to be able to log in with the expired password. This period
is referred to as the inactivity period. This field may be altered using
the chage command with the -I option or the passwd command with the -i
option. An empty field disables this feature.

Field 8 (Account Expiry): Determines the number of days since the UNIX
time when the user account will expire and no longer be available. This
field may be altered using the chage command with the -E option. An
empty field disables this feature.

Field 9 (Reserved): Reserved for future use.

\

A head and tail from the shadow file for the first and last three lines
is shown below:

\

<div>

![](image-M3491OWY.jpg){height="100%"}

</div>

The output indicates the root user with UID 0 followed by two service
accounts (bin and daemon). The last three lines display the three user
accounts that were created earlier as part of some of the exercises.
Notice that login names are used as a common key between the shadow and
passwd files.

\

Let's verify the permissions and ownership on the shadow file:

\

<div>

![](image-C1CNVHT9.jpg){height="100%"}

</div>

The access permissions on the file are 000 (no permissions at all), and
it is owned by the root user. There is a special mechanism in place that
is employed in the background to update this file when a user account is
added, modified, deleted, or the password changed. This will be
discussed in Chapter 21 "Security Enhanced Linux".

::: {style="page-break-before: always;"}
:::

[]{#chapter0182.html}

## The group File {.style3}

\

The group file is a simple plaintext file and contains critical group
information. Each row in the file stores information for one group
entry. Every user on the system must be a member of at least one group,
which is referred to as the User Private Group (UPG). By default, a
group name matches the username it is associated with. Additional groups
may be set up, and users with common file access requirements can be
added to them. There are four colon-separated fields per line entry. A
sample row from the file is exhibited in Figure 5-3.

\

::: {style="text-align: center;"}
![](image-SOA84JMN.jpg){height="100%"}
:::

Figure 5-3 The group File

\

Here is a description for each field:

\

Field 1 (Group Name): Holds a group name that must begin with a letter.
Group names with up to 255 characters, including the underscore (\_) and
hyphen (-) characters, are supported. It is not recommended to include
special characters and uppercase letters in group names.

Field 2 (Encrypted Password): Can be empty or contain an "x" (points to
the /etc/gshadow file for the actual password), or a hashed group-level
password. You can set a password on a group if you want non-members to
be able to change their group identity temporarily using the newgrp
command. The non-members must enter the correct password in order to do
so.

Field 3 (GID): Holds a GID, which is also placed in the GID field of the
passwd file. By default, groups are created with GIDs starting at 1000
and with the same name as the username. The system allows several users
to belong to a single group; it also allows a single user to be a member
of multiple groups at the same time.

Field 4 (Group Members): Lists the membership for the group. Note that a
user's primary group is always defined in the GID field of the passwd
file.

\

A head and tail from the group file for the first and last three lines
is shown below:

\

<div>

![](image-8WT79POA.jpg){height="100%"}

</div>

The output discloses the root user with GID 0 followed by two group
service accounts (bin and daemon). The last three lines showcase the
three groups that were created earlier as part of some of the exercises.

\

Let's verify the permissions and ownership on the group file:

\

<div>

![](image-NB3LUOLI.jpg){height="100%"}

</div>

The access permissions on the file are 644 (world-readable and
owner-writable), and it is owned by the root user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0183.html}

## The gshadow File {.style3}

\

The shadow password implementation also provides an added layer of
protection at the group level. With this mechanism in place, the group
passwords are hashed and stored in a more secure file /etc/gshadow.
Unlike the group file, which is world-readable and owner-writable, the
gshadow file has no access permissions at all. This is done to safeguard
the file's content.

\

The gshadow file stores hashed group-level passwords. Each row in the
file corresponds to one entry in the group file. There are four
colon-separated fields per line entry. A sample row from this file is
exhibited in Figure 5-4.

\

::: {style="text-align: center;"}
![](image-SC1V0Y14.jpg){height="100%"}
:::

Figure 5-4 The gshadow File

\

Here is a description for each field:

\

Field 1 (Group Name): Consists of a group name as appeared in the group
file.

Field 2 (Encrypted Password): Can contain a hashed password, which may
be set with the gpasswd command for non-group members to access the
group temporarily using the newgrp command. A single exclamation mark
(!) or a null value in this field allows group members passwordless
access and restricts non-members from switching into this group.

Field 3 (Group Administrators): Lists usernames of group administrators
that are authorized to add or remove members with the gpasswd command.

Field 4 (Members): Holds a comma-separated list of members.

\

The gpasswd command is used to add group administrators, add or delete
group members, assign or revoke a group-level password, and disable the
ability of the newgrp command to access a group. This command picks up
the default values from the /etc/login.defs file. Additional discussion
on this command is beyond the scope; however, you can view the manual
pages of this command for details on its usage.

\

A head and tail from the gshadow file for the first and last three lines
is shown below:

\

<div>

![](image-D45PVK6Q.jpg){height="100%"}

</div>

The output indicates the root user with GID 0 followed by two group
service accounts (bin and daemon). The last three lines exhibit the
three groups that were created earlier as part of some of the exercises.
Notice that group names are used as a common key between the gshadow and
group files.

\

Let's verify the permissions and ownership on the gshadow file:

\

<div>

![](image-516R0JR4.jpg){height="100%"}

</div>

The access permissions on the file are 000 (no permissions at all) and
it is owned by the root user. There is a special mechanism in place that
is employed in the background to update this file when a group account
is added, modified, deleted, or the group password changed. This will be
discussed further in Chapter 21 "Security Enhanced Linux".

::: {style="page-break-before: always;"}
:::

[]{#chapter0184.html}

## The useradd and login.defs Configuration Files {.style3}

\

The useradd command (discussed in the next section) picks up the default
values from the /etc/default/useradd and /etc/login.defs files for any
options that are not specified at the command line when executing it.
Moreover, the login.defs file is also consulted by the usermod, userdel,
chage, and passwd commands (also discussed in the next section) as
needed. Both files store several defaults including those that affect
the password length and password lifecycle. You can use the cat or less
command to view the useradd file content or display the settings with
the useradd command as follows:

\

<div>

![](image-EPNL0W66.jpg){height="100%"}

</div>

There are a multitude of defaults defined with the directives. These
include the starting GID (GROUP) provided the USERGROUPS_ENAB directive
in the login.defs file is set to no, home directory location (HOME),
number of inactivity days between password expiry and permanent account
disablement (INACTIVE), account expiry date (EXPIRE), login shell
(SHELL), skeleton directory location to copy user initialization files
from (SKEL), and whether to create mail spool directory
(CREATE_MAIL_SPOOL). You will find a description for some of these in
the next section.

\

The other file login.defs comprises of additional directives that set
several defaults. User and group management commands consult this file
to obtain information that is not supplied at the command line. A grep
on the file with uncommented and non-empty lines is shown below:

\

<div>

![](image-0XMDFW99.jpg){height="100%"}

</div>

\

The grep command is discussed in detail in Chapter 07 "The Bash Shell".

\

Most of these directives are elaborated in Table 5-1.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  MAIL_DIR                            Specifies the mail directory
                                      location

  UMASK                               Defines the permissions to be set
                                      on the user home directory at
                                      creation based on this umask value

  HOME_MODE                           The mode for new user home
                                      directories. The umask value is
                                      used if not specified with the
                                      command.

  PASS_MAX_DAYS, PASS_MIN_DAYS, and   Define password aging attributes.
  PASS_WARN_AGE                       See Chapter 06 "Advanced User
                                      Management" for details.

  UID_MIN, UID_MAX, GID_MIN, and      Identify the ranges of UIDs and
  GID_MAX                             GIDs to be allocated to new users
                                      and groups

  SYS_UID_MIN, SYS_UID_MAX,           Identify the ranges of UIDs and
  SYS_GID_MIN, and SYS_GID_MAX        GIDs to be allocated to new service
                                      users and groups

  ENCRYPT_METHOD                      Specifies the encryption method for
                                      user passwords

  USERGROUPS_ENAB                     If set to yes, (1) the useradd
                                      command will create a group
                                      matching the name of the user and
                                      (2) the userdel command will delete
                                      a user's group if it contains no
                                      more members.

  CREATE_HOME                         Defines whether to create a home
                                      directory
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 5-1 login.defs File Directives

\

There are many more directives available that can be added to this file
for more control and flexibility. Check the manual pages of the file for
details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0185.html}

## User Account Management {.style3}

\

Managing user accounts involves creating, assigning passwords to,
modifying, and deleting them. RHEL provides a set of tools for
performing these operations. These tools are useradd to add a new user
to the system, usermod to modify the attributes of an existing user, and
userdel to remove a user from the system. In addition, the passwd
command is available to set or modify a user's password.

::: {style="page-break-before: always;"}
:::

[]{#chapter0186.html}

## The useradd, usermod, and userdel Commands {.style3}

\

This set of commands is used to add, modify, and delete a user account
from the system. The useradd command adds entries to the four user
authentication files for each account added to the system. It creates a
home directory for the user and copies the default user startup files
from the skeleton directory /etc/skel into the user's home directory. It
can also be used to update the default settings that are used at the
time of new user creation for unspecified settings. The useradd command
supports a variety of flags; Table 5-2 lists some common options in both
short and long versions.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -b (\--base-dir)                    Defines the absolute path to the
                                      base directory for placing user
                                      home directories. The default is
                                      /home.

  -c (\--comment)                     Describes useful information about
                                      the user.

  -d (\--home-dir)                    Defines the absolute path to the
                                      user home directory.

  -D (\--defaults)                    Displays the default settings from
                                      the /etc/default/useradd file and
                                      modifies them.

  -e (\--expiredate)                  Specifies a date on which a user
                                      account is automatically disabled.
                                      The format for the date
                                      specification is YYYY-MM-DD.

  -f (\--inactive)                    Denotes maximum days of inactivity
                                      between password expiry and
                                      permanent account disablement.

  -g (\--gid)                         Specifies the primary GID. Without
                                      this option, a group account
                                      matching the username is created
                                      with the GID matching the UID.

  -G (\--groups)                      Specifies the membership to
                                      supplementary groups.

  -k (\--skel)                        Specifies the location of the
                                      skeleton directory (default is
                                      /etc/skel), which stores default
                                      user startup files. These files are
                                      copied to the user's home directory
                                      at the time of account creation.
                                      Three hidden bash shell
                                      files---.bash_profile, .bashrc, and
                                      .bash_logout---are available in
                                      this directory by default. You can
                                      customize these files or add your
                                      own to be used for accounts created
                                      thereafter.

  -m (\--create-home)                 Creates a home directory if it does
                                      not already exist.

  -o (\--non-unique)                  Creates a user account sharing the
                                      UID of an existing user. When two
                                      users share a UID, both get
                                      identical rights on each other's
                                      files. This should only be done in
                                      specific situations.

  -r (\--system)                      Creates a service account with a
                                      UID below 1000 and a never-expiring
                                      password.

  -s (\--shell)                       Defines the absolute path to the
                                      shell file. The default is
                                      /bin/bash.

  -u (\--uid)                         Indicates a unique UID. Without
                                      this option, the next available UID
                                      from the /etc/passwd file is used.

  login                               Specifies a login name to be
                                      assigned to the user account.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 5-2 useradd Command Options

\

You can modify the attributes of a user account with the usermod
command. The syntax of this command is very similar to that of the
useradd's, with most switches identical. Table 5-3 describes the options
that are specific to usermod only, and shows them in both short and long
versions. There are two additional flags of interest that are discussed
in Chapter 06 "Advanced User Management".

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -a (\--append)                      Adds a user to one or more
                                      supplementary groups

  -l (\--login)                       Specifies a new login name

  -m (\--move-home)                   Creates a home directory and moves
                                      the content over from the old
                                      location
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 5-3 usermod Command Options

\

The userdel command is straightforward. It removes entries for the
specified user from the authentication files, and deletes the user's
home directory if the -r flag is also specified. The -f option may be
used to force the removal even if the user is still logged in.

::: {style="page-break-before: always;"}
:::

[]{#chapter0187.html}

## Exercise 5-1: Create a User Account with Default Attributes {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create a user account user2 using the
defaults defined in the useradd and login.defs files. You will assign
this user a password and show the new line entries from all four
authentication files.

\

1\. Create user2 with all the default values:

\

<div>

![](image-4WA63694.jpg){height="100%"}

</div>

2\. Assign this user a password and enter it twice when prompted:

\

<div>

![](image-ZT4MTK7E.jpg){height="100%"}

</div>

3\. grep for user2: on the authentication files to examine what the
useradd command has added:

\

<div>

![](image-WRP7F67U.jpg){height="100%"}

</div>

The command used the next available UID (1003) and GID (1003), and the
default settings for the home directory (/home/user2) and shell file
(/bin/bash).

\

4\. Test this new account by logging in as user2 and then run the id and
groups commands to verify the UID, GID, and group membership
information:

\

<div>

![](image-5F827BSA.jpg){height="100%"}

</div>

The above outputs confirmed the UID and username, GID and group name,
and primary group name.

::: {style="page-break-before: always;"}
:::

[]{#chapter0188.html}

## Exercise 5-2: Create a User Account with Custom Values {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create an account user3 with UID 1010, home
directory /usr/user3a, and shell /bin/sh. You will assign this user a
password and exhibit the new line entries from all four authentication
files.

\

1\. Create user3 with UID 1010 (-u), home directory /usr/user3a (-d),
and shell /bin/sh (-s):

\

<div>

![](image-T1S1QLMJ.jpg){height="100%"}

</div>

2\. Assign user1234 as password (passwords assigned in the following way
is not recommended; however, it is okay in a lab environment):

\

<div>

![](image-169L50ZY.jpg){height="100%"}

</div>

3\. grep for user3: on the four authentication files to see what was
added for this user:

\

<div>

![](image-WNLRKEKA.jpg){height="100%"}

</div>

4\. Test this account by switching to or logging in as user3 and
entering user1234 as the password. Run the id and groups commands for
further verification.

::: {style="page-break-before: always;"}
:::

[]{#chapter0189.html}

## Exercise 5-3: Modify and Delete a User Account {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will modify certain attributes for user2 and then
delete it. You will change the login name to user2new, UID to 2000, home
directory to /home/user2new, and login shell to /sbin/nologin. You will
display the line entry for user2new from the passwd file for validation.
Finally, you will remove this user and confirm the deletion.

\

1\. Modify the login name for user2 to user2new (-l), UID to 2000 (-u),
home directory to /home/user2new (-m and -d), and login shell to
/sbin/nologin (-s). Notice that the options are specified in a different
sequence.

\

<div>

![](image-YKO6ZTZC.jpg){height="100%"}

</div>

2\. Obtain the information for user2new from the passwd file for
confirmation:

\

<div>

![](image-58AC3E3X.jpg){height="100%"}

</div>

3\. Remove user2new along with their home and mail spool directories
(-r):

\

<div>

![](image-87BQNHPH.jpg){height="100%"}

</div>

4\. Confirm the user deletion:

\

<div>

![](image-RKHYG0YK.jpg){height="100%"}

</div>

Nothing is returned in the output, which means this user does not exist
in the passwd file any longer. This confirms the removal.

::: {style="page-break-before: always;"}
:::

[]{#chapter0190.html}

## No-Login (Non-Interactive) User Account

\

The nologin shell is a special purpose program that can be employed for
user accounts that do not require login access to the system. It is
located in the /usr/sbin (or /sbin) directory. With this shell assigned,
the user is refused with the message, "This account is currently not
available." displayed on the screen. If a custom message is required,
you can create a file called nologin.txt in the /etc directory and add
the desired text to it. The content of this file is printed on the
screen upon user access denial instead of the default message.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: If a no-login user is able to log in with their credentials,
there is a problem. Use the grep command against the /etc/passwd file to
ensure '/sbin/nologin' is there in the shell field for that user.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Typical examples of user accounts that do not require login access are
the service accounts such as ftp, mail, and sshd. Let's take a look at
the passwd file and list such users:

\

<div>

![](image-MPEAZYWM.jpg){height="100%"}

</div>

This output returns a truncated list of non-interactive user accounts.
There are tens of them, and they grow as you install more services on
the system.

::: {style="page-break-before: always;"}
:::

[]{#chapter0191.html}

## Exercise 5-4: Create a User Account with No-Login Access {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create an account user4 with all the default
attributes but with a non-interactive shell. You will assign this user
the nologin shell to prevent them from signing in. You will display the
new line entry from the passwd file and test the account.

\

1\. Create user4 with non-interactive shell file /sbin/nologin:

\

<div>

![](image-H6Q6CNK5.jpg){height="100%"}

</div>

2\. Assign user1234 as password:

\

<div>

![](image-HCH7YTI9.jpg){height="100%"}

</div>

3\. grep for user4 on the passwd file and verify the shell field
containing the nologin shell:

\

<div>

![](image-MBLAIBKB.jpg){height="100%"}

</div>

4\. Test this account by attempting to log in or switch:

\

<div>

![](image-DG1UEWSN.jpg){height="100%"}

</div>

As mentioned earlier, you may create the /etc/nologin.txt file and add a
custom message to it. The new message will appear on your next login
attempt.

::: {style="page-break-before: always;"}
:::

[]{#chapter0192.html}

## Chapter Summary {.style3}

\

We started this chapter by discovering various tools that are employed
to monitor user login and system reboot activities. This information is
stored in several system files and may be used for testing, auditing, or
troubleshooting reasons. Most of these tools can be executed by normal
users to obtain desired results; however, others may require privileged
access of the root user in order to be viewed.

\

Next, we looked closely at the four local user authentication files:
passwd, shadow, group, and gshadow. We examined their contents and
syntax to comprehend what they store and how. These files are critical
to the user login process as well as the functioning of applications and
services.

\

Finally, we explored user management tools and put them into action in
exercises to create, modify, and delete user accounts. These tools offer
a number of switches to add accounts with default and custom attributes,
as well as user accounts that do not require login access.

::: {style="page-break-before: always;"}
:::

[]{#chapter0193.html}

## Review Questions {.style3}

\

1\. UID 999 is reserved for normal users. True or False?

2\. Which file is assigned to users to deny them login access?

3\. You execute the lastb command as a normal user. The output reports
an error. What do you need to do to run this command successfully?

4\. What would the command useradd -D do?

5\. What does the lastlog command do?

6\. What would the command useradd user500 do?

7\. The id and groups commands are useful for listing a user
identification. True or False.

8\. Name the three fundamental user account classes in RHEL.

9\. Every user in RHEL gets a private group by default. True or False?

10\. What does the "x" in the password field in the passwd file imply?

11\. Name the file that the who command consults to display logged-in
users.

12\. What information does the lastb command provide?

13\. The who command may be used to view logged out users. True or
False?

14\. What would the userdel command do if it is run with the -r option?

15\. Name the four local user authentication files.

16\. The passwd file contains secondary user group information. True or
False?

17\. What is the first UID assigned to a normal user?

18\. What is the first GID assigned to a group?

19\. What is the name of the default backup file for shadow?

20\. Which file does the last command consult to display reports?

::: {style="page-break-before: always;"}
:::

[]{#chapter0194.html}

## Answers to Review Questions {.style3}

\

1\. False. UID 999 is reserved for system accounts.

2\. The /sbin/nologin file is assigned to users to deny them login.

3\. You need to run the lastb command as root or with the root
privilege.

4\. This command displays the defaults settings used at the time of user
creation or modification.

5\. The lastlog command provides information about recent user logins.

6\. The command provided will add user500 with all predefined default
values.

7\. False. Only the id command is used for this purpose.

8\. The three fundamental user account categories are root, normal, and
system.

9\. True.

10\. The "x" in the password field implies that the hashed password is
stored in the shadow file.

11\. The who command consults the /run/utmp file to list logged-in
users.

12\. The lastb command reports the history of unsuccessful user login
attempts.

13\. False. The who command shows currently logged-in users only.

14\. The userdel command with -r will delete the specified user along
with their home directory.

15\. The passwd, shadow, group, and gshadow files.

16\. False. The passwd file contains primary user group information.

17\. The first UID assigned to a normal user is 1000.

18\. The first GID assigned to a normal user is 1000.

19\. The name of the default backup file for shadow is shadow-.

20\. The last command consults the /var/log/wtmp file to display
reports.

::: {style="page-break-before: always;"}
:::

[]{#chapter0195.html}

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

[]{#chapter0196.html}

## Lab 5-1: Check User Login Attempts {.style3}

\

As root on server3, execute the last, lastb, and lastlog commands, and
observe the outputs. Check which users recently logged in and out
successfully (last) and unsuccessfully (lastb). List the timestamps when
the system was last rebooted (last). Check the last login status for
each user (lastlog). Use the vim editor to record your results. (Hint:
User Login Activity and Information).

::: {style="page-break-before: always;"}
:::

[]{#chapter0197.html}

## Lab 5-2: Verify User and Group Identity {.style3}

\

As user1 on server3, run the who and w commands one at a time, and
compare the outputs. Execute the id and groups commands, and compare the
outcomes. Examine the extra information that the id command shows, but
not the groups command. (Hint: User Login Activity and Information).

::: {style="page-break-before: always;"}
:::

[]{#chapter0198.html}

## Lab 5-3: Create Users {.style3}

\

As root on server3, create user account user4100 with UID 4100 and home
directory under /usr. Create another user account user4200 with default
attributes. Assign both users a password. View the contents of the
passwd, shadow, group, and gshadow files, and observe what has been
added for the two new users. (Hint: Local User Authentication Files, and
User Account Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0199.html}

## Lab 5-4: Create User with Non-Interactive Shell {.style3}

\

As root on server3, create user account user4300 with the disability of
logging in. Assign this user a password. Try to log on with this user
and see is displayed on the screen. View the content of the passwd file,
and see what prevents this user from logging in. (Hint: Local User
Authentication Files, and User Account Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0200.html}

## Chapter 06 {style="text-align: right"}

\

### Advanced User Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Configure password aging attributes on local user accounts

\

Lock and unlock user account

\

Understand, create, modify, and delete local groups and group
memberships

\

Switch into another user account

\

Configure who can execute which privileged commands

\

Identify and manage file owners and owning groups

\

#### RHCSA Objectives:

\

05\. Log in and switch users in multi-user targets

49\. Change passwords and adjust password aging for local user accounts
(only the second part of this objective "adjust password aging for local
user accounts" is covered in this chapter; the first part is in Chapter
05)

50\. Create, delete, and modify local groups and group memberships

51\. Configure superuser access

::: {style="page-break-before: always;"}
:::

\

Password aging attributes may be set on user accounts for increased
control on their logins and passwords. This can be done for an
individual user or applied to all users. Password aging information for
users is stored in one of the authentication files that was discussed at
length in the previous chapter. Individual user accounts may be
prevented from logging in to the system by locking their access for a
period of time or permanently. This lock may be lifted when required.
Setting password aging and locking/unlocking accounts are administrative
functions and must be performed by a user with elevated privileges of
the root user.

\

Users are apportioned membership to a single group at the time of their
addition to the system. Later, they may be assigned membership to
additional groups. Members of the same group possess the same access
rights on files and directories. Other users and members of other groups
may optionally be given access to those files. Group membership
information is stored in user and group authentication files that were
examined in the previous chapter as well.

\

::: {style="text-align: center;"}
![](image-6TLJEZFQ.jpg){height="100%"}
:::

Users may switch into other user accounts, including the root user,
provided they know the target user's password. Normal users may be
allowed access to privileged commands by defining them appropriately in
a configuration file. Each file that exists on the system regardless of
its type has an owning user and an owning group. Similarly, every file
that a user creates is in the ownership of that user. The ownership may
be changed and given to another user by a super user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0201.html}

## Password Aging and its Management {.style3}

\

As mentioned, password aging is a secure mechanism to control user
passwords in Linux. The key advantages include setting restrictions on
password expiry, account disablement, locking and unlocking users, and
password change frequency. These controls are applied to all user
accounts at the time of their creation and can be set explicitly on a
per-user basis later. You can even choose to inactivate it completely
for an individual user.

\

Password aging information is stored in the /etc/shadow file (fields 4
to 8) and its default policies in the /etc/login.defs configuration
file. These files were thoroughly examined in Chapter 05 "Basic User
Management". In this section, we explore the aging management
tools---chage and passwd--- and look at how to employ them to apply
password controls on user accounts, user100 and user200. Alongside chage
and passwd, the usermod command can also be used to implement two aging
attributes (user expiry and password expiry); however, this section
focuses on this command's ability to lock and unlock user accounts.

::: {style="page-break-before: always;"}
:::

[]{#chapter0202.html}

## The chage Command {.style3}

\

The chage command is used to set or alter password aging parameters on a
user account. This command changes various fields in the shadow file
depending on which option(s) you pass to it. There are plenty of
switches available with the command in both short and long formats.
Table 6-1 describes most of them.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -d (\--lastday)                     Specifies an explicit date in the
                                      YYYY-MM-DD format, or the number of
                                      days since the UNIX time when the
                                      password was last modified. With -d
                                      0, the user is forced to change the
                                      password at next login. It
                                      corresponds to field 3 in the
                                      shadow file.

  -E (\--expiredate)                  Sets an explicit date in the
                                      YYYY-MM-DD format, or the number of
                                      days since the UNIX time on which
                                      the user account is deactivated.
                                      This feature can be disabled with
                                      -E -1. It corresponds to field 8 in
                                      the shadow file.

  -I (\--inactive)                    Defines the number of days of
                                      inactivity after the password
                                      expiry and before the account is
                                      locked. The user may be able to log
                                      in during this period with their
                                      expired password. This feature can
                                      be disabled with -I -1. It
                                      corresponds to field 7 in the
                                      shadow file.

  -l                                  Lists password aging attributes set
                                      on a user account.

  -m (\--mindays)                     Indicates the minimum number of
                                      days that must elapse before the
                                      password can be changed. A value of
                                      0 allows the user to change their
                                      password at any time. It
                                      corresponds to field 4 in the
                                      shadow file.

  -M (\--maxdays)                     Denotes the maximum number of days
                                      of password validity before the
                                      user password expires and it must
                                      be changed. This feature can be
                                      disabled with -M -1. It corresponds
                                      to field 5 in the shadow file.

  -W (\--warndays)                    Designates the number of days for
                                      which the user gets alerts to
                                      change their password before it
                                      expires. It corresponds to field 6
                                      in the shadow file.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 6-1 chage Command Options

\

You will use most of these flags used in Exercise 6-1 and later in this
chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0203.html}

## Exercise 6-1: Set and Confirm Password Aging with chage {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will configure password aging for user100 using
the chage command. You will set mindays to 7, maxdays to 28, and
warndays to 5, and verify the new settings. You will then rerun the
command and set account expiry to December 31, 2023. You will complete
the exercise with another confirmation.

\

1\. Set password aging parameters for user100 to mindays (-m) 7, maxdays
(-M) 28, and warndays (-W) 5:

\

<div>

![](image-L64NDIOP.jpg){height="100%"}

</div>

2\. Confirm the new settings:

\

<div>

![](image-UF9216RK.jpg){height="100%"}

</div>

The bottom three rows in the output confirm the new settings. The
current password expiry (February 26, 2023) reflects the 28-day duration
from January 29, 2023 when this command was executed.

\

3\. Set the account expiry to December 31, 2023:

\

<div>

![](image-J549MFAK.jpg){height="100%"}

</div>

4\. Verify the new account expiry setting:

\

<div>

![](image-B9W55BEK.jpg){height="100%"}

</div>

The middle row reflects the new account expiry for user100. Similarly,
you can use the -d and -I options with the chage command as required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0204.html}

## The passwd Command {.style3}

\

The common use of the passwd command is to set or modify a user's
password; however, you can also use this command to modify the password
aging attributes and lock or unlock their account. Table 6-2 lists some
key options in both short and long formats.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -d (\--delete)                      Deletes a user password without
                                      expiring the user account.

  -e (\--expire)                      Forces a user to change their
                                      password upon next logon.

  -i (\--inactive)                    Defines the number of days of
                                      inactivity after the password
                                      expiry and before the account is
                                      locked. It corresponds to field 7
                                      in the shadow file.

  -l (\--lock)                        Locks a user account.

  -n (\--minimum)                     Specifies the number of days that
                                      must elapse before the password can
                                      be changed. It corresponds to field
                                      4 in the shadow file.

  -S (\--status)                      Displays the status information for
                                      a user.

  -u (\--unlock)                      Unlocks a locked user account.

  -w (\--warning)                     Designates the number of days for
                                      which the user gets alerts to
                                      change their password before it
                                      actually expires. It corresponds to
                                      field 6 in the shadow file.

  -x (\--maximum)                     Denotes the maximum number of days
                                      of password validity before the
                                      user password expires and it must
                                      be changed. It corresponds to field
                                      5 in the shadow file.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 6-2 passwd Command Options

\

Most of these flags will be used in the next few exercises.

::: {style="page-break-before: always;"}
:::

[]{#chapter0205.html}

## Exercise 6-2: Set and Confirm Password Aging with passwd {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will configure password aging for user200 using
the passwd command. You will set mindays to 10, maxdays to 90, and
warndays to 14, and verify the new settings.

\

Next, you will set the number of inactivity days to 5 and ensure that
the user is forced to change their password upon next login. You will
complete the exercise with another verification.

\

1\. Set password aging attributes for user200 to mindays (-n) 10,
maxdays (-x) 90, and warndays (-w) 14:

\

<div>

![](image-5KC7T1K6.jpg){height="100%"}

</div>

2\. Confirm the new settings:

\

<div>

![](image-LZKYAFJS.jpg){height="100%"}

</div>

The output confirms the three new settings (10, 90, and 14).

\

3\. Set the number of inactivity days to 7:

\

<div>

![](image-2T17OBKE.jpg){height="100%"}

</div>

4\. Confirm the new setting:

\

<div>

![](image-0NQ9KU3J.jpg){height="100%"}

</div>

The output verifies the new setting (7).

\

5\. Ensure that the user is forced to change their password at next
login:

\

<div>

![](image-NP96ZW94.jpg){height="100%"}

</div>

6\. Display the new setting for confirmation:

\

<div>

![](image-Y6779TNV.jpg){height="100%"}

</div>

The output shows a date prior to the UNIX time. This user will be
prompted to change their password when they attempt to log in the next
time.

::: {style="page-break-before: always;"}
:::

[]{#chapter0206.html}

## The usermod Command {.style3}

\

The common use of the usermod command is to modify a user's attribute,
but it can also lock or unlock their account. Table 6-3 explains the two
options in both short and long formats.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -L (\--lock)                        Locks a user account by placing a
                                      single exclamation mark (!) at the
                                      beginning of the password field and
                                      before the hashed password string.

  -U (\--unlock)                      Unlocks a user's account by
                                      removing the exclamation mark (!)
                                      from the beginning of the password
                                      field.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 6-3 usermod Command Options for User Lock/Unlock

\

Let's apply these options in the next exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0207.html}

## Exercise 6-3: Lock and Unlock a User Account with usermod and passwd {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will disable the ability for user200 to log in
using the usermod and passwd commands. You will verify the change and
then reverse it.

\

1\. Obtain the current password information for user200 from the shadow
file:

\

<div>

![](image-CJ0NB6US.jpg){height="100%"}

</div>

An unlocked user account never has its password field begin with an
exclamation mark (!). The above output is indicative of the fact that
the account is currently not locked.

\

2\. Lock the account for user200:

\

<div>

![](image-VPDT4JEF.jpg){height="100%"}

</div>

3\. Confirm the change:

\

<div>

![](image-4MH6J3BG.jpg){height="100%"}

</div>

Notice that an exclamation mark (!) is prepended to the encrypted
password, which indicates a locked account.

\

4\. Unlock the account with either of the following:

\

<div>

![](image-98LS1470.jpg){height="100%"}

</div>

Verify the reversal with the grep command as demonstrated in step 3. You
can also try to log in as user200 for an additional validation. The grep
command is discussed in detail in Chapter 07 "The Bash Shell".

::: {style="page-break-before: always;"}
:::

[]{#chapter0208.html}

## Linux Groups and their Management {.style3}

\

Linux groups are collections of one or more users with identical
permission requirements on files and directories. They allow group
members to collaborate on files of common interest.

\

Group information is stored in the /etc/group file and the default
policies in the /etc/login.defsconfiguration file. Furthermore, the
/etc/gshadow file stores group administrator information and group-level
passwords. These files were thoroughly examined in Chapter 05 "Basic
User Management".

\

This section explores group management tools---groupadd, groupmod, and
groupdel---and looks at how to utilize them to create, alter, and erase
groups. Additional group administration operations, such as adding and
deleting group administrators, and setting and revoking group-level
passwords, are beyond the scope.

::: {style="page-break-before: always;"}
:::

[]{#chapter0209.html}

## The groupadd, groupmod, and groupdel Commands {.style3}

\

This set of management commands is used to add, modify, and delete a
group from the system. The groupadd command adds entries to the group
and gshadow files for each group added to the system. Table 6-4 lists
and explains some of the groupadd command options in both short and long
formats.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  -g (\--gid)                         Specifies the GID to be assigned to
                                      the group

  -o (\--non-unique)                  Creates a group with a matching GID
                                      of an existing group. When two
                                      groups have an identical GID,
                                      members of both groups get
                                      identical rights on each other's
                                      files. This should only be done in
                                      specific situations.

  -r                                  Creates a system group with a GID
                                      below 1000

  groupname                           Specifies a group name
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 6-4 groupadd Command Options

\

The groupadd command picks up the default values from the login.defs
file.

\

You can modify the attributes of a group with the groupmod command. The
syntax of this command is very similar to the groupadd with most options
identical. The only flag that is additional with this command is -n,
which can change the name of an existing group.

\

The groupdel command is straightforward. It removes entries for the
specified group from both group and gshadow files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0210.html}

## Exercise 6-4: Create a Group and Add Members {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will create a group called linuxadm with GID 5000
and another group called dba sharing the GID 5000. You will add user1 as
a secondary member to group dba.

\

1\. Create the group linuxadm with GID 5000:

\

<div>

![](image-EK83P8T1.jpg){height="100%"}

</div>

2\. Create a group called dba with the same GID as that of group
linuxadm:

\

<div>

![](image-3ABZFNJO.jpg){height="100%"}

</div>

3\. Confirm the creation of both groups:

\

<div>

![](image-NVG6IT5W.jpg){height="100%"}

</div>

The GID for both groups is identical.

\

4\. Add user1 as a secondary member of group dba using the usermod
command. The existing membership for the user must remain intact.

\

<div>

![](image-FQA7TJPF.jpg){height="100%"}

</div>

5\. Verify the updated group membership information for user1 by
extracting the relevant entry from the group file, and running the id
and groups command for user1:

\

<div>

![](image-YL0O61MT.jpg){height="100%"}

</div>

The output confirms the primary (user1) and secondary (dba) group
memberships for user1.

::: {style="page-break-before: always;"}
:::

[]{#chapter0211.html}

## Exercise 6-5: Modify and Delete a Group Account {.style3}

\

This exercise should be done on server1 as root.

\

In this exercise, you will change the linuxadm group name to sysadm and
the GID to 6000. You will add user200 to sysadm group as a secondary
member. You will remove the sysadm group and verify.

\

1\. Alter the name of linuxadm to sysadm:

\

<div>

![](image-WOL7VX6L.jpg){height="100%"}

</div>

2\. Change the GID of sysadm to 6000:

\

<div>

![](image-69RMTR9B.jpg){height="100%"}

</div>

3\. Add user200 to sysadm as a secondary member:

\

<div>

![](image-JQY3PU6R.jpg){height="100%"}

</div>

4\. Confirm the above actions:

\

<div>

![](image-9D5J49CZ.jpg){height="100%"}

</div>

The outputs confirm both actions. The new group name is sysadm and the
new GID is 6000. user200 is a member of the sysadm group. Also notice
that the linuxadm group does not exist anymore. The second command
returned nothing for it.

\

5\. Delete the sysadm group and confirm:

\

<div>

![](image-AM54G831.jpg){height="100%"}

</div>

The second command returns nothing, which confirms the group deletion.

::: {style="page-break-before: always;"}
:::

[]{#chapter0212.html}

## Substituting Users and Doing as Superuser {.style3}

\

In real world Linux environments, you'll always sign in as a normal
user. Normal users have limited rights on the system. Their profiles are
set to allow them to accomplish routine jobs efficiently and securely.
This is done to secure the overall system functionality and to prevent
unexpected issues. There are times though when a normal user needs to
assume the identity of a different user to carry out a task as that user
or execute a command successfully that requires elevated privileges.
Linux offers two fundamental tools to support users in both situations.

::: {style="page-break-before: always;"}
:::

[]{#chapter0213.html}

## Substituting (or Switching) Users {.style3}

\

Even though you can log in to the system directly as root, it is not a
recommended practice. Instead, log in with a normal user account and
then switch to the root account if necessary. This is safer and ensures
system security and protection. In addition to becoming root, you can
switch into another user account. In either case, you'll need to know
the password for the target user in order for a successful switch. The
su command has the ability to switch into other user accounts.

\

To switch from user1 (assuming you are logged in as user1) into root
without executing the startup scripts (startup scripts are explained
later in this chapter) for the target user, run the su command and enter
the root user password when prompted:

\

<div>

![](image-UTF9MKID.jpg){height="100%"}

</div>

Press Ctrl+d key combination to return to the user1 command prompt. Then
rerun the su command with the hyphen character (-) specified to ensure
that startup scripts for the target user are also executed to provide an
environment similar to that of a real login:

\

<div>

![](image-8P7PZ8GR.jpg){height="100%"}

</div>

To switch into a different user account, such as user100, specify the
name of the target user with the command. You must enter the password of
the target user when prompted.

\

<div>

![](image-KDULSR0D.jpg){height="100%"}

</div>

RHEL offers two tools---whoami (who am i) and logname (login
name)---that show a user's current identity (after su'ing into the
target user) and the identity of the user who originally logged in.
Let's see what they report after switching into user100:

\

<div>

![](image-NQLBEFMU.jpg){height="100%"}

</div>

The whoami command returns the effective (current) username (user100),
and the logname command reports the user's real (original) username
(user1).

\

To issue a command as a different user without switching into that user,
use the -c option with su. For example, the firewall-cmd command with
the \--list-services option requires superuser privileges. user1 can use
su as follows and execute this privileged command to obtain desired
results:

\

<div>

![](image-Z8FQI6D8.jpg){height="100%"}

</div>

The root user can switch into any user account that exists on the system
without being prompted for that user's password.

\

The firewall-cmd command is used to manage the Linux firewall at the
command line. It is discussed in detail in Chapter 19 "The Linux
Firewall".

\

Although the su command does provide the flexibility and convenience,
switching into the root account to execute privileged actions is not
recommended. There is a preferred method available in Linux that should
be used instead. The following section sheds light on it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0214.html}

## Doing as Superuser (or Doing as Substitute User) {.style3}

\

On production Linux servers, there are necessary steps to ensure that
users have the ability to carry out their assigned job without hassle.
In most cases, this requires privileged access to certain tools and
functions, which the root user is normally allowed to run.

\

RHEL provides normal users the ability to run a set of privileged
commands or to access non-owning files without the knowledge of the root
password. This allows the flexibility of assigning a specific command or
a set of commands to an individual user or a group of users based on
their needs. These users can then precede one of those commands with a
utility called sudo (superuser do, a.k.a. substitute user do) at the
time of executing that command. The users are prompted to enter their
own password, and if correct, the command is executed successfully for
them. The sudo utility is designed to provide protected access to
administrative functions as defined in the /etc/sudoers file or files in
the drop-in directory /etc/sudoers.d. It can also be used to allow a
user or a group of users to run scripts and applications owned by a
different user.

\

Any normal user that requires privileged access to administrative
commands or non-owning files is defined in the sudoers file. This file
may be edited with a command called visudo, which creates a copy of the
file as sudoers.tmp and applies the changes there. After the visudo
session is over, the updated file overwrites the original sudoers file
and sudoers.tmp is deleted. This is done to prevent multiple users
editing this file simultaneously.

\

The syntax for user and group entries in the file is similar to the
following example entries for user user1 and group dba:

\

  ----------------------- ----------------------- -----------------------
  user1                   ALL=(ALL)               ALL

  %dba                    ALL=(ALL)               ALL
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

These entries may be added to the beginning of the file, and they are
intended to provide full access to every administrative function to
user1 and members of the dba group (group is prefixed by the percentage
sign (%)). In other words, user1 and dba group members will have full
root user authority on the system.

\

When user1 or a dba group member attempts to access a privileged
function, they will be required to enter their own password. For
instance:

\

<div>

![](image-0YWP6JCH.jpg){height="100%"}

</div>

If you want user1 and dba group members not to be prompted for their
passwords, modify the entries in the sudoers file to look like:

\

  ----------------------- ----------------------- -----------------------
  user1                   ALL=(ALL)               NOPASSWD:ALL

  %dba                    ALL=(ALL)               NOPASSWD:ALL
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Rather than allowing them full access to the system, you can restrict
their access to the functions that they need access to. For example, to
limit their access to a single command /usr/bin/cat, modify the
directives as follows:

\

  ----------------------------------- -----------------------------------
  user1                               ALL=/usr/bin/cat

  %dba                                ALL=/usr/bin/cat
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

These users should now be able to use the cat command to view the
content of the /etc/sudoers or any other file that requires the root
privilege. Try cat /etc/sudoers as user1 and then again as sudo cat
/etc/sudoers. You will see the difference.

\

Configuring sudo to work the way it has just been explained may result
in a cluttered sudoers file with too many entries to fulfill diversified
needs of users and groups. A preferred method is to use predefined
aliases---User_Alias and Cmnd_Alias---to configure groups of users and
commands, and assign access as required. For instance, you can define a
Cmnd_Alias called PKGCMD containing yum and rpm package management
commands, and a User_Alias called PKGADM for user1, user100, and
user200. These users may or may not belong to the same Linux group.

\

Next, assign PKGCMD to PKGADM. This way one rule is set that allows a
group of users access to a group of commands. You can add or remove
commands and users anytime as needed, and the change will take effect
right away. Here is what this configuration will look like:

\

  ----------------------------------- -----------------------------------
  Cmnd_Alias                          PKGCMD = /usr/bin/yum, /usr/bin/rpm

  User_Alias                          PKGADM = user1, user100, user200

  PKGADM                              ALL = PKGCMD
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Append the above to the bottom of the sudoers file and then run the yum
or rpm command preceded by sudo as one of the users listed. You will be
able to perform software management tasks just like the root user.

\

The sudo command logs successful authentication and command data to the
/var/log/secure file under the name of the actual user executing the
command (and not root).

\

The sudoers file contains several examples with a brief explanation. It
is a good idea to look at those examples for additional understanding.

\

Now that the normal user user1 is added to the sudoers configuration
file, you will be using this user account with sudo where appropriate in
the examples and exercises in the remainder of the book.

::: {style="page-break-before: always;"}
:::

[]{#chapter0215.html}

## Owning User and Owning Group {.style3}

\

In Linux, every file and directory has an owner. By default, the creator
assumes the ownership, but this may be altered and allocated to a
different user if required.

\

Similarly, every user is a member of one or more groups. A group is a
collection of users with common permission requirements. By default, the
owner's group is assigned to a file or directory.

\

Let's create a file file1 as user1 in their home directory and exhibit
the file's long listing:

\

<div>

![](image-OMQMO2GZ.jpg){height="100%"}

</div>

The output indicates that the owner of file1 is user1 who belongs to
group user1. If you wish to view the corresponding UID and GID instead,
you can specify the -n option with the command:

\

<div>

![](image-BFQWNC1V.jpg){height="100%"}

</div>

Linux provides the chown and chgrp commands that can alter the ownership
and owning group for files and directories; however, you must have the
root user privilege to make these modifications.

::: {style="page-break-before: always;"}
:::

[]{#chapter0216.html}

## Exercise 6-6: Modify File Owner and Owning Group {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will first create a file file10 and a directory
dir10 as user1 under /tmp, and then change the ownership for file10 to
user100 and the owning group to dba in two separate transactions. Then
you'll apply ownership on file10 to user200 and owning group to user100
at the same time. Finally, you will change the two attributes on the
directory to user200:dba recursively. Make sure to use sudo where
necessary.

\

1\. Change into the /tmp directory and create file10 and dir10:

\

<div>

![](image-D7YT61QY.jpg){height="100%"}

</div>

2\. Check and validate that both attributes are set to user1:

\

<div>

![](image-WSGPH1TS.jpg){height="100%"}

</div>

3\. Set the ownership to user100 and confirm:

\

<div>

![](image-NCGYFBYV.jpg){height="100%"}

</div>

4\. Alter the owning group to dba and verify:

\

<div>

![](image-RVKU8H6A.jpg){height="100%"}

</div>

5\. Change the ownership to user200 and owning group to user100 and
confirm:

\

<div>

![](image-LGXEJQYG.jpg){height="100%"}

</div>

6\. Modify the ownership to user200 and owning group to dba recursively
on dir10 and validate:

\

<div>

![](image-77LMTNLZ.jpg){height="100%"}

</div>

You can also use ls -lR dir10 to view file and directory information
under dir10; however, it will show nothing as the directory is currently
empty.

::: {style="page-break-before: always;"}
:::

[]{#chapter0217.html}

## Chapter Summary {.style3}

\

At the outset, we described various aging attributes for user login and
password controls that are available to us. We also looked at files that
store default attributes that are applied to user accounts at the time
of their creation. These defaults may be modified if necessary.

\

Next, we modified aging attributes for certain user accounts with the
help of the tools we learned. We also employed a tool with a pair of
flags to deny and restore user access to the system.

\

We examined group management commands and used them in exercises to
create, modify, and delete group accounts, and add users to
supplementary groups. The set of the management commands is
straightforward and easy to use, but they require execution by a
privileged user.

\

We looked at a couple of tools towards the end of the chapter to switch
into other user accounts, including the root user, and to run privileged
commands as a normal user. The use of the latter tool is recommended.

\

Finally, we discussed ownership and owning groups on files and
directories, and how they are assigned. We performed exercises to
understand who can modify them and how.

::: {style="page-break-before: always;"}
:::

[]{#chapter0218.html}

## Review Questions {.style3}

\

1\. The chown command may be used to modify both ownership and group
membership on a file. True or False?

2\. What would the command passwd -n 7 -x 15 -w 3 user5 do?

3\. Write the two command names for managing all of the password aging
attributes.

4\. What would the command chage -d 0 user60 do?

5\. Which file has the default password aging settings defined?

6\. What would the command chage -E 2024-10-22 user10 do?

7\. What would the command chage -l user5 do?

8\. Which two commands can be used to lock and unlock a user account?

9\. When using sudo, log files record activities under the root user
account. True or False?

10\. What is the difference between running the su command with and
without the hyphen sign?

11\. What is the significance of the -o option with the groupadd and
groupmod commands?

12\. What would the entry user10 ALL=(ALL) NOPASSWD:ALL in the sudoers
file imply?

13\. Which command can be used to display the effective (current)
username?

14\. What is the recommended location to store custom sudo rules?

15\. What would the command passwd -l user10 do?

16\. The chgrp command may be used to modify both ownership and group
membership on a file. True or False?

::: {style="page-break-before: always;"}
:::

[]{#chapter0219.html}

## Answers to Review Questions {.style3}

\

1\. True.

2\. The command will set mindays to 7, maxdays to 15, and warndays to 3
for user5.

3\. The passwd and chage commands.

4\. The command provided will force user60 to change their password at
next login.

5\. The /etc/login.defs file has the defaults for password aging
defined.

6\. The command provided will set October 22, 2024, as the expiry date
for user10.

7\. The command provided will display password aging attributes for
user5.

8\. The usermod and passwd commands can be used to lock and unlock a
user account.

9\. False. The activities are registered under the username who invokes
the sudo command.

10\. With the dash sign the su command processes the specified user's
startup files, and it won't without this sign.

11\. The -o option lets the commands share a GID between two or more
groups.

12\. It will give user10 passwordless access to all privileged commands.

13\. The whoami command reports the effective username of the user
running this command.

14\. The custom sudo rules should be stored in files under the
/etc/sudoers.d directory.

15\. This command will lock user10.

16\. False.

::: {style="page-break-before: always;"}
:::

[]{#chapter0220.html}

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

[]{#chapter0221.html}

## Lab 6-1: Create User and Configure Password Aging {.style3}

\

As root on server3, create group lnxgrp with GID 6000. Create user
user5000 with UID 5000 and GID 6000. Assign this user a password, and
establish password aging attributes so that this user cannot change
their password within 4 days after setting it and with a password
validity of 30 days. This user should start getting warning messages for
changing password 10 days prior to account lock down. This user account
needs to expire on the 20th of December 2023. (Hint1: Chapter 05: Local
User Authentication Files, and User Account Management). (Hint2:
Password Aging and its Management, and Linux Groups and their
Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0222.html}

## Lab 6-2: Lock and Unlock User {.style3}

\

As root on server3, lock the user account for user5000 using the passwd
command, and confirm by examining the change in the /etc/shadow file.
Try to log in with user5000 and observe what happens. Use the usermod
command and unlock this account. Verify the unlocking by checking the
entry for the user in the /etc/shadow file. (Hint: Password Aging and
its Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0223.html}

## Lab 6-3: Modify Group {.style3}

\

As root on server3, modify the GID from 6000 to 7000 for the lnxgrp
group. Add users user1000 and user2000 as supplementary members (create
users if needed). Change the group's name to dbagrp, and verify. (Hint:
Linux Groups and their Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0224.html}

## Lab 6-4: Configure sudo Access {.style3}

\

As root on server3, add a rule for user5000 to the /etc/sudoers file to
allow this user full root access on the system. Make sure that this user
is not prompted for a password when they use sudo to execute a command.
Now switch into this user account and try running sudo vgs, and see if
that works. (Hint: Substituting Users and Doing as Superuser).

::: {style="page-break-before: always;"}
:::

[]{#chapter0225.html}

## Lab 6-5: Modify Owning User and Group {.style3}

\

As user1 on server3, create file f6 and directory d6 under /tmp. Change
owning user for f6 to user90 (create user) using sudo chown, and owning
group to dbagrp with sudo chgrp. Change owning user and group on d6 to
user90:g1 (create group) recursively using sudo chown. (Hint: Owing User
and Owning Group).

::: {style="page-break-before: always;"}
:::

[]{#chapter0226.html}

## Chapter 07 {style="text-align: right"}

\

### The Bash Shell {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Introduction to the bash shell

\

Understand, set, and unset shell and environment variables

\

Comprehend and use command and variable expansions

\

Grasp and utilize input, output, and error redirections

\

Know and use history substitution, command line editing, tab completion,
tilde substitution, and command aliasing

\

Identify and use metacharacters, wildcard characters, pipes, and
pipelines

\

Discover the use of quoting mechanisms and regular expressions

\

Identify and examine shell startup files

\

#### RHCSA Objectives:

\

##### 02. Use input-output redirection (\>, \>\>, \|, 2\>, etc.)

##### 03. Use grep and regular expressions to analyze text

::: {style="page-break-before: always;"}
:::

\

Shells allow users to interact with the operating system for execution
of their instructions through programs, commands, and applications. RHEL
supports a variety of shells of which the bash shell is the most common.
It is also the default shell for users in RHEL 9. This shell offers a
variety of features that help users and administrators perform their job
with ease and flexibility. Some of these features include recalling a
command from history and editing it at the command line before running
it, sending output and error messages to non-default target locations,
creating command shortcuts, sending output of one command as input to
the next, assigning the output of a command to a variable, using special
characters to match a string of characters, treating a special character
as a literal character, and so on.

\

::: {style="text-align: center;"}
![](image-2K3HBJX1.jpg){height="100%"}
:::

Regular expressions are text patterns for matching against an input
provided in a search operation. Text patterns may include any sequenced
or arbitrary characters or character range. RHEL offers a powerful
command to work with pattern matching.

\

At login, plenty of system and user startup scripts are executed to set
up the user environment. The system startup scripts may be customized
for all users by the Linux administrator and the user startup scripts
may be modified by individual users as per their need.

::: {style="page-break-before: always;"}
:::

[]{#chapter0227.html}

## The Bourne-Again Shell {.style3}

\

A shell is referred to as the command interpreter, and it is the
interface between a user and the Linux kernel. The shell accepts
instructions (commands) from users (or programs), interprets them, and
passes them on to the kernel for processing. The kernel utilizes all
hardware and software components required for a successful processing of
the instructions. When concluded, it returns the results to the shell,
which then exhibits them on the screen. The shell also shows appropriate
error messages, if generated. In addition, the shell delivers a
customizable environment to users.

\

A widely used shell by Linux users and administrators is the bash
(bourne-again shell) shell. Bash is a replacement for the older Bourne
shell with numerous enhancements and plenty of new features incorporated
from other shells. It is the default shell in most popular Linux
distributions including RHEL 9 and offers several features such as
variable manipulation, variable substitution, command substitution,
input and output redirections, history substitution, tab completion,
tilde substitution, alias substitution, metacharacters, pattern
matching, filename globbing, quoting mechanisms, conditional execution,
flow control, and shell scripting. This section discusses all of these
features except for the last three.

\

The bash shell is identified by the \$ sign for normal users and the \#
sign for the root user. The bash shell is resident in the /usr/bin/bash
file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0228.html}

## Shell and Environment Variables {.style3}

\

A variable is a transient storage for data in memory. It retains
information that is used for customizing the shell environment and
referenced by many programs to function properly. The shell stores a
value in a variable, and one or more white space characters must be
enclosed within quotation marks.

\

There are two types of variables: local (or shell) and environment. A
local variable is private to the shell in which it is created, and its
value cannot be used by programs that are not started in that shell.
This introduces the concept of current shell and sub-shell (or child
shell). The current shell is where a program is executed, whereas a
sub-shell (or child shell) is created within a shell to run a program.
The value of a local variable is only available in the current shell.

\

The value of an environment variable is inherited from the current shell
to the sub-shell during the execution of a program. In other words, the
value stored in an environment variable is accessible to the program, as
well as any sub-programs that it spawns during its lifecycle. Any
environment variable set in a sub-shell is lost when the sub-shell
terminates.

\

There are a multitude of predefined environment variables that are set
for each user upon logging in. Use the env or the printenv command to
view their values. Run these commands on server1 as user1 and observe
the output. There should be around 25 of them. Some of the common
predefined environment variables are described in Table 7-1.

\

  ----------------------------------- -----------------------------------
  Variable                            Description

  DISPLAY                             Stores the hostname or IP address
                                      for graphical terminal sessions

  HISTFILE                            Defines the file for storing the
                                      history of executed commands

  HISTSIZE                            Defines the maximum size for the
                                      HISTFILE

  HOME                                Sets the home directory path

  LOGNAME                             Retains the login name

  MAIL                                Contains the path to the user mail
                                      directory

  PATH                                Defines a colon-separated list of
                                      directories to be searched when
                                      executing a command. A correct
                                      setting of this variable eliminates
                                      the need to specify the absolute
                                      path of a command to run it.

  PPID                                Holds the identifier number for the
                                      parent program

  PS1                                 Defines the primary command prompt

  PS2                                 Defines the secondary command
                                      prompt

  PWD                                 Stores the current directory
                                      location

  SHELL                               Holds the absolute path to the
                                      primary shell file

  TERM                                Holds the terminal type value

  UID                                 Holds the logged-in user's UID

  USER                                Retains the name of the logged-in
                                      user
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 7-1 Common Predefined Environment Variables

\

RHEL provides the echo command to view the values stored in variables.
For instance, to view the value for the PATH variable, run the echo
command and ensure to prepend the variable name (PATH) with the \$ sign:

\

<div>

![](image-5GS9TC6O.jpg){height="100%"}

</div>

Try running echo \$HOME, echo \$SHELL, echo \$TERM, echo \$PPID, echo
\$PS1, and echo \$USER and see what values they store.

::: {style="page-break-before: always;"}
:::

[]{#chapter0229.html}

## Setting and Unsetting Variables {.style3}

\

Shell and environment variables may be set or unset at the command
prompt or via programs, and their values may be viewed and used as
necessary. We define and undefine variables and view their values using
built-in shell commands such as export, unset, and echo. It is
recommended to use uppercase letters to name variables so as to
circumvent any possible conflicts with a command, program, file, or
directory name that exist somewhere on the system. To understand how
variables are defined, viewed, made environment, and undefined, a few
examples are presented below. We run the commands as user1.

\

To define a local variable called VR1:

\

<div>

![](image-WPDFW9GI.jpg){height="100%"}

</div>

To view the value stored in VR1:

\

<div>

![](image-9WQZ779H.jpg){height="100%"}

</div>

Now type bash at the command prompt to enter a sub-shell and then run
echo \$VR1 to check whether the variable is visible in the sub-shell.
You will not find it there, as it was not an environment variable. Exit
out of the sub-shell by typing exit.

\

To make this variable an environment variable, use the export command:

\

<div>

![](image-BT1FTJSE.jpg){height="100%"}

</div>

Repeat the previous test by running the bash command and then the echo
\$VR1. You should be able to see the variable in the sub-shell, as it is
now an environment variable. Exit out of the sub-shell with the exit
command.

\

To undefine this variable and erase it from the shell environment:

\

<div>

![](image-AEZCZDUJ.jpg){height="100%"}

</div>

To define a local variable that contains a value with one or more white
spaces:

\

<div>

![](image-0FK5RU91.jpg){height="100%"}

</div>

To define and make the variable an environment variable at the same
time:

\

<div>

![](image-Q8O0VWMS.jpg){height="100%"}

</div>

The echo command is restricted to showing the value of a specific
variable and the env and printenv commands display the environment
variables only. If you want to view both local and environment
variables, use the set command. Try running set and observe the output.

::: {style="page-break-before: always;"}
:::

[]{#chapter0230.html}

## Command and Variable Substitutions {.style3}

\

The primary command prompt ends in the \# sign for the root user and in
the \$ sign for normal users. Customizing this prompt to exhibit useful
information such as who you are, the system you are logged on to, and
your current location in the directory tree is a good practice. By
default, this setting is already in place through the PS1 environment
variable, which defines the primary command prompt. You can validate
this information by looking at the command prompt \[user1@server1
\~\]\$.

\

You can also view the value stored in PS1 by issuing echo \$PS1. The
value is \\u@\\h \\W\\\$. The \\u translates into the logged-in
username, \\h represents the hostname of the system, \\W shows your
current working directory, and \\\$ indicates the end of the command
prompt.

\

[Exercise 7-1 demonstrates how to employ the command and variable
substitution features to customize the primary command prompt for user1.
You will use the hostname command and assign its output to the PS1
variable. This is an example of command substitution. Note that the
command whose output you want assigned to a variable must be
encapsulated within either backticks \`hostname\` or parentheses
\$(hostname).](#chapter0231.html)

\

There are two instances of the variable substitution feature employed in
Exercise 7-1. The LOGNAME and the PWD environment variables to display
the username and to reflect the current directory location.

::: {style="page-break-before: always;"}
:::

[]{#chapter0231.html}

## Exercise 7-1: Modify Primary Command Prompt {.style3}

\

This exercise should be done on server1 as user1.

\

In this exercise, you will customize the primary shell prompt to display
the information enclosed within the quotes "\< username on hostname in
pwd \>: " using the variable and command substitution features. You will
do this at the command prompt. You will then edit the \~/.bash_profile
file for user1 and define the new value in there for permanence (see
Shell Startup Files later in this chapter to understand the purpose of
.bash_profile), otherwise, the value will be lost when user1 closes the
terminal window or logs off.

\

1\. Change the value of the variable PS1 to reflect the desired
information:

\

<div>

![](image-7OGEOS7L.jpg){height="100%"}

</div>

The prompt has changed to display the desired information.

\

2\. Edit the .bash_profile file for user1 and define the value exactly
as it was run in Step 1.

3\. Test by logging off and logging back in as user1. The new command
prompt will be displayed.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0232.html}

## Input, Output, and Error Redirections {.style3}

\

Programs read input from the keyboard and write output to the terminal
window where they are initiated. Any errors, if encountered, are printed
on the terminal window too. This is the default behavior. The bash
handles input, output, and errors as character streams. If you do not
want input to come from the keyboard or output and error to go to the
terminal screen, the shell gives you the flexibility to redirect input,
output, and error messages to allow programs and commands to read input
from a non-default source, and forward output and errors to one or more
non-default destinations.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You may be asked to run a command and redirect its output
and/or error messages to a file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The default (or the standard) locations for the three streams are
referred to as standard input (or stdin), standard output (or stdout),
and standard error (or stderr). These locations may also be epitomized
using the opening angle bracket symbol (\<) for stdin, and the closing
angle bracket symbol (\>) for stdout and stderr. Alternatively, you may
use the file descriptors (the digits 0, 1, and 2) to represent the three
locations.

\

### Redirecting Standard Input {.style3}

Input redirection instructs a command to read input from an alternative
source, such as a file, instead of the keyboard. The opening angle
bracket (\<) is used for input redirection. For example, run the
following to have the cat command read the /etc/redhat-release file and
display its content on the standard output (terminal screen):

\

<div>

![](image-EK3MAMAX.jpg){height="100%"}

</div>

\

### Redirecting Standard Output {.style3}

Output redirection sends the output generated by a command to an
alternative destination, such as a file, instead of to the terminal
window. The closing angle bracket (\>) is used for this purpose. For
instance, the following directs the ls command output to a file called
ls.out. This will overwrite any existing ls.out file if there is one;
otherwise, a new file will be created.

\

<div>

![](image-OK6JB8LG.jpg){height="100%"}

</div>

The above can also be run as ls 1\> ls.out where the digit "1"
represents the standard output location.

\

If you want to prevent an inadvertent overwriting of the output file,
you can enable the shell's noclobber feature with the set command and
confirm its activation by re-issuing the above redirection example:

\

<div>

![](image-69YI6NBX.jpg){height="100%"}

</div>

You are denied the action.

\

You can disable the noclobber option by running set +o noclobber at the
command prompt.

\

To direct the ls command to append the output to the ls.out file instead
of overwriting it, use the two closing angle brackets (\>\>):

\

<div>

![](image-HVJTY278.jpg){height="100%"}

</div>

Again, the equivalent for the above is ls 1\>\> ls.out.

\

### Redirecting Standard Error {.style3}

Error redirection forwards any error messages generated to an
alternative destination rather than to the terminal window. An
alternative destination could be a file. For example, the following
directs the find command issued as a normal user to search for all
occurrences of files by the name core in the entire directory tree and
sends any error messages produced to /dev/null (/dev/null is a special
file that is used to discard data). This way only the useful output is
exhibited on the screen and errors are thrown away.

\

<div>

![](image-CSKLLD4A.jpg){height="100%"}

</div>

\

### Redirecting both Standard Output and Error {.style3}

You may redirect both output and error to alternative locations as well.
For instance, issue the following to forward them both to a file called
outerr.out:

\

<div>

![](image-S964X4SR.jpg){height="100%"}

</div>

This example will produce a listing of the /usr directory and save the
result in outerr.out. At the same time, it will generate an error
message complaining about the non-existence of /cdr, and it will send it
to the same file as well.

\

Another method to run the above command is by typing ls /usr /cdr 1\>
outerr.out 2\>&1, which essentially means to redirect file descriptor 1
to file outerr.out as well as to file descriptor 2.

\

You can exchange &\> with &\>\> in the above example to append the
information in the file rather than overwriting it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0233.html}

## History Substitution {.style3}

\

History substitution (a.k.a. command history or history expansion) is a
time-saver bash shell feature that keeps a log of all commands or
commandsets that you run at the command prompt in chronological order
with one command or commandset per line. The history feature is enabled
by default; however, you can disable and re-enable it if required. The
bash shell stores command history in a file located in the user's home
directory and in system memory. You may retrieve the commands from
history, modify them at the command prompt, and rerun them.

\

There are three variables---HISTFILE, HISTSIZE, and HISTFILESIZE---that
control the location and history storage. HISTFILE defines the name and
location of the history file to be used to store command history, and
the default is .bash_history in the user's home directory. HISTSIZE
dictates the maximum number of commands to be held in memory for the
current session. HISTFILESIZE sets the maximum number of commands
allowed for storage in the history file at the beginning of the current
session and are written to the HISTFILE from memory at the end of the
current terminal session. Usually, HISTSIZE and HISTFILESIZE are set to
a common value. These variables and their values can be viewed with the
echo command. The following shows the settings for user1:

\

<div>

![](image-ZCW97PGT.jpg){height="100%"}

</div>

The values of any of these variables may be altered for individual users
by editing the .bashrc or .bash_profile file in the user's home
directory. A discussion on these files is provided later in this
chapter.

\

In RHEL, the history command displays or reruns previously executed
commands. This command gets the history data from the system memory as
well as from the .bash_history file. By default, it shows all entries.
Run this command at the prompt without any options and it will dump
everything on the screen:

\

<div>

![](image-NRYZJRO3.jpg){height="100%"}

</div>

The history command has some useful options. Let's use them and observe
the impact on the output.

\

To display this command and the ten preceding entries:

\

<div>

![](image-3KBPB5XG.jpg){height="100%"}

</div>

To re-execute a command by its line number (line 15 for example):

\

<div>

![](image-2JUC75PN.jpg){height="100%"}

</div>

To re-execute the most recent occurrence of a command that started with
a particular letter or series of letters (ch for example):

\

<div>

![](image-02DCY2V0.jpg){height="100%"}

</div>

To issue the most recent command that contained "grep":

\

<div>

![](image-3UIHU0VP.jpg){height="100%"}

</div>

To remove entry 24 from history:

\

<div>

![](image-L6LOII03.jpg){height="100%"}

</div>

To repeat the last command executed:

\

<div>

![](image-6ZQ8SXMQ.jpg){height="100%"}

</div>

The second exclamation mark (!) in the above example is used to retrieve
the last executed command.

\

You may disable the shell's history expansion feature by issuing set +o
history at the command prompt and re-enable it with set -o history. The
set command is used in this way to enable or disable a bash shell
feature.

::: {style="page-break-before: always;"}
:::

[]{#chapter0234.html}

## Editing at the Command Line {.style3}

\

While typing a command with a multitude of options and arguments at the
command prompt, you often need to move the cursor backward to add or
modify something. For instance, if you are typing a long command as a
normal user and then realize the command needs to have sudo added at the
beginning, move the cursor quickly to the start of the command. This is
a shortcut to save time. There are plenty of key combinations for rapid
movement on the command line. Table 7-2 lists and explains several of
these.

\

  ----------------------------------- -----------------------------------
  Key Combinations                    Action

  Ctrl+a / Home                       Moves the cursor to the beginning
                                      of the command line

  Ctrl+e / End                        Moves the cursor to the end of the
                                      command line

  Ctrl+u                              Erase the entire line

  Ctrl+k                              Erase from the cursor to the end of
                                      the command line

  Alt+f                               Moves the cursor to the right one
                                      word at a time

  Alt+b                               Moves the cursor to the left one
                                      word at a time

  Ctrl+f / Right arrow                Moves the cursor to the right one
                                      character at a time

  Ctrl+b / Left arrow                 Moves the cursor to the left one
                                      character at a time
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 7-2 Helpful Command Line Editing Shortcuts

\

For normal users and administrators who often work at the command line,
these key combinations will be very helpful in saving time.

::: {style="page-break-before: always;"}
:::

[]{#chapter0235.html}

## Tab Completion {.style3}

\

Tab completion (a.k.a. command line completion) is a bash shell feature
whereby typing one or more initial characters of a file, directory, or
command name at the command line and then hitting the Tab key twice
automatically completes the entire name. In case of multiple
possibilities matching the entered characters, it completes up to the
point they have in common and prints the rest of the possibilities on
the screen. You can then type one or more following characters and press
Tab again to further narrow down the possibilities. When the desired
name appears, press Enter to accept it and perform the action. One of
the major benefits of using this feature is the time saved on typing
long file, directory, or command names.

\

Try this feature out on your Linux terminal window and get yourself
familiarized with it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0236.html}

## Tilde Substitution {.style3}

\

Tilde substitution (or tilde expansion) is performed on words that begin
with the tilde character (\~). The rules to keep in mind when using the
\~ are:

\

1\. If \~ is used as a standalone character, the shell refers to the
\$HOME directory of the user running the command. The following example
displays the \$HOME directory of user1:

\

<div>

![](image-7UWB1S17.jpg){height="100%"}

</div>

2\. If the plus sign (+) follows the \~, the shell refers to the current
directory. For example, if user1 is in the /usr/bin directory and does
\~+, the output exhibits the user's current directory location:

\

<div>

![](image-9NMAPSC0.jpg){height="100%"}

</div>

3\. If the hyphen character (-) follows the \~, the shell refers to the
previous working directory. For example, if user1 switches into the
/usr/share/man directory from /usr/bin and does \~-, the output displays
the user's last working directory:

\

<div>

![](image-GY13GV9O.jpg){height="100%"}

</div>

4\. If a username has the \~ prepended, the shell refers to the \$HOME
directory of that user:

\

<div>

![](image-G7UFKIUF.jpg){height="100%"}

</div>

Tilde substitution can also be used with commands such as cd and ls. For
instance, to cd into the home directory of user1 (or any other user for
that matter) from anywhere in the directory structure, specify the login
name with the \~:

\

<div>

![](image-Q5FWRT44.jpg){height="100%"}

</div>

This command is only successful if user1 has the right permissions to
navigate into the target user's home directory. Let's try this example
as the root user:

\

<div>

![](image-PPS5MWSH.jpg){height="100%"}

</div>

The above example demonstrates the navigation into the home directory of
user100 as the root user. By default, root has full rights to cd into
any users' home directory.

\

Another example below exhibits how a user can cd into one of their
subdirectories (such as /home/user1/dir1) directly from anywhere
(/etc/systemd/system) in the directory structure (create dir1 for this
test):

\

<div>

![](image-8THMO19P.jpg){height="100%"}

</div>

Try using the \~ with the ls command. For example, run sudo ls -ld
\~root/Desktop as user1.

::: {style="page-break-before: always;"}
:::

[]{#chapter0237.html}

## Alias Substitution {.style3}

\

Alias substitution (a.k.a. command aliasing or alias) allows you to
define a shortcut for a lengthy and complex command or a set of
commands. Defining and using aliases saves time and saves you from
typing. The shell executes the corresponding command or commandset when
an alias is run.

\

The bash shell includes several predefined aliases that are set during
user login. These aliases may be viewed with the alias command. The
following shows all the aliases that are currently set for user1:

\

<div>

![](image-3T256Z47.jpg){height="100%"}

</div>

There are a few additional default aliases set for the root user. Run
alias as root:

\

<div>

![](image-B6OF4RJE.jpg){height="100%"}

</div>

Many aliases have the option "color" set to auto, which implies that the
output will highlight the file names and pattern matches in a color.
Table 7-3 describes the common aliases from the previous two outputs.

\

  ----------------------- ----------------------- -----------------------
  Alias                   Value                   Definition

  cp                      cp -i                   Issues the cp command
                                                  in interactive mode

  ll                      ls -l                   Shows the ls command
                                                  output in long format

  mv                      mv -i                   Executes the mv command
                                                  in interactive mode

  rm                      rm -i                   Runs the rm command in
                                                  interactive mode
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Table 7-3 Predefined Aliases

\

In addition to listing the set aliases, the alias command can also be
used to define new aliases. The opposite function of unsetting an alias
is performed with the unalias command. Both alias and unalias are
internal shell commands. Let's look at a few examples.

\

Create an alias "search" to abbreviate the find command with several
switches and arguments. Enclose the entire command within single
quotation marks ('') to ensure white spaces are taken care of. Do not
leave any spaces before and after the equal sign (=).

\

<div>

![](image-4WR8W83A.jpg){height="100%"}

</div>

Now, when you type the string "search" at the command prompt and press
the Enter key, the shell will trade the alias "search" with what is
stored in it and will run it. Essentially, you have created a shortcut
to that lengthy command.

\

Sometimes you define an alias by a name that matches the name of some
system command or program. In this situation, the shell gives the
execution precedence to the alias. This means the shell will run the
alias and not the command or the program. For example, the rm command
deletes a file without giving any warning if run as a normal user. To
prevent accidental deletion of files with rm, you may create an alias by
the same name as the command but with the interactive option added, as
shown below:

\

<div>

![](image-LI5IDFOB.jpg){height="100%"}

</div>

When you execute rm now to remove a file, the shell will run what is
stored in the rm alias and not the command rm. If you wish to run the rm
command instead, run it by preceding a backslash (\\) with it:

\

<div>

![](image-8U2YK2N3.jpg){height="100%"}

</div>

You can use the unalias command to unset one or more specified aliases
if they are no longer in need. The following will undefine the two
aliases that were defined for our examples:

\

<div>

![](image-XWV4OMK3.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0238.html}

## Metacharacters and Wildcard Characters {.style3}

\

Metacharacters are special characters that possess special meaning to
the shell. Some of them are the dollar sign (\$), caret (\^), period
(.), asterisk (\*), question mark (?), pipe (\|), angle brackets (\<
\>), curly brackets ({}), square brackets (\[\]), parentheses (()), plus
(+), exclamation mark (!), semicolon (;), and backslash (\\) characters.
They are used in pattern matching (a.k.a. filename expansion or file
globbing) and regular expressions. This sub-section discusses the
metacharacters (\* ? \[\] !) that are used in pattern matching. The \*,
?, and \[\] characters are also referred to as wildcard characters.

\

### The \* Character {.style3}

The asterisk (\*) matches zero to an unlimited number of characters
except for the leading period (.) in a hidden filename. See the
following examples on usage.

\

To list all files in the /etc directory that begin with letters "ma" and
followed by any characters:

\

<div>

![](image-7LPDVJU5.jpg){height="100%"}

</div>

To list all hidden files and directories in /home/user1:

\

<div>

![](image-EH3IVN5U.jpg){height="100%"}

</div>

To list all files in the /var/log directory that end in ".log":

\

<div>

![](image-3OTPZU65.jpg){height="100%"}

</div>

The \* is probably the most common metacharacter that is used in pattern
matching.

\

### The ? Character {.style3}

The question mark (?) matches exactly one character except for the
leading period in a hidden filename. See the following example to
understand its usage.

\

To list all files and directories under /var/log with exactly four
characters in their names:

\

<div>

![](image-57GHFDSP.jpg){height="100%"}

</div>

The ? is another metacharacter that is used widely in pattern matching.

\

### The Square Brackets \[\] and the Exclamation Mark ! {.style3}

The square brackets (\[\]) can be used to match either a set of
characters or a range of characters for a single character position.

\

For a set of characters specified in this enclosure, the order in which
they are listed has no importance. This means the shell will interpret
\[xyz\], \[yxz\], \[xzy\], and \[zyx\] alike during pattern matching. In
the following example, two characters are enclosed within the square
brackets. The output will include all files and directories that begin
with either of the two characters and followed by any number of
characters.

\

<div>

![](image-QYKB8Q0A.jpg){height="100%"}

</div>

A range of characters must be specified in a proper sequence such as
\[a-z\] or \[0-9\]. The following example matches all directory names
that begin with any letter between "m" and "o" in the
/etc/systemd/system directory:

\

<div>

![](image-2IEV1IYG.jpg){height="100%"}

</div>

The shell enables the exclamation mark (!) to inverse the matches. For
instance, \[!a-d\]\* would exclude all filenames that begin with any of
the first four alphabets. The following example will produce the reverse
of what the previous example did:

\

<div>

![](image-830BNNQZ.jpg){height="100%"}

</div>

The output will have a multitude of filenames printed.

::: {style="page-break-before: always;"}
:::

[]{#chapter0239.html}

## Piping Output of One Command as Input to Another {.style3}

\

The pipe, represented by the vertical bar (\|) and normally resides with
the backslash (\\) on most keyboards, is used to send the output of one
command as input to the next. This character is also used to define
alternations in regular expressions. You can use the pipe operator as
many times in a command as you require.

\

The /etc directory contains plenty of files, but they all do not fit on
one terminal screen when you want to see its long listing. You can use
the pipe operator to pipe the output to the less command in order to
view the directory listing one screenful at a time:

\

<div>

![](image-D2C20HIJ.jpg){height="100%"}

</div>

In another example, the last command is run and its output is piped to
the nl command to number each output line:

\

<div>

![](image-JYEYMUD9.jpg){height="100%"}

</div>

\

The nl command reveals numbering for each line in the output.

\

The following example sends the output of ls to grep for the lines that
do not contain the pattern "root". The new output is further piped for a
case-insensitive selection of all lines that exclude the pattern "dec".
The filtered output is numbered, and the final result shows the last
four lines on the display.

\

<div>

![](image-CSXAKP5Z.jpg){height="100%"}

</div>

A construct like the above with multiple pipes is referred to as a
pipeline.

::: {style="page-break-before: always;"}
:::

[]{#chapter0240.html}

## Quoting Mechanisms {.style3}

\

As you know, metacharacters have special meaning to the shell. In order
to use them as regular characters, the bash shell offers three quoting
mechanisms to disable their special meaning and allow the shell to treat
them as literal characters. These mechanisms are available through the
use of the backslash (\\), single quotation (''), and double quotation
("") characters, and work by prepending a special character to the
backslash, or enclosing it within single or double quotation marks.

\

### Prefixing with a Backslash \\ {.style3}

The backslash character (\\), also referred to as the escape character
in shell terminology, instructs the shell to mask the meaning of any
special character that follows it. For example, if a file exists by the
name \* and you want to remove it with the rm command, you will have to
escape the \* so that it is treated as a regular character, not as a
wildcard character.

\

<div>

![](image-3JAUF7Y9.jpg){height="100%"}

</div>

In the above example, if you forget to escape the \*, the rm command
will remove all files from the directory.

\

### Enclosing within Single Quotes '' {.style3}

The single quotation marks ('') instructs the shell to mask the meaning
of all encapsulated special characters. For example, LOGNAME is a
variable, and its value can be viewed with the echo command:

\

<div>

![](image-7KSYB8AX.jpg){height="100%"}

</div>

If you encapsulate \$LOGNAME within single quotes, the echo command will
exhibit the entire string as is:

\

<div>

![](image-KS93V35S.jpg){height="100%"}

</div>

In the above example, the shell interprets the \$ sign as a literal
character, and that's why the echo command displays what is inside the
enclosure, including the \$ rather than the value of the variable.

\

### Enclosing within Double Quotes "" {.style3}

The double quotation marks ("") commands the shell to mask the meaning
of all but the backslash (\\), dollar sign (\$), and single quotes ('').
These three special characters retain their special meaning when they
are enclosed within double quotes. Look at the following examples to
understand its usage.

\

<div>

![](image-X7PFNPD6.jpg){height="100%"}

</div>

The above three instances confirm the use of the double quotes as a
special character pair, as depicted in the outputs.

::: {style="page-break-before: always;"}
:::

[]{#chapter0241.html}

## Regular Expressions {.style3}

\

A regular expression, also referred to as a regexp or simply regex, is a
text pattern or an expression that is matched against a string of
characters in a file or supplied input in a search operation. The
pattern may include a single character, multiple random characters, a
range of characters, word, phrase, or an entire sentence. Any pattern
containing one or more white spaces must be surrounded by quotation
marks.

\

RHEL provides a powerful tool called grep (global regular expression
print or get regular expression and print) to work with pattern matching
in regular expressions. This tool searches the contents of one or more
text files or input supplied for a match. If the expression is matched,
grep prints every line containing that expression on the screen without
changing the source content. grep has plenty of options and it accepts
expressions in various forms.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: The grep command is a handy tool to extract needed information
from a file or command output. The extracted information can then be
redirected to a file. The sequence of the grep'ed data remains
unchanged.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Let's consider the following examples to comprehend the usage of the
grep command.

\

To search for the pattern "operator" in the /etc/passwd file:

\

<div>

![](image-IE9HSIXA.jpg){height="100%"}

</div>

To search for the space-separated pattern "aliases and functions" in the
\$HOME/.bashrc file:

\

<div>

![](image-89EF7JW6.jpg){height="100%"}

</div>

To search for the pattern "nologin" in the passwd file and exclude (-v)
the lines in the output that contain this pattern. Add the -n switch to
show the line numbers associated with the matched lines.

\

<div>

![](image-61ZRASOW.jpg){height="100%"}

</div>

To find any duplicate entries for the root user in the passwd file.
Prepend the caret sign (\^) to the pattern "root" to mark the beginning
of a line.

\

<div>

![](image-D43UXGPI.jpg){height="100%"}

</div>

To identify all users in the passwd file with bash as their primary
shell. Append the \$ sign to the pattern "bash" to mark the end of a
line.

\

<div>

![](image-Q8HN7IKE.jpg){height="100%"}

</div>

To show the entire login.defs file but exclude all the empty lines:

\

<div>

![](image-0PVWFTJ7.jpg){height="100%"}

</div>

To perform a case-insensitive search (-i) for all the lines in the
/etc/bashrc file that match the pattern "path."

\

<div>

![](image-HN9UC2YR.jpg){height="100%"}

</div>

To print all the lines from the /etc/lvm/lvm.conf file that contain an
exact match for a word (-w). You can use the period character (.) in the
search string to match a single position. The following example searches
for words in the lvm.conf file that begin with letters "acce" followed
by exactly two characters:

\

<div>

![](image-ZDZ90S3C.jpg){height="100%"}

</div>

In addition to the caret (\^), dollar (\$), and period (.), the asterisk
(\*), question mark (?), square brackets (\[\]), and curly brackets ({})
are also used in regular expressions.

\

To print all the lines from the ls command output that include either
(-E) the pattern "cron" or "ly". The pipe \| character is used as an OR
operator in this example. This is referred to as alternation. Regex
allows you to add more patterns to this set if desired. For instance, if
you search for three patterns, use 'pattern1\|pattern2\|pattern3'. The
patterns must be enclosed within single or double quotes. Here is what
you will issue when you want to look for the patterns "cron" and "ly" in
the /etc directory listing:

\

<div>

![](image-XVP75PQA.jpg){height="100%"}

</div>

To show all the lines from the /etc/ssh/sshd_config file but exclude
(-v) the empty lines and the rows that begin with the hash (#) character
(commented lines). Using the -e flag multiple times as shown below is
equivalent to how "-E 'pattern1\|pattern2'" was used in the above
example.

\

<div>

![](image-JKKKW4GX.jpg){height="100%"}

</div>

You can combine options and employ diverse regular expression criteria
to perform complex matches on input. Issue man 7 regex in a terminal
window to learn more about regex. Also consult the manual pages of the
grep command to view available options and other details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0242.html}

## Shell Startup Files {.style3}

\

Earlier in this chapter, you used local and environment variables and
learned how to modify the primary command prompt to add useful
information to it. In other words, you modified the default shell
environment to suit your needs. You stored the PS1 value in a shell
startup file to ensure the changes are always available after you log
off and log back in.

\

Modifications to the default shell environment can be stored in startup
(or initialization) files. These files are sourced by the shell
following user authentication at the time of logging in and before the
command prompt appears. In addition, aliases, functions, and scripts can
be added to these files as well. There are two types of startup files:
system-wide and per-user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0243.html}

## System-wide Shell Startup Files

\

System-wide startup files set the general environment for all users at
the time of their login to the system. These files are located in the
/etc directory and are maintained by the Linux administrator.
System-wide files can be modified to include general environment
settings and customizations.

\

[Table 7-4 lists and describes system-wide startup files for bash shell
users.](#chapter0243.html)

\

  ----------------------------------- -----------------------------------
  File                                Comments

  /etc/bashrc                         Defines functions and aliases, sets
                                      umask for user accounts with a
                                      non-login shell, establishes the
                                      command prompt, etc. It may include
                                      settings from the shell scripts
                                      located in the /etc/profile.d
                                      directory.

  /etc/profile                        Sets common environment variables
                                      such as PATH, USER, LOGNAME, MAIL,
                                      HOSTNAME, HISTSIZE, and HISTCONTROL
                                      for all users, establishes umask
                                      for user accounts with a login
                                      shell, processes the shell scripts
                                      located in the /etc/profile.d
                                      directory, and so on.

  /etc/profile.d                      Contains scripts for bash shell
                                      users that are executed by the
                                      /etc/profile file.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 7-4 System-wide Startup Files

\

Excerpts from the bashrc and profile files and a list of files in the
profile.d directory are displayed below:

\

<div>

![](image-NRO2CSNF.jpg){height="100%"}

</div>

Any file in the profile.d directory can be edited and updated.
Alternatively, you can create your own file and define any customization
that you want.

::: {style="page-break-before: always;"}
:::

[]{#chapter0244.html}

## Per-user Shell Startup Files

\

Per-user shell startup files override or modify system default
definitions set by the system-wide startup files. These files may be
customized by individual users to suit their needs. By default, two such
files, in addition to the .bash_logout file, are located in the skeleton
directory /etc/skel and are copied into user home directories at the
time of user creation.

\

You may create additional files in your home directories to set more
environment variables or shell properties if required.

\

[Table 7-5 lists and describes per-user startup files for bash shell
users.](#chapter0244.html)

\

  ----------------------------------- -----------------------------------
  File                                Comments

  .bashrc                             Defines functions and aliases. This
                                      file sources global definitions
                                      from the /etc/bashrc file.

  .bash_profile                       Sets environment variables and
                                      sources the .bashrc file to set
                                      functions and aliases.

  .gnome2/                            Directory that holds environment
                                      settings when GNOME desktop is
                                      started. Only available if GNOME is
                                      installed.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 7-5 Per-user Startup Files

\

Excerpts from the .bashrc and .bash_profile files are exhibited below:

\

<div>

![](image-I4JTBKFM.jpg){height="100%"}

</div>

The order in which the system-wide and per-user startup files are
executed is important to grasp. The system runs the /etc/profile file
first, followed by .bash_profile, .bashrc, and finally the /etc/bashrc
file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: For persistence, per-user settings must be added to an
appropriate file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

There is also a per-user file .bash_logout in the user's home directory.
This file is executed when the user leaves the shell or logs off. This
file may be customized as well.

::: {style="page-break-before: always;"}
:::

[]{#chapter0245.html}

## Chapter Summary {.style3}

\

In this chapter, we explored the bash shell, which has numerous features
that are essential for users and administrators alike. We touched upon a
few that are more prevalent. These features included variable settings,
command prompt customization using substitution techniques,
input/output/error redirections, history expansion, command line
editing, filename completion, tilde substitution, and command aliasing.

\

We continued to examine additional bash shell features and expanded on
metacharacters, wildcard characters, pipe symbol, and quoting
mechanisms. We demonstrated an example of building a pipeline by
incorporating multiple pipe characters between commands.

\

Finally, we analyzed various system-wide and per-user shell
initialization scripts that are executed upon logging in to set a user
environment. These scripts may be customized for all users or individual
users to suit specific needs.

::: {style="page-break-before: always;"}
:::

[]{#chapter0246.html}

## Review Questions {.style3}

\

1\. What would the command ls /cdr /usr \> output do? Assume /cdr does
not exist.

2\. What is the name of the command that allows a user to define
shortcuts to lengthy commands?

3\. Which file typically defines the history variables for all users?

4\. You have a command running that is tied to your terminal window. You
want to get the command prompt back without terminating the running
command. Which key combination would you press to return to the command
prompt?

5\. Name the three quoting mechanisms?

6\. What would the command export VAR1="I passed RHCSA" do?

7\. Name the default filename and location where user command history is
stored?

8\. What is the primary function of the shell in Linux?

9\. What would the command cd \~user20 do if executed as user10?

10\. You want to change the command prompt for yourself. Where (the bash
shell file) would you define it so that you get the custom command
prompt whenever you log in?

11\. What is the other name for the command line completion feature?

12\. What is a common use of the pipe symbol?

13\. Which directory location stores most, if not all, privileged
commands?

14\. You have a file called "?" in your home directory along with other
one-letter files. What would you run to delete the "?" file only?

15\. Which command would you use to display all matching lines from a
text file?

16\. What would the command ls \> ls.out do?

::: {style="page-break-before: always;"}
:::

[]{#chapter0247.html}

## Answers to Review Questions {.style3}

\

1\. The command provided will redirect ls /usr output to the specified
file and ls /cdr (error) to the terminal.

2\. The alias command.

3\. /etc/profile is the file where the history variables are defined for
all users.

4\. The Ctrl+z key combination will suspend the running program and give
you access to the command prompt.

5\. The three quoting mechanisms are backslash, single quotation mark,
and double quotation mark.

6\. The command provided will set an environment variable with the
quoted string as its value.

7\. The user command history is stored in \~/.bash_history file.

8\. The shell acts as an interface between a user and the system.

9\. The command provided will allow user10 to cd into user20's home
directory provided user10 has proper access permissions.

10\. You can define it in the \~/.bash_profile file.

11\. The other name for the command line completion feature is tab
completion.

12\. A common use of the pipe character is to receive the output of one
command and pass it along to the next command as an input.

13\. Privileged commands are stored in /usr/sbin directory.

14\. You can issue rm \\? to remove the file.

15\. The grep command.

16\. The command provided will redirect the ls command output to the
specified file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0248.html}

## Do-It-Yourself Challenge Labs {.style3}

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

[]{#chapter0249.html}

## Lab 7-1: Customize the Command Prompt {.style3}

\

As user1 on server3, customize the primary shell prompt to display the
information enclosed within the quotes "\<user1@server1 in /etc \>: "
when this user switches into the /etc directory. The prompt should
always reflect the current directory path. Add this to the appropriate
per-user startup file for permanence. (Hint: Command and Variable
Substitutions).

::: {style="page-break-before: always;"}
:::

[]{#chapter0250.html}

Lab 7-2: Redirect the Standard Input, Output, and Error

\

As user1 on server3, run the ls command on /etc, /dvd, and /var. Have
the output printed on the screen and the errors forwarded to file
/tmp/ioerror. Check both files after the command execution and analyze
the results. (Hint: Input, Output, and Error Redirections).

::: {style="page-break-before: always;"}
:::

[]{#chapter0251.html}

## Chapter 08 {style="text-align: right"}

\

### Linux Processes and Job Scheduling {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Identify and display system and user executed processes

\

View process states and priorities

\

Examine and change process niceness and priority

\

Understand signals and their use in controlling processes

\

Review job scheduling

\

Control who can schedule jobs

\

Schedule and manage jobs (tasks) using at

\

Comprehend crontab and understand the syntax of crontables

\

Schedule and manage jobs using cron

\

#### RHCSA Objectives:

\

19\. Identify CPU/memory intensive processes, adjust process priority
with renice, and kill processes

20\. Adjust process scheduling

38\. Schedule tasks using at and cron

::: {style="page-break-before: always;"}
:::

\

Aprocess is any program, command, or application running on the system.
Every process has a unique numeric identifier, and it is managed by the
kernel through its entire lifespan. It may be viewed, listed, and
monitored, and can be launched at a non-default priority based on the
requirement and available computing resources. A process may also be
re-prioritized while it is running. A process is in one of several
states at any given time during its lifecycle. A process may be tied to
the terminal window where it is initiated, or it may run on the system
as a service.

\

There are plenty of signals that may be passed to a process to
accomplish various actions. These actions include hard killing a
process, soft terminating it, and forcing it to restart with the same
identifier.

\

::: {style="text-align: center;"}
![](image-BR20BNCA.jpg){height="100%"}
:::

Job scheduling allows a user to schedule a command for a one-time or
recurring execution in the future. A job is submitted and managed by
authorized users only. All executed jobs are logged.

::: {style="page-break-before: always;"}
:::

[]{#chapter0252.html}

## Processes and Priorities {.style3}

\

A process is a unit for provisioning system resources. It is any
program, application, or command that runs on the system. A process is
created in memory when a program, application, or command is initiated.
Processes are organized in a hierarchical fashion. Each process has a
parent process (a.k.a. a calling process) that spawns it. A single
parent process may have one or many child processes and passes many of
its attributes to them at the time of their creation. Each process is
assigned an exclusive identification number known as the Process
IDentifier (PID), which is used by the kernel to manage and control the
process through its lifecycle. When a process completes its lifespan or
is terminated, this event is reported back to its parent process, and
all the resources provisioned to it (cpu cycles, memory, etc.) are then
freed and the PID is removed from the system.

\

Plenty of processes are spawned at system boot, many of which sit in the
memory and wait for an event to trigger a request to use their services.
These background system processes are called daemons and are critical to
system operation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0253.html}

## Process States {.style3}

\

A process changes its operating state multiple times during its
lifecycle. Many factors, such as load on the processor, availability of
free memory, priority of the process, and response from other
applications, affect how often a process jumps from one operating state
to another. It may be in a non-running condition for a while or waiting
for other process to feed it information so that it can continue to run.

\

There are five basic process states: running, sleeping, waiting,
stopped, and zombie. Each process is in one state at any given time. See
Figure 8-1.

\

::: {style="text-align: center;"}
![](image-5YWJN0KN.jpg){height="100%"}
:::

Figure 8-1 Process State Transition

\

Running: The process is being executed by the system CPU.

Sleeping: The process is waiting for input from a user or another
process.

Waiting: The process has received the input it was waiting for and is
now ready to run as soon as its turn comes.

Stopped: The process is currently halted and will not run even when its
turn comes unless a signal is sent to change its behavior. (Signals are
explained later in this chapter.)

Zombie: The process is dead. A zombie process exists in the process
table alongside other process entries, but it takes up no resources. Its
entry is retained until its parent process permits it to die. A zombie
process is also called a defunct process.

::: {style="page-break-before: always;"}
:::

[]{#chapter0254.html}

## Viewing and Monitoring Processes with ps {.style3}

\

A system may have hundreds or thousands of processes running
concurrently depending on the purpose of the system. These processes may
be viewed and monitored using various native tools such as ps (process
status) and top (table of processes). The ps command offers plentiful
switches that influence its output, whereas top is used for real-time
viewing and monitoring of processes and system resources.

\

Without any options or arguments, ps lists processes specific to the
terminal where this command is issued:

\

<div>

![](image-2T0S653J.jpg){height="100%"}

</div>

The above output returns the elementary information about processes in
four columns. These processes are tied to the current terminal window.
It exhibits the PID, the terminal (TTY) the process spawned in, the
cumulative time (TIME) the system CPU has given to the process, and the
name of the actual command or program (CMD) being executed.

\

Some common options that can be used with the ps command to generate
detailed reports include -e (every), -f (full-format), -F (extra
full-format), and -l (long format). A combination of -e, -F, and -l (ps
-eFl) produces a very thorough process report, however, that much detail
may not be needed in most situations. Other common options such as
\--forest and -x will report the output in tree-like hierarchy and
include the daemon processes as well. Check the manual pages of the
command for additional options and their usage.

\

Here are a few sample lines from the beginning and end of the output
when ps is executed with -e and -f flags on the system.

\

<div>

![](image-QQABWO1C.jpg){height="100%"}

</div>

This output is disseminated across eight columns showing details about
every process running on the system. Table 8-1 describes the content
type of each column.

\

  ----------------------------------- -----------------------------------
  Column                              Description

  UID                                 User ID or name of the process
                                      owner

  PID                                 Process ID of the process

  PPID                                Process ID of the parent process

  C                                   CPU utilization for the process

  STIME                               Process start date or time

  TTY                                 The controlling terminal the
                                      process was started on. "Console"
                                      represents the system console and
                                      "?" represents a daemon process.

  TIME                                Aggregated execution time for a
                                      process

  CMD                                 The command or program name
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 8-1 ps Command Output Description

\

The ps output above pinpoints several daemon processes running in the
background. These processes are not associated with any terminal, which
is why there is a ? in the TTY column. Notice the PID and PPID numbers.
The smaller the number, the earlier it is started. The process with PID
0 is started first at system boot, followed by the process with PID 1,
and so on. Each PID has an associated PPID in column 3. The owner of
each process is exposed in the UID column along with the name of the
command or program under CMD.

\

Information for each running process is recorded and maintained in the
/proc file system, which ps and many other commands reference to acquire
desired data for viewing.

\

The ps command output may be customized to view only the desired
columns. For instance, if you want to produce an output with the command
name in column 1, PID in column 2, PPID in column 3, and owner name in
column 4, run it as follows:

\

<div>

![](image-P86YLM59.jpg){height="100%"}

</div>

Make sure the -o option is specified for a user-defined format and there
is no white space before or after the column names. You can add or
remove columns and switch their positions as needed.

\

Another switch to look at with the ps command is -C (command list). This
option is used to list only those processes that match the specified
command name. For example, run it to check how many sshd processes are
currently running on the system:

\

<div>

![](image-CQ26C6T5.jpg){height="100%"}

</div>

The output exhibits multiple background sshd processes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0255.html}

## Viewing and Monitoring Processes with top {.style3}

\

The other popular tool for viewing process information is the top
command. This command displays statistics in real time and continuously,
and may be helpful in identifying possible performance issues on the
system. A sample of a running top session is shown below:

\

<div>

![](image-9U9PV626.jpg){height="100%"}

</div>

Press q or Ctrl+c to quit.

\

The top output may be divided into two major portions: the summary
portion and the tasks portion. The summary area spreads over the first
five lines of the output, and it shows the information as follows:

\

Line 1: Indicates the system uptime, number of users logged in, and
system load averages over the period of 1, 5, and 15 minutes. See the
description for the uptime command output in

[Chapter 02 "Initial Interaction with the System".](#chapter0049.html)

Line 2: Displays the task (or process) information, which includes the
total number of tasks running on the system and how many of them are in
running, sleeping, stopped, and zombie states.

Line 3: Shows the processor usage that includes the CPU time in
percentage spent in running user and system processes, in idling and
waiting, and so on.

Line 4: Depicts memory utilization that includes the total amount of
memory allocated to the system, and how much of it is free, in use, and
allocated for use in buffering and caching.

Line 5: Exhibits swap (virtual memory) usage that includes the total
amount of swap allocated to the system, and how much of it is free and
in use. The "avail Mem" shows an estimate of the amount of memory
available for starting new processes without using the swap.

\

The second major portion in the top command output showcases the details
for each process in 12 columns as described below:

\

Columns 1 and 2: Pinpoint the process identifier (PID) and owner (USER)

Columns 3 and 4: Display the process priority (PR) and nice value (NI)

Columns 5 and 6: Depict amounts of virtual memory (VIRT) and non-swapped
resident memory (RES) in use

Column 7: Shows the amount of shareable memory available to the process
(SHR)

Column 8: Represents the process status (S)

Columns 9 and 10: Express the CPU (%CPU) and memory (%MEM) utilization

Column 11: Exhibits the CPU time in hundredths of a second (TIME+)

Column 12: Identifies the process name (COMMAND)

\

While in top, you can press "o" to re-sequence the process list, "f" to
add or remove fields, "F" to select the field to sort on, and "h" to
obtain help. top is highly customizable. See the command's manual pages
for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0256.html}

## Listing a Specific Process {.style3}

\

Though the tools discussed so far provide a lot of information about
processes including their PIDs, Linux also offers the pidof and pgrep
commands to list only the PID of a specific process. These commands have
a few switches available to modify their behavior; however, their most
elementary use is to pass a process name as an argument to view its PID.
For instance, to list the PID of the rsyslogd daemon, use either of the
following:

\

<div>

![](image-472TCNXI.jpg){height="100%"}

</div>

Both commands produce an identical result if used without an option.

::: {style="page-break-before: always;"}
:::

[]{#chapter0257.html}

## Listing Processes by User and Group Ownership {.style3}

\

A process can be listed by its ownership or owning group. You can use
the ps command for this purpose. For example, to list all processes
owned by user1, specify the -U (or -u) option with the command and then
the username:

\

<div>

![](image-WLH9Y8KU.jpg){height="100%"}

</div>

The command lists the PID, TTY, TIME, and CMD name for all the processes
owned by user1. You can specify the -G (or -g) option instead and the
name of an owning group to print processes associated with that group
only:

\

<div>

![](image-NJVHX90K.jpg){height="100%"}

</div>

The above output reveals all the running processes with root as their
owning group.

::: {style="page-break-before: always;"}
:::

[]{#chapter0258.html}

## Understanding Process Niceness and Priority {.style3}

\

Linux is a multitasking operating system. It runs numerous processes on
a single processor core by giving each process a slice of time. The
process scheduler on the system performs rapid switching of processes,
giving the notion of concurrent execution of multiple processes.

\

A process is spawned at a certain priority, which is established at
initiation based on a numeric value called niceness (a.k.a. a nice
value). There are 40 niceness values, with -20 being the highest or the
most favorable to the process, and +19 being the lowest or the least
favorable to the process. Most system-started processes run at the
default niceness of 0. A higher niceness lowers the execution priority
of a process, and a lower niceness increases it. In other words, a
process running at a higher priority gets more CPU attention. A child
process inherits the niceness of its calling process in its priority
calculation. Though programs are normally run at the default niceness,
you can choose to initiate them at a different niceness to adjust their
priority based on urgency, importance, or system load. As a normal user,
you can only make your processes nicer, but the root user can raise or
lower the niceness of any process.

\

RHEL provides the nice command to launch a program at a non-default
priority and the renice command to alter the priority of a running
program.

\

The default niceness can be viewed with the nice command as follows:

\

<div>

![](image-DZFM9QSL.jpg){height="100%"}

</div>

The ps command with the -l option along with the -ef options can be used
to list priority (PRI, column 7) and niceness (NI, column 8) for all
processes:

\

<div>

![](image-5QPXBUA4.jpg){height="100%"}

</div>

The output indicates that the first two processes are running at the
default niceness of 0 and the next three at the highest niceness of -20.
These values are used by the process scheduler to adjust the execution
time of the processes on the CPU. The ps command maintains an internal
mapping between niceness levels and priorities. A niceness of 0 (NI
column) corresponds to priority 80 (PR column), and a niceness of -20
(NI column) maps to priority 60 (PR column).

\

In contrast to the niceness-priority mapping that the ps command uses,
the top command displays it differently. For a 0-80 ps mapping, the top
session will report it 0-20. Likewise, ps' (-20)-60 will be the same as
the top's (-20)-0.

::: {style="page-break-before: always;"}
:::

[]{#chapter0259.html}

## Exercise 8-1: Start Processes at Non-Default Priorities {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

You will need two terminal sessions to perform this exercise. Let's call
them Terminal 1 and Terminal 2.

\

In this exercise, you will launch the top program three times and
observe how the ps command reports the priority and niceness values. You
will execute the program the first time at the default priority, the
second time at a lower priority, and the third time at a higher
priority. You will control which priority to run the program at by
specifying a niceness value with the nice command. You will verify the
new niceness and priority after each execution of the top session.

\

1\. Run the top command at the default priority/niceness in Terminal 1:

\

<div>

![](image-NX19F2O8.jpg){height="100%"}

</div>

2\. Check the priority and niceness for the top command in Terminal 2
using the ps command:

\

<div>

![](image-CWI4DBM5.jpg){height="100%"}

</div>

The command reports the values as 80 and 0, which are the defaults.

\

3\. Terminate the top session in Terminal 1 by pressing the letter q and
relaunch it at a lower priority with a nice value of +2:

\

<div>

![](image-C97PWI8J.jpg){height="100%"}

</div>

4\. Check the priority and niceness for the top command in Terminal 2
using the ps command:

\

<div>

![](image-6P3O8KHV.jpg){height="100%"}

</div>

The command reports the new values as 82 and 2.

\

5\. Terminate the top session in Terminal 1 by pressing the letter q and
relaunch it at a higher priority with a nice value of -10. Use sudo for
root privileges.

\

<div>

![](image-BA4277WB.jpg){height="100%"}

</div>

6\. Check the priority and niceness for the top command in Terminal 2
using the ps command:

\

<div>

![](image-J4877DNH.jpg){height="100%"}

</div>

As you can see, the process is running at a higher priority (70) with a
nice value of -10. Terminate the top session by pressing the letter q.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0260.html}

## Exercise 8-2: Alter Process Priorities {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

You will need two terminal sessions to perform this exercise. Let's call
them Terminal 1 and Terminal 2.

\

In this exercise, you will launch the top program at the default
priority and alter its priority without restarting it. You will set a
new priority by specifying a niceness value with the renice command. You
will verify the new niceness and priority after each execution of the
top session.

\

1\. Run the top command at the default priority/niceness in Terminal 1:

\

<div>

![](image-KOWFPB1H.jpg){height="100%"}

</div>

2\. Check the priority and niceness for the top command in Terminal 2
using the ps command:

\

<div>

![](image-RPCJG0EU.jpg){height="100%"}

</div>

The command reports the values as 80 and 0, which are the defaults.

\

3\. While the top session is running in Terminal 1, increase its
priority by renicing it to -5 in Terminal 2. Use the command
substitution to get the PID of top. Prepend the renice command by sudo.

\

<div>

![](image-TI4GZLZS.jpg){height="100%"}

</div>

The output indicates the old (0) and new (-5) priorities for the
process.

\

4\. Validate the above change with ps. Focus on columns 7 and 8.

\

<div>

![](image-ZXQM8G2A.jpg){height="100%"}

</div>

As you can see, the process is now running at a higher priority (75)
with a nice value of -5.

\

5\. Repeat the above but set the process to run at a lower priority by
renicing it to 8:

\

<div>

![](image-2O1CQAIK.jpg){height="100%"}

</div>

The output indicates the old (-5) and new (8) priorities for the
process.

\

6\. Validate the above change with ps. Focus on columns 7 and 8.

\

<div>

![](image-TN53XVDV.jpg){height="100%"}

</div>

The process is reported to now running at a lower priority (88) with
niceness 8.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0261.html}

## Controlling Processes with Signals {.style3}

\

A system may have hundreds or thousands of processes running on it.
Sometimes it becomes necessary to alert a process of an event. This is
done by sending a control signal to the process. Processes may use
signals to alert each other as well. The receiving process halts its
execution as soon as it gets the signal and takes an appropriate action
as per the instructions enclosed in the signal. The instructions may
include terminating the process gracefully, killing it abruptly, or
forcing it to re-read its configuration.

\

There are plentiful signals available for use, but only a few are
common. Each signal is associated with a unique numeric identifier, a
name, and an action. A list of available signals can be viewed with the
kill command using the -l option:

\

<div>

![](image-AWPNXQBB.jpg){height="100%"}

</div>

The output returns 64 signals available for process-to-process and
user-to-process communication. Table 8-2 describes the control signals
that are most often used.

\

  ----------------------- ----------------------- -----------------------
  Signal Number           Signal Name             Action

  1                       SIGHUP                  Hang up signal causes a
                                                  process to disconnect
                                                  itself from a closed
                                                  terminal that it was
                                                  tied to. Also used to
                                                  instruct a running
                                                  daemon to re-read its
                                                  configuration without a
                                                  restart.

  2                       SIGINT                  The \^c (Ctrl+c) signal
                                                  issued on the
                                                  controlling terminal to
                                                  interrupt the execution
                                                  of a process.

  9                       SIGKILL                 Terminates a process
                                                  abruptly

  15                      SIGTERM                 Sends a soft
                                                  termination signal to
                                                  stop a process in an
                                                  orderly fashion. This
                                                  is the default signal
                                                  if none is specified
                                                  with the command.

  18                      SIGCONT                 Same as using the bg
                                                  command to resume

  19                      SIGSTOP                 Same as using Ctrl+z to
                                                  suspend a job

  20                      SIGTSTP                 Same as using the fg
                                                  command
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Table 8-2 Control Signals

\

The commands used to pass a signal to a process are kill and pkill.
These commands are usually used to terminate a process. Ordinary users
can kill processes that they own, while the root user privilege is
needed to kill any process on the system.

\

The kill command requires one or more PIDs, and the pkill command
requires one or more process names to send a signal to. You can specify
a non-default signal name or number with either utility.

\

Let's look at a few examples to understand the usage of these tools.

\

To pass the soft termination signal to the crond daemon, use either of
the following:

\

<div>

![](image-36BT3VMP.jpg){height="100%"}

</div>

The pidof command in the above example is used to discover the PID of
the crond process using command substitution and it is then passed to
the kill command for termination. You may also use the pgrep command to
determine the PID of a process, as demonstrated in the next example. Use
ps -ef \| grep crond to confirm the termination.

\

Using the pkill or kill command without specifying a signal name or
number sends the default signal of 15 to the process. This signal may or
not terminate the process. Some processes ignore the soft termination
signal as they might be in a waiting state. These processes may be ended
forcefully using signal 9 in any of the following ways:

\

<div>

![](image-Z7GDROPY.jpg){height="100%"}

</div>

You may run the killall command to terminate all processes that match a
criterion. Here is how you can use this command to kill all crond
processes (assuming there are many of them running):

\

<div>

![](image-DBURS3XF.jpg){height="100%"}

</div>

There are plenty of options available with the kill, killall, pkill,
pgrep, and pidof commands. Consult respective manual pages for more
details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0262.html}

## Job Scheduling {.style3}

\

Job scheduling allows a user to submit a command for execution at a
specified time in the future. The execution of the command could be one
time or periodic based on a pre-determined time schedule. A one-time
execution may be scheduled for an activity that needs to be performed at
a time of low system usage. One example of such an activity would be the
execution of a lengthy shell program. In contrast, a recurring activity
could include creating a compressed archive, trimming log files,
monitoring the system, running a custom script, or removing unwanted
files from the system.

\

Job scheduling and execution is taken care of by two service daemons:
atd and crond. While atd manages the jobs scheduled to run one time in
the future, crond is responsible for running jobs repetitively at
pre-specified times. At startup, this daemon reads the schedules in
files located in the /var/spool/cron and /etc/cron.d directories, and
loads them in the memory for on-time execution. It scans these files at
short intervals and updates the in-memory schedules to reflect any
modifications. This daemon runs a job at its scheduled time only and
does not entertain any missed jobs. In contrast, the atd daemon retries
a missed job at the same time next day. For any additions or changes,
neither daemon needs a restart.

::: {style="page-break-before: always;"}
:::

[]{#chapter0263.html}

## Controlling User Access {.style3}

\

By default, all users are allowed to schedule jobs using the at and cron
services. However, this access may be controlled and restricted to
specific users only. This can be done by listing users in the allow or
deny file located in the /etc directory for either service. These files
are named at.allow and at.deny for the at service and cron.allow and
cron.deny for the cron service.

\

The syntax for the four files is identical. You only need to list
usernames that are to be allowed or denied access to these scheduling
tools. Each file takes one username per line. The root user is always
permitted; it is affected neither by the existence or non-existence of
these files nor by the inclusion or exclusion of its entry in these
files.

\

[Table 8-3 shows various combinations and their impact on user
access.](#chapter0263.html)

\

  ----------------------- ----------------------- -----------------------
  at.allow / cron.allow   at.deny / cron.deny     Impact

  Exists, and contains    Existence does not      All users listed in
  user entries            matter                  allow files are
                                                  permitted

  Exists, but is empty    Existence does not      No users are permitted
                          matter                  

  Does not exist          Exists, and contains    All users, other than
                          user entries            those listed in deny
                                                  files, are permitted

  Does not exist          Exists, but is empty    All users are permitted

  Does not exist          Does not exist          No users are permitted
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Table 8-3 User Access Restrictions to Scheduling Tools

\

By default, the deny files exist and are empty, and the allow files are
non-existent. This opens up full access to using both tools for all
users.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: One username is entered per line entry in an appropriate allow
or deny file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The following message appears if an unauthorized user attempts to
execute at:

\

<div>

![](image-VWFIN965.jpg){height="100%"}

</div>

And the following warning is displayed for unauthorized access attempt
to the cron service:

\

<div>

![](image-NIP1DRXO.jpg){height="100%"}

</div>

To generate the denial messages, you need to place entries for user1 in
the deny files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0264.html}

## Scheduler Log File {.style3}

\

All activities for atd and crond services are logged to the
/var/log/cron file. Information such as the time of activity, hostname,
process name and PID, owner, and a message for each invocation is
captured. The file also keeps track of other events for the crond
service such as the service start time and any delays. A few sample
entries from the log file are shown below:

\

<div>

![](image-ME7X1OWZ.jpg){height="100%"}

</div>

The truncated output shows some past entries from the file. You need the
root user privilege to be able to read the file content.

::: {style="page-break-before: always;"}
:::

[]{#chapter0265.html}

## Using at {.style3}

\

The at command is used to schedule a one-time execution of a program in
the future. All submitted jobs are spooled in the /var/spool/at
directory and executed by the atd daemon at the specified time. Each
submitted job will have a file created containing the settings for
establishing the user's shell environment to ensure a successful
execution. This file also includes the name of the command or program to
be run. There is no need to restart the daemon after a job submission.

\

There are multiple ways and formats for expressing the time with at.
Some examples are:

\

  ----------------------------------- -----------------------------------
  at 1:15am                           (executes the task at the next 1:15
                                      a.m.)

  at noon                             (executes the task at 12:00 p.m.)

  at 23:45                            (executes the task at 11:45 p.m.)

  at midnight                         (executes the task at 12:00 a.m.)

  at 17:05 tomorrow                   (executes the task at 5:05 p.m. on
                                      the next day)

  at now + 5 hours                    (executes the task 5 hours from
                                      now. We can specify minutes, days,
                                      or weeks in place of hours)

  at 3:00 10/15/23                    (executes the task at 3:00 a.m. on
                                      October 15, 2023)
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

at assumes the current year and today's date if the year and date are
not mentioned.

\

You may supply a filename with the at command using the -f option. The
command will execute that file at the specified time. For instance, the
following will run /home/user1/.bash_profile file for user1 2 hours from
now:

\

<div>

![](image-EZ7PXBXJ.jpg){height="100%"}

</div>

The above will be executed as scheduled and will have an entry placed
for it in the log file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0266.html}

## Exercise 8-3: Submit, View, List, and Erase an at Job {.style3}

\

This exercise should be done on server1 as user1.

\

In this exercise, you will submit an at job as user1 to run the date
command at 11:30 p.m. on March 31, 2023, and have the output and any
error messages generated redirected to the /tmp/date.out file. You will
list the submitted job, exhibit its contents for verification, and then
remove the job.

\

1\. Run the at command and specify the correct execution time and date
for the job. Type the entire command at the first at\> prompt and press
Enter. Press Ctrl+d at the second at\> prompt to complete the job
submission and return to the shell prompt.

\

<div>

![](image-UPDGEA0O.jpg){height="100%"}

</div>

The system assigned job ID 2 to it, and the output also pinpoints the
job's execution time.

\

2\. List the job file created in the /var/spool/at directory:

\

<div>

![](image-5C170TNI.jpg){height="100%"}

</div>

3\. List the spooled job with the at command. You may alternatively use
atq to list it.

\

<div>

![](image-LFXE8NVO.jpg){height="100%"}

</div>

4\. Display the content of this file with the at command and specify the
job ID:

\

<div>

![](image-NJLJSZ5H.jpg){height="100%"}

</div>

5\. Remove the spooled job with the at command by specifying its job ID.
You may alternatively run atrm 2 to delete it.

\

<div>

![](image-9PRXKDXI.jpg){height="100%"}

</div>

This should erase the job file from the /var/spool/at directory. You can
confirm the deletion by running atq or at -l.

::: {style="page-break-before: always;"}
:::

[]{#chapter0267.html}

## Using crontab {.style3}

\

Using the crontab command is the other method for scheduling tasks for
running in the future. Unlike atd, crond executes cron jobs on a regular
basis if they comply with the format defined in the /etc/crontab file.
Crontables (another name for crontab files) are located in the
/var/spool/cron directory. Each authorized user with a scheduled job has
a file matching their login name in this directory.

\

For example, the crontable for user1 would be /var/spool/cron/user1. The
other two locations where system crontables can be stored are the
/etc/crontab file and the /etc/cron.d directory; however, only the root
user is allowed to create, modify, and delete them. The crond daemon
scans entries in the files at the three locations to determine job
execution schedules. The daemon runs the commands or programs at the
specified time and adds a log entry to the /var/log/cron file for each
invocation. There is no need to restart the daemon after submitting a
new or modifying an existing cron job.

\

The crontab command is used to edit (-e), list (-l), and remove (-r)
crontables. The -u option is also available for users who wish to modify
a different user's crontable, provided they are allowed to do so and the
other user is listed in the cron.allow file. The root user can also use
the -u flag to alter other users' crontables even if the affected users
are not listed in the allow file. By default, crontab files are opened
in the vim editor when the crontab command is issued to edit them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0268.html}

## Syntax of User Crontables {.style3}

\

The /etc/crontab file specifies the syntax that each user cron job must
comply with in order for crond to interpret and execute it successfully.
Based on this structure, each line in a user crontable with an entry for
a scheduled job is comprised of six fields. Fields 1 to 5 are for the
schedule, field 6 may contain the login name of the executing user, and
the rest for the command or program to be executed. See Figure 8-2 for
the syntax.

\

::: {style="text-align: center;"}
![](image-GWSG7KXY.jpg){height="100%"}
:::

Figure 8-2 Syntax of Crontables

\

A description of each field is provided in Table 8-4.

\

  ----------------------- ----------------------- -----------------------
  Field                   Field Content           Description

  1                       Minute of the hour      Valid values are 0 (the
                                                  exact hour) to 59. This
                                                  field can have one
                                                  specific value as in
                                                  field 1, multiple
                                                  comma-separated values
                                                  as in field 2, a range
                                                  of values as in field
                                                  3, a mix of fields 2
                                                  and 3 (1-5,6-19), or an
                                                  \* representing every
                                                  minute of the hour as
                                                  in field 5.

  2                       Hour of the day         Valid values are 0
                                                  (midnight) to 23. Same
                                                  usage applies as
                                                  described for field 1.

  3                       Day of the month        Valid values are 1 to
                                                  31. Same usage applies
                                                  as described for field
                                                  1.

  4                       Month of the year       Valid values are 1 to
                                                  12 or jan to dec. Same
                                                  usage applies as
                                                  described for field 1.

  5                       Day of the week         Valid values are 0 to 7
                                                  or sun to sat, with 0
                                                  and 7 representing
                                                  Sunday, 1 representing
                                                  Monday, and so on. Same
                                                  usage applies as
                                                  described for field 1.

  6                       Command or program to   Specifies the full path
                          execute                 name of the command or
                                                  program to be executed,
                                                  along with any options
                                                  or arguments that it
                                                  requires.
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Table 8-4 Crontable Syntax Explained

\

Furthermore, step values may be used with \* and ranges in the
crontables using the forward slash character (/). Step values allow the
number of skips for a given value. For example, \*/2 in the minute field
would mean every second minute, \*/3 would mean every third minute,
0-59/4 would mean every fourth minute, and so on. Step values are also
supported in the same format in fields 2 to 5.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Make sure you understand and memorize the order of the fields
defined in crontables.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Consult the manual pages of the crontab configuration file (man 5
crontab) for more details on the syntax.

::: {style="page-break-before: always;"}
:::

[]{#chapter0269.html}

## Exercise 8-4: Add, List, and Erase a Cron Job {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

For this exercise, assume that all users are currently denied access to
cron.

\

In this exercise, you will submit a cron job as user1 to echo "Hello,
this is a cron test.". You will schedule this command to execute at
every fifth minute past the hour between 10:00 a.m. and 11:00 a.m. on
the fifth and twentieth of every month. You will have the output
redirected to the /tmp/hello.out file, list the cron entry, and then
remove it.

\

1\. Edit the /etc/cron.allow file and add user1 to it:

\

<div>

![](image-XR18P20C.jpg){height="100%"}

</div>

2\. Open the crontable and append the following schedule to it. Save the
file when done and exit out of the editor.

\

<div>

![](image-USG2I636.jpg){height="100%"}

</div>

3\. Check for the presence of a new file by the name user1 under the
/var/spool/cron directory:

\

<div>

![](image-XCVAY7OR.jpg){height="100%"}

</div>

4\. List the contents of the crontable:

\

<div>

![](image-NCXRMCNC.jpg){height="100%"}

</div>

5\. Remove the crontable and confirm the deletion:

\

<div>

![](image-Y48V5AOY.jpg){height="100%"}

</div>

Do not run crontab -r if you do not wish to remove the crontab file.
Instead, edit the file with crontab -e and just erase the entry.

::: {style="page-break-before: always;"}
:::

[]{#chapter0270.html}

## Chapter Summary {.style3}

\

This chapter discussed two major topics: process management and job
scheduling.

\

It is vital for users, developers, and administrators alike to have a
strong grasp on running processes, resources they are consuming, process
owners, process execution priorities, etc. They should learn how to list
processes in a variety of ways. We looked at the five states a process
is in at any given time during its lifecycle. We examined the concepts
of niceness and reniceness for increasing or decreasing a process's
priority. We analyzed some of the many available signals and looked at
how they could be passed to running processes to perform an action on
them.

\

The second and the last topic talked about submitting and managing tasks
to run in the future one time or on a recurring basis. We learned about
the service daemons that handle the task execution and the control files
where we list users who can or cannot submit jobs. We looked at the log
file that stores information for all executed jobs. We reviewed the
syntax of the crontable and examined a variety of date/time formats for
use with both at and cron job submission. We performed two exercises to
gain a grasp on their usage.

::: {style="page-break-before: always;"}
:::

[]{#chapter0271.html}

## Review Questions {.style3}

\

1\. The default location to send application error messages is the
system log file. True or False?

2\. What are the five process states?

3\. Signal 9 is used for a hard termination of a process. True or False?

4\. You must restart the crond service after modifying the /etc/crontab
file. True or False?

5\. What are the background service processes normally referred to in
Linux?

6\. What is the default nice value?

7\. The parent process gets the nice value of its child process. True or
False?

8\. When would the cron daemon execute a job that is submitted as \*/10
\* 2-6 6 \* /home/user1/script1.sh?

9\. What is the other command besides ps to view running processes?

10\. Every process that runs on the system has a unique identifier
called UID. True or False?

11\. Why would you use the renice command?

12\. What are the two commands to list the PID of a specific process?

13\. By default the \*.allow files exist. True or False?

14\. Where do the scheduling daemons store log information of executed
jobs?

15\. Which user does not have to be explicitly defined in either
\*.allow or \*.deny file to run the at and cron jobs?

16\. When would the at command execute a job that is submitted as at
01:00 12/12/2020?

17\. What are the two commands that you can use to terminate a process?

18\. What is the directory location where user crontab files are stored?

19\. What would the nice command display without any options or
arguments?

20\. Which command can be used to edit crontables?

::: {style="page-break-before: always;"}
:::

[]{#chapter0272.html}

## Answers to Review Questions {.style3}

\

1\. False. The default location is the user screen where the program is
initiated.

2\. The five process states are running, sleeping, waiting, stopped, and
zombie.

3\. True.

4\. False. The crond daemon does not need a restart after a crontable is
modified.

5\. The background service processes are referred to as daemons.

6\. The default nice value is zero.

7\. False. The child process inherits its parent's niceness.

8\. The cron daemon will run the script every tenth minute past the hour
on the 2nd, 3rd, 4th, 5th, and 6th day of every sixth month.

9\. The top command.

10\. False. It is called the PID.

11\. The renice command is used to change the niceness of a running
process.

12\. The pidof and pgrep commands.

13\. False. By default, the \*.deny files exist.

14\. The scheduling daemons store log information of executed jobs in
the /var/log/cron file.

15\. The root user.

16\. The at command will run it at 1am on December 12, 2020.

17\. The kill and pkill commands.

18\. The user crontab files are stored in the /var/spool/cron directory.

19\. The nice command displays the default nice value when executed
without any options.

20\. You can use the crontab command with the -e option to edit
crontables.

::: {style="page-break-before: always;"}
:::

[]{#chapter0273.html}

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

[]{#chapter0274.html}

## Lab 8-1: Nice and Renice a Process {.style3}

\

As user1 with sudo on server3, open two terminal sessions. Run the top
command in terminal 1. Run the pgrep or ps command in terminal 2 to
determine the PID and the nice value of top. Stop top on terminal 1 and
relaunch at a lower priority (+8). Confirm the new nice value of the
process in terminal 2. Issue the renice command in terminal 2 and
increase the priority of top to -10, and validate. (Hint: Processes and
Priorities).

::: {style="page-break-before: always;"}
:::

[]{#chapter0275.html}

## Lab 8-2: Configure a User Crontab File {.style3}

\

As user1 on server3, run the tty and date commands to determine the
terminal file (assume /dev/pts/1) and current system time. Create a cron
entry to display "Hello World" on the terminal. Schedule echo "Hello
World" \> /dev/tty/1 to run 3 minutes from the current system time. As
root, ensure user1 can schedule cron jobs. (Hint: Job Scheduling).

::: {style="page-break-before: always;"}
:::

[]{#chapter0276.html}

## Chapter 09 {style="text-align: right"}

\

### Basic Package Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Overview of Red Hat packages, naming, and management tools

\

Package dependency and database

\

Query, install, upgrade, freshen, overwrite, and remove packages

\

Extract package files from installable package

\

Validate package integrity and authenticity

\

View GPG keys and verify package attributes

\

Manage packages using the rpm command

\

#### RHCSA Objectives:

\

42\. Install and update software packages from Red Hat Network, a remote
repository, or from the local file system (part of this objective is
also covered in Chapter 10)

::: {style="page-break-before: always;"}
:::

\

The Red Hat software management system is known as RPM Package Manager
(RPM). RPM also refers to one or more files that are packaged together
in a special format and stored in files with the .rpm extension. These
rpm files (also called rpms, rpm packages, or packages) are manipulated
by the RPM package management system. Each package included in and
available for RHEL is in this file format. Packages have meaningful
names and contain necessary files, as well as metadata structures such
as ownership, permissions, and directory location for each included
file. Packages may be downloaded and saved locally or on a network share
for quick access, and they may have dependencies over files or other
packages. In other words, a package may require the presence of
additional files, another package, or a group of packages in order to be
installed successfully and operate properly. Once a package has been
installed and its metadata information stored in a package database,
future attempts to update the package are reflected in the metadata as
well.

\

::: {style="text-align: center;"}
![](image-7CRO31UX.jpg){height="100%"}
:::

RHEL provides a powerful tool for the installation and administration of
RPM packages. The rpm command is flexible and offers multitude of
options and subcommands to perform functions such as querying,
installing, upgrading, freshening, removing, and decompressing packages,
and validating package integrity and authenticity.

::: {style="page-break-before: always;"}
:::

[]{#chapter0277.html}

## Package Overview {.style3}

\

RHEL is essentially a set of packages grouped together to create an
operating system. They are prepackaged for installation and assembled
for various intended use cases. They are built around the Linux kernel
and include thousands of packages that are digitally signed, tested, and
certified. There are several basic and advanced concepts associated with
packages, packaging, and their management that are touched upon in this
and the next chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0278.html}

## Packages and Packaging {.style3}

\

A software package is a group of files organized in a directory
structure along with metadata and intelligence that make up a software
application. They are available in two types: binary (or installable)
and source. Binary packages are installation-ready and are bundled for
distribution. They have .rpm extension and contain install scripts, pre-
and post-installation scripts, executables, configuration files, library
files, dependency information, where to install files, and
documentation. The documentation includes detailed instructions on how
to install and uninstall the package, manual pages for the configuration
files and commands, and other necessary information pertaining to the
installation and usage of the package.

\

All metadata related to packages is stored at a central location and
includes information such as package version, installation location,
checksum values, and a list of included files with their attributes.
This allows the package management toolset to handle package
administration tasks efficiently by referencing this metadata.

\

The package intelligence is used by the package administration toolset
for a successful completion of the package installation process. It may
include information on prerequisites, user account setup (if required),
and any directories and soft links that need to be created. The
intelligence also includes the reverse of this process for
uninstallation.

\

Source packages come with the original unmodified version of the
software that may be unpacked, modified as desired, and repackaged in
the binary format for installation or redistribution. They are
identified with the .src extension.

::: {style="page-break-before: always;"}
:::

[]{#chapter0279.html}

## Package Naming {.style3}

\

Red Hat software packages follow a standard naming convention.
Typically, there are five parts to a package name: (1) the package name,
(2) the package version, (3) the package release (revision or build),
(4) the Enterprise Linux the package is created for, and (5) the
processor architecture the package is built for. An installable package
name always has the .rpm extension; however, this extension is removed
from the installed package name.

\

For example, if the name of an installable package is
openssl-3.0.1-43.el9_0.x86_64.rpm, its installed name would be
openssl-3.0.1-43.el9_0.x86_64. Here is a description of each part of the
package name:

\

openssl: package name

3.0.1: version

43: release

el9_0: stands for Enterprise Linux 9.0 (not all packages have it)

x86_64: processor architecture the package is created for. You may see
"noarch" for platform-independent packages that can be installed on any
hardware architecture, or "src" for source code packages.

### .rpm: the extension {.style3}

::: {style="page-break-before: always;"}
:::

[]{#chapter0280.html}

## Package Dependency {.style3}

\

An installable package may require the presence of one or more
additional packages in order to be installed successfully. Likewise, a
software package component may require the functionality provided by one
or more packages to exist in order to operate as expected. This is
referred to as package dependency, where one package depends on one or
more other packages for installation or execution. Package dependency
information is recorded in each package's metadata from where it is read
by package handling utilities.

::: {style="page-break-before: always;"}
:::

[]{#chapter0281.html}

## Package Database {.style3}

\

Metadata for installed packages and package files is stored and
maintained in the /var/lib/rpm directory. This directory location is
referred to as the package database, and it is referenced by package
manipulation utilities to obtain package name and version data and
information about ownerships, permissions, timestamps, and sizes for
each and every file that is part of the package. The package database
also contains information on dependencies. All this data aids management
commands in listing and querying packages, verifying dependencies and
file attributes, installing new packages, upgrading and uninstalling
existing packages, and carrying out other package handling tasks.

\

The package database does not update existing package information by
simply adding available enhancements. It removes the metadata of the
package being replaced and then adds the information of the replacement
package. In RHEL 9, it can maintain multiple versions of a single
package alongside their metadata.

::: {style="page-break-before: always;"}
:::

[]{#chapter0282.html}

## Package Management Tools {.style3}

\

The primary tool for package management on Red Hat Enterprise Linux is
called rpm (redhat package manager). This tool offers abundant options
for flexible package handling; however, a major caveat is that it does
not automatically resolve package dependencies. To overcome this gap, a
more innovative tool called yum (yellowdog update, modified) was
introduced, which offered an easier method for package management that
can find, get, and install all required dependent packages
automatically.

\

Starting in RHEL 8, a major enhancement to yum was introduced known as
dnf. dnf does not have an official acronym, but some documentation
refers to it as dandified yum. You may still use the yum command;
however, it is simply a soft link to dnf.

\

This chapter focuses on the use of the rpm command. Chapter 10 "Advanced
Package Management" details the dnf command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0283.html}

## Package Management with rpm {.style3}

\

The rpm command handles package management tasks including querying,
installing, upgrading, freshening, overwriting, removing, extracting,
validating, and verifying packages. As mentioned, this command has a
major drawback as it does not have the ability to automatically satisfy
package dependencies, which can be frustrating during software
installation and upgrade. The rpm command works with both installed and
installable packages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0284.html}

## The rpm Command {.style3}

\

Before getting into the details, let's look at some common rpm command
options. Table 9-1 describes query options in both short and long option
formats. You may use either format.

\

  ----------------------------------- -----------------------------------
  Query Options                       Description

  -q (\--query)                       Queries and displays packages

  -qa (\--query \--all)               Lists all installed packages

  -qc (\--query \--configfiles)       Lists configuration files in a
                                      package

  -qd (\--query \--docfiles)          Lists documentation files in a
                                      package

  -qf (\--query \--file)              Exhibits what package a file comes
                                      from

  -qi (\--query \--info)              Shows installed package information
                                      including version, size,
                                      installation status and date,
                                      signature, and description

  -qip (\--query \--info \--package)  Shows installable package
                                      information including version,
                                      size, installation status and date,
                                      signature, and description

  -ql (\--query \--list)              Lists all files in a package

  -qR (\--query \--requires)          Lists files and packages a package
                                      depends on (requires)

  -q \--whatprovides                  Lists packages that provide the
                                      specified package or file

  -q \--whatrequires                  Lists packages that require the
                                      specified package or file
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 9-1 rpm Command Query Options

\

[Table 9-2 describes options related to package installation, removal,
and verification. These options are also available in both short and
long formats. You may use either format.](#chapter0284.html)

\

  ----------------------------------- -----------------------------------
  Install/Remove Options              Description

  -e (\--erase)                       Removes a package

  \--force                            Installs and replaces a package or
                                      files of the same version

  -F (\--freshen)                     Upgrades an installed package

  -h (\--hash)                        Shows installation progress with
                                      hash marks

  -i (\--install)                     Installs a package

  \--import                           Imports a public key

  -K                                  Validates the signature and package
                                      integrity

  -U (\--upgrade)                     Upgrades an installed package or
                                      loads it if it is not already
                                      installed

  -v (\--verbose) or -vv              Displays detailed information

  -V (\--verify)                      Verifies the integrity of a package
                                      or package files
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 9-2 rpm Command Install/Remove/Verify Options

\

The examples in this chapter employ most of these options in short
format to understand how they are used to achieve desired results.

::: {style="page-break-before: always;"}
:::

[]{#chapter0285.html}

## Exercise 9-1: Mount RHEL 9 ISO Persistently {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will attach the RHEL 9 ISO image to the RHEL9-VM1
in VirtualBox and mount the image on /mnt directory on server1 to access
and manipulate the software packages in it with the rpm command. You
will ensure that the image is automatically mounted on each system
reboot. You will confirm access to the packages by listing the
subdirectories that store them.

\

1\. Go to the VirtualBox VM Manager and make sure that the RHEL 9 image
is attached to RHEL9-VM1 as depicted below:

\

::: {style="text-align: center;"}
![](image-3IUDQLIY.jpg){height="100%"}
:::

2\. Open the /etc/fstab file in the vim editor (or another editor of
your choice) and add the following line entry at the end of the file to
mount the DVD image (/dev/sr0) in read-only (ro) mode on the /mnt
directory.

\

<div>

![](image-GKVBSV1F.jpg){height="100%"}

</div>

\

sr0 represents the first instance of the optical device and iso9660 is
the standard format for optical file systems.

\

3\. Mount the file system as per the configuration defined in the
/etc/fstab file using the mount command with the -a (all) option:

\

<div>

![](image-WN2O9LX7.jpg){height="100%"}

</div>

The command should return without displaying anything in the output.
This will confirm that the new entry was placed correctly in the file.
See Chapter 14 "Local File Systems and Swap" for details on mount and
mount point concepts.

\

4\. Verify the mount using the df command:

\

<div>

![](image-XCXMURUM.jpg){height="100%"}

</div>

The image and the packages therein can now be accessed via the /mnt
directory just like any other local directory on the system.

\

5\. List the two directories---/mnt/BaseOS/Packages and
/mnt/AppStream/Packages---that contain all the software packages
(directory names are case sensitive):

\

<div>

![](image-N9EJWUVQ.jpg){height="100%"}

</div>

There are thousands of files in the two locations, each representing a
single rpm package.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0286.html}

## Querying Packages {.style3}

\

You can query for packages in the package database or at the specified
location. The following are some examples.

\

To query all installed packages:

\

<div>

![](image-KVRH8WB8.jpg){height="100%"}

</div>

To query whether the specified package is installed:

\

<div>

![](image-7LJUV3DF.jpg){height="100%"}

</div>

To list all files in a package:

\

<div>

![](image-OI67ZMJO.jpg){height="100%"}

</div>

To list only the documentation files in a package:

\

<div>

![](image-X3FZ4AZB.jpg){height="100%"}

</div>

To list only the configuration files in a package:

\

<div>

![](image-LV8EF2LY.jpg){height="100%"}

</div>

To identify which package owns the specified file:

\

<div>

![](image-DCUD60EC.jpg){height="100%"}

</div>

To display information about an installed package including version,
release, installation status, installation date, size, signatures,
description, and so on:

\

<div>

![](image-NUG658MG.jpg){height="100%"}

</div>

To list all file and package dependencies for a given package:

\

<div>

![](image-1T92ARNR.jpg){height="100%"}

</div>

To query an installable package for metadata information (version,
release, architecture, description, size, signatures, etc.):

\

<div>

![](image-S85KT7A3.jpg){height="100%"}

</div>

To determine what packages require the specified package in order to
operate properly:

\

<div>

![](image-NU6MSOGS.jpg){height="100%"}

</div>

The above output lists all the packages that will require the specified
package "lvm2" in order to work fully and properly.

::: {style="page-break-before: always;"}
:::

[]{#chapter0287.html}

## Installing a Package {.style3}

\

Installing a package creates the necessary directory structure for the
package, installs the required files, and runs any post-installation
steps. The following command installs a package called
zsh-5.8-9.el9.x86_64.rpm on the system:

\

<div>

![](image-2TVCC9ZZ.jpg){height="100%"}

</div>

If this package required the presence of any missing packages, you would
see an error message related to failed dependencies. In that case, you
would have to first install the missing packages for this package to be
loaded successfully.

::: {style="page-break-before: always;"}
:::

[]{#chapter0288.html}

## Upgrading a Package {.style3}

\

Upgrading a package upgrades an installed version of the package. In the
absence of an existing version, the upgrade simply installs the package.

\

To upgrade a package called sushi, use the -U option with the rpm
command. Notice that the sushi package is located in a different
directory than the zsh package in the previous example.

\

<div>

![](image-3A75NDMP.jpg){height="100%"}

</div>

The command makes a backup of all the affected configuration files
during the upgrade process and adds the extension .rpmsave to them. In
the above example, the sushi package was installed, as it was not
already on the system.

::: {style="page-break-before: always;"}
:::

[]{#chapter0289.html}

## Freshening a Package {.style3}

\

Freshening a package requires that an older version of the package must
already exist on the system.

\

To freshen the sushi package, use the -F option:

\

<div>

![](image-BSHGZDB2.jpg){height="100%"}

</div>

The above command did nothing because the same package version specified
with the command is already installed on the system. It will only work
if a new version of the installed package is available.

::: {style="page-break-before: always;"}
:::

[]{#chapter0290.html}

## Overwriting a Package {.style3}

\

Overwriting a package replaces the existing files associated with the
package of the same version.

\

To overwrite the package zsh-5.8-9.el9.x86_64 that was installed
earlier, use the \--replacepkgs option:

\

<div>

![](image-0R848G66.jpg){height="100%"}

</div>

The installation progress indicates that the zsh package was replaced
successfully. This action is particularly useful when you suspect
corruption in one or more installed package files and you want to start
afresh.

::: {style="page-break-before: always;"}
:::

[]{#chapter0291.html}

## Removing a Package {.style3}

\

Removing a package uninstalls the package and all its associated files
and the directory structure.

\

To remove the package sushi, use the -e option and specify -v for
verbosity:

\

<div>

![](image-5NST2QJN.jpg){height="100%"}

</div>

This command performs a dependency inspection to check whether there are
any packages that require the existence of the package being weeded out
and fails the removal if it detects a dependency.

::: {style="page-break-before: always;"}
:::

[]{#chapter0292.html}

## Extracting Files from an Installable Package {.style3}

\

Files in an installable package can be extracted using the rpm2cpio
command for reasons such as examining the contents of the package,
replacing a corrupted or lost command, or replacing a critical
configuration file of an installed package to its original state.

\

Assuming you have lost the /etc/chrony.conf configuration file, which is
part of a package called chrony, and want to retrieve it from its
installable package and put it back, you'll first need to determine what
package this file comes from:

\

<div>

![](image-NEU611T3.jpg){height="100%"}

</div>

Now use the rpm2cpio command to extract (-i) all files from the chrony
package (located under /mnt/BaseOS/Packages) and create (-d) the
necessary directory structure during the retrieval. Extract the files in
a temporary location such as the /tmp directory before you proceed with
overwriting the destination under /etc.

\

<div>

![](image-JBL7UWTA.jpg){height="100%"}

</div>

Run find to locate the chrony.conf file:

\

<div>

![](image-MM81KW15.jpg){height="100%"}

</div>

The above output shows that the file is under /tmp/etc. You can copy it
to the /etc directory now, and you're back in business.

::: {style="page-break-before: always;"}
:::

[]{#chapter0293.html}

## Validating Package Integrity and Credibility {.style3}

\

Before it is installed, a package may be checked for integrity
(completeness and error-free state) and credibility (authenticity) after
it has been copied to another location, downloaded from the web, or
obtained elsewhere. Use the MD5 checksum for verifying its integrity and
the GNU Privacy Guard (GnuPG or GPG) public key signature for ensuring
the credibility of its developer or publisher. This will ensure an
uncorrupted and genuine piece of software.

\

The commercial version of GPG is referred to as PGP (Pretty Good
Privacy).

\

To check the integrity of a package such as chrony-4.2-1.el9.x86_64.rpm
located in /mnt/BaseOS/Packages:

\

<div>

![](image-LY0BKMSI.jpg){height="100%"}

</div>

The OK in the output confirms that the package is free of corruption.

\

Red Hat signs their products and updates with a GPG key and includes
necessary public keys in the products for verification. For RHEL, the
keys are in files on the installation media and are copied to the
/etc/pki/rpm-gpg/ directory during the OS installation. Refer to Table
9-3 for a list of files in that directory and a short explanation.

\

  ----------------------------------- -----------------------------------
  GPG File                            Description

  RPM-GPG-KEY-redhat-release          Used for packages shipped after
                                      November 2009 and their updates

  RPM-GPG-KEY-redhat-beta             Used for beta test products shipped
                                      after November 2009
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 9-3 Red Hat GPG Key Files

\

To check the credibility of a package, import the relevant GPG key and
then verify the package. The table above shows that the GPG file for the
recent packages is RPM-GPG-KEY-redhat-release. In the following example,
run the rpm command to import the GPG key from this file and verify the
signature for the chrony-4.2-1.el9.x86_64.rpm package using the -K
option with the command:

\

<div>

![](image-EH27MRJZ.jpg){height="100%"}

</div>

The OK validates the package signature and certifies the authenticity
and integrity of the package.

::: {style="page-break-before: always;"}
:::

[]{#chapter0294.html}

## Viewing GPG Keys {.style3}

\

The GPG key imported in the previous subsection can be viewed with the
rpm command. You can list the key and display its details as well. Run
the command as follows to list the imported key:

\

<div>

![](image-VPSN5Z3N.jpg){height="100%"}

</div>

The output suggests that there are two GPG public keys currently
imported on the system. Let's view the details for the second one:

\

<div>

![](image-G7PT26K1.jpg){height="100%"}

</div>

The output returns both the metadata and the key data for the specified
GPG public key.

::: {style="page-break-before: always;"}
:::

[]{#chapter0295.html}

## Verifying Package Attributes {.style3}

\

Verifying the integrity of an installed package compares the attributes
of files in the package with the original file attributes saved and
stored in the package database at the time of package installation. The
verification process uses the rpm command with the -V option to compare
the owner, group, permission mode, size, modification time, digest, and
type among other attributes. The command returns to the prompt without
exhibiting anything if it detects no changes in the attributes. You can
use the -v or -vv option with the command for increased verbosity.

\

Run this check on the at package:

\

<div>

![](image-D2WMRQ14.jpg){height="100%"}

</div>

The command returned nothing, which implies that the file attributes are
intact. Now change the permissions on one of the files,
/etc/sysconfig/atd, in this package to 770 from the current value of
644, and then re-execute the verification test:

\

<div>

![](image-UPQVWKVC.jpg){height="100%"}

</div>

The output is indicative of a change in the permission mode on the atd
file in the at package. You may alternatively run the verification check
directly on the file by adding the -f option to the command and passing
the filename as an argument:

\

<div>

![](image-QYIWLA1I.jpg){height="100%"}

</div>

The output returns three columns: column 1 contains nine fields, column
2 shows the file type, and column 3 expresses the full path of the file.
The command performs a total of nine checks, as illustrated by the codes
in column 1 of the output, and displays any changes that have occurred
since the package that contains the file was installed. Each of these
codes has a meaning. Table 9-4 lists the codes with description as they
appear from left to right. The period character (.) appears for an
attribute that is not in an altered state.

\

  ----------------------------------- -----------------------------------
  Code                                Description

  S                                   Appears if the file size is
                                      different

  M                                   Appears if the (mode) permission or
                                      file type is altered

  5                                   Appears if MD5 checksum does not
                                      match

  D                                   Appears if the file is a device
                                      file and its major or minor number
                                      has changed

  L                                   Appears if the file is a symlink
                                      and its path has altered

  U                                   Appears if the ownership has
                                      modified

  G                                   Appears if the group membership has
                                      modified

  T                                   Appears if timestamp has changed

  P                                   Appears if capabilities have
                                      altered

  .                                   Appears if no modification is
                                      detected
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 9-4 Package Verification Codes

\

Column 2 in the output above exposes a code that represents the type of
file. Table 9-5 lists them.

\

  ----------------------------------- -----------------------------------
  File Type                           Description

  c                                   Configuration file

  d                                   Documentation file

  g                                   Ghost file

  l                                   License file

  r                                   Readme file
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 9-5 File Type Codes

\

Based on the information in the tables, the /etc/sysconfig/atd is a
configuration file with a modified permission mode. Reset the attribute
to its previous value and rerun the check to ensure the file is back to
its original state.

\

<div>

![](image-UUK2OG0K.jpg){height="100%"}

</div>

The command produced no output, which confirms the integrity of the file
as well as the package.

::: {style="page-break-before: always;"}
:::

[]{#chapter0296.html}

## Exercise 9-2: Perform Package Management Using rpm {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will verify the integrity and authenticity of a
package called rmt located in the /mnt/BaseOS/Packages directory on the
installation image and then install it. You will display basic
information about the package, show files it contains, list
documentation files, verify the package attributes, and erase the
package.

\

1\. Run the ls command on the /mnt/BaseOS/Packages directory to confirm
that the rmt package is available:

\

<div>

![](image-U6IH11U0.jpg){height="100%"}

</div>

2\. Run the rpm command and verify the integrity and credibility of the
package:

\

<div>

![](image-UERUIEPM.jpg){height="100%"}

</div>

3\. Install the package:

\

<div>

![](image-0N02V3EZ.jpg){height="100%"}

</div>

4\. Show basic information about the package:

\

<div>

![](image-B0QB0UUI.jpg){height="100%"}

</div>

5\. Show all the files the package contains:

\

<div>

![](image-QUWE2D1D.jpg){height="100%"}

</div>

6\. List the documentation files the package has:

\

<div>

![](image-VPE8XTFS.jpg){height="100%"}

</div>

7\. Verify the attributes of each file in the package. Use verbose mode.

\

<div>

![](image-9J7W5IUW.jpg){height="100%"}

</div>

8\. Remove the package:

\

<div>

![](image-GNPL0KOW.jpg){height="100%"}

</div>

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0297.html}

## Chapter Summary {.style3}

\

This chapter is the first of the two chapters (second one being the next
chapter) with coverage on software management. It covered the
foundational topics and set the groundwork for more advanced features
and functions.

\

We learned the concepts around packages, packaging, naming convention,
dependency, and patch database. We looked at the variety of options
available with the rpm utility to perform package administration tasks
and put many of them into action to demonstrate their usage. Moreover,
we employed appropriate options to view and validate package metadata
information, GPG keys, and package attributes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0298.html}

## Review Questions {.style3}

\

1\. What would the rpm -ql zsh command do?

2\. What is the difference between installing and upgrading a package?

3\. Package database is located in the /var/lib/rpm directory. True or
False?

4\. What would the rpm -qf /bin/bash command do?

5\. Name the directory where RHEL 9 stores GPG signatures.

6\. What would the options ivh cause the rpm command to do?

7\. State the purpose of the rpm2cpio command.

8\. What is the difference between freshening and upgrading a package?

9\. The rpm command automatically takes care of package dependencies.
True or False?

10\. What would the rpm -qa command do?

::: {style="page-break-before: always;"}
:::

[]{#chapter0299.html}

## Answers to Review Questions {.style3}

\

1\. The command provided will list all the files that are included in
the installed zsh package.

2\. Installing will install a new package whereas upgrading will upgrade
an existing package or install it if it does not already exist.

3\. True.

4\. The command provided will display information about the /bin/bash
file.

5\. RHEL 9 stores GPG signatures in the /etc/pki/rpm-gpg directory.

6\. The rpm command will install the specified package and show
installation details and hash signs for progress.

7\. The rpm2cpio command is used to extract files from the specified
package.

8\. Both are used to upgrade an existing package, but freshening
requires an older version of the package to exist.

9\. False.

10\. The command provided will list all installed packages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0300.html}

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

[]{#chapter0301.html}

## Lab 9-1: Install and Verify Packages {.style3}

\

As user1 with sudo on server3, make sure the RHEL 9 ISO image is
attached to the VM and mounted. Use the rpm command and install the zsh
package by specifying its full path. Run the rpm command again and
perform the following on the zsh package: (1) show information, (2)
validate integrity, and (3) display attributes. (Hint: Package
Management with rpm).

::: {style="page-break-before: always;"}
:::

[]{#chapter0302.html}

## Lab 9-2: Query and Erase Packages {.style3}

\

As user1 with sudo on server3, make sure the RHEL 9 ISO image is
attached to the VM and mounted. Use the rpm command to perform the
following: (1) check whether the setup package is installed, (2) display
the list of configuration files in the setup package, (3) show
information for the zlib-devel package on the ISO image, (4) reinstall
the zsh package (\--reinstall -vh), and (5) remove the zsh package.
(Hint: Package Management with rpm).

::: {style="page-break-before: always;"}
:::

[]{#chapter0303.html}

## Chapter 10 {style="text-align: right"}

\

### Advanced Package Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Describe package groups

\

Understand application streams

\

Software repositories and how to access them

\

Perform software management operations using dnf

\

List, install, update, and delete individual packages and package groups

\

Show package information, determine provider, and search metadata

\

Exhibit package group information

\

#### RHCSA Objectives:

\

42\. Install and update software packages from Red Hat Network, a remote
repository, or from the local file system (part of this objective is
covered in Chapter 09)

::: {style="page-break-before: always;"}
:::

\

This is the second of the two chapters that discusses software
administration in RHEL. While the first chapter ( Chapter 09 ) expounds
upon the basic concepts of rpm package management and demonstrates a
basic command to manipulate individual packages, this chapter elaborates
on the concepts and handling of package groups. It also presents a
coverage on the concept of software repositories and how to configure
them.

\

::: {style="text-align: center;"}
![](image-2A9A67LB.jpg){height="100%"}
:::

The dnf command is superior to the rpm tool in the sense that it
performs automatic dependency checks and marks any identified extra
packages for installation. There are numerous options and subcommands
available with this advanced tool and it is capable of interacting with
software repositories as well.

::: {style="page-break-before: always;"}
:::

[]{#chapter0304.html}

## Advanced Package Management Concepts {.style3}

\

We discussed and grasped the basic package management concepts and
employed the rpm utility in a variety of ways to manipulate individual
packages. The focus of this chapter will be on understanding advanced
software packaging and distribution techniques, and using a tool that is
capable of handling a single package, discrete packages, and collection
of packages, efficiently.

\

RHEL 9 is shipped with two core repositories called BaseOS and
Application Stream (AppStream).

::: {style="page-break-before: always;"}
:::

[]{#chapter0305.html}

## Package Groups {.style3}

\

A package group is a collection of correlated packages designed to serve
a common purpose. It provides the convenience of querying, installing,
and deleting as a single unit rather than dealing with packages
individually. There are two types of package groups: environment groups
and package groups. The environment groups available in RHEL 9 are
server, server with GUI, minimal install, workstation, virtualization
host, and custom operating system. These are listed on the software
selection window during RHEL 9 installation. The package groups include
container management, smart card support, security tools, system tools,
network servers, etc.

::: {style="page-break-before: always;"}
:::

[]{#chapter0306.html}

## BaseOS Repository {.style3}

\

The BaseOS repository includes the core set of RHEL 9 components
including the kernel, modules, bootloader, and other foundational
software packages. These components lay the foundation to install and
run software applications and programs. BaseOS repository components are
available in the traditional rpm format.

::: {style="page-break-before: always;"}
:::

[]{#chapter0307.html}

## AppStream Repository {.style3}

\

The AppStream repository comes standard with core applications, as well
as several add-on applications many of them in the traditional rpm
format and some in the new modular format. These add-ons include web
server software, development languages, database software, etc. and are
shipped to support a variety of use cases and deployments.

::: {style="page-break-before: always;"}
:::

[]{#chapter0308.html}

## Benefits of Segregation {.style3}

\

There are two fundamental benefits to a segregation of the BaseOS
components from other applications: (1) it separates the application
components from the core operating system elements, and (2) it allows
publishers to deliver and administrators to apply application updates
more frequently. In RHEL version 7 and older, an OS update would update
all installed components including the kernel, service, and application
components to the latest versions by default. This could result in an
unstable system or a misbehaving application due to an unwanted upgrade
of one or more packages. By detaching the base OS components from the
applications, either of the two can be updated independent of the other.
This provides enhanced flexibility in tailoring the system components
and application workloads without impacting the underlying stability of
the system.

::: {style="page-break-before: always;"}
:::

[]{#chapter0309.html}

## dnf Repository {.style3}

\

A dnf repository (yum repository or simply a repo) is a digital library
for storing software packages. A repository is accessed for package
retrieval, query, update, and installation, and it may be free or for a
fee. The two repositories---BaseOS and AppStream---come preconfigured
with the RHEL 9 ISO image. There are a number of other repositories
available on the Internet that are maintained by software publishers
such as Red Hat and CentOS. Furthermore, you can build private custom
repositories for internal IT use for stocking and delivering software.
This may prove to be a good practice for an organization with a large
Linux server base, as it manages dependencies automatically and aids in
maintaining software consistency across the board. These repositories
can also be used to store in-house developed packages.

\

It is important to obtain software packages from authentic and reliable
sources such as Red Hat to prevent potential damage to your system and
to circumvent possible software corruption.

\

There is a process to create repositories and to access preconfigured
repositories. Creating repositories is beyond the scope of this book,
but you will configure access to the BaseOS and AppStream repositories
via a definition file to support the exercises and lab environment.

\

A sample repo definition file is shown below with some key directives:

\

\[BaseOS_RHEL_9\]

name= RHEL 9 base operating system components

baseurl=file:///mnt/BaseOS

enabled=1

gpgcheck=0

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Knowing how to configure a dnf repository using a URL plays an
important role in completing some of the RHCSA exam tasks successfully.
Use two forward slash characters (//) with the baseurl directive for an
FTP, HTTP, or HTTPS source.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The above example shows five lines from a sample repo file. Line 1
defines an exclusive ID within the square brackets. Line 2 is a brief
description of the repo with the "name" directive. Line 3 is the
location of the repodata directory with the "baseurl" directive. Line 4
shows whether this repository is active. Line 5 shows if packages are to
be GPG-checked for authenticity.

\

Each repository definition file must have a unique ID, a description,
and a baseurl directive defined at a minimum; other directives are set
as required. The baseurl directive for a local directory path is defined
as file:///local_path (the first two forward slash characters represent
the URL convention, and the third forward slash is for the absolute path
to the destination directory), and for FTP and HTTP(S) sources as
ftp://hostname/network_path and http(s)://hostname/network_path,
respectively. The network path must include a resolvable hostname or an
IP address.

::: {style="page-break-before: always;"}
:::

[]{#chapter0310.html}

## Software Management with dnf {.style3}

\

Software for enterprise Linux distributions such as Red Hat and CentOS
is available in the rpm format. These distributions offer tools to work
with individual packages as well as package groups. The rpm command was
used in the previous chapter to query, list, install, and erase
packages, in addition to a few other tasks that it can perform. This
command is limited to managing one package at a time.

\

A more capable tool for managing a single package or a group of packages
is referred to as dnf (or yum). This tool has an associated
configuration file that can define settings to control its behavior.

::: {style="page-break-before: always;"}
:::

[]{#chapter0311.html}

## dnf Configuration File {.style3}

\

The key configuration file for dnf is dnf.conf that resides in the
/etc/dnf directory. The "main" section in the file sets directives that
have a global effect on dnf operations. You can define separate sections
for each custom repository that you plan to set up on the system.
However, the preferred location to store configuration for each custom
repository in their own definition files is in the /etc/yum.repos.d
directory, which is the default location created for this purpose. The
default content of this configuration file is listed below:

\

<div>

![](image-XPOZIW0J.jpg){height="100%"}

</div>

[Table 10-1 explains the above and a few other directives that you may
define in the file. The directives in Table 10-1 are listed in an
alphabetical order.](#chapter0311.html)

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  best                                Specifies whether to install (or
                                      upgrade to) the latest available
                                      version

  clean_requirements_on_remove        Defines whether to remove
                                      dependencies during a package
                                      removal process that are no longer
                                      in use

  debuglevel                          Sets the level between 1 (minimum)
                                      and 10 (maximum) at which the debug
                                      is to be recorded in the logfile.
                                      Default is 2. A value of 0 disables
                                      this feature.

  gpgcheck                            Indicates whether to check the GPG
                                      signature for package authenticity.
                                      Default is 1 (enabled).

  installonly_limit                   Specifies a count of packages that
                                      can be installed concurrently.
                                      Default is 3.

  keepcache                           Defines whether to store the
                                      package and header cache following
                                      a successful installation. Default
                                      is 0 (disabled).

  logdir                              Sets the directory location to
                                      store the log files. Default is
                                      /var/log.

  obsoletes                           Checks and removes any obsolete
                                      dependent packages during installs
                                      and updates. Default is 1
                                      (enabled).
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 10-1 Directive Settings in dnf.conf File

\

There are a multitude of additional directives available that you may
want to set in the main section of this file or in custom repository
definition files. Run man 5 dnf.conf for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0312.html}

## The dnf Command {.style3}

\

The dnf command is the advanced package management tool in RHEL. This
utility requires the system to have access to a local or remote software
repository or to a local installable package file. The Red Hat
Subscription Management (RHSM) service available in the Red Hat Customer
Portal offers access to official Red Hat software repositories. There
are other web-based repositories that host packages that you may want to
install and use. Alternatively, you can set up a local, custom
repository on your RHEL system and add packages of your choice to it.

\

The primary benefit of using dnf over rpm is the former's ability to
resolve dependencies automatically by identifying and installing any
packages required for a successful installation of the specified
software. With multiple repositories in place, dnf extracts the software
from wherever it finds it.

\

dnf invokes the rpm utility in the background and can perform numerous
operations on individual packages or package groups such as listing,
querying, installing, and removing them.

\

[Table 10-2 summarizes the software handling tasks that dnf can perform
on packages. It also lists two subcommands (clean and repolist) that are
for repository operations. The subcommands are sequenced alphabetically.
Refer to the dnf command manual pages for additional subcommands,
operators, options, and examples.](#chapter0312.html)

\

  ----------------------------------- -----------------------------------
  Subcommand                          Description

  check-update                        Checks if updates are available for
                                      installed packages

  clean                               Removes cached data

  history                             Displays previous dnf activities as
                                      recorded in the
                                      /var/lib/dnf/history directory

  info                                Shows details for a package

  install                             Installs or updates a package

  list                                Lists installed and available
                                      packages

  provides                            Searches for packages that contain
                                      the specified file or feature

  reinstall                           Reinstalls the exact version of an
                                      installed package

  remove                              Removes a package and its
                                      dependencies

  repolist                            Lists enabled repositories

  repoquery                           Runs queries on available packages

  search                              Searches package metadata for the
                                      specified string

  upgrade                             Updates each installed package to
                                      the latest version
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 10-2 dnf Subcommands for Package and Repository Manipulation

\

[Table 10-3 lists and describes dnf subcommands that are intended for
operations on package groups.](#chapter0312.html)

\

  ----------------------------------- -----------------------------------
  Subcommand                          Description

  group install                       Installs or updates a package group

  group info                          Returns details for a package group

  group list                          Lists available package groups

  group remove                        Removes a package group
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 10-3 dnf Subcommands for Package Group Manipulation

\

You will use most of the subcommands from the two Tables in the examples
and exercises that follow, but first you'll need to create a definition
file and configure access to the two repositories available on the RHEL
9 ISO image.

::: {style="page-break-before: always;"}
:::

[]{#chapter0313.html}

## Exercise 10-1: Configure Access to Pre-Built Repositories {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will set up access to the two dnf repositories
that are available on RHEL 9 image. You've already configured an
automatic mounting of RHEL 9 image on /mnt in Chapter 09 "Basic Package
Management". You will create a definition file for the repositories and
confirm.

\

1\. Verify that the image is currently mounted:

\

<div>

![](image-L4U16DAS.jpg){height="100%"}

</div>

2\. Create a definition file called local.repo in the /etc/yum.repos.d
directory using the vim editor and define the following data for both
repositories in it:

\

<div>

![](image-F90YG1AS.jpg){height="100%"}

</div>

3\. Confirm access to the repositories:

\

<div>

![](image-JLG0R8I5.jpg){height="100%"}

</div>

\

<div>

![](image-2E1B8HCW.jpg){height="100%"}

</div>

Ignore any lines that are related to subscription and system
registration (not shown in the above output). The output provides
details for the two repositories. It shows the rate at which the command
read the repo data (lines 3 and 4) followed by separate metadata
sections for each repository. Each section contains repository ID, name,
count of packages, total size of all the packages, mount location, and
the file holding the repo information. As depicted, the AppStream repo
consists of 5,472 packages and the BaseOS repo contains 1,137 packages.
Both repos are enabled and are ready for use.

\

We have divided software administration operations into two sections
below to focus on individual packages and package groups.

::: {style="page-break-before: always;"}
:::

[]{#chapter0314.html}

## Individual Package Management {.style3}

\

The dnf command can be used to perform a variety of operations on
individual packages, just like the rpm command. The following
subsections elaborate with examples on using this tool to list, install,
query, and remove packages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0315.html}

## Listing Available and Installed Packages {.style3}

\

Listing the packages that are available for installation from one or
more enabled repositories helps you understand what is in the current
software inventory and what is needed. Likewise, listing the packages
that are already installed on the system enables you to make important
decisions as to whether they should be retained, upgraded, downgraded,
or erased. The dnf command lists available packages as well as installed
packages.

\

To list all packages available for installation from all enabled repos,
run a query against the two repositories that we configured earlier, as
those are the only ones you currently have access to. The following
command will result in a long output.

\

<div>

![](image-P75SPRD8.jpg){height="100%"}

</div>

\

<div>

![](image-KX3XY2DR.jpg){height="100%"}

</div>

To limit the above to the list of packages that are available only from
a specific repo:

\

<div>

![](image-IOO8OQP9.jpg){height="100%"}

</div>

You can grep for an expression to narrow down your search. For example,
to find whether the BaseOS repo includes the zsh package, run the
following:

\

<div>

![](image-HB4G6I1W.jpg){height="100%"}

</div>

To list all installed packages on the system:

\

<div>

![](image-PY4I52WH.jpg){height="100%"}

</div>

The graphic above shows the output in three columns: package name,
package version, and the repo it was installed from. \@anaconda means
the package was installed at the time of RHEL installation.

\

To list all installed packages and all packages available for
installation from all enabled repositories:

\

<div>

![](image-AB7TH0PO.jpg){height="100%"}

</div>

\

<div>

![](image-4KNWGQM2.jpg){height="100%"}

</div>

The @ sign that precedes a repository name in column 3 identifies the
package as installed.

\

To list all packages available from all enabled repositories that should
be able to update:

\

<div>

![](image-VIXJE8YM.jpg){height="100%"}

</div>

To list whether a package (bc, for instance) is installed or available
for installation from any enabled repository:

\

<div>

![](image-07918YLP.jpg){height="100%"}

</div>

To list all installed packages whose names begin with the string "gnome"
followed by any number of characters:

\

<div>

![](image-SX46OSHN.jpg){height="100%"}

</div>

To list recently added packages:

\

<div>

![](image-E2IAYMJZ.jpg){height="100%"}

</div>

Refer to the repoquery and list subsections of the dnf command manual
pages for more options and examples.

::: {style="page-break-before: always;"}
:::

[]{#chapter0316.html}

## Installing and Updating Packages {.style3}

\

Installing a package creates the necessary directory tree for the
specified and dependent packages, installs the required files, and runs
any post-installation steps. If the package being loaded is already
present, the dnf command updates it to the latest available version. By
default, dnf prompts for a yes or no confirmation unless the -y flag is
entered with the command.

\

The following attempts to install a package called keybinder3, but
proceeds with an update if it detects the presence of an older version:

\

<div>

![](image-5QFN5UQV.jpg){height="100%"}

</div>

\

<div>

![](image-LOACB9HT.jpg){height="100%"}

</div>

The above dnf command example resolved dependencies and showed a list of
the packages that it would install. It exhibited the size of the
packages and the amount of disk space that the installation would
consume. It downloaded the packages after confirmation to proceed and
installed them. It completed the installation after every package was
verified. A list of the installed packages was displayed at the bottom
of the output.

\

To install or update a package called dcraw located locally at
/mnt/AppStream/Packages:

\

<div>

![](image-2NMORC8P.jpg){height="100%"}

</div>

To update an installed package (autofs, for example) to the latest
available version. Note that dnf will fail if the specified package is
not already installed.

\

<div>

![](image-5MBYWKO9.jpg){height="100%"}

</div>

To update all installed packages to the latest available versions:

\

<div>

![](image-HX7IE4ZG.jpg){height="100%"}

</div>

Refer to the install and update subsections of the dnf command manual
pages for more options and examples.

::: {style="page-break-before: always;"}
:::

[]{#chapter0317.html}

## Exhibiting Package Information {.style3}

\

Displaying information for a package shows its name, architecture it is
built for, version, release, size, whether it is installed or available
for installation, repo name it was installed or is available from, short
and long descriptions, license, and so on. This information can be
viewed by supplying the info subcommand to dnf.

\

To view information about a package called autofs:

\

<div>

![](image-VA4SFPXY.jpg){height="100%"}

</div>

The output shows that autofs is not currently installed, but it is
available for installation from the BaseOS repo. The info subcommand
automatically determines whether the specified package is installed.

\

Refer to the info subsection of the dnf command's manual pages for more
options available for viewing package information.

::: {style="page-break-before: always;"}
:::

[]{#chapter0318.html}

## Removing Packages {.style3}

\

Removing a package uninstalls it and removes all associated files and
directory structure. It also erases any dependencies as part of the
deletion process. By default, dnf prompts for a yes or no confirmation
unless the -y flag is specified at the command line.

\

To remove a package called keybinder3:

\

<div>

![](image-R39CARXZ.jpg){height="100%"}

</div>

The above output resolved dependencies and showed a list of the packages
that it would remove. It displayed the amount of disk space that their
removal would free up. After confirmation to proceed, it erased the
identified packages and verified their removal. A list of the removed
packages was exhibited at the bottom of the output.

\

Refer to the remove subsection of the dnf command's manual pages for
more options and examples available for removing packages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0319.html}

## Exercise 10-2: Manipulate Individual Packages {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will perform management operations on a package
called cifs-utils. You will determine if this package is already
installed and if it is available for installation. You will display its
information before installing it. You will install the package and
exhibit its information. Finally, you will erase the package along with
its dependencies and confirm the removal.

\

1\. Check whether the cifs-utils package is already installed:

\

<div>

![](image-EGOVTKJP.jpg){height="100%"}

</div>

The command returned to the prompt without any output, which implies
that the specified package is not installed.

\

2\. Determine if the cifs-utils package is available for installation:

\

<div>

![](image-6AWTPRD9.jpg){height="100%"}

</div>

The package is available for installation. The output shows its version
as well.

\

3\. Display detailed information about the package:

\

<div>

![](image-VFBX39N9.jpg){height="100%"}

</div>

The output is indicative of the fact that the package is available for
installation from the BaseOS repo.

\

4\. Install the package:

\

<div>

![](image-E36FJDAN.jpg){height="100%"}

</div>

5\. Display the package information again:

\

<div>

![](image-6ZDXM0BM.jpg){height="100%"}

</div>

The output reveals that the package is now installed.

\

6\. Remove the package:

\

<div>

![](image-4SFL3YEO.jpg){height="100%"}

</div>

7\. Confirm the removal:

\

<div>

![](image-FVANQ567.jpg){height="100%"}

</div>

The no output above confirms that the package is not loaded on the
system.

::: {style="page-break-before: always;"}
:::

[]{#chapter0320.html}

## Determining Provider and Searching Package Metadata {.style3}

\

Determining package contents includes search operations on installed and
available packages. For instance, you can determine what package a
specific file belongs to or which package comprises a certain string.
The following examples show how to carry out these tasks.

\

To search for packages that contain a specific file such as /etc/passwd,
use the provides or the whatprovides subcommand with dnf:

\

<div>

![](image-XPAK0ELP.jpg){height="100%"}

</div>

The output returns two instances of the file. The first one indicates
that the passwd file is part of a package called setup, which was
installed during RHEL installation, and the second instance shows it as
part of the setup package from the BaseOS repository.

\

With the provides (whatprovides) subcommand, you can also use a wildcard
character for filename expansion. For example, the following command
will list all packages that contain filenames beginning with
"system-config" followed by any number of characters:

\

<div>

![](image-XW0UP1HX.jpg){height="100%"}

</div>

To search for all the packages that match the specified string in their
name or summary:

\

<div>

![](image-KUNHGB9G.jpg){height="100%"}

</div>

The above outcome depicts three matches, two in package names and one in
summary.

::: {style="page-break-before: always;"}
:::

[]{#chapter0321.html}

## Package Group Management {.style3}

\

The dnf command can be used to perform ample operations on package
groups by specifying the group subcommand with it. The following
subsections elaborate with examples on using this tool to list, install,
query, and remove groups of packages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0322.html}

## Listing Available and Installed Package Groups {.style3}

\

The group list subcommand can be used with dnf to list the package
groups available for installation from either or both repos, as well as
to list the package groups that are already installed.

\

To list all available and installed package groups from all
repositories:

\

<div>

![](image-W7C8QKJC.jpg){height="100%"}

</div>

The output reveals two categories of package groups: an environment
group and a group. An environment group is a larger collection of RHEL
packages that provides all necessary software to build the operating
system foundation for a desired purpose. The Server with GUI environment
group was selected at the time of installing server1, which installed a
multitude of packages as well as the GNOME desktop. See Table 1-2 in
Chapter 01 "Local Installation" for a description of other environment
groups.

\

A group, on the other hand, is a small bunch of RHEL packages that serve
a common purpose. It also saves time on the deployment of individual and
dependent packages. The above output shows two installed and several
available package groups.

\

To display the number of installed and available package groups:

\

<div>

![](image-2MIXMQDS.jpg){height="100%"}

</div>

To list all installed and available package groups including those that
are hidden:

\

<div>

![](image-32L923JP.jpg){height="100%"}

</div>

Try group list with \--installed and \--available options to narrow down
the output list.

\

To list all packages that a specific package group such as Base (not
shown in the above output) contains:

\

<div>

![](image-7KI5ABVP.jpg){height="100%"}

</div>

You may use the -v option with group info for more information. Refer to
the group list and group info subsections of the dnf command's manual
pages for more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0323.html}

## Installing and Updating Package Groups {.style3}

\

Installing a package group creates the necessary directory structure for
all the packages included in the group and all dependent packages,
installs the required files, and runs any post-installation steps. If
the package group is being loaded or part of it is already present, the
command attempts to update all the packages included in the group to the
latest available versions. By default, dnf prompts for a yes or no
confirmation unless the -y flag is entered with the command.

\

The following example attempts to install a package group called smart
card support, but proceeds with an update if it detects the presence of
an older version. You may enclose the group name within either single or
double quotation marks.

\

<div>

![](image-9WAQL7P3.jpg){height="100%"}

</div>

\

<div>

![](image-LF9LNFIF.jpg){height="100%"}

</div>

The output discloses that the command installed five packages located
across the two repositories to complete the installation of the package
group.

\

To update the smart card support group to the latest version:

\

<div>

![](image-6F2P5EZR.jpg){height="100%"}

</div>

The above command will update all the packages within the package group
to their latest versions if it has access to them. Refer to the group
install and group update subsections of the dnf command's manual pages
for more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0324.html}

## Removing Package Groups {.style3}

\

Removing a package group uninstalls all the included packages and
deletes all associated files and directory structure. It also erases any
dependencies as part of the deletion process. By default, dnf prompts
for a yes or no confirmation unless the -y flag is specified at the
command line.

\

To erase the smart card support package group that was installed
earlier:

\

<div>

![](image-2N3ZZD33.jpg){height="100%"}

</div>

The above output resolved dependencies and showed a list of the packages
that it would remove. It displayed the amount of disk space that their
removal would free up. After confirmation to proceed, it erased the
identified packages and verified their removal. A list of the removed
packages was exposed at the bottom of the output.

\

Refer to the remove subsection of the dnf command's manual pages for
more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0325.html}

## Exercise 10-3: Manipulate Package Groups {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will perform management operations on a package
group called system tools. You will determine if this group is already
installed and if it is available for installation. You will list the
packages it contains and install it. Finally, you will remove the group
along with its dependencies and confirm the removal.

\

1\. Check whether the system tools package group is already installed:

\

<div>

![](image-Y2859G3Y.jpg){height="100%"}

</div>

The output does not show it installed.

\

2\. Determine if this package group is available for installation:

\

<div>

![](image-P7DKXRKX.jpg){height="100%"}

</div>

The group is available for installation.

\

3\. Display the list of packages this group contains:

\

<div>

![](image-EY2LZWUE.jpg){height="100%"}

</div>

The output returns a long list of packages that are included in this
group. All the packages will be installed as part of the group
installation.

\

4\. Install the group:

\

<div>

![](image-5Y67BFXE.jpg){height="100%"}

</div>

5\. Remove the group:

\

<div>

![](image-8SBRXCOM.jpg){height="100%"}

</div>

6\. Confirm the removal:

\

<div>

![](image-3ZU9LNX9.jpg){height="100%"}

</div>

\

<div>

![](image-CLH1C1UT.jpg){height="100%"}

</div>

The package group is not listed in the above output, which confirms its
removal.

::: {style="page-break-before: always;"}
:::

[]{#chapter0326.html}

## Chapter Summary {.style3}

\

This chapter is the second of the two chapters (the first one being
Chapter 09) with coverage on software management. This chapter covers
advanced topics: yum repositories and package groups.

\

We looked at the concept of package repositories and demonstrated
setting up access to a local repo. Employing repositories for package
installation and automatic dependency selection make software
installation much easier than to use the rpm command.

\

We learned about package groups and the benefits of using them in
contrast to handling individual software packages.

\

Finally, we examined the dnf command and discovered its benefits over
the standard rpm command. dnf offers a variety of options and
subcommands that we employed in this chapter to demonstrate installing,
listing, querying, updating, and deleting individual packages and
package groups. Other management operations such as exhibiting package
data, ascertaining provider, and searching metadata for information were
also covered.

::: {style="page-break-before: always;"}
:::

[]{#chapter0327.html}

## Review Questions {.style3}

\

1\. What dnf subcommand would we use to check available updates for
installed packages?

2\. What is the concept of module in RHEL 9?

3\. What must be the extension of a yum repository file?

4\. What would the dnf list zsh command do?

5\. What would the dnf list installed \*gnome\* command do?

6\. How many package names can be specified at a time with the dnf
install command?

7\. Name the two default yum repositories that contain all the packages
for RHEL 9?

8\. What would the dnf group info Base command do?

9\. Which dnf subcommand can be used to list all available repositories?

10\. What is the use of the -y option with the dnf group install
command?

11\. What is the main advantage of using dnf over rpm?

12\. We can update all the packages within a package group using the
groupupdate subcommand with dnf. True or False?

13\. What would the dnf info zsh command do?

::: {style="page-break-before: always;"}
:::

[]{#chapter0328.html}

## Answers to Review Questions {.style3}

\

1\. The check-update subcommand.

2\. A module is a collection of packages, including the dependent
packages, that are required to install an application.

3\. The extension of a yum repository configuration file must be .repo
in order to be recognized as a valid repo file.

4\. The command provided will display installed and available zsh
package.

5\. The command provided will display all installed packages that
contain gnome in their names.

6\. There is no limit.

7\. The two yum repositories the BaseOS and AppStream.

8\. The command provided will list all packages in the specified package
group.

9\. The repolist subcommand.

10\. dnf will not prompt for user confirmation if the -y option is used
with it.

11\. dnf resolves and installs dependent packages automatically.

12\. True.

13\. The command provided will display the header information for the
zsh package.

::: {style="page-break-before: always;"}
:::

[]{#chapter0329.html}

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

[]{#chapter0330.html}

## Lab 10-1: Configure Access to RHEL 9 Repositories {.style3}

\

As user1 with sudo on server3, make sure the RHEL 9 ISO image is
attached to the VM and mounted. Create a definition file under
/etc/yum.repos.d, and define two blocks (one for BaseOS and another for
AppStream). Verify the configuration with dnf repolist. You should see
numbers in thousands under the Status column for both repositories.
(Hint1: Chapter 09: Package Management with rpm). (Hint2: Chapter 10:
Software Management with dnf).

::: {style="page-break-before: always;"}
:::

[]{#chapter0331.html}

## Lab 10-2: Install and Manage Individual Packages {.style3}

\

As user1 with sudo on server3 and using the dnf command, list all
installed and available packages separately. Show which package contains
the /etc/group file. Install the package httpd. Review /var/log/dnf.log
for confirmation. Perform the following on the httpd package: (1) show
information, (2) list dependencies, and (3) remove it. (Hint: Individual
Package Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0332.html}

## Lab 10-3: Install and Manage Package Groups {.style3}

\

As user1 with sudo on server3 and using the dnf command, list all
installed and available package groups separately. Install package
groups Security Tools and Scientific Support. Review /var/log/dnf.log
for confirmation. Show the packages included in the Scientific Support
package group and delete this group. (Hint: Package Group Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0333.html}

## Chapter 11 {style="text-align: right"}

\

### Boot Process, GRUB2, and the Linux Kernel {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Linux boot process: firmware, bootloader, kernel, and initialization

\

Understand and interact with GRUB2 to boot into different targets

\

Modify GRUB2 configuration

\

Boot system into specific targets

\

Reset lost or forgotten root user password

\

Linux kernel, packages, version anatomy, and key directories

\

Download and install a new kernel version

\

#### RHCSA Objectives:

\

18\. Interrupt the boot process in order to gain access to a system

43\. Modify the system bootloader

::: {style="page-break-before: always;"}
:::

\

RHEL goes through multiple phases during the boot process. It starts
selective services during its transition from one phase into another. It
presents the administrator an opportunity to interact with a preboot
program to boot the system into a non-default target, pass an option to
the kernel, or reset the lost or forgotten root user password. It
launches a number of services during its transition to the default or
specified target.

\

::: {style="text-align: center;"}
![](image-GLL6B3U1.jpg){height="100%"}
:::

The kernel controls everything on the system. It controls the system
hardware, enforces security and access controls, and runs, schedules,
and manages processes and service daemons. The kernel is comprised of
several modules. A new kernel must be installed or an existing kernel
must be upgraded when the need arises from an application or
functionality standpoint.

::: {style="page-break-before: always;"}
:::

[]{#chapter0334.html}

## Linux Boot Process {.style3}

\

RHEL goes through a boot process after the system has been powered up or
restarted. The boot process lasts until all enabled services are
started. A login prompt will appear on the screen, which allows users to
log in to the system. The boot process is automatic, but you may need to
interact with it to take a non-default action, such as booting an
alternative kernel, booting into a non-default operational state,
repairing the system, recovering from an unbootable state, and so on.
The boot process on an x86 computer may be split into four major phases:
(1) the firmware phase, (2) the bootloader phase, (3) the kernel phase,
and (4) the initialization phase. The system accomplishes these phases
one after the other while performing and attempting to complete the
tasks identified in each phase.

::: {style="page-break-before: always;"}
:::

[]{#chapter0335.html}

## The Firmware Phase (BIOS and UEFI) {.style3}

\

The firmware is the BIOS (Basic Input/Output System) or the UEFI
(Unified Extensible Firmware Interface) code that is stored in flash
memory on the x86-based system board. It runs the Power-On-Self-Test
(POST) to detect, test, and initialize the system hardware components.
While doing so, it installs appropriate drivers for the video hardware
and exhibit system messages on the screen. The firmware scans the
available storage devices to locate a boot device, starting with a
512-byte image that contains 446 bytes of the bootloader program, 64
bytes for the partition table, and the last two bytes with the boot
signature. This 512-byte tiny area is referred to as the Master Boot
Record (MBR) and it is located on the first sector of the boot disk. As
soon as it discovers a usable boot device, it loads the bootloader into
memory and passes control over to it.

\

The BIOS is a small memory chip in the computer that stores system date
and time, list and sequence of boot devices, I/O configuration, etc.
This configuration is customizable. Depending on the computer hardware,
you need to press a key to enter the BIOS setup or display a menu to
choose a source to boot the system. The computer goes through the
hardware initialization phase that involves detecting and diagnosing
peripheral devices. It runs the POST on the devices as it finds them,
installs drivers for the graphics card and the attached monitor, and
begins exhibiting system messages on the video hardware. It discovers a
usable boot device, loads the bootloader program into memory, and passes
control over to it. Boot devices on most computers support booting from
optical and USB flash devices, hard drives, network, and other media.

\

The UEFI is a new 32/64-bit architecture-independent specification that
computer manufacturers have widely adopted in their latest hardware
offerings replacing BIOS. This mechanism delivers enhanced boot and
runtime services, and superior features such as speed over the legacy
16-bit BIOS. It has its own device drivers, is able to mount and read
extended file systems, includes UEFI-compliant application tools, and
supports one or more bootloader programs. It comes with a boot manager
that allows you to choose an alternative boot source. Most computer
manufacturers have customized the features for their hardware platform.
You may find varying menu interfaces among other differences.

::: {style="page-break-before: always;"}
:::

[]{#chapter0336.html}

## The Bootloader Phase {.style3}

\

Once the firmware phase is over and a boot device is detected, the
system loads a piece of software called bootloader that is located in
the boot sector of the boot device. RHEL uses GRUB2 (GRand Unified
Bootloader) version 2 as the bootloader program. GRUB2 supports both
BIOS and UEFI firmware.

\

The primary job of the bootloader program is to spot the Linux kernel
code in the /boot file system, decompress it, load it into memory based
on the configuration defined in the /boot/grub2/grub.cfg file, and
transfer control over to it to further the boot process. For UEFI-based
systems, GRUB2 looks for the EFI system partition /boot/efi instead, and
runs the kernel based on the configuration defined in the
/boot/efi/EFI/redhat/grub.efi file. The next section details the
interaction with the bootloader.

::: {style="page-break-before: always;"}
:::

[]{#chapter0337.html}

## The Kernel Phase {.style3}

\

The kernel is the central program of the operating system, providing
access to hardware and system services. After getting control from the
bootloader, the kernel extracts the initial RAM disk (initrd) file
system image found in the /boot file system into memory, decompresses
it, and mounts it as read-only on /sysroot to serve as the temporary
root file system. The kernel loads necessary modules from the initrd
image to allow access to the physical disks and the partitions and file
systems therein. It also loads any required drivers to support the boot
process. Later, it unmounts the initrd image and mounts the actual
physical root file system on / in read/write mode.

\

At this point, the necessary foundation has been built for the boot
process to carry on and to start loading the enabled services. The
kernel executes the systemd process with PID 1 and passes the control
over to it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0338.html}

## The Initialization Phase {.style3}

\

This is the fourth and the last phase in the boot process. systemd takes
control from the kernel and continues the boot process. It is the
default system initialization scheme used in RHEL 9. It starts all
enabled userspace system and network services and brings the system up
to the preset boot target.

\

A boot target is an operational level that is achieved after a series of
services have been started to get to that state. More on targets later
in this chapter.

\

The system boot process is considered complete when all enabled services
are operational for the boot target and users are able to log in to the
system. A detailed discussion on systemd is furnished in Chapter 12
"System Initialization, Message Logging, and System Tuning".

::: {style="page-break-before: always;"}
:::

[]{#chapter0339.html}

## The GRUB2 Bootloader {.style3}

\

After the firmware phase has concluded, the bootloader presents a menu
with a list of bootable kernels available on the system and waits for a
predefined amount of time before it times out and boots the default
kernel. You may want to interact with GRUB2 before the autoboot times
out to boot with a non-default kernel, boot to a different target, or
customize the kernel boot string.

\

Pressing a key before the timeout expires allows you to interrupt the
autoboot process and interact with GRUB2. If you wish to boot the system
using the default boot device with all the configured default settings,
do not press any key, as shown in Figure 11-1, and let the system go
through the autoboot process.

\

::: {style="text-align: center;"}
![](image-KI0NX1B0.jpg){height="100%"}
:::

Figure 11-1 GRUB2 Menu

\

The line at the bottom in Figure 11-1 shows the autoboot countdown in
seconds. The default value is 5 seconds. If you press no keys within the
5 seconds, the highlighted kernel will boot automatically.

::: {style="page-break-before: always;"}
:::

[]{#chapter0340.html}

## Interacting with GRUB2 {.style3}

\

The GRUB2 main menu shows a list of bootable kernels at the top. You can
change the selection using the Up or Down arrow key. It lets you edit a
selected kernel menu entry by pressing an e or go to the grub\> command
prompt by pressing a c.

\

In the edit mode, GRUB2 loads the configuration for the selected kernel
entry from the /boot/grub2/grub.cfg file in an editor, enabling you to
make a desired modification before booting the system. For instance, you
can boot the system into a less capable operating target by adding
"rescue", "emergency", or "3" to the end of the line that begins with
the keyword "linux", as depicted in Figure 11-2. Press Ctrl+x when done
to boot. Remember that this is a one-time temporary change and it won't
touch the grub.cfg file.

\

::: {style="text-align: center;"}
![](image-64CTDI7S.jpg){height="100%"}
:::

Figure 11-2 GRUB2 Kernel Entry Edit

\

If you do not wish to boot the system at this time, you can press ESC to
discard the changes and return to the main menu.

\

The grub\> command prompt appears when you press Ctrl+c while in the
edit window or a c from the main menu. The command mode provides you
with the opportunity to execute debugging, recovery, and many other
tasks. You can view available commands by pressing the TAB key. See
Figure 11-3.

\

::: {style="text-align: center;"}
![](image-XZ619VZP.jpg){height="100%"}
:::

Figure 11-3 GRUB2 Commands

\

There are over one hundred commands available to perform a variety of
tasks at the GRUB2 level.

::: {style="page-break-before: always;"}
:::

[]{#chapter0341.html}

## Understanding GRUB2 Configuration Files {.style3}

\

The GRUB2 configuration file, grub.cfg, is located in the /boot/grub2
directory. This file is referenced at boot time. This file is generated
automatically when a new kernel is installed or upgraded, so it is not
advisable to modify it directly, as your changes will be overwritten.
The primary source file that is used to regenerate grub.cfg is called
grub, and it is located in the /etc/default directory. This file defines
the directives that govern how GRUB2 should behave at boot time. Any
changes made to the grub file will only take effect after the
grub2-mkconfig utility has been executed.

\

Let's analyze the two files to understand their syntax and contents.

\

### The /etc/default/grub File {.style3}

The grub file defines the directives that control the behavior of GRUB2
at boot time. Any changes in this file must be followed by the execution
of the grub2-mkconfig command in order to be reflected in grub.cfg.

\

Here is an enumerated list of the default settings from the grub file,
followed by an explanation in Table 11-1:

\

<div>

![](image-SLTUKGRN.jpg){height="100%"}

</div>

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  GRUB_TIMEOUT                        Defines the wait time, in seconds,
                                      before booting off the default
                                      kernel. Default value is 5.

  GRUB_DISTRIBUTOR                    Sets the name of the Linux
                                      distribution

  GRUB_DEFAULT                        Boots the selected option from the
                                      previous system boot

  GRUB_DISABLE_SUBMENU                Enables/disables the appearance of
                                      GRUB2 submenu

  GRUB_TERMINAL_OUTPUT                Sets the default terminal

  GRUB_CMDLINE_LINUX                  Specifies the command line options
                                      to pass to the kernel at boot time

  GRUB_DISABLE_RECOVERY               Lists/hides system recovery entries
                                      in the GRUB2 menu

  GRUB_ENABLE_BLSCFG                  Defines whether to use the new
                                      bootloader specification to manage
                                      bootloader configuration
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 11-1 GRUB2 Default Settings

\

Generally, you do not need to make any changes to this file, as the
default settings are good enough for normal system operation.

\

### The grub.cfg File {.style3}

The grub.cfg is the main GRUB2 configuration file that supplies
boot-time configuration information. This file is located in the
/boot/grub2 directory on BIOS-based systems and in the
/boot/efi/EFI/redhat directory on UEFI-based systems. This file can be
recreated manually with the grub2-mkconfig utility, or it is
automatically regenerated when a new kernel is installed or upgraded. In
either case, this file will lose any previous manual changes made to it.

\

During the recreation process, the grub2-mkconfig command also uses the
settings defined in helper scripts located in the /etc/grub.d directory.
There are plenty of files located here, as shown below:

\

<div>

![](image-R1989XH9.jpg){height="100%"}

</div>

The first script, 00_header, sets the GRUB2 environment; the 10_linux
script searches for all installed kernels on the same disk partition;
the 30_os-prober searches for the presence of other operating systems;
and 40_custom and 41_custom store user customizations. An example would
be to add custom entries to the boot menu.

\

The grub.cfg file also sources the grubenv file located in the
/boot/grub2 directory for kernel options and other settings. Here is
what this file contains on server1:

\

<div>

![](image-4VDOD6IG.jpg){height="100%"}

</div>

If a new kernel is installed, the existing kernel entries remain intact.
All bootable kernels are listed in the GRUB2 menu, and any of the kernel
entries can be selected to boot.

\

## Exercise 11-1: Change Default System Boot Timeout {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will change the default system boot timeout value
to 8 seconds persistently, and validate.

\

1\. Edit the /etc/default/grub file and change the setting as follows:

\

<div>

![](image-UQCPFURL.jpg){height="100%"}

</div>

2\. Execute the grub2-mkconfig command to reproduce grub.cfg:

\

<div>

![](image-YRZSX2GQ.jpg){height="100%"}

</div>

3\. Restart the system with sudo reboot and confirm the new timeout
value when GRUB2 menu appears.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0342.html}

## Booting into Specific Targets {.style3}

\

RHEL boots into graphical target state by default if the Server with GUI
software selection is made during installation. It can also be directed
to boot into non-default but less capable operating targets from the
GRUB2 menu. Additionally, in situations when it becomes mandatory to
boot the system into an administrative state for implementing a function
that cannot be otherwise performed in other target states or for system
recovery, RHEL offers emergency and rescue boot targets. These special
target levels can be launched from the GRUB2 interface by selecting a
kernel, pressing e to enter the edit mode, and appending the desired
target name to the line that begins with the keyword "linux".

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You must know how to boot a RHEL 9 system into a specific
target from the GRUB2 menu to modify the fstab file or reset an unknown
root user password.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Here is how you would append "emergency" to the kernel line entry:

\

<div>

![](image-3BFW34RH.jpg){height="100%"}

</div>

Press Ctrl+x after making the modification to boot the system into the
supplied target. You will be required to enter the root user password to
log on. Run reboot after you are done to reboot the system.

\

<div>

![](image-VFAG48NT.jpg){height="100%"}

</div>

Similarly, you can append "rescue" (or simply "1", "s", or "single") to
the "linux" line and press Ctrl+x to boot into the rescue target.

::: {style="page-break-before: always;"}
:::

[]{#chapter0343.html}

## Exercise 11-2: Reset the root User Password {.style3}

\

This exercise should be done on server1.

\

For this exercise, assume that the root user password is lost, stolen,
or forgotten, and it needs to be reset.

\

In this exercise, you will terminate the boot process at an early stage
to be placed in a special debug shell to reset the root password.

\

1\. Reboot or reset server1, and interact with GRUB2 by pressing a key
before the autoboot times out. Highlight the rescue kernel entry in the
GRUB2 menu and press e to enter the edit mode. Scroll down to the line
entry that begins with the keyword "linux" and press the End key to go
to the end of that line:

\

<div>

![](image-2066CCQ8.jpg){height="100%"}

</div>

2\. Modify this kernel string and append "rd.break" to the end of the
line to make the boot process stop after the initial ram disk (rd) has
been loaded into memory. It should look like:

\

<div>

![](image-RIS8ABOF.jpg){height="100%"}

</div>

3\. Press Ctrl+x when done to boot to the special shell. The system
mounts the root file system read-only on the /sysroot directory. Press
the Enter key when prompted to enter the maintenance mode:

\

<div>

![](image-XF4L26QO.jpg){height="100%"}

</div>

4\. Make /sysroot appear as mounted on / using the chroot command, and
confirm:

\

<div>

![](image-HA8XJT3V.jpg){height="100%"}

</div>

5\. Remount the root file system in read/write mode to allow the passwd
command to modify the shadow file and replace the password:

\

<div>

![](image-ERAPZ0IU.jpg){height="100%"}

</div>

6\. Enter a new password for root by invoking the passwd command:

\

<div>

![](image-5CHNU1P4.jpg){height="100%"}

</div>

7\. Create a hidden file called .autorelabel to instruct the operating
system to run SELinux relabeling on all files, including the shadow file
that was updated with the new root password, on the next reboot:

\

<div>

![](image-KP42M3WI.jpg){height="100%"}

</div>

\

SELinux is discussed in detail in Chapter 20 "Security Enhanced Linux".

\

8\. Issue the exit command to return to the chroot shell and then again
to relabel SELinux and restart the system to boot to the default target.

\

<div>

![](image-6IS3N618.jpg){height="100%"}

</div>

Depending on the system size and disk speed, it might take a few minutes
for the system to complete the relabeling process and return to a fully
functional state.

::: {style="page-break-before: always;"}
:::

[]{#chapter0344.html}

## The Linux Kernel {.style3}

\

The kernel is the core of the Linux system. It manages hardware,
enforces security, regulates access to the system, as well as handles
processes, services, and application workloads. It is a collection of
software components called modules that work in tandem to provide a
stable and controlled platform. Modules are device drivers that control
hardware devices---the processor, memory, storage, controller cards, and
peripheral equipment, and interact with software subsystems, such as
storage management, file systems, networking, and virtualization.

\

Some of these modules are static to the kernel and are integral to
system functionality, while others are loaded dynamically as needed,
making the kernel speedier and more efficient in terms of overall
performance and less vulnerable to crashes. RHEL 9 is shipped with
kernel version 5.14.0 for the 64-bit Intel/AMD processor architecture
computers with single, multi-core, and multi-processor configurations.
On a Linux system, uname -m reveals the architecture of the system.

\

The default kernel installed during the installation is usually adequate
for most system needs; however, it requires a rebuild when a new
functionality is added or removed. The new functionality may be
introduced by installing a new kernel, upgrading an existing one,
installing a new hardware device, or changing a critical system
component. Likewise, an existing functionality that is no longer needed
may be removed to make the overall footprint of the kernel smaller,
resulting in improved performance and reduced memory utilization.

\

To control the behavior of the modules, and the kernel in general, a
variety of tunable parameters are set that define a baseline for kernel
functionality. Some of these parameters must be tuned to allow certain
applications and database software to be installed smoothly and operate
properly.

\

RHEL allows you to generate and store several custom kernels with varied
configuration and required modules, but only one of them can be active
at a time. A different kernel may be loaded by interacting with GRUB2.

::: {style="page-break-before: always;"}
:::

[]{#chapter0345.html}

## Kernel Packages {.style3}

\

Just like any other software that comes in the rpm format for RHEL, the
software comprising the kernel is no different. There is a set of core
kernel packages that must be installed on the system at a minimum to
make it work. Additional packages providing supplementary kernel support
are also available. Table 11-2 lists and describes the core and some
add-on kernel packages.

\

  ----------------------------------- -----------------------------------
  Kernel Package                      Description

  kernel                              Contains no files, but ensures
                                      other kernel packages are
                                      accurately installed

  kernel-core                         Includes a minimal number of
                                      modules to provide core
                                      functionality

  kernel-devel                        Includes support for building
                                      kernel modules

  kernel-headers                      Includes files to support the
                                      interface between the kernel and
                                      userspace libraries and programs

  kernel-modules                      Contains modules for common
                                      hardware devices

  kernel-modules-extra                Contains modules for not-so-common
                                      hardware devices

  kernel-tools                        Includes tools to manipulate the
                                      kernel

  kernel-tools-libs                   Includes the libraries to support
                                      the kernel tools
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 11-2 Kernel Packages

\

Moreover, packages containing the source code for RHEL 9 are also
available for those who wish to customize and recompile the code for
their precise needs.

\

Currently, the following kernel packages are installed on server1:

\

<div>

![](image-8UG681GQ.jpg){height="100%"}

</div>

The output returns six kernel packages that were loaded during the OS
installation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0346.html}

## Analyzing Kernel Version {.style3}

\

Sometimes you need to ascertain the version of the kernel running on the
system to check for compatibility with an application or database that
you need to deploy. RHEL has a basic tool available to extract the
version. The uname command with the -r switch depicts this information,
as follows:

\

<div>

![](image-RVFUDZEM.jpg){height="100%"}

</div>

The output shows the current kernel version in use is
5.14.0-162.6.1.el9_1.x86_64. An anatomy of the version is illustrated in
Figure 11-4 and explained subsequently.

\

::: {style="text-align: center;"}
![](image-28ZJEP8O.jpg){height="100%"}
:::

Figure 11-4 Anatomy of a Kernel Version

\

From left to right:

\

\(5\) major version of the Linux kernel. It changes when significant
alterations, enhancements, and updates to the previous major version are
made.

\

\(14\) major revision of the 5 th major version

\

\(0\) represents patched version of 5.14 with minor bug and security
hole fixes, minor enhancements, and so on.

\

(162.6.1) Red Hat customized version of 5.14.0

\

(el9_1) Enterprise Linux this kernel is built for

\

(x86_64) architecture this kernel is built for

\

A further analysis designates that 5.14.0 holds the general Linux kernel
version information, the numbers and letters (162.6.1.el9_1) represent
the Red Hat specific information, and x86_64 identifies the hardware
architecture type.

::: {style="page-break-before: always;"}
:::

[]{#chapter0347.html}

## Understanding Kernel Directory Structure {.style3}

\

Kernel and its support files are stored at different locations in the
directory hierarchy, of which three locations---/boot, /proc, and
/usr/lib/modules---are noteworthy.

\

### The /boot Location {.style3}

/boot is essentially a file system that is created at system
installation. It houses the Linux kernel, GRUB2 configuration, and other
kernel and boot support files. A long listing produces the following
output for this file system:

\

<div>

![](image-ABTYD56Z.jpg){height="100%"}

</div>

The output displays several files, five of which are for the kernel and
two for its rescue version. The vmlinuz is the main kernel file with
config, initramfs, symvers, and System.map storing the kernel's
configuration, boot image, CRC values of all the variables used in the
kernel and modules, and mapping, respectively.

\

The files for the rescue version have the string "rescue" embedded
within their names, as indicated in the above output.

\

The efi and grub2 subdirectories under /boot hold bootloader information
specific to firmware type used on the system: UEFI or BIOS. For server1,
grub2 contains GRUB2 information as shown below:

\

<div>

![](image-TL0VEPM9.jpg){height="100%"}

</div>

The files grub.cfg and grubenv contain critical data with the former
holding bootable kernel information and the latter stores the
environment information that the kernel uses.

\

The subdirectory loader under /boot is the storage location for
configuration of the running and rescue kernels. The configuration is
stored in files under the entries subdirectory, as shown below:

\

<div>

![](image-HWP7VBRR.jpg){height="100%"}

</div>

The files are named using the machine id of the system as stored in the
/etc/machine-id file and the kernel version they are for. The content of
the kernel file is presented below:

\

<div>

![](image-1T8ZI22I.jpg){height="100%"}

</div>

The "title" is displayed on the bootloader screen where the countdown to
autoboot a selected kernel entry runs. Other than the kernel version,
and the default kernel and boot image filenames, the environment
variables "kernelopts" and "tuned_params" supply various values to the
booting kernel to control its behavior.

\

### The /proc Location {.style3}

/proc is a virtual, memory-based file system. Its contents are created
and updated in memory at system boot and during runtime, and they are
destroyed at system shutdown. It maintains information about the current
state of the kernel, which includes hardware configuration and status
information about processor, memory, storage, file systems, swap,
processes, network interfaces and connections, routing, etc. This data
is kept in tens of thousands of zero-byte files organized in a hierarchy
of hundreds of subdirectories. A long directory listing of /proc is
provided below:

\

<div>

![](image-KKPVRQW3.jpg){height="100%"}

</div>

Some subdirectory names are numerical and contain information about a
specific process, and the process ID matches the subdirectory name.
Within each subdirectory are other files and subdirectories containing a
plethora of information, such as memory segments for processes and
configuration data for system components. You can view the configuration
of a particular item using any text file viewing tool. The following
show selections from the cpuinfo and meminfo files that hold processor
and memory information:

\

<div>

![](image-19YPNNFN.jpg){height="100%"}

</div>

The data stored under /proc is referenced by many system utilities,
including top, ps, uname, free, uptime, and w to produce their output.

\

### The /usr/lib/modules Location {.style3}

This directory holds information about kernel modules. Underneath it are
subdirectories specific to the kernels installed on the system. For
example, the long listing of /usr/lib/modules below shows that there is
only one kernel installed. The name of the subdirectory corresponds with
the installed kernel version.

\

<div>

![](image-4ZWOSW28.jpg){height="100%"}

</div>

And this subdirectory contains:

\

<div>

![](image-7J6ZA4XD.jpg){height="100%"}

</div>

There are several files and a few subdirectories here; they hold
module-specific information for the kernel version.

\

One of the key subdirectories is
/usr/lib/modules/5.14.0-162.6.1.el9_1.x86_64/kernel/drivers, which
stores modules for a variety of hardware and software components in
various subdirectories, as shown in the listing below:

\

<div>

![](image-V61A48MA.jpg){height="100%"}

</div>

Additional modules may be installed on the system to support more
components.

::: {style="page-break-before: always;"}
:::

[]{#chapter0348.html}

## Installing the Kernel {.style3}

\

Installing kernel packages requires extra care because it could leave
your system in an unbootable or undesirable state. It is advisable to
have the bootable medium handy prior to starting the kernel install
process. By default, the dnf command adds a new kernel to the system,
leaving the existing kernel(s) intact. It does not replace or overwrite
any existing kernel files.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Always install a new version of the kernel instead of
upgrading it. The upgrade process removes any existing kernel and
replaces it with a new one. In case of a post-installation issue, you
will not be able to revert to the old working kernel.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

A new version of the kernel is typically required if an application
needs to be deployed on the system that requires a different kernel to
operate. When deficiencies or bugs are identified in the existing
kernel, it can hamper the kernel's smooth operation. In either case, the
new kernel addresses existing issues as well as adds bug fixes, security
updates, new features, and improved support for hardware devices.

\

The dnf command is the preferred tool to install a kernel, as it
resolves and installs any required dependencies automatically. The rpm
command may alternatively be used; however, you must install any
reported dependencies manually.

\

The kernel packages for RHEL 9 are available to subscribers for download
on Red Hat's Customer Portal. You need a user account in order to log in
and download.

::: {style="page-break-before: always;"}
:::

[]{#chapter0349.html}

## Exercise 11-3: Download and Install a New Kernel {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will download the latest available kernel packages
from the Red Hat Customer Portal and install them using the dnf command.
You will ensure that the existing kernel and its configuration remain
intact.

\

1\. Check the version of the running kernel:

\

<div>

![](image-IT42GL17.jpg){height="100%"}

</div>

The output discloses the current active kernel version as
5.14.0-162.6.1.el9_1.x86_64.

\

2\. List the kernel packages currently installed:

\

<div>

![](image-OMXIZ896.jpg){height="100%"}

</div>

There are five kernel packages on the system as reported.

\

3\. Access the Red Hat Customer Portal webpage at access.redhat.com and
click Log In to sign in to the portal using the credentials you
used/created in Chapter 01 "Local Installation" for the developer
account:

\

::: {style="text-align: center;"}
![](image-VN25C5XG.jpg){height="100%"}
:::

4\. Click Downloads at the top:

\

::: {style="text-align: center;"}
![](image-080SANBI.jpg){height="100%"}
:::

5\. Click "Red Hat Enterprise Linux" under "By Category" on the next
screen:

\

<div>

![](image-I8UAM5D1.jpg){height="100%"}

</div>

6\. Click Packages and enter "kernel" in the Search bar to narrow the
list of available packages:

\

<div>

![](image-0W3JFF6K.jpg){height="100%"}

</div>

7\. Click "Download Latest" beside the packages kernel, kernel-core,
kernel-modules, kernel-tools, and kernel-tools-libs to download them.
These are the new packages for the version you currently have on the
system.

8\. Once downloaded, move the packages to the /tmp directory using the
mv command.

9\. List the packages after moving them:

\

<div>

![](image-M0OOKCGZ.jpg){height="100%"}

</div>

10\. Install all five packages at once using the dnf command:

\

<div>

![](image-65MXH9K5.jpg){height="100%"}

</div>

11\. Confirm the installation:

\

<div>

![](image-PYXRYFE0.jpg){height="100%"}

</div>

\

<div>

![](image-DP49QUZT.jpg){height="100%"}

</div>

The output indicates that packages for a higher kernel version
5.14.0-162.12.1.el9_1 have been installed. It also shows the presence of
the previous kernel packages.

\

12\. The /boot/grub2/grubenv file now has the directive "saved_entry"
set to the new kernel, which implies that this new kernel will boot on
the next system restart:

\

<div>

![](image-XSA44WUG.jpg){height="100%"}

</div>

13\. Reboot the system. You will see the new kernel entry in the GRUB2
boot list at the top. The system will autoboot this new default kernel.

\

<div>

![](image-4EEZ7V5S.jpg){height="100%"}

</div>

14\. Run the uname command after the system has been booted up to
confirm the loading of the new kernel:

\

<div>

![](image-DPVQ9V1O.jpg){height="100%"}

</div>

The new kernel is active.

\

15\. You can also view the contents of the version and cmdline files
under /proc to verify the active kernel:

\

<div>

![](image-XIIHM3OP.jpg){height="100%"}

</div>

This concludes the process of downloading and installing a new kernel on
RHEL 9.

::: {style="page-break-before: always;"}
:::

[]{#chapter0350.html}

## Chapter Summary {.style3}

\

This chapter presented a high-level look at the Linux boot process,
highlighting the four phases the system passes through and the
complexities involved. We reviewed firmware and looked at preboot
administration tasks, which included interacting with the bootloader
program, booting into specific targets, and an analysis of the
bootloader configuration files. We performed a critical exercise that
focused on resetting a forgotten or lost root user password.

\

The next major topic discussed the Linux kernel, its key components and
management. We explored various packages that made up the core kernel
software, performed an anatomy of its versioning, and examined key
directories and file systems that are employed to hold kernel-specific
information. Before the chapter was concluded, we downloaded and
installed a new kernel without impacting the old one.

::: {style="page-break-before: always;"}
:::

[]{#chapter0351.html}

## Review Questions {.style3}

\

1\. You want to view the parameters passed to the kernel at boot time.
Which virtual file would you look at?

2\. UEFI is replacing BIOS on new computers. True or False?

3\. You have changed the timeout value in the grub configuration file
located in the /etc/default directory. Which command would you run now
to ensure the change takes effect on next system reboots?

4\. Name the location of the grub.efi file in the UEFI-based systems.

5\. What is the name of the default bootloader program in RHEL 9?

6\. Which file stores the location of the boot partition on the BIOS
systems?

7\. You have lost the root user password and you need to reset it. What
would you add to the default kernel boot string to break the boot
process at an early stage?

8\. The systemd command may be used to rebuild a new kernel. True or
False?

9\. What does the chroot command do?

10\. At what stage should you interrupt the boot sequence to boot the
system into a non-default target?

11\. Which two files would you view to obtain processor and memory
information?

12\. By default, GRUB2 is stored in the MBR on a BIOS-based system. True
or False?

13\. You have installed a new version of the kernel. What would you now
have to do to make it the default boot kernel?

14\. What is the system initialization and service management scheme
called?

::: {style="page-break-before: always;"}
:::

[]{#chapter0352.html}

## Answers to Review Questions {.style3}

\

1\. The cmdline file in the /proc file system.

2\. True.

3\. You will need to run the grub2-mkconfig command.

4\. The grub.efi file is located in the /boot/efi/EFI/redhat directory.

5\. GRUB2.

6\. The grub.cfg file stores the location information of the boot
partition.

7\. You would add rd.break to the kernel boot string.

8\. False.

9\. The chroot command changes the specified directory path to /.

10\. At the GRUB2 stage.

11\. The cpuinfo and meminfo files in the /proc file system.

12\. True.

13\. Nothing. The install process takes care of that.

14\. It is called systemd.

::: {style="page-break-before: always;"}
:::

[]{#chapter0353.html}

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

[]{#chapter0354.html}

## Lab 11-1: Enable Verbose System Boot {.style3}

\

As user1 with sudo on server3, remove "quiet" from the end of the value
of the variable GRUB_CMDLINE_LINUX in the /etc/default/grub file and run
grub2-mkconfig to apply the update. Reboot the system and observe that
the system now displays verbose information during the boot process.
(Hint: The GRUB2 Bootloader and Exercise 11-1).

::: {style="page-break-before: always;"}
:::

[]{#chapter0355.html}

## Lab 11-2: Reset root User Password {.style3}

\

As root on server4, reset the root user password by booting the system
into emergency mode with SELinux disabled. Log in with root and enter
the new password after the reboot for validation. (Hint: The GRUB2
Bootloader and Exercise 11-2).

::: {style="page-break-before: always;"}
:::

[]{#chapter0356.html}

## Lab 11-3: Install New Kernel {.style3}

\

As user1 with sudo on server3, check the current version of the kernel
using the uname or rpm command. Download a higher version from the Red
Hat Customer Portal and install it. Reboot the system and ensure the new
kernel is listed on the bootloader menu. (Hint: The Linux Kernel and
Exercise 11-3).

::: {style="page-break-before: always;"}
:::

[]{#chapter0357.html}

## Chapter 12 {style="text-align: right"}

\

### System Initialization, Message Logging, and System Tuning {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Understand systemd, units, and targets

\

Analyze service and target unit configuration files

\

List and view status of running units

\

Manage service units and target units

\

Display and configure default system boot target

\

Switch into non-default targets

\

Analyze system log configuration file

\

Examine log file rotation settings

\

Review boot and system log files

\

Record custom messages in system log file

\

Describe systemd journal service

\

Retrieve and scrutinize messages from journal

\

Store journal information persistently

\

Know system tuning and apply tuning profile

\

#### RHCSA Objectives:

\

16\. Boot, reboot, and shut down a system normally

17\. Boot systems into different targets manually

24\. Start, stop, and check the status of network services

39\. Start and stop services and configure services to start
automatically at boot

40\. Configure systems to boot into a specific target automatically

46\. Configure network services to start automatically at boot

22\. Locate and interpret system log files and journals

23\. Preserve system journals

21\. Manage tuning profiles

::: {style="page-break-before: always;"}
:::

\

Systemd is the default system initialization and service management
scheme in RHEL. It can boot the system into one of several predefined
targets and it is used to handle operational states of services. It
employs the concepts of units and targets for initialization, service
administration, and state changes. A good grasp of what unit and target
configuration files store is key to understanding how systemd operates.

\

::: {style="text-align: center;"}
![](image-4HBCT875.jpg){height="100%"}
:::

Alerts and messages generated by system services and user activities are
forwarded to predefined locations for storage. These alerts and messages
include those that are produced during system boot time. The log data
may be analyzed for debugging or auditing purposes. Log files grow over
time and need to be rotated periodically to prevent the file system
space from filling up. There are configuration files that define the
default and custom locations to direct the log messages to and to
configure rotation settings. The system log file records custom messages
sent to it. systemd includes a service for viewing and managing system
logs in addition to the traditional logging service. This service
maintains a log of runtime activities for faster retrieval and can be
configured to store the information permanently.

\

System tuning service is employed to monitor connected devices and to
tweak their parameters to improve performance or conserve power. A
recommended tuning profile may be identified and activated for optimal
performance and power saving.

::: {style="page-break-before: always;"}
:::

[]{#chapter0358.html}

## System Initialization and Service Management {.style3}

\

systemd (short for system daemon) is the system initialization and
service management mechanism. It has fast-tracked system initialization
and state transitioning by introducing features such as parallel
processing of startup scripts, improved handling of service
dependencies, and on-demand activation of services. Moreover, it
supports snapshotting of system states, tracks processes using control
groups, and automatically maintains mount points. systemd is the first
process with PID 1 that spawns at boot and it is the last process that
is terminated at shut down.

\

systemd spawns several processes during a service startup. It places the
processes in a private hierarchy composed of control groups (or cgroups
for short) to organize processes for the purposes of monitoring and
controlling system resources such as processor, memory, network
bandwidth, and disk I/O. This includes limiting, isolating, and
prioritizing their usage of resources. This way resources can be
distributed among users, databases, and applications based on need and
priority, resulting in overall improved system performance.

\

In order to benefit from parallelism, systemd initiates distinct
services concurrently, taking advantage of multiple CPU cores and other
compute resources. To that end, systemd creates sockets for all enabled
services that support socket-based activation instantaneously at the
very beginning of the initialization process. It passes them on to
service daemon processes as they attempt to start in parallel. This
approach lets systemd handle inter-service order dependencies and allows
services to start without any delays. With systemd, dependent daemons
need not be running; they only need the correct socket to be available.
systemd creates sockets first, starts daemons next, and caches any
client requests to daemons that have not yet started in the socket
buffer. It fills the pending client requests when the daemons they were
awaiting come online.

\

Socket is a communication method that allows two processes on the same
or different systems to talk.

\

During the operational state, systemd maintains the sockets and uses
them to reconnect other daemons and services that were interacting with
an old instance of a daemon before that daemon was terminated or
restarted. Likewise, services that use activation based on D-Bus
(Desktop Bus) are started when a client application attempts to
communicate with them for the first time. Additional methods used by
systemd for activation are device-based and path-based, with the former
starting the service when a specific hardware type such as USB is
plugged in, and the latter starting the service when a particular file
or directory alters its state.

\

D-Bus is another communication method that allows multiple services
running in parallel on a system to talk to one another on the same or
remote system.

\

With on-demand activation, systemd defers the startup of
services---Bluetooth and printing---until they are actually needed
during the boot process or during runtime. Together, parallelization and
on-demand activation save time and compute resources, and contribute to
expediting the boot process considerably.

\

Another major benefit of parallelism witnessed at system boot is when
systemd uses the autofs service to temporarily mount the configured file
systems. During the boot process, the file systems are checked that may
result in unnecessary delays. With autofs, the file systems are
temporarily mounted on their normal mount points, and as soon as the
checks on the file systems are finished, systemd remounts them using
their standard devices. Parallelism in file system mounts does not
affect the root and virtual file systems.

::: {style="page-break-before: always;"}
:::

[]{#chapter0359.html}

## Units {.style3}

\

Units are systemd objects used for organizing boot and maintenance
tasks, such as hardware initialization, socket creation, file system
mounts, and service startups. Unit configuration is stored in their
respective configuration files, which are auto-generated from other
configurations, created dynamically from the system state, produced at
runtime, or user-developed. Units are in one of several operational
states, including active, inactive, in the process of being activated or
deactivated, and failed. Units can be enabled or disabled. An enabled
unit can be started to an active state; a disabled unit cannot be
started.

\

Units have a name and a type, and they are encoded in files with names
in the form unitname.type. Some examples are tmp.mount, sshd.service,
syslog.socket, and umount.target. There are two types of unit
configuration files: (1) system unit files that are distributed with
installed packages and located in the /usr/lib/systemd/system directory,
and (2) user unit files that are user-defined and stored in the
/etc/systemd/user directory (run ls -l on both directories to list their
contents).

\

There are additional system units that are created at runtime and
destroyed when they are no longer needed. They are located in the
/run/systemd/system directory. These runtime unit files take precedence
over the system unit files, and the user unit files take priority over
the runtime files.

\

Unit configuration files are a direct replacement of the initialization
scripts found in the /etc/rc.d/init.d directory in older RHEL releases.

\

systemd includes eleven unit types, which are described in Table 12-1.

\

  ----------------------------------- -----------------------------------
  Unit Type                           Description

  Automount                           Offers automount capabilities for
                                      on-demand mounting of file systems

  Device                              Exposes kernel devices in systemd
                                      and may be used to implement
                                      device-based activation

  Mount                               Controls when and how to mount or
                                      unmount file systems

  Path                                Activates a service when monitored
                                      files or directories are accessed

  Scope                               Manages foreign processes instead
                                      of starting them

  Service                             Starts, stops, restarts, or reloads
                                      service daemons and the processes
                                      they are made up of

  Slice                               May be used to group units, which
                                      manage system processes in a
                                      tree-like structure for resource
                                      management

  Socket                              Encapsulates local inter-process
                                      communication or network sockets
                                      for use by matching service units

  Swap                                Encapsulates swap partitions

  Target                              Defines logical grouping of units

  Timer                               Useful for triggering activation of
                                      other units based on timers
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 12-1 systemd Unit Types

\

Unit files contain common and specific configuration elements. Common
elements fall under the \[Unit\] and \[Install\] sections, and comprise
the description, documentation location, dependency information,
conflict information, and other options that are independent of the type
of unit. The unit-specific configuration data is located under the unit
type section: \[Service\] for the service unit type, \[Socket\] for the
socket unit type, and so forth. A sample unit file for sshd.service is
shown below from the /usr/lib/systemd/system directory:

\

<div>

![](image-W99S3SUU.jpg){height="100%"}

</div>

Units can have dependency relationships among themselves based on a
sequence (ordering) or a requirement. A sequence outlines one or more
actions that need to be taken before or after the activation of a unit
(the Before and After directives). A requirement specifies what must
already be running (the Requires directive) or not running (the
Conflicts directive) in order for the successful launch of a unit. For
instance, the graphical.target unit file tells us that the system must
already be operating in the multi-user mode and not in rescue mode in
order for it to boot successfully into the graphical mode. Another
option, Wants, may be used instead of Requires in the \[Unit\] or
\[Install\] section so that the unit is not forced to fail activation if
a required unit fails to start. Run man systemd.unit for details on
systemd unit files.

\

There are a few other types of dependencies that you may see in other
unit configuration files. systemd generally sets and maintains
inter-service dependencies automatically; however, this can be done
manually if needed.

::: {style="page-break-before: always;"}
:::

[]{#chapter0360.html}

## Targets {.style3}

\

Targets are simply logical collections of units. They are a special
systemd unit type with the .target file extension. They share the
directory locations with other unit configuration files. Targets are
used to execute a series of units. This is typically true for booting
the system to a desired operational run level with all the required
services up and running. Some targets inherit services from other
targets and add their own to them. systemd includes several predefined
targets that are described in Table 12-2.

\

  ----------------------------------- -----------------------------------
  Target                              Description

  halt                                Shuts down and halts the system

  poweroff                            Shuts down and powers off the
                                      system

  shutdown                            Shuts down the system

  rescue                              Single-user target for running
                                      administrative and recovery
                                      functions. All local file systems
                                      are mounted. Some essential
                                      services are started, but
                                      networking remains disabled.

  emergency                           Runs an emergency shell. The root
                                      file system is mounted in read-only
                                      mode; other file systems are not
                                      mounted. Networking and other
                                      services remain disabled.

  multi-user                          Multi-user target with full network
                                      support, but without GUI

  graphical                           Multi-user target with full network
                                      support and GUI

  reboot                              Shuts down and reboots the system

  default                             A special soft link that points to
                                      the default system boot target
                                      (multi-user.target or
                                      graphical.target)

  hibernate                           Puts the system into hibernation by
                                      saving the running state of the
                                      system on the hard disk and
                                      powering it off. When powered up,
                                      the system restores from its saved
                                      state rather than booting up.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 12-2 systemd Targets

\

Target unit files contain all information under the \[Unit\] section,
and it comprises the description, documentation location, and dependency
and conflict information. A sample file for the graphical.target target
is shown below from the /usr/lib/systemd/system directory:

\

<div>

![](image-G7WLS56W.jpg){height="100%"}

</div>

The file shows four dependencies: Requires, Wants, Conflicts, and After.
It suggests that the system must have already accomplished the
rescue.service, rescue.target, multi-user.target, and
display-manager.service levels in order to be declared running in the
graphical target. Run man systemd.target for details on systemd targets.

::: {style="page-break-before: always;"}
:::

[]{#chapter0361.html}

## The systemctl Command {.style3}

\

systemd comes with a set of management tools for querying and
controlling operations. The primary tool for interaction in this command
suite is systemctl. The systemctl command performs administrative
functions and supports plentiful subcommands and flags. Table 12-3 lists
and describes some common operations.

\

  ----------------------------------- -----------------------------------
  Subcommand                          Description

  daemon-reload                       Re-reads and reloads all unit
                                      configuration files and recreates
                                      the entire user dependency tree.

  enable (disable)                    Activates (deactivates) a unit for
                                      autostart at system boot

  get-default (set-default)           Shows (sets) the default boot
                                      target

  get-property (set-property)         Returns (sets) the value of a
                                      property

  is-active                           Checks whether a unit is running

  is-enabled                          Displays whether a unit is set to
                                      autostart at system boot

  is-failed                           Checks whether a unit is in the
                                      failed state

  isolate                             Changes the running state of a
                                      system

  kill                                Terminates all processes for a unit

  list-dependencies                   Lists dependency tree for a unit

  list-sockets                        Lists units of type socket

  list-unit-files                     Lists installed unit files

  list-units                          Lists known units. This is the
                                      default behavior when systemctl is
                                      executed without any arguments.

  mask (unmask)                       Prohibits (permits) auto and manual
                                      activation of a unit to avoid
                                      potential conflict

  reload                              Forces a running unit to re-read
                                      its configuration file. This action
                                      does not change the PID of the
                                      running unit.

  restart                             Stops a running unit and restarts
                                      it

  show                                Shows unit properties

  start (stop)                        Starts (stops) a unit

  status                              Presents the unit status
                                      information
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 12-3 systemctl Subcommands

\

You will use a majority of these subcommands with systemctl going
forward. Refer to the manual pages of the command for more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0362.html}

## Listing and Viewing Units {.style3}

\

The systemctl command is used to view and manage all types of units. The
following examples demonstrate common operations pertaining to viewing
and querying units.

\

To list all units that are currently loaded in memory along with their
status and description, run the systemctl command without any options or
subcommands. A long output is generated. The graphic below shows a few
starting and concluding lines followed by a brief explanation.

\

<div>

![](image-LS70BQ0X.jpg){height="100%"}

</div>

\

<div>

![](image-R5SHK2RA.jpg){height="100%"}

</div>

Here is a breakdown of the above graphic: the UNIT column shows the name
of the unit and its location in the tree, the LOAD column reflects
whether the unit configuration file was properly loaded (other
possibilities are not found, bad setting, error, and masked), the ACTIVE
column returns the high-level activation state (other possible states
are active, reloading, inactive, failed, activating, and deactivating),
the SUB column depicts the low-level unit activation state (reports
unit-specific information), and the DESCRIPTION column illustrates the
unit's content and functionality.

\

By default, the systemctl command lists only the active units. You can
use the \--all option to include the inactive units too.

\

To list all (\--all) active and inactive units of type (-t) socket:

\

<div>

![](image-KH1A3KSD.jpg){height="100%"}

</div>

To list all units of type socket (column 2) currently loaded in memory
and the service they activate (column 3), sorted by the listening
address (column 1):

\

<div>

![](image-2IYK4UUY.jpg){height="100%"}

</div>

To list all unit files (column 1) installed on the system and their
current state (column 2). This will generate a long list of units in the
output. The following only shows a selection.

\

<div>

![](image-KNG8RPUS.jpg){height="100%"}

</div>

To list all units that failed (\--failed) to start at the last system
boot:

\

<div>

![](image-D0XSKYHZ.jpg){height="100%"}

</div>

To list the hierarchy of all dependencies (required and wanted units)
for the current default target:

\

<div>

![](image-X2T71TNX.jpg){height="100%"}

</div>

To list the hierarchy of all dependencies (required and wanted units)
for a specific unit such as atd.service:

\

<div>

![](image-H8GYR159.jpg){height="100%"}

</div>

There are other listing subcommands and additional flags available that
can be used to produce a variety of reports.

::: {style="page-break-before: always;"}
:::

[]{#chapter0363.html}

## Managing Service Units {.style3}

\

The systemctl command offers several subcommands to manage service
units, including starting, stopping, restarting, and checking their
status. These and other management operations are summarized in Table
12-3 earlier. The following examples demonstrate their use on a service
unit called atd.

\

To check the current operational status and other details for the atd
service:

\

<div>

![](image-RLW0SGAL.jpg){height="100%"}

</div>

The above output reveals a lot of information about the atd service. On
line 1, it shows the service description (read from the
/usr/lib/systemd/system/atd.service file). Line 2 illustrates the load
status, which reveals the current load status of the unit configuration
file in memory. Other possibilities for "Loaded" include "error" (if
there was a problem loading the file), \"not-found\" (if no file
associated with this unit was found), \"bad-setting\" (if a key setting
was missing), and \"masked\" (if the unit configuration file is masked).
Line 2 also tells us whether the service is set (enabled or disabled)
for autostart at system boot.

\

Line 3 exhibits the current activation status and the time the service
was started. An activation status designates the current state of the
service. Possible states include:

\

Active (running): The service is running with one or more processes

Active (exited): Completed a one-time configuration

Active (waiting): Running but waiting for an event

Inactive: Not running

Activating: In the process of being activated

Deactivating: In the process of being deactivated

Failed: If the service crashed or could not be started

\

The output also depicts the PID of the service process and other
information.

\

To disable the atd service from autostarting at the next system reboot:

\

<div>

![](image-JCGIU7R6.jpg){height="100%"}

</div>

To re-enable atd to autostart at the next system reboot:

\

<div>

![](image-E6EYIKX5.jpg){height="100%"}

</div>

To check whether atd is set to autostart at the next system reboot:

\

<div>

![](image-AKPBU3O6.jpg){height="100%"}

</div>

To check whether the atd service is running:

\

<div>

![](image-IS96Q3OT.jpg){height="100%"}

</div>

To stop and restart atd, run either of the following:

\

<div>

![](image-TBBVII8J.jpg){height="100%"}

</div>

To show the details of the atd service:

\

<div>

![](image-6IYFJ7YW.jpg){height="100%"}

</div>

To prohibit atd from being enabled or disabled:

\

<div>

![](image-RXUU6A1J.jpg){height="100%"}

</div>

Try disabling or enabling atd and observe the effect of the previous
command:

\

<div>

![](image-G4O1KUU8.jpg){height="100%"}

</div>

Reverse the effect of the mask subcommand and try disable and enable
operations:

\

<div>

![](image-RLZIX9D6.jpg){height="100%"}

</div>

Notice that the unmask subcommand has removed the restriction that was
placed on the atd service.

::: {style="page-break-before: always;"}
:::

[]{#chapter0364.html}

## Managing Target Units {.style3}

\

The systemctl command is also used to manage the target units. It can be
used to view or change the default boot target, switch from one running
target into another, and so on. These operations are briefed in Table
12-3 earlier. Let's look at some examples.

\

To view what units of type (-t) target are currently loaded and active:

\

<div>

![](image-A463ZA3C.jpg){height="100%"}

</div>

For each target unit, the above output returns the target unit's name,
load state, high-level and low-level activation states, and a short
description. Add the \--all option to the above to see all loaded
targets in either active or inactive state.

\

### Viewing and Setting Default Boot Target {.style3}

The systemctl command is used to view the current default boot target
and to set it. Let's use the get-default and set-default subcommands
with systemctl to perform these operations.

\

To check the current default boot target:

\

<div>

![](image-MRZG1Q7R.jpg){height="100%"}

</div>

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You may have to modify the default boot target persistently.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

To change the current default boot target from graphical.target to
multi-user.target:

\

<div>

![](image-MIKVWSXB.jpg){height="100%"}

</div>

The command simply removes the existing symlink (default.target)
pointing to the old boot target and replaces it with the new target file
path.

\

Execute sudo systemctl set-default graphical to revert the default boot
target to graphical.

\

### Switching into Specific Targets {.style3}

The systemctl command can be used to transition the running system from
one target state into another. There are a variety of potential targets
available to switch into as listed in Table 12-2 earlier; however, only
a few of them---graphical, multi-user, reboot, shutdown---are typically
used. The rescue and emergency targets are for troubleshooting and
system recovery purposes, poweroff and halt are similar to shutdown, and
hibernate is suitable for mobile devices. Consider the following
examples that demonstrate switching targets.

\

The current default target on server1 is graphical. To switch into
multi-user, use the isolate subcommand with systemctl:

\

<div>

![](image-QHV2PNOF.jpg){height="100%"}

</div>

This should stop the graphical service on the system and display the
text-based console login screen, as shown below:

\

<div>

![](image-UYKHJFV6.jpg){height="100%"}

</div>

Type in a username such as user1 and enter the password to log in:

\

<div>

![](image-FESM01ZP.jpg){height="100%"}

</div>

To return to the graphical target:

\

<div>

![](image-PT7C279V.jpg){height="100%"}

</div>

The graphical login screen should appear shortly and you should be able
to log back in.

\

To shut down the system and power it off, use the following or simply
run the poweroff command:

\

<div>

![](image-YAUS6GLP.jpg){height="100%"}

</div>

To shut down and reboot the system, use the following or simply run the
reboot command:

\

<div>

![](image-GJW81SP0.jpg){height="100%"}

</div>

The halt, poweroff, and reboot commands are mere symbolic links to the
systemctl command, as the following long listing suggests:

\

<div>

![](image-8NIP3CL6.jpg){height="100%"}

</div>

The halt, poweroff, and reboot commands are available in RHEL 9 for
compatibility reasons. It is recommended to use the systemctl command
instead when switching system states.

\

The three commands, without any arguments, perform the same action that
the shutdown command would with the "-H now", "-P now", and "-r now"
arguments, respectively. In addition, it also broadcasts a warning
message to all logged-in users, blocks new user login attempts, waits
for the specified amount of time for users to save their work and log
off, stops the services, and eventually shut the system down to the
specified target state.

::: {style="page-break-before: always;"}
:::

[]{#chapter0365.html}

## System Logging {.style3}

\

System logging (syslog for short) is one of the most rudimentary
elements of an operating system. Its purpose is to capture messages
generated by the kernel, daemons, commands, user activities,
applications, and other events, and forwarded them to various log files,
which store them for security auditing, service malfunctioning, system
troubleshooting, or informational purposes.

\

The daemon that is responsible for system logging is called rsyslogd
(rocket-fast system for log processing). This service daemon is
multi-threaded, with support for enhanced filtering,
encryption-protected message relaying, and a variety of configuration
options. The rsyslogd daemon reads its configuration file
/etc/rsyslog.conf and the configuration files located in the
/etc/rsyslog.d directory at startup. The default depository for most
system log files is the /var/log directory. Other services such as
audit, Apache, and GNOME desktop manager have subdirectories under
/var/log for storing their respective log files.

\

The rsyslog service is modular, allowing the modules listed in its
configuration file to be dynamically loaded in the kernel as and when
needed. Each module brings a new functionality to the system upon
loading.

\

The rsyslogd daemon can be stopped manually using systemctl stop
rsyslog. Replace stop with start, restart, reload, and status as
appropriate.

\

A PID is assigned to the daemon at startup and a file by the name
rsyslogd.pid is created in the /run directory to save the PID. The
reason this file is created and stores the PID is to prevent the
initiation of multiple instances of this daemon.

::: {style="page-break-before: always;"}
:::

[]{#chapter0366.html}

## The Syslog Configuration File {.style3}

\

The rsyslog.conf is the primary syslog configuration file located in the
/etc directory . The default uncommented line entries from the file are
shown below and explained thereafter. Section headings have been added
to separate the directives in each section.

\

<div>

![](image-XGIYZ4QC.jpg){height="100%"}

</div>

\

\#### GLOBAL DIRECTIVES \####

\

<div>

![](image-1TZ90V6M.jpg){height="100%"}

</div>

\

<div>

![](image-F8N6G689.jpg){height="100%"}

</div>

As depicted, the syslog configuration file contains three sections:
Global Directives, Modules, and Rules. The Global Directives section
contains three active directives. The definitions in this section
influence the overall functionality of the rsyslog service. The first
directive sets the location for the storage of auxiliary files
(/var/lib/rsyslog). The second directive instructs the rsyslog service
to save captured messages using traditional file formatting. The third
directive directs the service to load additional configuration from
files located in the /etc/rsyslog.d/ directory.

\

The Modules section defines two modules---imuxsock and imjournal---and
they are loaded on demand. The imuxsock module furnishes support for
local system logging via the logger command, and the imjournal module
allows access to the systemd journal.

\

The Rules section has many two-field line entries. The left field is
called selector, and the right field is referred to as action. The
selector field is further divided into two period-separated sub-fields
called facility (left) and priority (right), with the former
representing one or more system process categories that generate
messages, and the latter identifying the severity associated with the
messages. The semicolon (;) character is used as a distinction mark if
multiple facility.priority groups are present. The action field
determines the destination to send the messages to.

\

There are numerous supported facilities such as auth, authpriv, cron,
daemon, kern, lpr, mail, news, syslog, user, uucp, and local0 through
local7. The asterisk (\*) character represents all of them.

\

Similarly, there are several supported priorities, and they include
emerg, alert, crit, error, warning, notice, info, debug, and none. This
sequence is in the descending criticality order. The asterisk (\*)
represents all of them. If a lower priority is selected, the daemon logs
all messages of the service at that and higher levels.

\

Line 1 under the Rules section instructs the syslog daemon to catch and
store informational messages from all services to the /var/log/messages
file and ignore all messages generated by mail, authentication, and cron
services. Lines 2, 3, and 4 command the daemon to collect and log all
messages produced by authentication, mail, and cron to the secure,
maillog, and cron files, respectively. Line 5 orders the daemon to
display emergency messages (omusrmsg stands for user message output
module) on the terminals of all logged-in users. Line 6 shows two
comma-separated facilities that are set at a common priority. These
facilities tell the daemon to gather critical messages from uucp and
news facilities and log them to the /var/log/spooler file. Line 7 (the
last line) is for recording the boot-time service startup status to the
/var/log/boot.log file.

\

If you have made any modifications to the syslog configuration file, you
need to run the rsyslogd command with the -N switch and specify a
numeric verbosity level to inspect the file for any syntax or typing
issues:

\

<div>

![](image-ZM4S649D.jpg){height="100%"}

</div>

The validation returns the version of the command, verbosity level used,
and the configuration file path. With no issues reported, the rsyslog
service can be restarted (or reloaded) in order for the changes to take
effect.

::: {style="page-break-before: always;"}
:::

[]{#chapter0367.html}

## Rotating Log Files {.style3}

\

RHEL records all system activities in log files that are stored in a
central location under the /var/log directory, as defined in the rsyslog
configuration file. A long listing of this directory reveals the files
along with subdirectories that may have multiple service-specific logs.
Here is a listing from server1:

\

<div>

![](image-QQOOTMDQ.jpg){height="100%"}

</div>

The output shows log files for various services. Depending on the usage
and the number of events generated and captured, log files may quickly
fill up the /var file system, resulting in unpredictable system
behavior. Also, they may grow to an extent that would make it difficult
to load, read, send, or analyze them. To avoid getting into any unwanted
situation, it's important to ensure that they're rotated on a regular
basis and their archives are removed automatically.

\

To that end, a systemd unit file called logrotate.timer under the
/usr/lib/systemd/system directory invokes the logrotate service
(/usr/lib/systemd/system/logrotate.service) on a daily basis. Here is
what this file contains:

\

<div>

![](image-UXLK7558.jpg){height="100%"}

</div>

The logrotate service runs rotations as per the schedule and other
parameters defined in the /etc/logrotate.conf and additional log
configuration files located in the /etc/logrotate.d directory. The
following shows the content of /etc/logrotate.conf:

\

<div>

![](image-F1TAN45G.jpg){height="100%"}

</div>

The file content includes the default log rotation frequency (weekly).
It indicates the period of time (4 weeks) to retain the rotated logs
before deleting them. Each time a log file is rotated, an empty
replacement file is created with the date as a suffix to its name, and
the rsyslog service is restarted. The script presents the option of
compressing the rotated files using the gzip utility. During the script
execution, the logrotate command checks for the presence of files in the
/etc/logrotate.d directory and includes them as necessary. The
directives defined in the logrotate.conf file have a global effect on
all log files. You can define custom settings for a specific log file in
logrotate.conf or create a separate file under /etc/logrotate.d. Any
settings defined in user-defined files overrides the global settings.

\

Here is the default list of additional log configuration files that
reside in the /etc/logrotate.d directory:

\

<div>

![](image-P7RQUVEV.jpg){height="100%"}

</div>

The above file listing shows files for a number of services---chrony,
dnf, rsyslog, samba, etc.---all with their own rules defined. The
following shows the file content for btmp (records of failed user login
attempts) that is used to control the rotation behavior for the
/var/log/btmp file:

\

<div>

![](image-VHMB8PN6.jpg){height="100%"}

</div>

The rotation is once a month. The replacement file will get read/write
permission bits for the owner (root) and the owning group (utmp), and
the rsyslog service will maintain only one rotated copy of the btmp
file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0368.html}

## The Boot Log File {.style3}

\

Logs generated during the system startup display the service startup
sequence with a status showing whether the service was started
successfully. This information may help in any post-boot troubleshooting
if required. Boot logs are stored in the boot.log file under /var/log.
Here are a few lines from the beginning of the file:

\

<div>

![](image-YM28MT86.jpg){height="100%"}

</div>

OK or FAILED within the square brackets indicates whether or not a
service was started.

::: {style="page-break-before: always;"}
:::

[]{#chapter0369.html}

## The System Log File {.style3}

\

The default location for storing most system activities, as defined in
the rsyslog.conf file, is the /var/log/messages file. This file saves
log information in plain text format and may be viewed with any file
display utility, such as cat, more, pg, less, head, or tail. This file
may be observed in real time using the tail command with the -f switch.
The messages file captures the date and time of the activity, hostname
of the system, name and PID of the service, and a short description of
the event being logged.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: It is helpful to "tail" the messages file when starting or
restarting a system service or during testing to identify any issues
encountered.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The following illustrates some recent entries from this file:

\

<div>

![](image-L0NUQHLU.jpg){height="100%"}

</div>

Each line entry represents the detail for a single event.

::: {style="page-break-before: always;"}
:::

[]{#chapter0370.html}

## Logging Custom Messages {.style3}

\

Many times, it is worthwhile to add a manual note to the system log file
to mark the start or end of an activity for future reference. This is
especially important when you run a script to carry out certain tasks
and you want to record the status or add comments at various stages
throughout its execution. This is also beneficial in debugging the
startup of an application to know where exactly it is failing.

\

The Modules section in the rsyslog.conf file provides the support via
the imuxsock module to record custom messages to the messages file using
the logger command. This command may be run by normal users or the root
user. The following example shows how to add a note indicating the
calling user has rebooted the system:

\

<div>

![](image-SJ8OORC8.jpg){height="100%"}

</div>

tail the last line from the messages file and you'll observe the message
recorded along with the timestamp, hostname, and PID:

\

<div>

![](image-QX4DHWSW.jpg){height="100%"}

</div>

You may add the -p option and specify a priority level either as a
numerical value or in the facility.priority format. The default priority
at which the events are recorded is user.notice. See the manual pages
for the logger command for more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0371.html}

## The systemd Journal {.style3}

\

In addition to the rsyslog service, RHEL offers a systemd-based logging
service for the collection and storage of logging data. This service is
implemented via the systemd-journald daemon. The function of this
service is to gather, store, and display logging events from a variety
of sources such as the kernel, rsyslog and other services, initial RAM
disk, and alerts generated during the early boot stage. It stores these
messages in the binary format in files called journals that are located
in the /run/log/journal directory. These files are structured and
indexed for faster and easier searches, and may be viewed and managed
using the journalctl command. As you know, /run is a virtual file system
that is created in memory at system boot, maintained during system
runtime, and destroyed at shutdown. Therefore, the data stored therein
is non-persistent, but you can enable persistent storage for the logs if
desired.

\

RHEL runs both rsyslogd and systemd-journald concurrently. In fact, the
data gathered by systemd-journald may be forwarded to rsyslogd for
further processing and persistent storage in text format.

\

The main configuration file for this service is
/etc/systemd/journald.conf, which contains numerous default settings
that affect the overall functionality of the service. These settings may
be modified as required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0372.html}

## Retrieving and Viewing Messages {.style3}

\

RHEL provides the journalctl command to retrieve messages from the
journal for viewing in a variety of ways using different options. One
common usage is to run the command without any options to see all the
messages generated since the last system reboot. The following shows a
few initial entries from the journal:

\

<div>

![](image-GW2A64CY.jpg){height="100%"}

</div>

Notice that the format of the messages is similar to that of the events
logged to the /var/log/messages file that you saw earlier. Each line
begins with a timestamp followed by the system hostname, process name
with or without a PID, and the actual message.

\

Let's run the journalctl command with different options to produce
various reports.

\

To display detailed output for each entry, use the -o verbose option:

\

<div>

![](image-PGD7D39A.jpg){height="100%"}

</div>

To view all events since the last system reboot, use the -b options:

\

<div>

![](image-X9FCN1P0.jpg){height="100%"}

</div>

You may specify -0 (default, since the last system reboot), -1 (the
previous system reboot), -2 (two reboots before), and so on to view
messages from previous system reboots.

\

To view only kernel-generated alerts since the last system reboot:

\

<div>

![](image-ZZNY2KP5.jpg){height="100%"}

</div>

To limit the output to view a specific number of entries only (3 in the
example below), use the -n option:

\

<div>

![](image-M3MS6IBH.jpg){height="100%"}

</div>

To show all alerts generated by a particular service, such as crond:

\

<div>

![](image-MRE8BVJ1.jpg){height="100%"}

</div>

To retrieve all messages logged for a certain process, such as the PID
associated with the chronyd service:

\

<div>

![](image-P5X3WMHT.jpg){height="100%"}

</div>

To reveal all messages for a particular system unit, such as
sshd.service:

\

<div>

![](image-HQ6YXSCB.jpg){height="100%"}

</div>

To view all error messages logged between a date range, such as January
25, 2023, and January 31, 2023:

\

<div>

![](image-0X8FCWW7.jpg){height="100%"}

</div>

To get all warning messages that have appeared today and display them in
reverse chronological order:

\

<div>

![](image-GFF7W41A.jpg){height="100%"}

</div>

You can specify the time range in hh:mm:ss format, or yesterday, today,
or tomorrow instead.

\

Similar to the -f (follow) option that is used with the tail command for
real-time viewing of a log file, you can use the same switch with
journalctl as well. Press Ctrl+c to terminate.

\

<div>

![](image-T0B3QSCO.jpg){height="100%"}

</div>

Check the manual pages of the journalctl command and the
systemd-journald service for more details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0373.html}

## Preserving Journal Information {.style3}

\

By default, journals are stored in the /run/log/journal directory for
the duration of system runtime. This data is transient and it does not
survive across reboots. The journalctl command examples demonstrated
earlier retrieve journal information from this temporary location. The
rsyslogd daemon, by default, reads the temporary journals and stores
messages in the /var/log/messages file. You can enable a separate
storage location for the journal to save all its messages there
persistently. The default is under the /var/log/journal directory. This
will make the journal information available for future reference.

\

The systemd-journald service supports four options with the Storage
directive in its configuration file journald.conf to control how the
logging data is handled. These options are described in Table 12-4.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  volatile                            Stores data in memory only

  persistent                          Stores data permanently under
                                      /var/log/journal and falls back to
                                      memory-only option if this
                                      directory does not exist or has a
                                      permission or other issue. The
                                      service creates /var/log/journal in
                                      case of its non-existence.

  auto                                Similar to "persistent" but does
                                      not create /var/log/journal if it
                                      does not exist. This is the default
                                      option.

  none                                Disables both volatile and
                                      persistent storage options. Not
                                      recommended.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 12-4 Journal Data Storage Options

\

The default (auto) option appears more suitable as it stores data in
both volatile and on-disk storage; however, you need to create the
/var/log/journal directory manually. This option provides two
fundamental benefits: faster query responses from in-memory storage and
access to historical log data from on-disk storage.

::: {style="page-break-before: always;"}
:::

[]{#chapter0374.html}

## Exercise 12-1: Configure Persistent Storage for Journal Information {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will run the necessary steps to enable and confirm
persistent storage for the journals.

\

1\. Create a subdirectory called journal under the /var/log directory
and confirm:

\

<div>

![](image-SSVIV3PQ.jpg){height="100%"}

</div>

2\. Restart the systemd-journald service and confirm:

\

<div>

![](image-4WXRMTI0.jpg){height="100%"}

</div>

3\. List the new directory and observe a subdirectory matching the
machine ID of the system as defined in the /etc/machine-id file is
created:

\

<div>

![](image-GVED5QN3.jpg){height="100%"}

</div>

Compare the name of the subdirectory with the ID stored in the
/etc/machine-id file. They are identical.

\

This log file is rotated automatically once a month based on the
settings in the journald.conf file. Check the manual pages of the
configuration file for details and relevant directives.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0375.html}

## System Tuning {.style3}

\

RHEL uses a system tuning service called tuned to monitor storage,
networking, processor, audio, video, and a variety of other connected
devices, and adjusts their parameters for better performance or power
saving based on a chosen profile. There are several predefined tuning
profiles for common use cases shipped with RHEL that may be activated
either statically or dynamically.

\

The tuned service activates a selected profile at service startup and
continues to use it until it is switched to a different profile. This is
the static behavior and it is enabled by default.

\

The dynamic alternative adjusts the system settings based on the live
activity data received from monitored system components to ensure
optimal performance. In most cases, the utilization of system components
varies throughout the day. For example, the disk and processor
utilization increases during a program startup and the network
connection use goes up during a large file transfer. A surge in a system
component activity results in heightened power consumption.

::: {style="page-break-before: always;"}
:::

[]{#chapter0376.html}

## Tuning Profiles {.style3}

\

tuned includes nine predefined profiles to support a variety of use
cases. In addition, you can create custom profiles from nothing or by
using one of the existing profiles as a template. In either case, you
need to store the custom profile under the /etc/tuned directory in order
to be recognized by the tuned service.

\

Tuning profiles may be separated into three groups: (1) optimized for
better performance, (2) geared towards power consumption, and (3) those
that offers a balance between the first two and the maximum
performance/power combination. Table 12-5 lists and describes common
profiles.

\

  ----------------------------------- -----------------------------------
  Profile                             Description

  Profiles Optimized for Better       
  Performance                         

  Desktop                             Based on the balanced profile for
                                      desktop systems. Offers improved
                                      throughput for interactive
                                      applications.

  Latency-performance                 For low-latency requirements

  Network-latency                     Based on the latency-performance
                                      for faster network throughput

  Network-throughput                  Based on the throughput-performance
                                      profile for maximum network
                                      throughput

  Virtual-guest                       Optimized for virtual machines

  Virtual-host                        Optimized for virtualized hosts

  Profiles Optimized for Power Saving 

  Powersave                           Saves maximum power at the cost of
                                      performance

  Balanced/Max Profiles               

  Balanced                            Preferred choice for systems that
                                      require a balance between
                                      performance and power saving

  Throughput-performance              Provides maximum performance and
                                      consumes maximum power
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 12-5 Tuning Profiles

\

Predefined profiles are located in the /usr/lib/tuned directory in
subdirectories matching their names. The following shows a long listing
of the directory:

\

<div>

![](image-0IW3L8D8.jpg){height="100%"}

</div>

The default active profile set on server1 and server2 is the
virtual-guest profile, as the two systems are hosted in a VirtualBox
virtualized environment.

::: {style="page-break-before: always;"}
:::

[]{#chapter0377.html}

## The tuned-adm Command {.style3}

\

tuned comes with a single profile management command called tuned-adm.
This tool can list active and available profiles, query current
settings, switch between profiles, and turn the tuning off. This command
can also recommend the best profile for the system based on many system
attributes. Refer to the manual pages of the command for more details.

\

The following exercise demonstrates the use of most of the management
operations listed above.

::: {style="page-break-before: always;"}
:::

[]{#chapter0378.html}

## Exercise 12-2: Manage Tuning Profiles {.style3}

\

This exercise should be done on server1 as user1 with sudo where
required.

\

In this exercise, you will install and start the tuned service and
enable it for auto-restart upon future system reboots. You will display
all available profiles and the current active profile. You will switch
to one of the available profiles and confirm. You will determine the
recommended profile for the system and switch to it. Finally, you will
deactivate tuning and reactivate it. You will confirm the activation to
conclude the exercise.

\

1\. Install the tuned package if it is not already installed:

\

<div>

![](image-DOZ3L6D2.jpg){height="100%"}

</div>

The output indicates that the software is already installed.

\

2\. Start the tuned service and set it to autostart at reboots:

\

<div>

![](image-GZMM1FDK.jpg){height="100%"}

</div>

3\. Confirm the startup:

\

<div>

![](image-5SDIX9UC.jpg){height="100%"}

</div>

4\. Display the list of available tuning profiles:

\

<div>

![](image-9BQU6WW7.jpg){height="100%"}

</div>

The output shows several predefined profiles as well as the current
active profile.

\

5\. List only the current active profile:

\

<div>

![](image-FKCADCVR.jpg){height="100%"}

</div>

6\. Switch to the powersave profile and confirm:

\

<div>

![](image-SI3GNXZ6.jpg){height="100%"}

</div>

The active profile is now powersave.

\

7\. Determine the recommended profile for server1 and switch to it:

\

<div>

![](image-PEYB6S9E.jpg){height="100%"}

</div>

The first instance of the command shows the best recommended profile for
server1 based on its characteristics, the second command instance
switched to the recommended profile, and the third instance confirmed
the switching.

\

8\. Turn off tuning:

\

<div>

![](image-2DTQXPL4.jpg){height="100%"}

</div>

The service will not perform any tuning until it is reactivated.

\

9\. Reactivate tuning and confirm:

\

<div>

![](image-TRKT2INU.jpg){height="100%"}

</div>

The tuning is re-enabled and the virtual-guest profile is in effect.
This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0379.html}

## Chapter Summary {.style3}

\

This chapter started with a discussion of systemd, the default service
management and system initialization scheme used in RHEL. We explored
key components of systemd, its key directories, and examined unit and
target configuration files. We utilized the lone systemd administration
command to switch system operational states, identify and set default
boot targets, and manage service start, stop, and status checking.

\

Next, we looked at the traditional system logging and systemd journaling
services. Both mechanisms have similarities and differences in how they
capture log data and where they direct it for storage and retrieval. We
examined the system log configuration file and the configuration file
that controls the log file rotation settings. The log subsystem proves
valuable when records are needed for monitoring, troubleshooting,
auditing, or reporting purpose.

\

Finally, we explored preconfigured tuning profiles and analyzed pros and
cons associated with each one of them. We demonstrated how to determine
a recommended profile for the system and how to set and activate it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0380.html}

## Review Questions {.style3}

\

1\. What is the PID of the systemd process?

2\. What is a target in systemd?

3\. You need to append a text string "Hello world" to the system log
file. What would be the command to achieve this?

4\. The systemd command may be used to rebuild a new kernel. True or
False?

5\. Which command is used to manage system services?

6\. Which configuration file must be modified to ensure journal log
entries are stored persistently?

7\. What is the recommended location to store custom log configuration
files?

8\. What would the command systemctl list-dependencies crond do?

9\. What would the command systemctl restart rsyslog do?

10\. What are the two common systemd targets production RHEL servers are
typically configured to run at?

11\. By default, log files are rotated automatically every week. True or
False?

12\. Name the two directory paths where systemd unit files are stored.

13\. What would you run to identify the recommended tuning profile for
the system?

14\. What would the command systemctl get-default do?

15\. systemd starts multiple services concurrently during system boot.
True or False?

16\. What is the name of the boot log file?

17\. Which systemctl subcommand is executed after a unit configuration
file has been modified to apply the changes?

18\. Which other logging service complements the rsyslog service?

19\. A RHEL system is booted up. You want to view all messages that were
generated during the boot process. Which log file would you look at?

::: {style="page-break-before: always;"}
:::

[]{#chapter0381.html}

## Answers to Review Questions {.style3}

\

1\. The PID of the systemd process is 1.

2\. A target is a collection of units.

3\. The command to accomplish the desired result would be logger -i
"Hello world".

4\. False.

5\. The systemctl command.

6\. The journald.conf file under the /etc/systemd directory.

7\. The recommended location to store custom log configuration files is
/etc/rsyslog.d directory.

8\. The command provided will display all dependent units associated
with the specified service.

9\. The command provided will restart the rsyslog service.

10\. The two common systemd boot targets are multi-user and graphical.

11\. True.

12\. The directory locations are /etc/systemd/system and
/usr/lib/systemd/system.

13\. The tuned-adm recommend command.

14\. The command provided will reveal the current default boot target.

15\. True.

16\. The boot.log file in the /var/log directory.

17\. The daemon-reload subcommand.

18\. The systemd-journald service.

19\. The /var/log/boot.log file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0382.html}

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

[]{#chapter0383.html}

## Lab 12-1: Modify Default Boot Target {.style3}

\

As user1 with sudo on server3, modify the default boot target from
graphical to multi-user, and reboot the system to test it. Run the
systemctl and who commands after the reboot for validation. Restore the
default boot target back to graphical and reboot to verify. (Hint:
System Initialization and Service Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0384.html}

## Lab 12-2: Record Custom Alerts {.style3}

\

As user1 with sudo on server3, write the message "This is \$LOGNAME
adding this marker on \$(date)" to the /var/log/messages file. Ensure
that variable and command expansions work. Verify the entry in the file.
(Hint: System Logging).

::: {style="page-break-before: always;"}
:::

[]{#chapter0385.html}

## Lab 12-3: Apply Tuning Profile {.style3}

\

As user1 with sudo on server3, identify the current system tuning
profile with the tuned-adm command. List all available profiles. List
the recommended profile for server3. Apply the "balanced" profile and
verify with tuned-adm. (Hint: System Tuning).

::: {style="page-break-before: always;"}
:::

[]{#chapter0386.html}









