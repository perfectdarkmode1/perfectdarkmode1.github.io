This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Understand the OpenSSH service,
versions, and algorithms

[![](images/00001.jpeg){.c37}]{.c36}Overview of encryption techniques
and authentication methods

[![](images/00001.jpeg){.c37}]{.c36}Describe OpenSSH administration
commands and configuration files

[![](images/00001.jpeg){.c37}]{.c36}Configure private/public key-based
authentication

[![](images/00001.jpeg){.c37}]{.c36}Access OpenSSH server from other
Linux systems

[![](images/00001.jpeg){.c37}]{.c36}Use OpenSSH client tools to transfer
files

[![](images/00001.jpeg){.c37}]{.c36}Synchronize files remotely over
OpenSSH

[RHCSA Objectives:]{.c39}

[04]{#part0031_split_000.html#id_770 .calibre10}. Access remote systems
using ssh

[26]{#part0031_split_000.html#id_792 .calibre10}. Securely transfer
files between systems

[57]{#part0031_split_000.html#id_821 .calibre10}. Configure key-based
authentication for SSH

::: {#part0031_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0031_split_001.html}

[ S]{.c42}[ecure]{.c43} Shell is a network service that delivers a
secure mechanism for data transmission between source and destination
systems over insecure network paths. It provides a set of utilities that
allows users to generate key pairs and use them to set up trusted logins
between systems for themselves. Additional utilities in the set gives
remote users the ability to log in, execute commands, and transfer files
securely over encrypted network channels. These tools have predominantly
supplanted their insecure counterparts in the corporate world.

**[The]{#part0031_split_001.html#id_506 .calibre10} OpenSSH Service**

*Secure Shell* (SSH) delivers a secure mechanism for data transmission
between source and destination systems over IP networks. It was designed
to replace the old remote login programs that transmitted user passwords
in clear text and data unencrypted. SSH employs digital signatures for
user authentication with encryption to secure a communication channel.
As a result, this makes it extremely hard for unauthorized people to
gain access to passwords or the data in transit. It also monitors the
data being transferred throughout a session to ensure integrity. SSH
includes a set of utilities for remote users to log in, transfer files,
and execute commands securely. Due to strong security features, SSH
utilities have supplanted their conventional, unsecure login and file
transfer counterpart programs.

*OpenSSH* is a free, open source implementation of the proprietary SSH.
Once applied successfully on the system, the unsecure
services---*telnet*, *rlogin*, *rcp*, and *ftp*---can be disabled after
a careful examination to eliminate potential impact. The secure command
that has substituted *telnet* and *rlogin* remote login services is
called *ssh*, and those for *rcp* and *ftp* are called *scp* and *sftp*,
respectively.

**[Common]{#part0031_split_001.html#id_507 .calibre10} Encryption
Techniques**

*Encryption* is a way of scrambling information with the intent to
conceal the real information from unauthorized access. OpenSSH can
utilize various encryption techniques during an end-to-end communication
session between two entities (client and server). The two common
techniques are *symmetric* and *asymmetric*. They are also referred to
as *secret key encryption* and *public key encryption* techniques.

**Symmetric Technique**

This technique uses a single key called a *secret* key that is generated
as a result of a negotiation process between two entities at the time of
their initial contact. Both sides use the same secret key during
subsequent communication for data encryption and decryption.

**Asymmetric Technique**

This technique uses a combination of *private* and *public* keys, which
are randomly generated and mathematically related strings of
alphanumeric characters attached to messages being exchanged. The client
transmutes the information with a *public* key and the server decrypts
it with the paired *private* key. The private key must be kept secure
since it is private to a single sender; the public key is disseminated
to clients. This technique is used for channel encryption as well as
user authentication.

**Authentication Methods**

Once an encrypted channel is established between the client and server,
additional negotiations take place between the two to authenticate the
user trying to access the server. OpenSSH offers several methods for
this purpose; they are listed below in the order in which they are
attempted during the authentication process:

[•]{.c85}GSSAPI-based (*Generic Security Service Application Program
Interface*) authentication

[•]{.c85}Host-based authentication

[•]{.c85}Public key-based authentication

[•]{.c85}Challenge-response authentication

[•]{.c85}Password-based authentication

Let's review each one in detail.

**GSSAPI-Based Authentication**

GSSAPI provides a standard interface that allows security mechanisms,
such as Kerberos, to be plugged in. OpenSSH uses this interface and the
underlying Kerberos for authentication. With this method, an exchange of
tokens takes place between the client and server to validate user
identity.

**Host-Based Authentication**

This type of authentication allows a single user, a group of users, or
all users on the client to be authenticated on the server. A user may be
configured to log in with a matching username on the server or as a
different user that already exists there. For each user that requires an
automatic entry on the server, a \~/*.shosts* file is set up containing
the client name or IP address, and, optionally, a different username.

The same rule applies to a group of users or all users on the client
that require access to the server. In that case, the setup is done in
the **etc*ssh/shosts.equiv* file on the server.

**Private/Public Key-Based Authentication**

This method uses a private/public key combination for user
authentication. The user on the client has a public key and the server
stores the corresponding private key. At the login attempt, the server
prompts the user to enter the passphrase associated with the key and
logs the user in if the passphrase and key are validated.

**ChallengeResponse Authentication**

This method is based on the response(s) to one or more arbitrary
challenge questions that the user has to answer correctly in order to be
allowed to log in to the server.

**Password-Based Authentication**

This is the last fall back option. The server prompts the user to enter
their password. It checks the password against the stored entry in the
*shadow* file and allows the user in if the password is confirmed.

Of the five authentication methods, the password-based method is common
and requires no further explanation. The GSSAPI-based, host-based, and
challenge-response methods are beyond the scope of this book. The
public/private authentication and encryption methods will be the focus
in the remainder of this chapter.

**OpenSSH Protocol Version and Algorithms**

OpenSSH has evolved over the years. Its latest and the default version
in RHEL 8, version 2, has numerous enhancements, improvements, and
sophisticated configuration options. It supports various algorithms for
data encryption and user authentication (digital signatures) such as
RSA, DSA, and ECDSA. RSA is more common and it is widely employed partly
because it supports both encryption and authentication. In contrast, DSA
and ECDSA are restricted to authentication only. These algorithms are
used to generate public and private key pairs for the asymmetric
technique.

RSA stands for *Rivest-Shamir-Adleman*, who first published this
algorithm, DSA for *Digital Signature Algorithm*, and ECDSA is an
acronym for *Elliptic Curve Digital Signature Algorithm*.

**[OpenSSH]{#part0031_split_001.html#id_508 .calibre10} Packages**

OpenSSH has three software packages that are of interest. These are
*openssh*, *openssh-clients*, and *openssh-server*. The *openssh*
package provides the *ssh-keygen* command and some library routines; the
*openssh-clients* package includes commands, such as *scp*, *sftp*,
*ssh*, and *ssh-copy-id*, and a client configuration file
**etc*ssh/ssh_config*; and the *openssh-server* package contains the
*sshd* service daemon, server configuration file **etc*ssh/sshd_config*,
and library routines. By default, all three packages are installed
during OS installation.

**[OpenSSH]{#part0031_split_001.html#id_509 .calibre10} Server Daemon
and Client Commands**

The OpenSSH server program *sshd* is preconfigured and operational on
new RHEL installations, allowing remote users to log in to the system
using an ssh client program such as PuTTY or the *ssh* command. This
daemon listens on well-known TCP port 22 as documented in the
**etc*ssh/sshd_config* file with the Port directive.

The client software includes plenty of utilities such as those listed
and described in [Table
19-1](#part0031_split_001.html#id_754){.calibre5}.

::: c49
  ------------- -------------------------------------------------------------------------------------
  **Command**   **Description**
  scp           The secure remote copy command that replaced the non-secure rcp command
  sftp          The secure remote copy command that replaced the non-secure ftp command
  ssh           The secure remote login command that replaced non-secure telnet and rlogin commands
  ssh-copy-id   Copies public key to remote systems
  ssh-keygen    Generates and manages private and public key pairs
  ------------- -------------------------------------------------------------------------------------

**[Table]{#part0031_split_001.html#id_754} 19-1 OpenSSH Client Tools**
:::

The use of these commands is demonstrated in the following subsections.

**[Server]{#part0031_split_001.html#id_510 .calibre10} Configuration
File**

The OpenSSH server daemon *sshd* has a configuration file that defines
default global settings on how it should operate. This file is located
in the **etc*ssh* directory and called *sshd_config*. There are a number
of directives preset in this file that affect all inbound ssh
communication and are tuned to work as-is for most use cases. In
addition, the **var*log/secure* log file is used to capture
authentication messages.

A few directives with their default values from the *sshd_config* file
are displayed below:

![](images/00920.jpeg){.image2}

  --------------------------------- ----------------------
  #Port                             22
  #Protocol                         2
  ListenAddress                     0.0.0.0
  SyslogFacility                    AUTHPRIV
  #LogLevel                         INFO
  PermitRootLogin                   yes
  #PubkeyAuthentication             yes
  AuthorizedKeysFile                .ssh/authorized_keys
  PasswordAuthentication            yes
  #PermitEmptyPasswords             no
  ChallengeResponseAuthentication   no
  UsePAM                            yes
  X11Forwarding                     yes
  --------------------------------- ----------------------

The above directives are elaborated in [Table
19-2](#part0031_split_001.html#id_755){.calibre5}.

::: c49
  --------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Directive**                     **Description**
  Port                              Specifies the port number to listen on. Default is 22.
  Protocol                          Specifies the default protocol version to use.
  ListenAddress                     Sets the local addresses the sshd service should listen on. Default is to listen on all local addresses.
  SyslogFacility                    Defines the facility code to be used when logging messages to the *var*log/secure file. This is based on the configuration in the *etc*rsyslog.conf file. Default is AUTHPRIV.
  LogLevel                          Identifies the level of criticality for the messages to be logged. Default is INFO.
  PermitRootLogin                   Allows or disallows the root user to log in directly to the system. Default is yes.
  PubKeyAuthentication              Enables or disables public key-based authentication. Default is yes.
  AuthorizedKeysFile                Sets the name and location of the file containing a user's authorized keys. Default is \~/.ssh/authorized_keys.
  PasswordAuthentication            Enables or disables local password authentication. Default is yes.
  PermitEmptyPasswords              Allows or disallows the use of null passwords. Default is no.
  ChallengeResponseAuthentication   Enables or disables challenge-response authentication mechanism. Default is yes.
  UsePAM                            Enables or disables user authentication via PAM. If enabled, only root will be able to run the sshd daemon. Default is yes.
  X11Forwarding                     Allows or disallows remote access to graphical applications. Default is yes.
  --------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0031_split_001.html#id_755} 19-2 OpenSSH Server
Configuration File**
:::

There are many more settings available that may be added to the file for
additional control. Check out the manual pages of the *sshd_config* file
(**man 5 sshd_config**) for details.

**Client Configuration File**

Each RHEL client machine that uses ssh to access a remote OpenSSH server
has a local configuration file that directs how the client should
behave. This file, *ssh_config*, is located in the **etc*ssh* directory.
There are a number of directives preset in this file that affect all
outbound ssh communication and are tuned to work as-is for most use
cases.

A few directives with their default values from the *ssh_config* file
are displayed below:

![](images/00921.jpeg){.image2}

  --------------------------- ----------------
  \# Host \*                  
  \# ForwardX11               no
  \# PasswordAuthentication   yes
  \# StrictHostKeyChecking    ask
  \# IdentityFile             \~/.ssh/id_rsa
  \# IdentityFile             \~/.ssh/id_dsa
  \# Port                     22
  \# Protocol                 2
  --------------------------- ----------------

The above directives are described in [Table
19-3](#part0031_split_001.html#id_756){.calibre5}.

::: c49
  ------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Directive**            **Description**
  Host                     Container that declares directives applicable to one host, a group of hosts, or all hosts. It ends when another occurrence of Host or Match is encountered. Default is \*, which sets global defaults for all hosts.
  ForwardX11               Enables or disables automatic redirection of X11 traffic over SSH connections. Default is no.
  PasswordAuthentication   Allows or disallows password authentication. Default is yes.
  StrictHostKeyChecking    Controls (1) whether to add host keys (host fingerprints) to */.ssh/known_hosts when accessing a host for the first time, and (2) what to do when the keys of a previously-accessed host mismatch with what is stored in* /.ssh/known_hosts. Options are:
                           **no:** adds new host keys and ignores changes to existing keys. **yes:** adds new host keys and disallows connections to hosts with non-matching keys. **accept-new:** adds new host keys and disallows connections to hosts with non-matching keys. **ask (default):** prompts whether to add new host keys and disallows connections to hosts with non-matching keys.
  IdentityFile             Defines the name and location of a file that stores a user's private key for their identity validation. Defaults are id_rsa, id_dsa, and id_ecdsa based on the type of algorithm used. Their corresponding public key files with .pub extension are also stored at the same directory location.
  Port                     Sets the port number to listen on. Default is 22.
  Protocol                 Specifies the default protocol version to use
  ------------------------ --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0031_split_001.html#id_756} 19-3 OpenSSH Client
Configuration File**
:::

The *\~/.ssh* directory does not exist by default; it is created when a
user executes the *ssh-keygen* command for the first time to generate a
key pair or connects to a remote ssh server and accepts its host key for
the first time. In the latter case, the client stores the server's host
key locally in a file called *known_hosts* along with its hostname or IP
address. On subsequent access attempts, the client will use this
information to verify the server's authenticity.

There are a lot more settings available that may be added to the file
for additional control. Check out the manual pages of the *ssh_config*
file (**man 5 ssh_config**) for details.

**[System]{#part0031_split_001.html#id_511 .calibre10} Access and File
Transfer**

A user must log in to the Linux system in order to use it or transfer
files. The login process identifies the user to the system. For
accessing a RHEL system remotely, use the *ssh* command, and the *scp*
or the *sftp* command for copying files. These commands require either a
resolvable hostname of the target system or its IP address in order to
try to establish a connection. All these commands are secure and may be
used over secure and unsecure network channels to exchange data.

The following subsections and exercises describe multiple access
scenarios including accessing a RHEL system (*server20*) from another
RHEL system (*server10*) and a Windows computer, accessing a RHEL system
(*server20*) using ssh keys, and transferring files using *scp* and
*sftp*.

**[Exercise]{#part0031_split_001.html#id_512 .calibre10} 19-1: Access
RHEL System from Another RHEL System**

This exercise should be done on *server10* and *server20* as *user1*.

This exercise works under two assumptions: (1) *user1* exists on both
*server10* and *server20*, and (2) hostname and IP mapping is in place
in the **etc*hosts* file ([Chapter
16](#part0028_split_000.html#page_375){.calibre5}). Use the IP address
in lieu of the hostname if the mapping is unavailable for *server20*.

In this exercise, you will issue the *ssh* command as *user1* on
*server10* to log in to *server20*. You will run appropriate commands on
*server20* for validation. You will log off and return to the
originating system.

1[.]{.c19}Issue the *ssh* command as *user1* on *server10*:

![](images/00922.jpeg){.image2}

Answer 'yes' to the question presented and press Enter to continue. This
step adds the hostname of *server20* to a file called *known_hosts*
under **home*user1/.ssh* directory on the originating computer
(*server10*). This message will not reappear on subsequent login
attempts to *server20* for this user. Enter the correct password for
*user1* to be allowed in. You will be placed in the home directory of
*user1* on *server20*. The command prompt will reflect that information.

2[.]{.c19}Issue the basic Linux commands *whoami*, *hostname*, and *pwd*
to confirm that you are logged in as *user1* on *server20* and placed in
the correct home directory:

![](images/00923.jpeg){.image2}

3[.]{.c19}Run the *logout* or the *exit* command or simply press the key
combination Ctrl+d to log off *server20* and return to *server10*:

![](images/00924.jpeg){.image2}

This concludes the exercise.

If you wish to log on as a different user such as *user2* (assuming
*user2* exists on the target server *server20*), you may run the *ssh*
command in either of the following ways:

![](images/00925.jpeg){.image2}

The above will allow you to log in if the password entered for *user2*
is valid.

**[Exercise]{#part0031_split_001.html#id_513 .calibre10} 19-2: Generate,
Distribute, and Use SSH Keys**

This exercise should be done on *server10* and *server20* as *user1* and
*sudo* where required.

In this exercise, you will generate a password-less ssh key pair using
RSA algorithm for *user1* on *server10*. You will display the private
and public file contents. You will distribute the public key to
*server20* and attempt to log on to *server20* from *server10*. You will
show the log file message for the login attempt.

1[.]{.c19}Log on to *server10* as *user1*.

2[.]{.c19}Generate RSA keys without a password (-N) and without detailed
output (-q). Press Enter when prompted to provide the filename to store
the private key.

![](images/00926.jpeg){.image2}

The content of the *id_rsa* (private key) file is shown below:

![](images/00927.jpeg){.image2}

The content of the *id_rsa.pub* (public key) file is displayed below:

![](images/00928.jpeg){.image2}

3[.]{.c19}Copy the public key file to *server20* under
**home*user1/.ssh* directory. Accept the fingerprints for *server20*
when prompted (only presented on the first login attempt). Enter the
password for *user1* set on *server20* to continue with the file copy.
The public key will be copied as *authorized_keys*.

![](images/00929.jpeg){.image2}

At the same time, this command also creates or updates the *known_hosts*
file on *server10* and stores the fingerprints for *server20* in it.
Here is what is currently stored in it:

![](images/00930.jpeg){.image2}

4[.]{.c19}On *server10*, run the *ssh* command as *user1* to connect to
*server20*. You will not be prompted for a password because there was
none assigned to the ssh keys.

![](images/00931.jpeg){.image2}

You can view this login attempt in the **var*log/secure* file on
*server20*:

![](images/00932.jpeg){.image2}

The log entry shows the timestamp, hostname, process name and PID,
username and source IP, and other relevant information. This file will
log all future login attempts for this user.

**[Executing]{#part0031_split_001.html#id_514 .calibre10} Commands
Remotely Using ssh**

The *ssh* command is a secure replacement for the legacy unsecure tools
*telnet*, *rlogin*, and *rsh*. It allows you to securely sign in to a
remote system or execute a command without actually logging on to it.
[Exercise 19-2](#part0031_split_001.html#id_513){.calibre5} demonstrated
how a user can log in using this command. The following shows a few
basic examples on how to use *ssh* to execute a command on a remote
system.

Invoke the *ssh* command on *server10* to execute the *hostname* command
on *server20*:

![](images/00933.jpeg){.image2}

Run the *nmcli* command on *server20* to show (s) active network
connections (c):

![](images/00934.jpeg){.image2}

You can run any command on *server20* this way without having to log in
to it.

**[Copying]{#part0031_split_001.html#id_515 .calibre10} Files Remotely
Using scp**

Similar to *ssh*, a user can execute the *scp* command to transfer files
from *server10* to *server20*, and vice versa. This program can be run
by a normal user as long as the user has the required read and write
permissions on the source and destination, or by the *root* user. Here
are a few examples to understand the program's syntax and usage.

To transfer the **etc*chrony.conf* file from *server20* to */tmp* on
*server10* and confirm:

![](images/00935.jpeg){.image2}

The program took not even a second to transfer the file. The file size
is 1103 bytes. The *ls* command confirms the pull.

Now let's transfer the entire **etc*sysconfig* directory (-r) from
*server10* into */tmp* on *server20* and confirm. Ignore any permission
errors reported in the output.

![](images/00936.jpeg){.image2}

Run the *ls* command on *server20* for verification:

![](images/00937.jpeg){.image2}

The output verifies the directory copy.

In the above examples, the user account that was used on the source and
target servers is the same user, *user1*. To transfer a file or
directory using a different user account on the target server, you need
to include that user's name with the command. You must know the password
for the user on the target server. Here is the syntax:

![](images/00938.jpeg){.image2}

Check the manual pages of the *scp* command for more details and usage
examples.

**[Transferring]{#part0031_split_001.html#id_516 .calibre10} Files
Remotely Using sftp**

The *sftp* command is an interactive file transfer tool that can be used
instead of *scp*. This tool can be launched as follows on *server10* to
connect to *server20*:

![](images/00939.jpeg){.image2}

Type ? at the prompt to list available commands along with a short
description:

![](images/00940.jpeg){.image2}

As shown in the above screenshot, there are many common commands
available at the sftp\> prompt. These include *cd* to change directory,
*get*/*put* to download/upload a file, *ls* to list files, *pwd* to
print working directory, *mkdir* to create a directory, *rename* to
rename a file, *rm* to remove a file, and *bye*/*quit/exit* to exit the
program and return to the command prompt. These commands will run on the
remote server (*server20*). The following screenshot shows how these
commands are used:

![](images/00941.jpeg){.image2}

Furthermore, there are four commands beginning with an 'l'---*lcd*,
*lls*, *lpwd*, and *lmkdir*---at the sftp\> prompt. These commands are
intended to be run on the source server (*server10*). Other Linux
commands are also available at the sftp\> prompt that you may use for
basic file management operations on the remote server.

Type *quit* at the sftp\> prompt to exit the program when you're done.

You may use either *sftp* or *scp* for transferring files depending on
your comfort level. Consult the manual pages of the commands for options
and additional details.

**[Synchronizing]{#part0031_split_001.html#id_517 .calibre10} Files
Remotely Using rsync**

The *rsync* (*remote synchronization*) program works in a manner similar
to the *cp*, *rcp*, and *scp* commands to copy files between the source
and destination. With *rsync*, the source and destination could be on
the same system or different systems. The first initiation of *rsync*
copies all files from the source to the destination with subsequent
executions copy only the updated files. The *rsync* command uses the ssh
protocol by default.

The following examples explain the usage of the program and introduce
some common flags.

To copy a single file such as *grub.conf* to */tmp* on the same system:

![](images/00942.jpeg){.image2}

The -a option in the above example instructs the command to perform an
archive operation and preserve all file attributes such as permissions,
ownership, symlinks, and timestamps. The -v switch is used for
verbosity.

The actual size of the *grub.cfg* file is 5,032 bytes. The additional
bytes sent (5,126 minus 5,032 = 94 bytes) contain the metadata and other
overhead, and the received bytes signify the metadata received. The
output displays the files being copied and the file transfer rate as
well.

Subsequent invocations of the above would produce an output similar to
the following if the file has not been modified:

![](images/00943.jpeg){.image2}

It shows no filenames under the file list, as there was no transfer
occurred.

To copy **etc*rsyslog.conf* to */tmp* to *server20* using in-transit
compression (-z) and displaying the transfer progress (-P):

![](images/00944.jpeg){.image2}

To copy the entire **home*user1* directory recursively (-r) from
*server20* to **tmp*trans* directory on *server10* (create **tmp*trans*
before running the *rsync* command):

![](images/00945.jpeg){.image2}

The *rsync* command is fast and versatile, and has numerous other
options available. Refer to the command's manual pages for a description
of options and usage examples.

**[Chapter]{#part0031_split_001.html#id_518 .calibre10} Summary**

This chapter discussed the open source version of the secure shell
service. It started with an overview of the service, and described what
it is, how it works, available versions, and algorithms employed. We
skimmed through various encryption techniques and authentication
methods. We touched upon the service daemon, client and server
configuration files, and commands. We demonstrated accessing a lab
server from another lab server. We generated and distributed
password-less private/public key pair and employed ssh utilities to
remote execute commands and transfer files.

Lastly, we examined a program that may be put into action to keep files
synchronized between two systems over an ssh channel.

**[Review]{#part0031_split_001.html#id_519 .calibre10} Questions**

1[.]{.c19}What is the secure equivalent for the *rcp* command?

2[.]{.c19}What would the command *ssh-keygen -N ""* do?

3[.]{.c19}The primary secure shell server configuration file is
*ssh_config*. True or False?

4[.]{.c19}Which three common algorithms are used with SSH version 2 for
encryption and/or authentication?

5[.]{.c19}What is the secure shell equivalent for the *telnet* command?

6[.]{.c19}True or False? By default, the *root* user can directly log on
to a RHEL system.

7[.]{.c19}What is the default location to store user SSH keys?

8[.]{.c19}What would the command *ssh-copy-id* do?

9[.]{.c19}What is the *rsync* command used for?

10[.]{.c23}Which two of the five authentication methods mentioned in
this chapter are more prevalent?

11[.]{.c23}What is the use of the *ssh-keygen* command?

12[.]{.c23}Name the default algorithm used with SSH.

13[.]{.c23}What kind of information does the *\~/.ssh/known_hosts* file
store?

14[.]{.c23}List the two encryption techniques described in this chapter.

15[.]{.c23}What is the default port used by the secure shell service?

16[.]{.c23}Which log file stores authentication messages?

17[.]{.c23}The *ssh* tool provides a non-secure tunnel over a network
for accessing a RHEL system. True or False?

18[.]{.c23}Name the SSH client-side configuration file.

19[.]{.c23}What would the command *ssh server10 ls* do?

**[Answers]{#part0031_split_001.html#id_520 .calibre10} to Review
Questions**

1[.]{.c19}The *scp* command is the secure equivalent for the *rcp*
command.

2[.]{.c19}The command provided will generate a password-less ssh key
pair using the default RSA algorithm.

3[.]{.c19}False. The primary secure shell configuration file is
*sshd_config*.

4[.]{.c19}The SSH version 2 uses RSA, DSA, and ECDSA algorithms.

5[.]{.c19}The secure equivalent for *telnet* is the *ssh* command.

6[.]{.c19}True.

7[.]{.c19}Under the *\~/.ssh* directory.

8[.]{.c19}The *ssh-copy-id* command is used to distribute the public key
to remote systems.

9[.]{.c19}The *rsync* command is used to maintain a copy of source files
at remote location.

10[.]{.c23}The public key-based and password-based authentication
methods are more prevalent.

11[.]{.c23}The *ssh-keygen* command is used to generate public/private
key combination for use with ssh.

12[.]{.c23}The default algorithm used with ssh is RSA.

13[.]{.c23}The *\~/.ssh/known_hosts* file stores fingerprints of remote
servers.

14[.]{.c23}The two encryption techniques are symmetric (secret key) and
asymmetric (public key).

15[.]{.c23}The default port used by the secure shell service is 22.

16[.]{.c23}The **var*log/secure* file stores authentication messages.

17[.]{.c23}False. The *ssh* command provides a secure tunnel over a
network.

18[.]{.c23}The client-side SSH configuration file is *ssh_config* and it
is located in the **etc*ssh* directory.

19[.]{.c23}The command provided will run the *ls* command on the
specified remote ssh server without the need for the user to log in.

**[Do-]{#part0031_split_001.html#id_521 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

**[Lab]{#part0031_split_001.html#id_522 .calibre10} 19-1: Establish
Key-Based Authentication**

As *user1* with *sudo* on *server10* and *server20*, create user account
*user20* and assign a password. As *user20* on *server10*, generate a
private/public key pair without a passphrase using the *ssh-keygen*
command. Distribute the public key to *server20* with the *ssh-copy-id*
command. Log on to *server20* as *user20* and accept the fingerprints
for the server if presented. On subsequent log in attempts from
*server10* to *server20*, *user20* should not be prompted for their
password. (Hint: System Access and File Transfer).

**[Lab]{#part0031_split_001.html#id_523 .calibre10} 19-2: Test the
Effect of PermitRootLogin Directive**

As *user1* with *sudo* on *server20*, edit the **etc*ssh/sshd_config*
file and change the value of the directive PermitRootLogin to "no". Use
the *systemctl* command to activate the change. As *root* on *server10*,
run **ssh server20** (or its IP address). You'll get permission denied
message. Reverse the change on *server20* and retry **ssh server20**.
You should be able to log in. (Hint: The OpenSSH Service).

[]{#part0032_split_000.html}
