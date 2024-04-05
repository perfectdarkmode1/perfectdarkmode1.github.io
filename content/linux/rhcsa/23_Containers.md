
This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Understand container technology

[![](images/00001.jpeg){.c37}]{.c36}Identify key Linux features that
establish the foundation to run containers

[![](images/00001.jpeg){.c37}]{.c36}Analyze container benefits

[![](images/00001.jpeg){.c37}]{.c36}A better home for containers

[![](images/00001.jpeg){.c37}]{.c36}Grasp the concepts of container
images and registries

[![](images/00001.jpeg){.c37}]{.c36}Compare pros and cons of root and
rootless containers

[![](images/00001.jpeg){.c37}]{.c36}Examine registry configuration file

[![](images/00001.jpeg){.c37}]{.c36}Work with container images (find,
inspect, pull, list, and delete)

[![](images/00001.jpeg){.c37}]{.c36}Administer basic containers (start,
list, stop, remove, interact with, run commands from outside, attach to,
run custom entry point commands, etc.)

[![](images/00001.jpeg){.c37}]{.c36}Implement advanced container
features (port mapping, environment variables, and persistent storage)

[![](images/00001.jpeg){.c37}]{.c36}Control container operational states
via systemd

[RHCSA Objectives:]{.c39}

[63]{#part0035_split_000.html#id_827 .calibre10}. Find and retrieve
container images from a remote registry

[64]{#part0035_split_000.html#id_828 .calibre10}. Inspect container
images

[65]{#part0035_split_000.html#id_829 .calibre10}. Perform container
management using commands such as podman and skopeo

[66]{#part0035_split_000.html#id_830 .calibre10}. Perform basic
container management such as running, starting, stopping, and listing
running containers

[67]{#part0035_split_000.html#id_831 .calibre10}. Run a service inside a
container

[68]{#part0035_split_000.html#id_832 .calibre10}. Configure a container
to start automatically as a systemd service

[69]{#part0035_split_000.html#id_833 .calibre10}. Attach persistent
storage to a container

::: {#part0035_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0035_split_001.html}

[ C]{.c42}[ontainers]{.c43} and containerization technologies such as
Docker and Kubernetes have received an overwhelming appreciation and
massive popularity in recent years. They are now part of many new
deployments. Containers offer an improved method to package distributed
applications, deploy them in a consistent manner, and run them in
isolation from one another on the same or different virtual or physical
server(s). Containers take advantage of the native virtualization
features available in the Linux kernel. Each container typically
encapsulates one self-contained application that includes all
dependencies such as library files, configuration files, software
binaries, and services.

This chapter presents an overview of container images, container
registries, and containers. It shows how to interact with images and
registries. It demonstrates how to launch, manage, and interact with
containers. It discusses advanced topics such as mapping a host port
with a container port, passing and setting environment variables, and
attaching host storage for data persistence. The chapter ends with a
detailed look at controlling the operational states of containers via
the systemd service. There are numerous exercises in the chapter to
support the concepts learned.

**[Introduction]{#part0035_split_001.html#id_597 .calibre10} to
Containers**

A *container* is essentially a set of processes that runs in complete
seclusion on a Linux system. A single Linux system running on bare metal
hardware or in a virtual machine may have tens or hundreds of containers
running. The underlying hardware may be located either on the ground or
in the cloud.

Traditionally, one or more software applications are deployed on a
single server. These applications may have conflicting requirements in
terms of shared library files, package dependencies, and software
version. Moreover, patching or an update to the operating system may
result in breaking an application functionality. To address these and
other potential challenges, developers perform an analysis on their
current deployments before they decide whether to collocate a new
application with an existing one or to go with a new server without
taking the risk of breaking the current operation.

Fortunately, there is a better choice available now in the form of
containers. Developers can now package their application alongside
dependencies, shared library files, environment variables, and other
specifics in a single image file and use that file to run the
application in a unique, isolated "virtual computer" called container.
Each container is treated as a complete whole, which can be tagged,
started, stopped, restarted, or even transported to another server
independent of other containers. This way any conflicts that may exist
among applications, within application components, or with the operating
system can be evaded. Applications encapsulated to run inside containers
are called *containerized applications*, and this is a growing trend for
architecting and deploying applications, application components, and
databases in real world environments.

**[Containers]{#part0035_split_001.html#id_598 .calibre10} and the Linux
Features**

The container technology employs some of the core features available in
the Linux kernel. These include control groups, namespaces, seccomp
(*secure computing mode*), and SELinux. A short description of each
feature is provided below:

**Control Groups**

*Control groups* (abbreviated as *cgroups*) splits processes into groups
to set limits on their consumption of compute resources---CPU, memory,
disk, and network I/O. These restrictions result in controlling
individual processes from over utilizing available resources.

**Namespaces**

*Namespaces* restrict the ability of process groups from seeing or
accessing system resources---PIDs, network interfaces, mount points,
hostname, etc.---thus instituting a layer of isolation between process
groups and the rest of the system. This feature guarantees a secure,
performant, and stable environment for containerized applications as
well as the host operating system.

**Secure Computing Mode (seccomp) and SELinux**

These Linux features impose security constraints thereby protecting
processes from one another and the host operating system from running
processes.

The container technology employs these characteristics to run processes
isolated in a highly secure environment with full control over what they
can or cannot do.

**[Benefits]{#part0035_split_001.html#id_599 .calibre10} of Using
Containers**

There are several benefits linked with using containers. These benefits
range from security to manageability and from independence to velocity.
The following provides a quick look at common containerization benefits:

**Isolation**

Containers are not affected due to changes in the host operating system
or in other hosted or containerized applications, as they run fully
isolated from the rest of the environment.

**Loose Coupling**

Containerized applications are loosely coupled with the underlying
operating system due to their self-containment and minimal level of
dependency.

**Maintenance Independence**

Maintenance is performed independently on individual containers.

**Less Overhead**

Containers require fewer system resources than do bare metal and virtual
servers.

**Transition Time**

Containers require a few seconds to start and stop.

**Transition Independence**

Transitioning from one state to another (start or stop) is independent
of other containers, and it does not affect or require a restart of any
underlying host operating system service.

**Portability**

Containers can be migrated to other servers without modifications to the
contained applications. The target servers may be bare metal or virtual
and located on-premises or in the cloud.

**Reusability**

The same container image can be used to run identical containers in
development, test, preproduction, and production environments. There is
no need to rebuild the image.

**Rapidity**

The container technology allows for accelerated application development,
testing, deployment, patching, and scaling. Also, there is no need for
an exhaustive testing.

**Version Control**

Container images can be version-controlled, which gives users the
flexibility in choosing the right version to run a container.

**[Container]{#part0035_split_001.html#id_600 .calibre10} Home: Bare
Metal or Virtual Machine**

A hypervisor software such as VMware ESXi, Oracle VirtualBox, Microsoft
Hyper-V, or KVM allows multiple virtual machines to run on the same bare
metal physical server. Each virtual machine runs an isolated,
independent instance of its own guest operating system. All virtual
machines run in parallel and share the resources of the underlying
hardware of the bare metal server. Each virtual machine may run multiple
applications that share the virtualized resources allocated to it. The
hypervisor runs a set of services on the bare metal server to enable
virtualization and support virtual machines, which introduces management
and operational overheads. Besides, any updates to the guest operating
system may require a reboot or result in an application failure.

Containers, in contrast, run directly on the underlying operating system
whether it be running on a bare metal server or in a virtual machine.
They share hardware and operating system resources securely among
themselves. This allows containerized applications to stay lightweight
and isolated, and run in parallel. Containers share the same Linux
kernel and require far fewer hardware resources than do virtual
machines, which contributes to their speedy start and stop. Given the
presence of an extra layer of hypervisor services, it may be more
beneficial and economical to run containers directly on non-virtualized
physical servers.

[Figure 23-1](#part0035_split_001.html#page_505){.calibre5} depicts how
applications are placed on traditional bare metal hardware, in virtual
machines, and to run as containers on bare metal servers.

::: c49
::: width_
![](images/01049.jpeg){.calibre13}
:::

**Figure 23-1 Container Home: Bare Metal or Virtual Machine**
:::

The added layer of hypervisor is shown in the middle stack. Any of the
above implementation can run multiple applications concurrently. A
decision as to which option to go with requires a careful use case
study; however, the benefits of running containers on bare metal servers
are obvious.

**[Container]{#part0035_split_001.html#id_601 .calibre10} Images and
Container Registries**

Launching a container requires a pre-packaged image to be available. A
container *image* is essentially a file that is built with all necessary
components---application binaries, library files, configuration
settings, environment variables, static data files, etc.---required by
an application to run smoothly, securely, and successfully included.
RHEL follows the *open container initiative* (OCI) to allow users to
build images based on industry standard specifications. An OCI-compliant
image can be executed and managed with OCI-compliant tools such as
*podman* (*pod manager*) and Docker. Images can be version-controlled
giving users the suppleness to use the latest or any of the previous
versions to launch their containers. A single image can be used to run
several containers at once.

Container images adhere to a standard naming convention for
identification. This is referred to as *fully qualified image name*
(FQIN). An FQIN is comprised of four components: (1) the storage
location (registry_name), (2) the owner or organization name
(user_name), (3) a unique repository name (repo_name), and (4) an
optional version (tag). The syntax of an FQIN is
*registry_name/user_name/repo_name:tag*.

Images are stored and maintained in public or private *registries*;
however, they need to be downloaded and made locally available for
consumption. There are several registries available on the Internet.
These include Red Hat Container Catalog at *registry.redhat.io* (or
*[registry.access.redhat.com](http://registry.access.redhat.com){.calibre5}*[),](http://registry.access.redhat.com){.calibre5}
Red Hat Quay at *quay.io*, and Docker Hub at
*[hub.docker.com](http://hub.docker.com.Additional){.calibre5}*[.Additional](http://hub.docker.com.Additional){.calibre5}
registries may be added as required. Private registries may require
authentication for access.

**Root vs. Rootless Containers**

Containers can be launched with the *root* user privileges. This gives
containers full access to perform administrative functions including the
ability to map privileged network ports (1024 and below). However,
launching containers with superuser rights opens a gate to potential
unauthorized access if a container is compromised due to a vulnerability
or misconfiguration.

To secure containers and the underlying operating system, the concept of
*rootless* container was instituted. Rootless containers allow normal,
unprivileged Linux users to run containers and interact with them just
like the *root* user, but without the ability to perform tasks that
require privileged access. Running containers without *root* is gaining
traction.

**[Working]{#part0035_split_001.html#id_602 .calibre10} with Images and
Containers**

To work with images and containers, a good comprehension of the
management commands and the configuration files involved is crucial. It
is also important to have the minimum required version of the necessary
software installed on the system to ensure the features you're looking
to implement are available. RHEL offers two commands---*podman* and
*skopeo*---to manage and interact with images, registries, and
containers. These tools can also be used to troubleshoot issues and
perform advanced management tasks; however, a discussion on those is
beyond the scope of this book.

**[Exercise]{#part0035_split_001.html#id_603 .calibre10} 23-1: Install
Necessary Container Support**

This exercise should be done on *server20* as *user1* with *sudo* where
required.

In this exercise, you will install the necessary software to set the
foundation for completing the exercises in the remainder of the chapter.
The standard RHEL 8.0 (and RHEL 8.2) image includes a module called
*container-tools* that consists of all the required components and
commands; however, a newer version is available in the Red Hat
Subscription Management (RHSM) service and that's what you will be
installing here to take advantage of the latest features and bug fixes.
You will use the standard *dnf* command to install the module.

1[.]{.c19}Register the system with RHSM to access the latest version of
the *container-tools* module. Use the credentials you created in
[Chapter 01](#part0013_split_000.html#page_1){.calibre5} "Local
Installation" to connect to the service. Enter your username at the
command line with the \--username option. Enter the *root* user password
first if you have invoked the *subscription-manager* command as a normal
user and then your Red Hat password.

![](images/01050.jpeg){.image2}

The system has been registered as indicated.

2[.]{.c19}Next, attach the server with the RHEL subscription using the
*attach* subcommand:

![](images/01051.jpeg){.image2}

*server20* is attached to the indicated subscription (Product Name) and
it has access to the Red Hat-maintained BaseOS and AppStream
repositories, which contain newer versions of the packages that the
corresponding repositories on the DVD image provide. The Red Hat repos
also incorporate a lot more software packages than do the DVD repos.

3[.]{.c19}Pull the metadata information for the Red Hat repositories:

![](images/01052.jpeg){.image2}

4[.]{.c19}Install the *container-tools* module:

![](images/01053.jpeg){.image2}

![](images/01054.jpeg){.image2}

See the *skopeo* and *podman* commands and their versions on the list of
installed packages above. They are now available on the system for
managing images and containers.

5[.]{.c19}Verify the module installation:

![](images/01055.jpeg){.image2}

The output confirms a successful installation (\[i\] beside the common
profile) of the *container-tools* module from RHSM.

This concludes the exercise.

**[The]{#part0035_split_001.html#id_604 .calibre10} podman Command**

Managing images and containers involves several operations such as
finding, inspecting, retrieving, and deleting images and running,
stopping, listing, and deleting containers. The *podman* command is used
for most of these operations. It supports numerous subcommands and
options. [Table 23-1](#part0035_split_001.html#id_762){.calibre5}
describes the ones that are used in this chapter.

::: c49
  -------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Subcommand**             **Description**
  **Image Management**       
  images                     Lists downloaded images from local storage
  inspect                    Examines an image and displays its details
  login/logout               Logs in/out to/from a container registry. A login may be required to access private and protected registries.
  pull                       Downloads an image to local storage from a registry
  rmi                        Removes an image from local storage
  search                     Searches for an image. The following options can be included with this subcommand:
                             1\. A partial image name in the search will produce a list of all images containing the partial name.
                             2\. The \--no-trunc option makes the command exhibit output without truncating it.
                             3\. The \--limit \<number\> option limits the displayed results to the specified number.
  tag                        Adds a name to an image. The default is 'latest' to classify the image as the latest version. Older images may have specific version identifiers.
  **Container Management**   
  attach                     Attaches to a running container
  exec                       Runs a process in a running container
  generate                   Generates a systemd unit configuration file that can be used to control the operational state of a container. The \--new option is important and is employed in later exercises.
  info                       Reveals system information, including the defined registries
  inspect                    Exhibits the configuration of a container
  ps                         Lists running containers (includes stopped containers with the -a option)
  rm                         Removes a container
  run                        Launches a new container from an image. Some options such as -d (detached), -i (interactive), and -t (terminal) are important and are employed in exercises where needed.
  start/stop/restart         Starts, stops, or restarts a container
  -------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0035_split_001.html#id_762} 23-1 Common podman
Subcommands**
:::

All the subcommands described in [Table
23-1](#part0035_split_001.html#id_762){.calibre5} are used in the
upcoming exercises. Consult the manual pages of the *podman* command for
details on the usage of these and other subcommands.

[**EXAM TIP:**]{.c56} A solid understanding of the usage of the podman
command is key to completing container tasks.

**[The]{#part0035_split_001.html#id_605 .calibre10} skopeo Command**

The *skopeo* command is utilized for interacting with local and remote
images and registries. It has numerous subcommands available; however,
you will be using only the *inspect* subcommand to examine the details
of an image stored in a remote registry. View the manual pages of
*skopeo* for details on the usage of the *inspect* and other
subcommands.

**[The]{#part0035_split_001.html#id_606 .calibre10} registries.conf
File**

The system-wide configuration file for image registries is the
*registries.conf* file and it resides in the **etc*containers*
directory. Normal Linux users may store a customized copy of this file,
if required, under the *\~/.config/containers* directory. The settings
stored in the peruser file will take precedence over those stored in the
system-wide file. This is especially useful for running rootless
containers.

This file defines searchable and blocked registries. There are three
sections---registries.search, registries.insecure, and registries.block,
as evident from the below output:

![](images/01056.jpeg){.image2}

The registries.search section lists the registries that are searched if
an FQIN is not specified at the command line. By default, there are
three registries on the list (see the above output). You will be using
*registry.redhat.io* (old name
*[registry.access.redhat.com](http://registry.access.redhat.com){.calibre5}*)
primarily and the other two if needed. If access to an additional
registry is necessary, simply add it to the list and place it according
to the preference. For instance, if you want a private registry called
*registry.private.myorg.io* to be added with the highest priority, edit
the *registries.conf* file and make the following change:

\[registries.search\]

registries = \['registry.private.myorg.io', 'registry.redhat.io',
'quay.io', 'docker.io'\]

If this private registry is the only one to be used, you can take the
rest of the registry entries out of the list. In that case, the line
entry will look like: registries = registry.private.myorg.io.

The registries.insecure section lists the registries that do not have
valid SSL/TLS certificates. Insecure registries may also be added to the
registries.search section. There are none included in the file by
default.

The regsitries.block section lists registries that must not be used.

[**EXAM TIP:**]{.c56} As there is no Internet access provided during Red
Hat exams, you may have to access a network-based registry to download
images.

The default content of the file is good for many use cases; however, you
may see additional or different entries on busy systems.

**[Viewing]{#part0035_split_001.html#id_607 .calibre10} Podman
Configuration and Version**

The *podman* command references various system runtime and configuration
files and runs certain Linux commands in the background to gather and
display information. For instance, it looks for registries and storage
data in the system-wide and peruser configuration files, pulls memory
information from the **proc*meminfo* file, executes **uname -r** to
obtain the kernel version, and so on. *podman*'s *info* subcommand shows
all this information. Here is a sample when this command is executed as
a normal user (*user1*):

![](images/01057.jpeg){.image2}

![](images/01058.jpeg){.image2}

The above output is self-explanatory.

Now, re-run the command as *root* (precede by *sudo* if running as
*user1*) and compare the values for the settings "rootless" under host
and "ConfigFile" and "ImageStore" under store. The differences lie
between where the root and rootless (normal) users store and obtain
configuration data, the number of container images they have locally
available, and so on.

Similarly, you can run the *podman* command as follows to check its
version:

![](images/01059.jpeg){.image2}

The output reveals the version (1.9.3) of the *podman* utility and this
is what you will be using to perform the forthcoming exercises.

**Image Management**

Images are stored in private or public registries and are pulled locally
for consumption. They can be searched through one or more registries and
their metadata can be examined before download. Downloaded images can be
removed when no longer needed to conserve local storage. The same pair
of commands---*podman* and *skopeo*---is employed for these operations.

**[Exercise]{#part0035_split_001.html#id_608 .calibre10} 23-2: Search,
Examine, Download, and Remove an Image**

This exercise should be done on *server20* as *user1* with *sudo* where
required.

In this exercise, you will look for an image called *mysql* in the
*quay.io* registry, examine its details, pull it to your system, confirm
the retrieval, and finally erase it from the local storage. You will use
the *podman* and *skopeo* commands as required for these operations.

1[.]{.c19}Find the *mysql* image in the specified registry (*quay.io*)
using *podman search*. You may add the \--no-trunc option to view full
output.

![](images/01060.jpeg){.image2}

There are several images containing the searched name. You will pick
app-sre/mysql for use in this exercise.

2[.]{.c19}Inspect the image without downloading it using *skopeo
inspect*. A long output will be generated. The command uses the
docker:// mechanism to access the image.

![](images/01061.jpeg){.image2}

![](images/01062.jpeg){.image2}

The output shows older versions under RepoTags, creation timestamp for
the latest version, the Docker version that was used to build this
image, and other information. It is a good practice to analyze the
metadata of an image prior to downloading and consuming it.

3[.]{.c19}Download the image by specifying the fully qualified image
name using *podman pull*:

![](images/01063.jpeg){.image2}

4[.]{.c19}List the image to confirm the retrieval using *podman images*:

![](images/01064.jpeg){.image2}

The output indicates the FQIN of the image, version (tag), image ID,
when it was created, and size.

5[.]{.c19}Display this image's details using *podman inspect*. The
command will generate a long output. You may pipe the output to the
*less* command to view one screenful of information at a time.

![](images/01065.jpeg){.image2}

6[.]{.c19}Remove the mysql image from local storage using *podman rmi*:

![](images/01066.jpeg){.image2}

The *podman* command shows the ID of the image after deletion.

7[.]{.c19}Confirm the removal using *podman images*:

![](images/01067.jpeg){.image2}

The image is no longer available in the local storage, which confirms
the removal.

This concludes the exercise.

**[Basic]{#part0035_split_001.html#id_609 .calibre10} Container
Management**

Managing containers involves common tasks such as starting, stopping,
listing, viewing information about, and deleting them. Depending on the
use case, containers can be launched in different ways. They can have a
name assigned or be nameless, have a terminal session opened for
interaction, execute an entry point command (the command specified at
the launch time) and be auto-terminated right after, and so on. Running
containers can be stopped and restarted, or discarded if no longer
needed. The *podman* command is utilized to start containers and manage
their lifecycle. This command is also employed to list stopped and
running containers, and view their details.

**Exercise 23-3: Run, Interact with, and Remove a Named Container**

This exercise should be done on *server20* as *user1* with *sudo* where
required.

In this exercise, you will run a container based on the latest version
of a *universal base image* (ubi) for RHEL 8 available in the Red Hat
Container Registry. This image provides the base operating system layer
for the deployment of containerized applications. You will assign this
container a name and run a few native Linux commands in a terminal
window interactively. You will exit out of the container and invoke a
command inside the container from *server20*. Finally, you will
reconnect to the container, exit out, and delete it to mark the
completion of the exercise.

1[.]{.c19}Delete the directory **etc*docker* (if it exists) to avoid
permission issues:

![](images/01068.jpeg){.image2}

2[.]{.c19}Launch a container using ubi8 (RHEL 8 image). Name this
container *rhel8-base-os* and open a terminal session (-t) for
interaction (-i). Use the *podman run* command.

![](images/01069.jpeg){.image2}

The above command downloaded the latest version of the specified image
automatically even though no FQIN was provided. This is because it
searched through the registries listed in the
**etc*containers/registries.conf* file and retrieved the image from
wherever it found it first (*registry.redhat.io*). It also opened a
terminal session inside the container as the *root* user to interact
with the containerized RHEL 8 OS. The container ID is reflected as the
hostname in the container's command prompt (last line in the output).
This is an auto-generated ID.

3[.]{.c19}Run a few basic commands such as *pwd*, *ls*, *cat*, and
*date* inside the container for verification:

![](images/01070.jpeg){.image2}

4[.]{.c19}Close the terminal session when done:

![](images/01071.jpeg){.image2}

5[.]{.c19}Execute a command inside the container directly from the host
using *podman exec*:

![](images/01072.jpeg){.image2}

6[.]{.c19}Reconnect to the container using *podman attach*:

![](images/01073.jpeg){.image2}

7[.]{.c19}Close the terminal session to return to the host system's
command prompt:

![](images/01074.jpeg){.image2}

8[.]{.c19}Delete the container using *podman rm*:

![](images/01075.jpeg){.image2}

Confirm the removal with **podman ps**.

This concludes the exercise.

**[Exercise]{#part0035_split_001.html#id_610 .calibre10} 23-4: Run a
Nameless Container and Auto-Remove it After Entry Point Command
Execution**

This exercise should be done on *server20* as *user1*.

In this exercise, you will launch a container based on the latest
version of a *universal base image* (ubi) for RHEL 7 available in the
Red Hat Container Registry. This image provides the base operating
system layer to deploy containerized applications. You will enter a
Linux command at the command line for execution inside the container as
an entry point command and ensure that the container is deleted right
after that.

1[.]{.c19}Start a container using ubi7 (RHEL 7 image) and run *ls* as an
entry point command. Use *podman run* with the \--rm option to remove
the container as soon as the entry point command has finished running.

![](images/01076.jpeg){.image2}

The *ls* command was executed successfully and the container was
terminated thereafter.

2[.]{.c19}Confirm the container removal with *podman ps*:

![](images/01077.jpeg){.image2}

The container no longer exists.

This concludes the exercise.

**[Advanced]{#part0035_split_001.html#id_611 .calibre10} Container
Management**

Containers run a variety of applications and databases that may need to
communicate with applications or databases running in other containers
on the same or different host system over certain network ports. Preset
environment variables may be passed when launching containers or new
variables may be set for containerized applications to consume for
proper operation. Information stored during an application execution is
lost when a container is restarted or erased. This behavior can be
overridden by making a directory on the host available inside the
container for saving data persistently. Containers may be configured to
start and stop with the transitioning of the host system via the systemd
service. These advanced tasks are also performed with the *podman*
command. Let's take a closer look.

**[Containers]{#part0035_split_001.html#id_612 .calibre10} and Port
Mapping**

Applications running in different containers often need to exchange data
for proper operation. For instance, a containerized Apache web server
may need to talk to a MySQL database instance running in a different
container. It may also need to talk to the outside world over a port
such as 80 or 8080. To support this traffic flow, appropriate port
mappings are established between the host system and each container.

[**EXAM TIP:**]{.c56} As a normal user, you cannot map a host port below
1024 to a container port.

**Exercise 23-5: Configure Port Mapping**

This exercise should be done on *server20* as *root*.

In this exercise, you will launch a container called *rhel7-port-map* in
detached mode (as a daemon) with host port 10000 mapped to port 8000
inside the container. You will use a version of the RHEL 7 image with
Apache web server software pre-installed. This image is available in the
Red Hat Container Registry. You will list the running container and
confirm the port mapping.

1[.]{.c19}Search for an Apache web server image for RHEL 7 using *podman
search*:

![](images/01078.jpeg){.image2}

The Red Hat Container Registry has an Apache web server image called
*httpd-24-rhel7* available as evident from the output.

2[.]{.c19}Log in to *registry.redhat.io* using the Red Hat credentials
to access the image:

![](images/01079.jpeg){.image2}

3[.]{.c19}Download the latest version of the Apache image using *podman
pull*:

![](images/01080.jpeg){.image2}

4[.]{.c19}Verify the download using *podman images*:

![](images/01081.jpeg){.image2}

5[.]{.c19}Launch a container named (\--name) *rhel7-port-map* in
detached mode (-d) to run the containerized Apache web server with host
port 10000 mapped to container port 8000 (-p). Use the *podman run*
command with appropriate flags.

![](images/01082.jpeg){.image2}

6[.]{.c19}Verify that the container was launched successfully using
*podman ps*:

![](images/01083.jpeg){.image2}

The container is running (up for 50 seconds and created 51 seconds ago).
The output also indicates the port mapping.

7[.]{.c19}You can also use *podman port* to view the mapping:

![](images/01084.jpeg){.image2}

Now any inbound web traffic on host port 10000 will be redirected to the
container.

This concludes the exercise.

**[Exercise]{#part0035_split_001.html#id_613 .calibre10} 23-6: Stop,
Restart, and Remove a Container**

This exercise should be done on *server20* as *root*.

This exercise is a continuation of [Exercise
23-5](#part0035_split_000.html#page_518){.calibre5} in which a container
named *rhel7-port-map* was launched.

In this exercise, you will stop the container, restart it, stop it
again, and then erase it. You will use appropriate *podman* subcommands
and verify each transition.

1[.]{.c19}Verify the current operational state of the container
*rhel7-port-map*:

![](images/01085.jpeg){.image2}

The container has been up and running for 8 minutes. It was created 8
minutes ago.

2[.]{.c19}Stop the container and confirm using the *stop* and *ps*
subcommands (the -a option with *ps* also includes the stopped
containers in the output):

![](images/01086.jpeg){.image2}

The container is in stopped (Exited) state for the past 5 seconds. It
was created 10 minutes ago.

3[.]{.c19}Start the container and confirm with the *start* and *ps*
subcommands:

![](images/01087.jpeg){.image2}

Observe the creation and running times.

4[.]{.c19}Stop the container and remove it using the *stop* and *rm*
subcommands:

![](images/01088.jpeg){.image2}

5[.]{.c19}Confirm the removal using the -a option with *podman ps* to
also include any stopped containers:

![](images/01089.jpeg){.image2}

The container no longer exists.

This concludes the exercise.

**[Containers]{#part0035_split_001.html#id_614 .calibre10} and
Environment Variables**

Many a times, it is necessary to pass a host's pre-defined environment
variable, such as PATH, to a containerized application for consumption.
Moreover, it may also be necessary at times to set new variables to
inject debugging flags or sensitive information such as passwords,
access keys, or other secrets for use inside containers. Passing host
environment variables and setting new environment variables is done at
the time of launching a container. The *podman* command allows multiple
variables to be passed or set with the -e option.

[**EXAM TIP:**]{.c56} Use the -e option with each variable that you want
to pass or set.

Refer to [Chapter 07](#part0019_split_000.html#page_151){.calibre5} "The
Bash Shell" for more information on variables, their types, and how to
define and view them.

**[Exercise]{#part0035_split_001.html#id_615 .calibre10} 23-7: Pass and
Set Environment Variables**

This exercise should be done on *server20* as *user1*.

In this exercise, you will launch a container using the latest version
of a ubi for RHEL 8 available in the Red Hat Container Registry. You
will inject the HISTSIZE environment variable and a variable called
SECRET with the value "secret123". You will name this container
*rhel8-env-vars* and have a shell terminal opened to check the variable
settings. Finally, you will remove this container.

1[.]{.c19}Launch a container with an interactive terminal session (-it)
and inject (-e) variables HISTSIZE and SECRET as directed. Use the
specified container image.

![](images/01090.jpeg){.image2}

The container is launched with a terminal opened for interaction.

2[.]{.c19}Verify both variables using the *echo* command:

![](images/01091.jpeg){.image2}

Both variables are set and show their respective values.

3[.]{.c19}Disconnect from the container using the *exit* command, and
stop and remove it using the *stop* and *rm* subcommands:

![](images/01092.jpeg){.image2}

At this point, you may want to confirm the deletion by running **podman
ps -a**.

This concludes the exercise.

**[Containers]{#part0035_split_001.html#id_616 .calibre10} and
Persistent Storage**

Containers are normally launched for a period of time to run an
application and are then stopped or deleted when their job is finished.
Any data that is produced during runtime is lost on their restart,
failure, or termination. This data may be saved for persistence on a
host directory by attaching it to a container. The containerized
application will see the attached directory just like any other local
directory and will use it to store data if it is configured to do so.
Any data that is saved on the directory will be available even after the
container is rebooted or removed. Later, this directory can be
re-attached to other containers to give them access to the stored data
or to save their own data. The source directory on the host may itself
exist on any local or remote file system.

[**EXAM TIP:**]{.c56} Proper ownership, permissions, and SELinux file
type must be set to ensure persistent storage is accessed and allows
data writes without issues.

There are a few simple steps that should be performed to configure a
directory before it can be attached to a container. These steps include
the correct ownership, permissions, and SELinux type (container_file_t).
The special SELinux file type is applied to prevent containerized
applications (especially those running in root containers) from gaining
undesired privileged access to host files and processes, or other
running containers on the host if compromised.

**[Exercise]{#part0035_split_001.html#id_617 .calibre10} 23-8: Attach
Persistent Storage and Access Data Across Containers**

This exercise should be done on *server20* as *user1* with *sudo* where
required.

In this exercise, you will set up a directory on *server20* and attach
it to a new container. You will write some data to the directory while
in the container. You will delete the container and launch another
container with the same directory attached. You will observe that the
saved data is available in the new container and is accessible. You will
remove the container to mark the completion of this exercise.

1[.]{.c19}Create a directory called */host_data*, set full permissions
on it, and confirm:

![](images/01093.jpeg){.image2}

2[.]{.c19}Launch a root container called *rhel7-persistent-data*
(\--name) in interactive mode (-it) using the latest ubi7 image. Specify
the attachment point (*/container_data*) to be used inside the container
for the host directory (*/host_data*) with the -v (volume) option. Add
:Z as shown to ensure the SELinux type container_file_t is automatically
set on the directory and files within.

![](images/01094.jpeg){.image2}

3[.]{.c19}Confirm the presence of the directory inside the container
using the *ls* command on */container_host*:

![](images/01095.jpeg){.image2}

The host directory is available as */container_data* inside the
container with the correct SELinux type.

4[.]{.c19}Create a file called *testfile* with the *echo* command under
*/container_host*:

![](images/01096.jpeg){.image2}

5[.]{.c19}Verify the file creation and the SELinux type on it:

![](images/01097.jpeg){.image2}

The file inherits the SELinux type from the parent directory.

6[.]{.c19}Exit out of the container and check the presence of the file
in the host directory:

![](images/01098.jpeg){.image2}

The output indicates the exact same attributes on the file.

7[.]{.c19}Stop and remove the container using the *stop* and *rm*
subcommands:

![](images/01099.jpeg){.image2}

8[.]{.c19}Launch a new root container called *rhel8-persistent-data*
(\--name) in interactive mode (-it) using the latest ubi8 image from any
of the defined registries. Specify the attachment point
(*/container_data2*) to be used inside the container for the host
directory (*/host_data*) with the -v (volume) option. Add :Z as shown to
ensure the SELinux type container_file_t is automatically set on the
directory and files within.

![](images/01100.jpeg){.image2}

9[.]{.c19}Confirm the presence of the directory inside the container
using the *ls* command on */container_host2*:

![](images/01101.jpeg){.image2}

The host directory is available as */container_data2* inside this new
container with the correct SELinux type. The output also confirms the
persistence of the *testfile* data that was written in the previous
container.

10[.]{.c23}Create a file called *testfile2* with the *echo* command
under */container_data2*:

![](images/01102.jpeg){.image2}

11[.]{.c23}Exit out of the container and confirm the existence of both
files in the host directory:

![](images/01103.jpeg){.image2}

12[.]{.c23}Stop and remove the container using the *stop* and *rm*
subcommands:

![](images/01104.jpeg){.image2}

13[.]{.c23}Re-check the presence of the files in the host directory:

![](images/01105.jpeg){.image2}

Both files still exist and they can be shared with other containers if
required.

This concludes the exercise.

**[Container]{#part0035_split_001.html#id_618 .calibre10} State
Management with systemd**

So far you have seen how containers are started, stopped, and deleted by
hand using the management command. In real life environments multiple
containers run on a single host and it becomes a challenging task to
change their operational state or delete them manually. In RHEL 8, these
administrative functions can be automated via the systemd service (refer
to [Chapter 12](#part0024_split_000.html#page_271){.calibre5} "System
Initialization, Message Logging, and System Tuning" for details on
systemd).

There are several steps that need to be completed to configure container
state management via systemd. These steps vary for root and rootless
container setups and include the creation of service unit files and
their storage in appropriate directory locations
(*\~/.config/systemd/user* for rootless containers and
**etc*systemd/system* for root containers). Once setup and enabled, the
containers will start and stop automatically as a systemd service with
the host state transition or manually with the *systemctl* command.

![](images/00002.jpeg){.image} The *podman* command to start and stop
containers is no longer needed if the systemd setup is in place. You may
experience issues if you continue to use *podman* for container state
transitioning.

The start and stop behavior for rootless containers differs slightly
from that of root containers. For the rootless setup, the containers are
started when the relevant user logs in to the host and stopped when that
user logs off from all their open terminal sessions; however, this
default behavior can be altered by enabling lingering for that user with
the *loginctl* command.

![](images/00002.jpeg){.image} User lingering is a feature that, if
enabled for a particular user, spawns a user manager for that user at
system startup and keeps it running in the background to support
long-running services configured for that user. The user need not log
in.

[**EXAM TIP:**]{.c56} Make sure that you use a normal user to launch
rootless containers and the root user (or sudo) to launch root
containers.

Rootless setup does not require elevated privileges of the *root* user.

**[Exercise]{#part0035_split_001.html#id_619 .calibre10} 23-9: Configure
a Root Container as a systemd Service**

This exercise should be done on *server20* as *user1* with *sudo* where
required.

In this exercise, you will create a systemd unit configuration file for
managing the state of your root containers. You will launch a new
container and use it as a template to generate a service unit file. You
will stop and remove the launched container to avoid conflicts with new
containers that will start. You will use the *systemctl* command to
verify the automatic container start, stop, and deletion.

1[.]{.c19}Launch a new container called *root-container* (\--name) in
detached mode (-d) using the latest ubi8:

![](images/01106.jpeg){.image2}

2[.]{.c19}Confirm the new container using *podman ps*. Note the
container ID.

![](images/01107.jpeg){.image2}

3[.]{.c19}Create (*generate*) a service unit file called
*root-container.service* under **etc*systemd/system* while ensuring that
the next new container that will be launched based on this configuration
file will not require the source container (\--new) to work. The *tee*
command will show the generated file content on the screen as well as
store it in the specified file.

![](images/01108.jpeg){.image2}

The unit file has the same syntax as any other systemd service
configuration file. There are three sections---Unit, Service, and
Install. (1) The unit section provides a short description of the
service, the manual page location, and the dependencies (wants and
after). (2) The service section highlights the full commands for
starting (ExecStart) and stopping (ExecStop) containers. It also
highlights the commands that will be executed before the container start
(ExecStartPre) and after the container stop (ExecStopPost). There are a
number of options and arguments with the commands to ensure a proper
transition. The restart on-failure stipulates that systemd will try to
restart the container in the event of a failure. (3) The install section
identifies the operational target the host needs to be running in before
this container service can start. See [Chapter
12](#part0024_split_000.html#page_271){.calibre5} "System
Initialization, Message Logging, and System Tuning" for details on
systemd units and targets. Also check out the manual pages for
*systemd.unit*, *systemd.target*, and *systemd.service* if interested.

4[.]{.c19}Stop and delete the source container (*root-container*) using
the *stop* and *rm* subcommands:

![](images/01109.jpeg){.image2}

Verify the removal by running **podman ps -a**.

5[.]{.c19}Update systemd to bring the new service to its control (reboot
the system if required):

![](images/01110.jpeg){.image2}

6[.]{.c19}Enable (enable) and start (\--now) the container service using
the *systemctl* command:

![](images/01111.jpeg){.image2}

7[.]{.c19}Check the running status of the new service with the
*systemctl* command:

![](images/01112.jpeg){.image2}

8[.]{.c19}Verify the launch of a new container (compare the container ID
with that of the source root container):

![](images/01113.jpeg){.image2}

9[.]{.c19}Restart the container service using the *systemctl* command:

![](images/01114.jpeg){.image2}

10[.]{.c23}Check the status of the container again. Observe the removal
of the previous container and the launch of a new container (compare
container IDs).

![](images/01115.jpeg){.image2}

Each time the *root-container* service is restarted or *server20* is
rebooted, a new container will be launched. You can verify this by
comparing their container IDs.

This concludes the exercise.

**[Exercise]{#part0035_split_001.html#id_620 .calibre10} 23-10:
Configure a Rootless Container as a systemd Service**

This exercise should be done on *server20* as *user1* with *sudo* where
required. Log in as *conuser1* as directed.

In this exercise, you will create a systemd unit configuration file for
managing the state of your rootless containers. You will launch a new
container as *conuser1* (create this user) and use it as a template to
generate a service unit file. You will stop and remove the launched
container to avoid conflicts with new containers that will start. You
will use the *systemctl* command as *conuser1* to verify the automatic
container start, stop, and deletion.

1[.]{.c19}Create a user account called *conuser1* and assign a simple
password:

![](images/01116.jpeg){.image2}

2[.]{.c19}Open a new terminal window on *server20* and log in as
*conuser1*. Create directory *\~/.config/systemd/user* to store a
service unit file:

![](images/01117.jpeg){.image2}

3[.]{.c19}Launch a new container called *rootless-container* (\--name)
in detached mode (-d) using the latest ubi8:

![](images/01118.jpeg){.image2}

4[.]{.c19}Confirm the new container using *podman ps*. Note the
container ID.

![](images/01119.jpeg){.image2}

5[.]{.c19}Create (*generate*) a service unit file called
*rootless-container.service* under *\~/.config/systemd/user* while
ensuring that the next new container that will be launched based on this
configuration file will not require the source container (\--new) to
work:

![](images/01120.jpeg){.image2}

6[.]{.c19}Display the content of the unit file:

![](images/01121.jpeg){.image2}

See [Exercise 23-9](#part0035_split_001.html#id_619){.calibre5} earlier
for an analysis of the file content.

7[.]{.c19}Stop and delete the source container *rootless-container*
using the *stop* and *rm* subcommands:

![](images/01122.jpeg){.image2}

Verify the removal by running **podman ps -a**.

8[.]{.c19}Update systemd to bring the new service to its control (reboot
the system if required). Use the \--user option with the *systemctl*
command.

![](images/01123.jpeg){.image2}

9[.]{.c19}Enable (enable) and start (\--now) the container service using
the *systemctl* command:

![](images/01124.jpeg){.image2}

10[.]{.c23}Check the running status of the new service using the
*systemctl* command:

![](images/01125.jpeg){.image2}

11[.]{.c23}Verify the launch of a new container (compare the container
ID with that of the source rootless container):

![](images/01126.jpeg){.image2}

12[.]{.c23}Enable the container service to start and stop with host
transition using the *loginctl* command (systemd login manager) and
confirm:

![](images/01127.jpeg){.image2}

13[.]{.c23}Restart the container service using the *systemctl* command:

![](images/01128.jpeg){.image2}

14[.]{.c23}Check the status of the container again. Observe the removal
of the previous container and the launch of a new container (compare
container IDs).

![](images/01129.jpeg){.image2}

Each time the *rootless-container* service is restarted or *server20* is
rebooted, a new container will be launched. You can verify this by
comparing their container IDs.

This concludes the exercise.

**[Chapter]{#part0035_split_001.html#id_621 .calibre10} Summary**

In this last chapter, we discussed the container technology that has
gained tremendous popularity and been deployed in massive numbers over
the recent years. It offers benefits that are unmatched with any
previous virtualization technology.

We analyzed the core components of the technology: images, registries,
and containers. We interacted with images located in remote registries
and local storage. We looked at a variety of ways to launch containers,
with and without a name. We examined the benefits and use cases for
mapping network ports, injecting environment variables, and making host
storage available inside containers for persistent data storage. The
last topic expounded on controlling the operational states of root and
rootless containers via systemd and ensuring that they are auto-started
and auto-stopped with the host startup and shutdown. The chapter
presented several exercises to reinforce the learning.

**[Review]{#part0035_split_001.html#id_622 .calibre10} Questions**

1[.]{.c19}How would you ensure that data stored inside a container will
not be deleted automatically when the container is restarted?

2[.]{.c19}What is the name of the primary tool that is used for
container management?

3[.]{.c19}Which option must be included with the *systemctl* command to
manage the state of a rootless container?

4[.]{.c19}Rootless containers are less secure than root containers. True
or False?

5[.]{.c19}What is one thing that you do not get with rootless
containers? Select from: security, ability to map privileged ports,
ability to pass environment variables, or can be managed via systemd.

6[.]{.c19}What is the significance of a tag in a container image?

7[.]{.c19}Which command would you use to inspect a container image
sitting in a remote registry?

8[.]{.c19}What would you run to remove all locally stored images in one
shot?

9[.]{.c19}Containers can be run on a bare metal server or in a virtual
machine. True or False?

10[.]{.c23}Which feature would you use to allow traffic flow for your
Apache web server running inside a container?

11[.]{.c23}It is mandatory to download an image prior to running a
container based off it. True or False?

12[.]{.c23}How would you connect to a container running in the
background?

13[.]{.c23}By default, any data saved inside a container is lost when
the container is restarted. True or False?

14[.]{.c23}Can a single host directory be attached to multiple
containers at the same time?

15[.]{.c23}Which of these---isolation, security, high transition time,
less overhead---is not a benefit of the container technology?

16[.]{.c23}What is the name and location of the system-wide file that
stores a list of insecure registries?

17[.]{.c23}How would you ensure that a rootless container for a specific
user is automatically started with the host startup without the need for
the user to log in?

18[.]{.c23}What would you run to remove all stopped containers?

19[.]{.c23}What is the default tag used with container images?

20[.]{.c23}The peruser systemd service configuration file is stored
under **etc*systemd/user* directory. True or False?

**Answers to Review Questions**

1[.]{.c19}Attach a host directory to the container and use it for
storing data that requires persistence.

2[.]{.c19}The primary container management tool is called *podman*.

3[.]{.c19}The \--user option is required with the *systemctl* command to
control the state of a rootless container.

4[.]{.c19}False.

5[.]{.c19}The ability to map privileged ports is not directly supported
with rootless containers.

6[.]{.c19}A tag is typically used to identify a version of the image.

7[.]{.c19}The *skopeo* command can be used to inspect an image located
in a remote registry.

8[.]{.c19}Execute *podman rmi -a* to remove all locally stored images.

9[.]{.c19}True.

10[.]{.c23}Map a host port with a container port.

11[.]{.c23}False. The specified image is automatically downloaded when
starting a container.

12[.]{.c23}Use the *podman attach* command to connect to a running
container.

13[.]{.c23}True.

14[.]{.c23}Yes, a single host directory can be attached to multiple
containers simultaneously.

15[.]{.c23}High transition time is not a container benefit.

16[.]{.c23}The file that stores insecure registry list is called
*registries.conf* and it lives in the **etc*containers* directory.

17[.]{.c23}Use the *loginctl* command as that user and enable lingering.

18[.]{.c23}Run *podman rm -a* to remove all stopped containers.

19[.]{.c23}The default tag is 'latest' that identifies the latest
version of an image.

20[.]{.c23}False. The peruser systemd unit configuration file is stored
under the user's home directory at *\~/.config/systemd/user*.

**[DIY]{#part0035_split_001.html#id_623 .calibre10} Challenge Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform these
labs without any additional help. A step-by-step guide is not provided,
as the implementation of these labs requires the knowledge that has been
presented in this chapter. Use defaults or your own thinking for missing
information.

**[Lab]{#part0035_split_001.html#id_624 .calibre10} 23-1: Prepare to
Launch Containers**

Create a new user account called *conadm* on *server10* and give them
full *sudo* rights. As *conadm*, register *server10* with RHSM using
your Red Hat credentials. Install the module *container-tools* from RHSM
and ensure that podman version is 1.9. (Hint: Chapters 05, 06, and 10).

**[Lab]{#part0035_split_001.html#id_625 .calibre10} 23-2: Launch a Named
Root Container with Port Mapping**

As *conadm* with *sudo* (where required) on *server10*, inspect the
latest version of RHEL 7 image and then download it to your computer.
Launch a container called *root-cont-port* in attached terminal mode
(-it) with host port 80 mapped to container port 8080. Run a few basic
Linux commands such as *ls*, *pwd*, *df*, *cat *etc*redhat-release*, and
*os-release* while in the container. Check to confirm the port mapping
from *server10*. (Hint: use the *skopeo* and *podman* commands).
**Note:** Do not remove the container yet.

**Lab 23-3: Launch a Nameless Rootless Container with Two Variables**

As *conadm* on *server10*, launch a container using the latest version
of ubi8 image in detached mode (-d) with two environment variables
VAR1=lab1 and VAR2=lab2 defined. Use the *exec* subcommand to check the
settings for the variables directly from *server10*. Delete the
container and the image when done. (Hint: use the *podman* command).

**[Lab]{#part0035_split_001.html#id_626 .calibre10} 23-4: Launch a Named
Rootless Container with Persistent Storage**

As *conadm* with *sudo* (where required) on *server10*, create a
directory called */host_perm1* with full permissions, and a file called
*str1* in it. Launch a container called *rootless-cont-str* in attached
terminal mode (-it) with the created directory mapped to */cont_perm1*
inside the container. While in the container, check access to the
directory and the presence of the file. Create a sub-directory and a
file under */cont_perm1* and exit out of the container shell. List
*/host_perm1* on *server10* to verify the sub-directory and the file.
Stop and delete the container. Remove */host_perm1*. (Hint: use the
*podman* command).

**[Lab]{#part0035_split_001.html#id_627 .calibre10} 23-5: Launch a Named
Rootless Container with Port Mapping, Environment Variables, and
Persistent Storage**

As *conadm* with *sudo* (where required) on *server10*, launch a named
rootless container called *rootless-cont-adv* in attached mode (-it)
with two variables (HISTSIZE=100 and MYNAME=RedHat), host port 9000
mapped to container port 8080, and */host_perm2* mounted at
*/cont_perm2*. Check and confirm the settings while inside the
container. Exit out of the container. **Note:** Do not remove the
container yet. (Hint: use the *podman* command).

**[Lab]{#part0035_split_001.html#id_628 .calibre10} 23-6: Control
Rootless Container States via systemd**

As *conadm* on *server10*, use the *rootless-cont-adv* container
launched in Lab 23-5 as a template and generate a systemd service
configuration file and store the file in the appropriate directory. Stop
and remove the source container *rootless-cont-adv*. Add the support for
the new service to systemd and enable the new service to auto-start at
system reboots. Perform the required setup to ensure the container is
launched without the need for the *conadm* user to log in. Reboot
*server10* and confirm a successful start of the container service and
the container. (Hint: use the *podman*, *systemctl*, and *loginctl*
commands).

**[Lab]{#part0035_split_001.html#id_629 .calibre10} 23-7: Control Root
Container States via systemd**

As *conadm* with *sudo* where required on *server10*, use the
*root-cont-port* container launched in Lab 23-2 as a template and
generate a systemd service configuration file and store the file in the
appropriate directory. Stop and remove the source container
*root-cont-port*. Add the support for the new service to systemd and
enable the service to auto-start at system reboots. Reboot *server10*
and confirm a successful start of the container service and the
container. (Hint: use the *podman* and *systemctl* commands).

[]{#part0036.html}




