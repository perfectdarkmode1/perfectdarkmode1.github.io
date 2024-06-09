## Chapter 18 {style="text-align: right"}

\

### The Secure Shell Service {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Understand the OpenSSH service, versions, and algorithms

\

Overview of encryption techniques and authentication methods

\

Describe OpenSSH administration commands and configuration files

\

Configure private/public key-based authentication

\

Access OpenSSH server from other Linux systems

\

Use OpenSSH client tools to transfer files

\

Synchronize files remotely over OpenSSH

\

#### RHCSA Objectives:

\

04\. Access remote systems using ssh

25\. Securely transfer files between systems

54\. Configure key-based authentication for SSH

::: {style="page-break-before: always;"}
:::

\

Secure Shell is a network service that delivers a secure mechanism for
data transmission between source and destination systems over insecure
network paths. It provides a set of utilities that allows users to
generate key pairs and use them to set up trusted logins between systems
for themselves.

\

::: {style="text-align: center;"}
![](image-T8F8RZ4U.jpg){height="100%"}
:::

Additional utilities in the set gives remote users the ability to log
in, execute commands, and transfer files securely over encrypted network
channels. These tools have predominantly supplanted their insecure
counterparts in the corporate world.

::: {style="page-break-before: always;"}
:::

[]{#chapter0544.html}

## The OpenSSH Service {.style3}

\

Secure Shell (SSH) delivers a secure mechanism for data transmission
between source and destination systems over IP networks. It was designed
to replace the old remote login programs that transmitted user passwords
in clear text and data unencrypted. SSH employs digital signatures for
user authentication with encryption to secure a communication channel.
As a result, this makes it extremely hard for unauthorized people to
gain access to passwords or the data in transit. It also monitors the
data being transferred throughout a session to ensure integrity. SSH
includes a set of utilities---ssh and sftp---for remote users to log in,
transfer files, and execute commands securely.

::: {style="page-break-before: always;"}
:::

[]{#chapter0545.html}

## Common Encryption Techniques {.style3}

\

Encryption is a way of scrambling information with the intent to conceal
the real information from unauthorized access. OpenSSH can utilize
various encryption techniques during an end-to-end communication session
between two entities (client and server). The two common techniques are
symmetric and asymmetric. They are also referred to as secret key
encryption and public key encryption techniques.

\

### Symmetric Technique {.style3}

This technique uses a single key called a secret key that is generated
as a result of a negotiation process between two entities at the time of
their initial contact. Both sides use the same secret key during
subsequent communication for data encryption and decryption.

\

### Asymmetric Technique {.style3}

This technique uses a combination of private and public keys, which are
randomly generated and mathematically related strings of alphanumeric
characters attached to messages being exchanged. The client transmutes
the information with a public key and the server decrypts it with the
paired private key. The private key must be kept secure since it is
private to a single sender; the public key is disseminated to clients.
This technique is used for channel encryption as well as user
authentication.

::: {style="page-break-before: always;"}
:::

[]{#chapter0546.html}

## Authentication Methods {.style3}

\

Once an encrypted channel is established between the client and server,
additional negotiations take place between the two to authenticate the
user trying to access the server. OpenSSH offers several methods for
this purpose; they are listed below in the order in which they are
attempted during the authentication process:

\

• GSSAPI-based ( Generic Security Service Application Program Interface
) authentication

• Host-based authentication

• Public key-based authentication

• Challenge-response authentication

• Password-based authentication

\

Let's review each one in detail.

\

### GSSAPI-Based Authentication {.style3}

GSSAPI provides a standard interface that allows security mechanisms,
such as Kerberos, to be plugged in. OpenSSH uses this interface and the
underlying Kerberos for authentication. With this method, an exchange of
tokens takes place between the client and server to validate user
identity.

\

### Host-Based Authentication {.style3}

This type of authentication allows a single user, a group of users, or
all users on the client to be authenticated on the server. A user may be
configured to log in with a matching username on the server or as a
different user that already exists there. For each user that requires an
automatic entry on the server, a \~/.shosts file is set up containing
the client name or IP address, and, optionally, a different username.

\

The same rule applies to a group of users or all users on the client
that require access to the server. In that case, the setup is done in
the /etc/ssh/shosts.equiv file on the server.

\

### Private/Public Key-Based Authentication {.style3}

This method uses a private/public key combination for user
authentication. The user on the client has a private key and the server
stores the corresponding public key. At the login attempt, the server
prompts the user to enter the passphrase associated with the key and
logs the user in if the passphrase and key are validated.

\

### Challenge-Response Authentication {.style3}

This method is based on the response(s) to one or more arbitrary
challenge questions that the user has to answer correctly in order to be
allowed to log in to the server.

\

### Password-Based Authentication {.style3}

This is the last fall back option. The server prompts the user to enter
their password. It checks the password against the stored entry in the
shadow file and allows the user in if the password is confirmed.

\

Of the five authentication methods, the password-based method is common
and requires no further explanation. The GSSAPI-based, host-based, and
challenge-response methods are beyond the scope of this book. The
public/private authentication and encryption methods will be the focus
in the remainder of this chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0547.html}

## OpenSSH Protocol Version and Algorithms {.style3}

\

OpenSSH has evolved over the years. Its latest and the default version
in RHEL 9, version 2, has numerous enhancements, improvements, and
sophisticated configuration options. It supports various algorithms for
data encryption and user authentication (digital signatures) such as
RSA, DSA, and ECDSA. RSA is more prevalent than the rest partly because
it supports both encryption and authentication. In contrast, DSA and
ECDSA are restricted to authentication only. These algorithms are used
to generate public and private key pairs for the asymmetric technique.

\

RSA stands for Rivest-Shamir-Adleman, who first published this
algorithm, DSA for Digital Signature Algorithm, and ECDSA is an acronym
for Elliptic Curve Digital Signature Algorithm.

::: {style="page-break-before: always;"}
:::

[]{#chapter0548.html}

## OpenSSH Packages {.style3}

\

OpenSSH has three software packages that are of interest. These are
openssh, openssh-clients, and openssh-server. The openssh package
provides the ssh-keygen command and some library routines; the
openssh-clients package includes commands, such as sftp, ssh, and
ssh-copy-id, and a client configuration file /etc/ssh/ssh_config; and
the openssh-server package contains the sshd service daemon, server
configuration file /etc/ssh/sshd_config, and library routines. By
default, all three packages are installed during OS installation.

::: {style="page-break-before: always;"}
:::

[]{#chapter0549.html}

## OpenSSH Server Daemon and Client Commands {.style3}

\

The OpenSSH server program sshd is preconfigured and operational on new
RHEL installations, allowing remote users to log in to the system using
an ssh client program such as PuTTY or the ssh command. This daemon
listens on well-known TCP port 22 as documented in the
/etc/ssh/sshd_config file with the Port directive.

\

A discussion around the scp command has been removed from the book, as
this tool is not recommended to be used due to some serious security
flaws; use sftp instead.

\

The client software includes plenty of utilities such as those listed
and described in Table 18-1.

\

  ----------------------------------- -----------------------------------
  Command                             Description

  sftp                                A secure remote file transfer
                                      program

  ssh                                 A secure remote login command

  ssh-copy-id                         Copies public key to remote systems

  ssh-keygen                          Generates and manages private and
                                      public key pairs
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 18-1 OpenSSH Client Tools

\

The use of these commands is demonstrated in the following subsections.

::: {style="page-break-before: always;"}
:::

[]{#chapter0550.html}

## Server Configuration File {.style3}

\

The OpenSSH service sshd has a configuration file that defines default
global settings on how it should operate. This file is located in the
/etc/ssh directory and called sshd_config. There are a number of
directives preset in this file that affect all inbound ssh communication
and are tuned to work as-is for most use cases. In addition, the
/var/log/secure log file is used to capture authentication messages.

\

A few directives with their default values from the sshd_config file are
displayed below:

\

<div>

![](image-UYPEB3P5.jpg){height="100%"}

</div>

The above directives are elaborated in Table 18-2.

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  Port                                Specifies the port number to listen
                                      on. Default is 22.

  Protocol                            Specifies the default protocol
                                      version to use.

  ListenAddress                       Sets the local addresses the sshd
                                      service should listen on. Default
                                      is to listen on all local
                                      addresses.

  SyslogFacility                      Defines the facility code to be
                                      used when logging messages to the
                                      /var/log/secure file. This is based
                                      on the configuration in the
                                      /etc/rsyslog.conf file. Default is
                                      AUTHPRIV.

  LogLevel                            Identifies the level of criticality
                                      for the messages to be logged.
                                      Default is INFO.

  PermitRootLogin                     Allows or disallows the root user
                                      to log in directly to the system.
                                      Default is yes.

  PubKeyAuthentication                Enables or disables public
                                      key-based authentication. Default
                                      is yes.

  AuthorizedKeysFile                  Sets the name and location of the
                                      file containing a user's authorized
                                      keys. Default is
                                      \~/.ssh/authorized_keys.

  PasswordAuthentication              Enables or disables local password
                                      authentication. Default is yes.

  PermitEmptyPasswords                Allows or disallows the use of null
                                      passwords. Default is no.

  ChallengeResponseAuthentication     Enables or disables
                                      challenge-response authentication
                                      mechanism. Default is yes.

  UsePAM                              Enables or disables user
                                      authentication via PAM. If enabled,
                                      only root will be able to run the
                                      sshd daemon. Default is yes.

  X11Forwarding                       Allows or disallows remote access
                                      to graphical applications. Default
                                      is yes.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 18-2 OpenSSH Server Configuration File

\

There are many more settings available that may be added to the file for
additional control. Check out the manual pages of the sshd_config file
(man 5 sshd_config) for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0551.html}

## Client Configuration File {.style3}

\

Each RHEL client machine that uses ssh to access a remote OpenSSH server
has a local configuration file that directs how the client should
behave. This file, ssh_config, is located in the /etc/ssh directory.
There are a number of directives preset in this file that affect all
outbound ssh communication and are tuned to work as-is for most use
cases.

\

A few directives with their default values from the ssh_config file are
displayed below:

\

<div>

![](image-E0QKD3CH.jpg){height="100%"}

</div>

The above directives are described in Table 18-3.

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  Host                                Container that declares directives
                                      applicable to one host, a group of
                                      hosts, or all hosts. It ends when
                                      another occurrence of Host or Match
                                      is encountered. Default is \*,
                                      which sets global defaults for all
                                      hosts.

  ForwardX11                          Enables or disables automatic
                                      redirection of X11 traffic over SSH
                                      connections. Default is no.

  PasswordAuthentication              Allows or disallows password
                                      authentication. Default is yes.

  StrictHostKeyChecking               Controls (1) whether to add host
                                      keys (host fingerprints) to
                                      \~/.ssh/known_hosts when accessing
                                      a host for the first time, and (2)
                                      what to do when the keys of a
                                      previously accessed host mismatch
                                      with what is stored in
                                      \~/.ssh/known_hosts. Options are:

                                      no: adds new host keys and ignores
                                      changes to existing keys.

                                      yes: adds new host keys and
                                      disallows connections to hosts with
                                      non-matching keys. accept-new: adds
                                      new host keys and disallows
                                      connections to hosts with
                                      non-matching keys. ask (default):
                                      prompts whether to add new host
                                      keys and disallows connections to
                                      hosts with non-matching keys.

  IdentityFile                        Defines the name and location of a
                                      file that stores a user's private
                                      key for their identity validation.
                                      Defaults are id_rsa, id_dsa, and
                                      id_ecdsa based on the type of
                                      algorithm used. Their corresponding
                                      public key files with .pub
                                      extension are also stored at the
                                      same directory location.

  Port                                Sets the port number to listen on.
                                      Default is 22.

  Protocol                            Specifies the default protocol
                                      version to use
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 18-3 OpenSSH Client Configuration File

\

The \~/.ssh directory does not exist by default; it is created when a
user executes the ssh-keygen command for the first time to generate a
key pair or connects to a remote ssh server and accepts its host key for
the first time. In the latter case, the client stores the server's host
key locally in a file called known_hosts along with its hostname or IP
address. On subsequent access attempts, the client will use this
information to verify the server's authenticity.

\

There are a lot more settings available that may be added to the file
for additional control. Check out the manual pages of the ssh_config
file (man 5 ssh_config) for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0552.html}

## System Access and File Transfer {.style3}

\

A user must log in to the Linux system in order to use it or transfer
files. The login process identifies the user to the system. For
accessing a RHEL system remotely, use the ssh command, and the sftp
command for copying files. These tools require either a resolvable
hostname of the target system or its IP address in order to establish a
connection. Both commands are secure and may be used over secure and
unsecure network channels for data exchange.

\

The following subsections and exercises describe multiple access
scenarios including accessing a RHEL system (server20) from another RHEL
system (server10) and a Windows computer, accessing a RHEL system
(server20) using ssh keys, and transferring files using sftp.

::: {style="page-break-before: always;"}
:::

[]{#chapter0553.html}

## Exercise 18-1: Access RHEL System from Another RHEL System {.style3}

\

This exercise should be done on server10 and server20 as user1.

\

This exercise works under two assumptions: (1) user1 exists on both
server10 and server20, and (2) hostname and IP mapping is in place in
the /etc/hosts file (Chapter 16). Use the IP address in lieu of the
hostname if the mapping is unavailable for server20.

\

In this exercise, you will issue the ssh command as user1 on server10 to
log in to server20. You will run appropriate commands on server20 for
validation. You will log off and return to the originating system.

\

1\. Issue the ssh command as user1 on server10:

\

<div>

![](image-C6AR1L63.jpg){height="100%"}

</div>

Answer 'yes' to the question presented and press Enter to continue. This
step adds the hostname of server20 to a file called known_hosts under
/home/user1/.ssh directory on the originating computer (server10). This
message will not reappear on subsequent login attempts to server20 for
this user. Enter the correct password for user1 to be allowed in. You
will be placed in the home directory of user1 on server20. The command
prompt will reflect that information.

\

2\. Issue the basic Linux commands whoami, hostname, and pwd to confirm
that you are logged in as user1 on server20 and placed in the correct
home directory:

\

<div>

![](image-UYW0XV6U.jpg){height="100%"}

</div>

3\. Run the logout or the exit command or simply press the key
combination Ctrl+d to log off server20 and return to server10:

\

<div>

![](image-P3O6NZMP.jpg){height="100%"}

</div>

This concludes the exercise.

\

If you wish to log on as a different user such as user2 (assuming user2
exists on the target server server20), you may run the ssh command in
either of the following ways:

\

<div>

![](image-B2SI8GOO.jpg){height="100%"}

</div>

The above will allow you to log in if the password entered for user2 is
valid.

::: {style="page-break-before: always;"}
:::

[]{#chapter0554.html}

## Exercise 18-2: Generate, Distribute, and Use SSH Keys {.style3}

\

This exercise should be done on server10 and server20 as user1 and sudo
where required. In this exercise, you will generate a passwordless ssh
key pair using RSA algorithm for user1 on server10. You will display the
private and public file contents. You will distribute the public key to
server20 and attempt to log on to server20 from server10. You will show
the log file message for the login attempt.

\

1\. Log on to server10 as user1.

2\. Generate RSA keys without a password (-N) and without detailed
output (-q). Press Enter when prompted to provide the filename to store
the private key.

\

<div>

![](image-18CH2YAQ.jpg){height="100%"}

</div>

The content of the id_rsa (private key) file is shown below:

\

<div>

![](image-57JMZECE.jpg){height="100%"}

</div>

The content of the id_rsa.pub (public key) file is displayed below:

\

<div>

![](image-ZF4UCGIL.jpg){height="100%"}

</div>

3\. Copy the public key file to server20 under /home/user1/.ssh
directory. Accept the fingerprints for server20 when prompted (only
presented on the first login attempt). Enter the password for user1 set
on server20 to continue with the file copy. The public key will be
copied as authorized_keys.

\

<div>

![](image-V0PMF9RX.jpg){height="100%"}

</div>

At the same time, this command also creates or updates the known_hosts
file on server10 and stores the fingerprints for server20 in it. Here is
what is currently stored in it:

\

<div>

![](image-OIHHXXPJ.jpg){height="100%"}

</div>

4\. On server10, run the ssh command as user1 to connect to server20.
You will not be prompted for a password because there was none assigned
to the ssh keys.

\

<div>

![](image-V02PXIDS.jpg){height="100%"}

</div>

You can view this login attempt in the /var/log/secure file on server20:

\

<div>

![](image-J24F26SQ.jpg){height="100%"}

</div>

The log entry shows the timestamp, hostname, process name and PID,
username and source IP, and other relevant information. This file will
log all future login attempts for this user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0555.html}

## Executing Commands Remotely Using ssh {.style3}

\

The ssh command allows you to securely sign in to a remote system or
execute a command without actually logging on to it. Exercise 18-2
demonstrated how a user can log in using this command. The following
shows a few basic examples on how to use ssh to execute a command on a
remote system.

\

Invoke the ssh command on server10 to execute the hostname command on
server20:

\

<div>

![](image-LHOE9L53.jpg){height="100%"}

</div>

Run the nmcli command on server20 to show (s) active network connections
(c):

\

<div>

![](image-FVC4GBQL.jpg){height="100%"}

</div>

You can run any command on server20 this way without having to log in to
it.

::: {style="page-break-before: always;"}
:::

[]{#chapter0556.html}

## Transferring Files Remotely Using sftp {.style3}

\

The sftp command is an interactive file transfer tool. This tool can be
launched as follows on server10 to connect to server20:

\

<div>

![](image-TAPZT0RN.jpg){height="100%"}

</div>

Type ? at the prompt to list available commands along with a short
description:

\

<div>

![](image-YLL4896K.jpg){height="100%"}

</div>

As shown in the above screenshot, there are many common commands
available at the sftp\> prompt. These include cd to change directory,
get/put to download/upload a file, ls to list files, pwd to print
working directory, mkdir to create a directory, rename to rename a file,
rm to remove a file, and bye/quit/exit to exit the program and return to
the command prompt. These commands will run on the remote server
(server20). The following screenshot shows how these commands are used:

\

<div>

![](image-7GQBAXOH.jpg){height="100%"}

</div>

Furthermore, there are four commands beginning with an 'l'---lcd, lls,
lpwd, and lmkdir---at the sftp\> prompt. These commands are intended to
be run on the source server (server10). Other Linux commands are also
available at the sftp\> prompt that you may use for basic file
management operations on the remote server.

\

Type quit at the sftp\> prompt to exit the program when you're done.

\

Consult the manual pages of the command for options and additional
details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0557.html}

## Chapter Summary {.style3}

\

This chapter discussed the open-source version of the secure shell
service. It started with an overview of the service, and described what
it is, how it works, available versions, and algorithms employed. We
skimmed through various encryption techniques and authentication
methods. We touched upon the service daemon, client and server
configuration files, and commands. We demonstrated accessing a lab
server from another lab server. We generated and distributed
passwordless private/public key pair and employed ssh utilities to
remote execute commands and transfer files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0558.html}

## Review Questions {.style3}

\

1\. Name the SSH client-side configuration file.

2\. What would the command ssh server10 ls do?

3\. What would the command ssh-keygen -N "" do?

4\. What is the default location to store user SSH keys?

5\. What would the command ssh-copy-id do?

6\. Which two of the five authentication methods mentioned in this
chapter are more prevalent?

7\. What is the use of the ssh-keygen command?

8\. Name the default algorithm used with SSH.

9\. The primary secure shell server configuration file is ssh_config.
True or False?

10\. Which three common algorithms are used with SSH version 2 for
encryption and/or authentication?

11\. What kind of information does the \~/.ssh/known_hosts file store?

12\. List the two encryption techniques described in this chapter.

13\. What is the default port used by the secure shell service?

14\. Which log file stores authentication messages?

15\. The ssh tool provides a non-secure tunnel over a network for
accessing a RHEL system. True or False?

::: {style="page-break-before: always;"}
:::

[]{#chapter0559.html}

## Answers to Review Questions {.style3}

\

1\. The client-side SSH configuration file is ssh_config and it is
located in the /etc/ssh directory.

2\. The command provided will run the ls command on the specified remote
ssh server without the need for the user to log in.

3\. The command provided will generate a passwordless ssh key pair using
the default RSA algorithm.

4\. Under the \~/.ssh directory.

5\. The ssh-copy-id command is used to distribute the public key to
remote systems.

6\. The public key-based and password-based authentication methods are
more prevalent.

7\. The ssh-keygen command is used to generate public/private key
combination for use with ssh.

8\. The default algorithm used with ssh is RSA.

9\. False. The primary secure shell configuration file is sshd_config.

10\. The SSH version 2 uses RSA, DSA, and ECDSA algorithms.

11\. The \~/.ssh/known_hosts file stores fingerprints of remote servers.

12\. The two encryption techniques are symmetric (secret key) and
asymmetric (public key).

13\. The default port used by the secure shell service is 22.

14\. The /var/log/secure file stores authentication messages.

15\. False. The ssh command provides a secure tunnel over a network.

::: {style="page-break-before: always;"}
:::

[]{#chapter0560.html}

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

[]{#chapter0561.html}

## Lab 18-1: Establish Key-Based Authentication {.style3}

\

As user1 with sudo on server30 and server40, create user account user20
and assign a password. As user20 on server40, generate a private/public
key pair without a passphrase using the ssh-keygen command. Distribute
the public key to server30 with the ssh-copy-id command. Log on to
server30 as user20 and accept the fingerprints for the server if
presented. On subsequent log in attempts from server40 to server30,
user20 should not be prompted for their password. (Hint: System Access
and File Transfer).

::: {style="page-break-before: always;"}
:::

[]{#chapter0562.html}

## Lab 18-2: Test the Effect of PermitRootLogin Directive {.style3}

\

As user1 with sudo on server40, edit the /etc/ssh/sshd_config file and
change the value of the directive PermitRootLogin to "no". Use the
systemctl command to activate the change. As root on server30, run ssh
server40 (or use its IP). You'll get permission denied message. Reverse
the change on server40 and retry ssh server40. You should be able to log
in. (Hint: The OpenSSH Service).

::: {style="page-break-before: always;"}
:::

[]{#chapter0563.html}
