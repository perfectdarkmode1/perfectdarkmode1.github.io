## Chapter 22 {style="text-align: right"}

\

### Containers {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Understand container technology

\

Identify key Linux features that establish the foundation to run
containers

\

Analyze container benefits

\

A better home for containers

\

Grasp the concepts of container images and registries

\

Compare pros and cons of root and rootless containers

\

Examine registry configuration file

\

Work with container images (find, inspect, pull, list, and delete)

\

Build container images using custom containerfile

\

Administer basic containers (start, list, stop, remove, interact with,
run commands from outside, attach to, run custom entry point commands,
etc.)

\

Implement advanced container features (port mapping, environment
variables, and persistent storage)

\

Control container operational states via systemd

\

#### RHCSA Objectives:

\

61\. Find and retrieve container images from a remote registry

62\. Inspect container images

63\. Perform container management using commands such as podman and
skopeo

64\. Build a container from a Containerfile

65\. Perform basic container management such as running, starting,
stopping, and listing running containers

66\. Run a service inside a container

67\. Configure a container to start automatically as a systemd service

68\. Attach persistent storage to a container

\

::: {style="page-break-before: always;"}
:::

\

Containers and containerization technologies such as Docker and
Kubernetes have received an overwhelming appreciation and massive
popularity in recent years. They are part of many new deployments.
Containers offer an improved method to package distributed applications,
deploy them in a consistent manner, and run them in isolation from one
another on the same or different virtual or physical server(s).
Containers take advantage of the native virtualization features
available in the Linux kernel. Each container typically encapsulates one
self-contained application that includes all dependencies such as
library files, configuration files, software binaries, and services.

\

::: {style="text-align: center;"}
![](image-RBOJBHPC.jpg){height="100%"}
:::

This chapter presents an overview of container images, container
registries, and containers. It shows how to interact with images and
registries. It demonstrates how to launch, manage, and interact with
containers. It discusses advanced topics such as mapping a host port
with a container port, passing and setting environment variables, and
attaching host storage for data persistence. The chapter ends with a
detailed look at controlling the operational states of containers via
the systemd service. There are numerous exercises in the chapter to
support the concepts learned.

::: {style="page-break-before: always;"}
:::

[]{#chapter0645.html}

## Introduction to Containers {.style3}

\

Traditionally, one or more applications are deployed on a single server.
These applications may have conflicting requirements in terms of shared
library files, package dependencies, and software versioning. Moreover,
patching or updating the operating system may result in breaking an
application functionality. To address these and other potential
challenges, developers perform an analysis on their current deployments
before they decide whether to collocate a new application with an
existing one or to go with a new server without taking the risk of
breaking the current operation.

\

Fortunately, there is a better choice available now in the form of
containers. Developers can now package their application alongside
dependencies, shared library files, environment variables, and other
specifics in a single image file and use that file to run the
application in a unique, isolated "environment" called container. A
container is essentially a set of processes that runs in complete
seclusion on a Linux system. A single Linux system running on bare metal
hardware or in a virtual machine may have tens or hundreds of containers
running at a time. The underlying hardware may be located either on the
ground or in the cloud.

\

Containers run on Windows as well.

\

Each container is treated as a complete whole, which can be tagged,
started, stopped, restarted, or even transported to another server
without impacting other running containers. This way any conflicts that
may exist among applications, within application components, or with the
operating system can be evaded. Applications encapsulated to run inside
containers are called containerized applications. Containerization is a
growing trend for architecting and deploying applications, application
components, and databases in real world environments.

::: {style="page-break-before: always;"}
:::

[]{#chapter0646.html}

## Containers and the Linux Features {.style3}

\

The container technology employs some of the core features available in
the Linux kernel. These features include control groups, namespaces,
seccomp (secure computing mode), and SELinux. A short description of
each of these is provided below:

\

### Control Groups {.style3}

Control groups (abbreviated as cgroups) split processes into groups to
set limits on their consumption of compute resources---CPU, memory,
disk, and network I/O. These restrictions result in controlling
individual processes from over utilizing available resources.

\

### Namespaces {.style3}

Namespaces restrict the ability of process groups from seeing or
accessing system resources---PIDs, network interfaces, mount points,
hostname, etc.---thus instituting a layer of isolation between process
groups and the rest of the system. This feature guarantees a secure,
performant, and stable environment for containerized applications as
well as the host operating system.

\

### Secure Computing Mode (seccomp) and SELinux {.style3}

These features impose security constraints thereby protecting processes
from one another and the host operating system from running processes.

\

The container technology employs these characteristics to run processes
isolated in a highly secure environment with full control over what they
can or cannot do.

::: {style="page-break-before: always;"}
:::

[]{#chapter0647.html}

## Benefits of Using Containers {.style3}

\

There are several benefits linked with using containers. These benefits
range from security to manageability and from independence to velocity.
The following provides a quick look at common containerization benefits:

\

### Isolation {.style3}

Containers are not affected due to changes in the host operating system
or in other hosted or containerized applications, as they run fully
isolated from the rest of the environment.

\

### Loose Coupling {.style3}

Containerized applications are loosely coupled with the underlying
operating system due to their self-containment and minimal level of
dependency.

\

### Maintenance Independence {.style3}

Maintenance is performed independently on individual containers.

\

### Less Overhead {.style3}

Containers require fewer system resources than do bare metal and virtual
servers.

\

### Transition Time {.style3}

Containers require a few seconds to start and stop.

\

### Transition Independence {.style3}

Transitioning from one state to another (start or stop) is independent
of other containers, and it does not affect or require a restart of any
underlying host operating system service.

\

### Portability {.style3}

Containers can be migrated to other servers without modifications to the
contained applications. The target servers may be bare metal or virtual
and located on-premises or in the cloud.

\

### Reusability {.style3}

The same container image can be used to run identical containers in
development, test, preproduction, and production environments. There is
no need to rebuild the image.

\

### Rapidity {.style3}

The container technology allows for accelerated application development,
testing, deployment, patching, and scaling. Also, there is no need for
an exhaustive testing.

\

### Version Control {.style3}

Container images can be version-controlled, which gives users the
flexibility in choosing the right version to run a container.

::: {style="page-break-before: always;"}
:::

[]{#chapter0648.html}

## Container Home: Bare Metal or Virtual Machine {.style3}

\

A hypervisor software such as VMware ESXi, Oracle VirtualBox VM Manager,
Microsoft Hyper-V, or KVM allows multiple virtual machines to run on the
same bare metal physical server. Each virtual machine runs an isolated,
independent instance of its own guest operating system. All virtual
machines run in parallel and share the resources of the underlying
hardware of the bare metal server. Each virtual machine may run multiple
applications that share the virtualized resources allocated to it. The
hypervisor runs a set of services on the bare metal server to enable
virtualization and support virtual machines, which introduces management
and operational overheads. Besides, any updates to the guest operating
system may require a reboot or result in an application failure.

\

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

\

[Figure 22-1 depicts how applications are placed on traditional bare
metal hardware, in virtual machines, and to run as containers on bare
metal servers.](#chapter0648.html)

\

::: {style="text-align: center;"}
![](image-3RXCU9W7.jpg){height="100%"}
:::

Figure 22-1 Container Home: Bare Metal or Virtual Machine

\

The added layer of hypervisor is shown in the middle stack. Any of the
above implementation can run multiple applications concurrently. A
decision as to which option to go with requires a careful use case
study; however, the benefits of running containers on bare metal servers
are obvious.

::: {style="page-break-before: always;"}
:::

[]{#chapter0649.html}

## Container Images and Container Registries {.style3}

\

Launching a container requires a pre-packaged image to be available. A
container image is essentially a static file that is built with all
necessary components---application binaries, library files,
configuration settings, environment variables, static data files,
etc.---required by an application to run smoothly, securely, and
independently. RHEL follows the open container initiative (OCI) to allow
users to build images based on industry standard specifications that
define the image format, host operating system metadata, and supported
hardware architectures. An OCI-compliant image can be executed and
managed with OCI-compliant tools such as podman (pod manager) and
Docker. Images can be version-controlled giving users the suppleness to
use the latest or any of the previous versions to launch their
containers. A single image can be used to run several containers at
once.

\

Container images adhere to a standard naming convention for
identification. This is referred to as fully qualified image name
(FQIN). An FQIN is comprised of four components: (1) the storage
location (registry_name), (2) the owner or organization name
(user_name), (3) a unique repository name (repo_name), and (4) an
optional version (tag). The syntax of an FQIN is
registry_hostname/user_name/repo_name:tag.

\

Images are stored and maintained in public or private registries;
however, they need to be downloaded and made locally available for
consumption. There are several registries available on the Internet.
These include registry.redhat.io (images based on official Red Hat
products; requires authentication), registry.access.redhat.com (requires
no authentication), registry.connect.redhat.com (images based on
third-party products), and hub.docker.com (Docker Hub). The three Red
Hat registries may be searched using the Red Hat Container Catalog at
catalog.redhat.com/software/containers/search. Additional registries may
be added as required. Private registries may also require authentication
for access.

::: {style="page-break-before: always;"}
:::

[]{#chapter0650.html}

## Rootful vs. Rootless Containers {.style3}

\

Containers can be launched with the root user privileges (sudo or
directly as the root user). This gives containers full access to perform
administrative functions including the ability to map privileged network
ports (1024 and below). However, launching containers with superuser
rights opens a gate to potential unauthorized access to the container
host if a container is compromised due to a vulnerability or
misconfiguration.

\

To secure containers and the underlying operating system, containers
should be launched and interacted with as normal Linux users. Such
containers are referred to as rootless containers. Rootless containers
allow regular, unprivileged users to run containers without the ability
to perform tasks that require privileged access.

::: {style="page-break-before: always;"}
:::

[]{#chapter0651.html}

## Working with Images and Containers {.style3}

\

To work with images and containers, a good comprehension of the
management commands and the configuration files involved is crucial. It
is also imperative to have the minimum required version of the necessary
software installed to ensure the features you're looking to implement
are available. RHEL offers two commands---podman and skopeo---to manage
and interact with images, registries, and containers. These tools can
also be used to troubleshoot issues and to perform advanced management
tasks; however, a discussion around debugging and advanced management is
beyond the scope of this book.

::: {style="page-break-before: always;"}
:::

[]{#chapter0652.html}

## Exercise 22-1: Install Necessary Container Support {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will install the necessary software to set the
foundation for completing the exercises in the remainder of the chapter.
The standard RHEL 9.1 image includes a package called container-tools
that consists of all the required components and commands. You will use
the standard dnf command to install the package.

\

1\. Install the container-tools package:

\

<div>

![](image-7S527XWZ.jpg){height="100%"}

</div>

See the skopeo and podman commands and their versions on the list of
installed packages above. They are now available on the system for
managing images and containers.

\

2\. Verify the package installation:

\

<div>

![](image-47PHPMF1.jpg){height="100%"}

</div>

The output confirms a successful installation of the container-tools
package.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0653.html}

## The podman Command {.style3}

\

Managing images and containers involves several operations such as
finding, inspecting, retrieving, and deleting images and running,
stopping, listing, and deleting containers. The podman command is used
for most of these operations. It supports numerous subcommands and
options. Table 22-1 describes the subcommands that are used in this
chapter.

\

  ----------------------------------- -----------------------------------
  Subcommand                          Description

  Image Management                    

  build                               Builds an image using instructions
                                      delineated in a Containerfile

  images                              Lists downloaded images from local
                                      storage

  inspect                             Examines an image and displays its
                                      details

  login/logout                        Logs in/out to/from a container
                                      registry. A login may be required
                                      to access private and protected
                                      registries.

  pull                                Downloads an image to local storage
                                      from a registry

  rmi                                 Removes an image from local storage

  search                              Searches for an image. The
                                      following options can be included
                                      with this subcommand:

                                      1\. A partial image name in the
                                      search will produce a list of all
                                      images containing the partial name.
                                      2. The \--no-trunc option makes the
                                      command exhibit output without
                                      truncating it. 3. The \--limit
                                      \<number\> option limits the
                                      displayed results to the specified
                                      number.

  tag                                 Adds a name to an image. The
                                      default is 'latest' to classify the
                                      image as the latest version. Older
                                      images may have specific version
                                      identifiers.

  Container Management                

  attach                              Attaches to a running container

  exec                                Runs a process in a running
                                      container

  generate                            Generates a systemd unit
                                      configuration file that can be used
                                      to control the operational state of
                                      a container. The \--new option is
                                      important and is employed in later
                                      exercises.

  info                                Reveals system information,
                                      including the defined registries

  inspect                             Exhibits the configuration of a
                                      container

  ps                                  Lists running containers (includes
                                      stopped containers with the -a
                                      option)

  rm                                  Removes a container

  run                                 Launches a new container from an
                                      image. Some options such as -d
                                      (detached), -i (interactive), and
                                      -t (terminal) are important and are
                                      employed in exercises where needed.

  start/stop/restart                  Starts, stops, or restarts a
                                      container
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 22-1 Common podman Subcommands

\

Consult the manual pages of the podman command for details on the usage
of these and other subcommands.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: A solid understanding of the usage of the podman command is
key to completing container tasks.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0654.html}

## The skopeo Command {.style3}

\

The skopeo command is utilized for interacting with local and remote
images and registries. It has numerous subcommands available; however,
you will be using only the inspect subcommand to examine the details of
an image stored in a remote registry. View the manual pages of skopeo
for details on the usage of the inspect and other subcommands.

::: {style="page-break-before: always;"}
:::

[]{#chapter0655.html}

## The registries.conf File {.style3}

\

The system-wide configuration file for image registries is the
registries.conf file and it resides in the /etc/containers directory.
Normal Linux users may store a customized copy of this file, if
required, under the \~/.config/containers directory. The settings stored
in the per-user file will take precedence over those stored in the
system-wide file. This is especially useful for running rootless
containers.

\

The registries.conf file defines searchable and blocked registries. The
below output shows the uncommented lines from the file:

\

<div>

![](image-E973K8JL.jpg){height="100%"}

</div>

The output shows three registries. The podman command searches these
registries for container images in the given order.

\

If access to an additional registry is necessary, simply add it to the
list and place it according to your preference. For instance, if you
want a private registry called registry.private.myorg.io to be added
with the highest priority, edit this file and make the following change:

\

unqualified-search-registries = \["registry.private.myorg.io",
"registry.access.redhat.com", "registry.redhat.io", "docker.io"\]

\

If this private registry is the only one to be used, you can take the
rest of the registry entries out of the list. In that case, the line
entry will look like:

\

unqualified-search-registries = \["registry.private.myorg.io"\]

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: As there is no Internet access provided during Red Hat exams,
you may have to access a network-based registry to download images.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

The default content of the file is good for many use cases; however, you
may see additional or different entries on busy systems.

::: {style="page-break-before: always;"}
:::

[]{#chapter0656.html}

## Viewing Podman Configuration and Version {.style3}

\

The podman command references various system runtime and configuration
files and runs certain Linux commands in the background to gather and
display information. For instance, it looks for registries and storage
data in the system-wide and per-user configuration files, pulls memory
information from the /proc/meminfo file, executes uname -r to obtain the
kernel version, and so on. podman's info subcommand shows all this
information. Here is a sample when this command is executed as a normal
user (user1):

\

<div>

![](image-EAOFWMO5.jpg){height="100%"}

</div>

The above output is self-explanatory.

\

Now, re-run the command as root (preceded by sudo if running as user1)
and compare the values for the settings "rootless" under host and
"ConfigFile" and "ImageStore" under store. The differences lie between
where the root and rootless (normal) users store and obtain
configuration data, the number of container images they have locally
available, and so on.

\

Similarly, you can run the podman command as follows to check its
version:

\

<div>

![](image-ZVQILNPH.jpg){height="100%"}

</div>

The output reveals the version (4.2.0) of the podman utility, and this
is what you will be using to perform the forthcoming exercises.

::: {style="page-break-before: always;"}
:::

[]{#chapter0657.html}

## Image Management {.style3}

\

Container images are available from numerous private and public
registries. They are pre-built for a variety of use cases. You can
search through registries to find the one that suits your needs. You can
examine their metadata before downloading them for consumption.
Downloaded images can be removed when no longer needed to conserve local
storage. The same pair of commands---podman and skopeo---is employed for
these operations.

::: {style="page-break-before: always;"}
:::

[]{#chapter0658.html}

## Exercise 22-2: Search, Examine, Download, and Remove an Image {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will log in to the registry.access.redhat.com
registry with the Red Hat credentials that you created in Chapter 01
"Local Installation" to download the RHEL 9.1 image. You will look for
an image called mysql-80 in the registry, examine its details, pull it
to your system, confirm the retrieval, and finally erase it from the
local storage. You will use the podman and skopeo commands as required
for these operations.

\

1\. Log in to the specified Red Hat registry:

\

<div>

![](image-7L5NV1W8.jpg){height="100%"}

</div>

2\. Confirm a successful login:

\

<div>

![](image-MMUVBVKX.jpg){height="100%"}

</div>

You should see your login name in the output.

\

3\. Find the mysql-80 image in the specified registry. Add the
\--no-trunc option to view full output.

\

<div>

![](image-YWS0BU60.jpg){height="100%"}

</div>

4\. Select the second image rhel9/mysql-80 for this exercise. Inspect
the image without downloading it using skopeo inspect. A long output
will be generated. The command uses the docker:// mechanism to access
the image.

\

<div>

![](image-WLEXSPUR.jpg){height="100%"}

</div>

The output shows older versions under RepoTags, the creation time for
the latest version, the build date of the image, a description, and
other information. It is a good practice to analyze the metadata of an
image prior to downloading and consuming it.

\

5\. Download the image by specifying the fully qualified image name
using podman pull:

\

<div>

![](image-85VEEMUM.jpg){height="100%"}

</div>

6\. List the image to confirm the retrieval using podman images:

\

<div>

![](image-6EXL0CPC.jpg){height="100%"}

</div>

The output indicates the FQIN of the image (repository), version (tag),
image ID, creation time, and size.

\

7\. Display the image's details using podman inspect. The command will
generate a long output. You may pipe the output to less to view one
screenful of information at a time.

\

<div>

![](image-K7A11DW2.jpg){height="100%"}

</div>

8\. Remove the mysql-80 image from local storage using podman rmi:

\

<div>

![](image-MOU8AU67.jpg){height="100%"}

</div>

The podman command shows the ID of the image after deletion.

\

9\. Confirm the removal using podman images:

\

<div>

![](image-OTL2HJWG.jpg){height="100%"}

</div>

The image is no longer available in the local storage, which confirms
the removal.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0659.html}

## Containerfile {.style3}

\

For specific use cases where an existing image does not fulfill a
requirement, you can build a custom image by outlining the steps you
need to be run in a file called Containerfile. The podman command can
then be used to read those instructions and executes them to produce a
new image.

\

The file name containerfile is widespread; however, in reality, you can
use any name of your liking.

\

There are several instructions, Table 22-2, that may be utilized inside
a Containerfile to perform specific functions during the build process.

\

  ----------------------------------- -----------------------------------
  Instruction                         Description

  CMD                                 Runs a command

  COPY                                Copies files to the specified
                                      location

  ENV                                 Defines environment variables to be
                                      used during the build process

  EXPOSE                              A port number that will be opened
                                      when a container is launched using
                                      this image

  FROM                                Identifies the base container image
                                      to use

  RUN                                 Executes the specified commands

  USER                                Defines a non-root user to run the
                                      commands as

  WORKDIR                             Sets the working directory. This
                                      directory is automatically created
                                      if it does not already exist.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 22-2 Common Containerfile Instructions

\

A sample container file is presented below:

\

<div>

![](image-KSBMSM9F.jpg){height="100%"}

</div>

The file contains five instructions with comments to self-explain their
purpose. The index.xhtml file may contain a basic statement such as
"This is a custom-built Apache web server container image based on RHEL
9".

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: A solid understanding of what each command instruction does
and how to use it within a containerfile is important.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0660.html}

## Exercise 22-3: Use Containerfile to Build Image {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will use a containerfile to build a custom image
based on the latest version of the RHEL 9 universal base image (ubi)
available from a Red Hat container registry. You will confirm the image
creation. You will use the podman command for these activities.

\

1\. Log in to the specified Red Hat registry:

\

<div>

![](image-DDBSKRK7.jpg){height="100%"}

</div>

2\. Confirm a successful login:

\

<div>

![](image-L21LI2S7.jpg){height="100%"}

</div>

3\. Create a file called containerfile with the following code:

\

<div>

![](image-Q0VFLFWJ.jpg){height="100%"}

</div>

4\. Create a file called testfile with some random text in it and place
it in the same directory as the containerfile.

5\. Build an image by specifying the containerfile name (-f) and an
image tag (-t) such as ubi9-simple-image. The period character at the
end represents the current directory and this is where both
containerfile and testfile are located.

\

<div>

![](image-PQOCOQSO.jpg){height="100%"}

</div>

The output indicates that podman downloaded the latest version of RHEL 9
ubi from the specified registry, ran the echo command, uploaded the
testfile to /tmp, and applied the tag to the custom image.

\

6\. Confirm image creation:

\

<div>

![](image-7T3F7NSO.jpg){height="100%"}

</div>

The output shows the downloaded image as well as the new custom image
along with their image IDs, creation time, and size. Do not remove the
custom image yet as you will be using it to launch a container in the
next section.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0661.html}

## Basic Container Management {.style3}

\

Managing containers involves common tasks such as starting, stopping,
listing, viewing information about, and deleting them. Depending on the
use case, containers can be launched in different ways. They can have a
name assigned or be nameless, have a terminal session opened for
interaction, execute an entry point command (the command specified at
the launch time) and be auto-terminated right after, and so on. Running
containers can be stopped and restarted, or discarded if no longer
needed. The podman command is utilized to start containers and manage
their lifecycle. This command is also employed to list stopped and
running containers, and view their details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0662.html}

## Exercise 22-4: Run, Interact with, and Remove a Named Container {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will run a container based on the latest version
of the RHEL 8 ubi available in the Red Hat container registry. You will
assign this container a name and run a few native Linux commands in a
terminal window interactively. You will exit out of the container to
mark the completion of the exercise.

\

1\. Launch a container using ubi8 (RHEL 8). Name this container
rhel8-base-os and open a terminal session (-t) for interaction (-i). Use
the podman run command.

\

<div>

![](image-10ROA005.jpg){height="100%"}

</div>

The above command downloaded the latest version of the specified image
automatically even though no FQIN was provided. This is because it
searched through the registries listed in the
/etc/containers/registries.conf file and retrieved the image from
wherever it found it first (registry.access.redhat.com). It also opened
a terminal session inside the container as the root user to interact
with the containerized RHEL 8 OS. The container ID is reflected as the
hostname in the container's command prompt (last line in the output).
This is an auto-generated ID.

\

If you encounter any permission issues, delete the /etc/docker directory
(if it exists) and try again.

\

2\. Run a few basic commands such as pwd, ls, cat, and date inside the
container for verification:

\

<div>

![](image-SRFIPI5K.jpg){height="100%"}

</div>

3\. Close the terminal session when done:

\

<div>

![](image-FO8IBQK2.jpg){height="100%"}

</div>

4\. Delete the container using podman rm:

\

<div>

![](image-8C2BNVUY.jpg){height="100%"}

</div>

Confirm the removal with podman ps.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0663.html}

## Exercise 22-5: Run a Nameless Container and Auto-Remove it After Entry Point Command Execution {.style3}

\

This exercise should be done on server20 as user1.

\

In this exercise, you will launch a container based on the latest
version of RHEL 7 ubi available in a Red Hat container registry. This
image provides the base operating system layer to deploy containerized
applications. You will enter a Linux command at the command line for
execution inside the container as an entry point command and the
container should be automatically deleted right after that.

\

1\. Start a container using ubi7 (RHEL 7) and run ls as an entry point
command. Use podman run with the \--rm option to remove the container as
soon as the entry point command has finished running.

\

<div>

![](image-PUT5F8WL.jpg){height="100%"}

</div>

The ls command was executed successfully, and the container was
terminated thereafter.

\

2\. Confirm the container removal with podman ps:

\

<div>

![](image-W2BP63JE.jpg){height="100%"}

</div>

The container no longer exists.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0664.html}

## Advanced Container Management {.style3}

\

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
service. These advanced tasks are also performed with the podman
command. Let's take a closer look.

::: {style="page-break-before: always;"}
:::

[]{#chapter0665.html}

## Containers and Port Mapping {.style3}

\

Applications running in different containers often need to exchange data
for proper operation. For instance, a containerized Apache web server
may need to talk to a MySQL database instance running in a different
container. It may also need to talk to the outside world over a port
such as 80 or 8080. To support this traffic flow, appropriate port
mappings are established between the host system and each container.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: As a normal user, you cannot map a host port below 1024 to a
container port.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0666.html}

## Exercise 22-6: Configure Port Mapping {.style3}

\

This exercise should be done on server20 as root.

\

In this exercise, you will launch a container called rhel7-port-map in
detached mode (as a daemon) with host port 10000 mapped to port 8000
inside the container. You will use a version of the RHEL 7 image with
Apache web server software pre-installed. This image is available from a
Red Hat container registry. You will list the running container and
confirm the port mapping.

\

1\. Search for an Apache web server image for RHEL 7 using podman
search:

\

<div>

![](image-LD9Q96RH.jpg){height="100%"}

</div>

The Red Hat Container Registry has an Apache web server image called
httpd-24-rhel7 available as evident from the output.

\

2\. Log in to registry.redhat.io using the Red Hat credentials to access
the image:

\

<div>

![](image-T8A77YJ9.jpg){height="100%"}

</div>

3\. Download the latest version of the Apache image using podman pull:

\

<div>

![](image-U4JN768V.jpg){height="100%"}

</div>

4\. Verify the download using podman images:

\

<div>

![](image-7K6QTB3O.jpg){height="100%"}

</div>

5\. Launch a container named (\--name) rhel7-port-map in detached mode
(-d) to run the containerized Apache web server with host port 10000
mapped to container port 8000 (-p). Use the podman run command with
appropriate flags.

\

<div>

![](image-6RCABII7.jpg){height="100%"}

</div>

6\. Verify that the container was launched successfully using podman ps:

\

<div>

![](image-AY6DSTAZ.jpg){height="100%"}

</div>

The container is running (up for 31 seconds and created 35 seconds ago).
The output also indicates the port mapping.

\

7\. You can also use podman port to view the mapping:

\

<div>

![](image-NT1HBUJ0.jpg){height="100%"}

</div>

Now any inbound web traffic on host port 10000 will be redirected to the
container.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0667.html}

## Exercise 22-7: Stop, Restart, and Remove a Container {.style3}

\

This exercise should be done on server20 as root.

\

This exercise is a continuation of Exercise 22-6 in which a container
named rhel7-port-map was launched.

\

In this exercise, you will stop the container, restart it, stop it
again, and then erase it. You will use appropriate podman subcommands
and verify each transition.

\

1\. Verify the current operational state of the container
rhel7-port-map:

\

<div>

![](image-GOTMCQ51.jpg){height="100%"}

</div>

The container has been up and running for 16 minutes. It was created 16
minutes ago as well.

\

2\. Stop the container and confirm using the stop and ps subcommands
(the -a option with ps also includes the stopped containers in the
output):

\

<div>

![](image-N4O5RM30.jpg){height="100%"}

</div>

The container has been in stopped (Exited) state for the past 11
seconds.

\

3\. Start the container and confirm with the start and ps subcommands:

\

<div>

![](image-2HORXORW.jpg){height="100%"}

</div>

Observe the creation and running times.

\

4\. Stop the container and remove it using the stop and rm subcommands:

\

<div>

![](image-874P9CLJ.jpg){height="100%"}

</div>

5\. Confirm the removal using the -a option with podman ps to also
include any stopped containers:

\

<div>

![](image-G3EIMFKS.jpg){height="100%"}

</div>

The container no longer exists.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0668.html}

## Containers and Environment Variables {.style3}

\

Many times it is necessary to pass a host's pre-defined environment
variable, such as PATH, to a containerized application for consumption.
Moreover, it may also be necessary at times to set new variables to
inject debugging flags or sensitive information such as passwords,
access keys, or other secrets for use inside containers. Passing host
environment variables or setting new environment variables is done at
the time of launching a container. The podman command allows multiple
variables to be passed or set with the -e option.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Use the -e option with each variable that you want to pass or
set.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Refer to Chapter 07 "The Bash Shell" for more information on variables,
their types, and how to define and view them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0669.html}

## Exercise 22-8: Pass and Set Environment Variables {.style3}

\

This exercise should be done on server20 as user1.

\

In this exercise, you will launch a container using the latest version
of a ubi for RHEL 9 available in a Red Hat container registry. You will
inject the HISTSIZE environment variable, and a variable called SECRET
with a value "secret123". You will name this container rhel9-env-vars
and have a shell terminal opened to check the variable settings.
Finally, you will remove this container.

\

1\. Launch a container with an interactive terminal session (-it) and
inject (-e) variables HISTSIZE and SECRET as directed. Use the specified
container image.

\

<div>

![](image-FWAEIG22.jpg){height="100%"}

</div>

The container is launched with a terminal opened for interaction.

\

2\. Verify both variables using the echo command:

\

<div>

![](image-ID5M2D5P.jpg){height="100%"}

</div>

Both variables are set and show their respective values.

\

3\. Disconnect from the container using the exit command, and stop and
remove it using the stop and rm subcommands:

\

<div>

![](image-MIFYAQHZ.jpg){height="100%"}

</div>

At this point, you may want to confirm the deletion by running podman ps
-a.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0670.html}

## Containers and Persistent Storage {.style3}

\

Containers are normally launched for a period of time to run an
application and then stopped or deleted when their job is finished. Any
data that is produced during runtime is lost on their restart, failure,
or termination. This data may be saved for persistence on a host
directory by attaching the host directory to a container. The
containerized application will see the attached directory just like any
other local directory and will use it to store data if it is configured
to do so. Any data that is saved on the directory will be available even
after the container is rebooted or removed. Later, this directory can be
re-attached to other containers to give them access to the stored data
or to save their own data. The source directory on the host may itself
exist on any local or remote file system.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Proper ownership, permissions, and SELinux file type must be
set to ensure persistent storage is accessed and allows data writes
without issues.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

There are a few simple steps that should be performed to configure a
host directory before it can be attached to a container. These steps
include the correct ownership, permissions, and SELinux type
(container_file_t). The special SELinux file type is applied to prevent
containerized applications (especially those running in root containers)
from gaining undesired privileged access to host files and processes, or
other running containers on the host if compromised.

::: {style="page-break-before: always;"}
:::

[]{#chapter0671.html}

## Exercise 22-9: Attach Persistent Storage and Access Data Across Containers {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will set up a directory on server20 and attach it
to a new container. You will write some data to the directory while in
the container. You will delete the container and launch another
container with the same directory attached. You will observe the
persistence of saved data in the new container and that it is
accessible. Finally, you will remove the container to mark the
completion of this exercise.

\

1\. Create a directory called /host_data, set full permissions on it,
and confirm:

\

<div>

![](image-A16DWUCR.jpg){height="100%"}

</div>

2\. Launch a root container called rhel9-persistent-data (\--name) in
interactive mode (-it) using the latest ubi9 image. Specify the
attachment point (/container_data) to be used inside the container for
the host directory (/host_data) with the -v (volume) option. Add :Z as
shown to ensure the SELinux type container_file_t is automatically set
on the directory and files within.

\

<div>

![](image-J58YZV29.jpg){height="100%"}

</div>

3\. Confirm the presence of the directory inside the container with ls
on /container_data:

\

<div>

![](image-YAZBQL1Y.jpg){height="100%"}

</div>

The host directory is available as /container_data inside the container
with the correct SELinux type.

\

4\. Create a file called testfile with the echo command under
/container_data:

\

<div>

![](image-GUR2WY2B.jpg){height="100%"}

</div>

5\. Verify the file creation and the SELinux type on it:

\

<div>

![](image-WXFVNGBI.jpg){height="100%"}

</div>

The file inherits the SELinux type from the parent directory.

\

6\. Exit out of the container and check the presence of the file in the
host directory:

\

<div>

![](image-LGGOCXKA.jpg){height="100%"}

</div>

The output indicates the exact same attributes on the file.

\

7\. Stop and remove the container using the stop and rm subcommands:

\

<div>

![](image-SJ1XC5F5.jpg){height="100%"}

</div>

8\. Launch a new root container called rhel8-persistent-data (\--name)
in interactive mode (-it) using the latest ubi8 image from any of the
defined registries. Specify the attachment point (/container_data2) to
be used inside the container for the host directory (/host_data) with
the -v (volume) option. Add :Z as shown to ensure the SELinux type
container_file_t is automatically set on the directory and files within.

\

<div>

![](image-TDQ6S8PC.jpg){height="100%"}

</div>

9\. Confirm the presence of the directory inside the container with ls
on /container_data2:

\

<div>

![](image-G3CA95LC.jpg){height="100%"}

</div>

The host directory is available as /container_data2 inside this new
container with the correct SELinux type. The output also confirms the
persistence of the testfile data that was written in the previous
container.

\

10\. Create a file called testfile2 with the echo command under
/container_data2:

\

<div>

![](image-9WEM9T51.jpg){height="100%"}

</div>

11\. Exit out of the container and confirm the existence of both files
in the host directory:

\

<div>

![](image-CPWY1M2L.jpg){height="100%"}

</div>

12\. Stop and remove the container using the stop and rm subcommands:

\

<div>

![](image-KA6BCU9P.jpg){height="100%"}

</div>

13\. Re-check the presence of the files in the host directory:

\

<div>

![](image-7QNGAUBV.jpg){height="100%"}

</div>

Both files still exist and they can be shared with other containers if
required.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0672.html}

## Container State Management with systemd {.style3}

\

So far you have seen how containers are started, stopped, and deleted by
hand using a management command. In real life environments multiple
containers run on a single host and it becomes a challenging task to
change their operational state or delete them manually. In RHEL 9, these
administrative functions can be automated via the systemd service (refer
to Chapter 12 "System Initialization, Message Logging, and System
Tuning" for details on systemd).

\

There are several steps that need to be completed to configure container
state management via systemd. These steps vary for rootful and rootless
container setups and include the creation of service unit files and
their storage in appropriate directory locations
(\~/.config/systemd/user for rootless containers and /etc/systemd/system
for rootful containers). Once setup and enabled, the containers will
start and stop automatically as a systemd service with the host state
transition or manually with the systemctl command.

\

The podman command to start and stop containers is no longer needed if
the systemd setup is in place. You may experience issues if you continue
to use podman for container state transitioning alongside.

\

The start and stop behavior for rootless containers differs slightly
from that of rootful containers. For the rootless setup, the containers
are started when the relevant user logs in to the host and stopped when
that user logs off from all their open terminal sessions; however, this
default behavior can be altered by enabling lingering for that user with
the loginctl command.

\

User lingering is a feature that, if enabled for a particular user,
spawns a user manager for that user at system startup and keeps it
running in the background to support long-running services configured
for that user. The user need not log in.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Make sure that you use a normal user to launch rootless
containers and the root user (or sudo) for rootful containers.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Rootless setup does not require elevated privileges of the root user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0673.html}

## Exercise 22-10: Configure a Rootful Container as a systemd Service {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will create a systemd unit configuration file for
managing the state of your rootful containers. You will launch a new
container and use it as a template to generate a service unit file. You
will stop and remove the launched container to avoid conflicts with new
containers that will start. You will use the systemctl command to verify
the automatic container start, stop, and deletion.

\

1\. Launch a new container called rootful-container (\--name) in
detached mode (-d) using the latest ubi9:

\

<div>

![](image-GBB88YS2.jpg){height="100%"}

</div>

2\. Confirm the new container using podman ps. Note the container ID.

\

<div>

![](image-MB7DJ9P4.jpg){height="100%"}

</div>

3\. Create (generate) a service unit file called
rootful-container.service under /etc/systemd/system while ensuring that
the next new container that will be launched based on this configuration
file will not require the source container (\--new) to work. The tee
command will show the generated file content on the screen as well as
store it in the specified file.

\

<div>

![](image-WPSNM6IW.jpg){height="100%"}

</div>

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
this container service can start. See Chapter 12 "System Initialization,
Message Logging, and System Tuning" for details on systemd units and
targets. Also check out the manual pages for systemd.unit,
systemd.target, and systemd.service for additional details.

\

4\. Stop and delete the source container (rootful-container) using the
stop and rm subcommands:

\

<div>

![](image-JYMYFBQG.jpg){height="100%"}

</div>

Verify the removal by running sudo podman ps -a.

\

5\. Update systemd to bring the new service under its control (reboot
the system if required):

\

<div>

![](image-F2PU9TRV.jpg){height="100%"}

</div>

6\. Enable (enable) and start (\--now) the container service using the
systemctl command:

\

<div>

![](image-QZCAXYM0.jpg){height="100%"}

</div>

7\. Check the running status of the new service with the systemctl
command:

\

<div>

![](image-RQQFVKL4.jpg){height="100%"}

</div>

8\. Verify the launch of a new container (compare the container ID with
that of the source root container):

\

<div>

![](image-0YT1Z6EP.jpg){height="100%"}

</div>

9\. Restart the container service using the systemctl command:

\

<div>

![](image-EQQS0107.jpg){height="100%"}

</div>

10\. Check the status of the container again. Observe the removal of the
previous container and the launch of a new container (compare container
IDs).

\

<div>

![](image-2CEM44G5.jpg){height="100%"}

</div>

Each time the rootful-container service is restarted or server20 is
rebooted, a new container will be launched. You can verify this by
comparing their container IDs.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0674.html}

## Exercise 22-11: Configure Rootless Container as a systemd Service {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required. Log in as conuser1 as directed.

\

In this exercise, you will create a systemd unit configuration file for
managing the state of your rootless containers. You will launch a new
container as conuser1 (create this user) and use it as a template to
generate a service unit file. You will stop and remove the launched
container to avoid conflicts with new containers that will start. You
will use the systemctl command as conuser1 to verify the automatic
container start, stop, and deletion.

\

1\. Create a user account called conuser1 and assign a simple password:

\

<div>

![](image-I0KM4A0W.jpg){height="100%"}

</div>

2\. Open a new terminal window on server20 and log in as conuser1.
Create directory \~/.config/systemd/user to store a service unit file:

\

<div>

![](image-AKFXDJT5.jpg){height="100%"}

</div>

3\. Launch a new container called rootless-container (\--name) in
detached mode (-d) using the latest ubi8:

\

<div>

![](image-9UWNQON2.jpg){height="100%"}

</div>

4\. Confirm the new container using podman ps. Note the container ID.

\

<div>

![](image-A3DCN57T.jpg){height="100%"}

</div>

5\. Create (generate) a service unit file called
rootless-container.service under \~/.config/systemd/user while ensuring
that the next new container that will be launched based on this
configuration will not require the source container (\--new) to work:

\

<div>

![](image-TOURUXBC.jpg){height="100%"}

</div>

6\. Display the content of the unit file:

\

<div>

![](image-OQQEHAMZ.jpg){height="100%"}

</div>

See Exercise 22-10 earlier for an analysis of the file content.

\

7\. Stop and delete the source container rootless-container using the
stop and rm subcommands:

\

<div>

![](image-X1URDZQJ.jpg){height="100%"}

</div>

Verify the removal by running podman ps -a.

\

8\. Update systemd to bring the new service to its control (reboot the
system if required). Use the \--user option with the systemctl command.

\

<div>

![](image-VWPJEHDC.jpg){height="100%"}

</div>

9\. Enable (enable) and start (\--now) the container service using the
systemctl command:

\

<div>

![](image-JA1NY1QC.jpg){height="100%"}

</div>

10\. Check the running status of the new service using the systemctl
command:

\

<div>

![](image-Q0H3HJ85.jpg){height="100%"}

</div>

11\. Verify the launch of a new container (compare the container ID with
that of the source rootless container):

\

<div>

![](image-I0VC7EFD.jpg){height="100%"}

</div>

12\. Enable the container service to start and stop with host transition
using the loginctl command (systemd login manager) and confirm:

\

<div>

![](image-198PLBRS.jpg){height="100%"}

</div>

13\. Restart the container service using the systemctl command:

\

<div>

![](image-Q63AQ3T5.jpg){height="100%"}

</div>

14\. Check the status of the container again. Observe the removal of the
previous container and the launch of a new container (compare container
IDs).

\

<div>

![](image-CSY20YV2.jpg){height="100%"}

</div>

Each time the rootless-container service is restarted or server20 is
rebooted, a new container will be launched. You can verify this by
comparing their container IDs.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0675.html}

## Chapter Summary {.style3}

\

In this last chapter, we discussed the container technology that has
gained tremendous popularity and been deployed in massive numbers
lately. It offers benefits that are unmatched with any previous
virtualization technology.

\

We analyzed the core components of the technology: images, registries,
and containers. We interacted with images located in remote registries
and local storage. We built a custom container image using a file that
consisted of instructions. We looked at a variety of ways to launch
containers, with and without a name. We examined the benefits and use
cases for mapping network ports, injecting environment variables, and
making host storage available inside containers for persistent data
storage. The last topic expounded on controlling the operational states
of rootful and rootless containers via systemd and ensuring that they
are auto-started and auto-stopped with the host startup and shutdown.
The chapter presented several exercises to reinforce the learning.

::: {style="page-break-before: always;"}
:::

[]{#chapter0676.html}

## Review Questions {.style3}

\

1\. Rootless containers are less secure than rootful containers. True or
False?

2\. Which of these---isolation, security, high transition time, less
overhead---is not a benefit of the container technology?

3\. What is the name and location of the system-wide file that stores a
list of insecure registries?

4\. What is one thing that you do not get with rootless containers?
Select from: security, ability to map privileged ports, ability to pass
environment variables, or can be managed via systemd.

5\. What is the significance of a tag in a container image?

6\. Which command would you use to inspect a container image sitting in
a remote registry?

7\. What would you run to remove all locally stored images in one shot?

8\. What is the default tag used with container images?

9\. The per-user systemd service configuration file is stored under
/etc/systemd/user directory. True or False?

10\. Containers can be run on a bare metal server or in a virtual
machine. True or False?

11\. Which feature would you use to allow traffic flow for your Apache
web server running inside a container?

12\. How would you ensure that data stored inside a container will not
be deleted automatically when the container is restarted?

13\. What is the name of the primary tool that is used for container
management?

14\. Which option must be included with the systemctl command to manage
the state of a rootless container?

15\. It is mandatory to download an image prior to running a container
based off it. True or False?

16\. How would you connect to a container running in the background?

17\. By default, any data saved inside a container is lost when the
container is restarted. True or False?

18\. What is the typical name of the file that furnishes instructions to
build custom images?

19\. Can a single host directory be attached to multiple containers at
the same time?

20\. How would you ensure that a rootless container for a specific user
is automatically started with the host startup without the need for the
user to log in?

21\. What would you run to remove all stopped containers?

::: {style="page-break-before: always;"}
:::

[]{#chapter0677.html}

## Answers to Review Questions {.style3}

\

1\. False.

2\. High transition time is not a container benefit.

3\. The file that stores insecure registry list is called
registries.conf and it lives in the /etc/containers directory.

4\. The ability to map privileged ports is not directly supported with
ootless containers.

5\. A tag is typically used to identify a version of the image.

6\. The skopeo command can be used to inspect an image located in a
remote registry.

7\. Execute podman rmi -a to remove all locally stored images.

8\. The default tag is 'latest' that identifies the latest version of an
image.

9\. False. The per-user systemd unit configuration file is stored under
the user's home directory at \~/.config/systemd/user.

10\. True.

11\. Map a host port with a container port.

12\. Attach a host directory to the container and use it for storing
data that requires persistence.

13\. The primary container management tool is called podman.

14\. The \--user option is required with the systemctl command to
control the state of a rootless container.

15\. False. The specified image is automatically downloaded when
starting a container.

16\. Use the podman attach command to connect to a running container.

17\. True.

18\. Containerfile is the typical name; however, you can use any name
that you want.

19\. Yes, a single host directory can be attached to multiple containers
simultaneously.

20\. Use the loginctl command as that user and enable lingering.

21\. Run podman rm -a to remove all stopped containers.

::: {style="page-break-before: always;"}
:::

[]{#chapter0678.html}

## DIY Challenge Labs {.style3}

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

[]{#chapter0679.html}

## Lab 22-1: Launch Named Root Container with Port Mapping {.style3}

\

Create a new user account called conadm on server30 and give them full
sudo rights. As conadm with sudo (where required) on server30, inspect
the latest version of ubi9 and then download it to your computer. Launch
a container called rootful-cont-port in attached terminal mode (-it)
with host port 80 mapped to container port 8080. Run a few basic Linux
commands such as ls, pwd, df, cat /etc/redhat-release, and os-release
while in the container. Check to confirm the port mapping from server30.
(Hint: use the skopeo and podman commands). Note: Do not remove the
container yet.

::: {style="page-break-before: always;"}
:::

[]{#chapter0680.html}

## Lab 22-2: Launch Nameless Rootless Container with Two Variables {.style3}

\

As conadm on server30, launch a container using the latest version of
ubi8 in detached mode (-d) with two environment variables VAR1=lab1 and
VAR2=lab2 defined. Use the exec subcommand to check the settings for the
variables directly from server30. Delete the container and the image
when done. (Hint: use the podman command).

::: {style="page-break-before: always;"}
:::

[]{#chapter0681.html}

## Lab 22-3: Launch Named Rootless Container with Persistent Storage {.style3}

\

As conadm with sudo (where required) on server30, create a directory
called /host_perm1 with full permissions, and a file called str1 in it.
Launch a container called rootless-cont-str in attached terminal mode
(-it) with the created directory mapped to /cont_perm1 inside the
container. While in the container, check access to the directory and the
presence of the file. Create a sub-directory and a file under
/cont_perm1 and exit out of the container shell. List /host_perm1 on
server30 to verify the sub-directory and the file. Stop and delete the
container. Remove /host_perm1. (Hint: use the podman command).

::: {style="page-break-before: always;"}
:::

[]{#chapter0682.html}

Lab 22-4: Launch Named Rootless Container with Port Mapping, Environment
Variables, and Persistent Storage

\

As conadm with sudo (where required) on server30, launch a named
rootless container called rootless-cont-adv in attached mode (-it) with
two variables (HISTSIZE=100 and MYNAME=RedHat), host port 9000 mapped to
container port 8080, and /host_perm2 mounted at /cont_perm2. Check and
confirm the settings while inside the container. Exit out of the
container. Note: Do not remove the container yet. (Hint: use the podman
command).

::: {style="page-break-before: always;"}
:::

[]{#chapter0683.html}

## Lab 22-5: Control Rootless Container States via systemd {.style3}

\

As conadm on server30, use the rootless-cont-adv container launched in
Lab 22-4 as a template and generate a systemd service configuration file
and store the file in the appropriate directory. Stop and remove the
source container rootless-cont-adv. Add the support for the new service
to systemd and enable the new service to auto-start at system reboots.
Perform the required setup to ensure the container is launched without
the need for the conadm user to log in. Reboot server30 and confirm a
successful start of the container service and the container. (Hint: use
the podman, systemctl, and loginctl commands).

::: {style="page-break-before: always;"}
:::

[]{#chapter0684.html}

## Lab 22-6: Control Rootful Container States via systemd {.style3}

\

As conadm with sudo where required on server10, use the
rootful-cont-port container launched in Lab 22-1 as a template and
generate a systemd service configuration file and store the file in the
appropriate directory. Stop and remove the source container
rootful-cont-port. Add the support for the new service to systemd and
enable the service to auto-start at system reboots. Reboot server10 and
confirm a successful start of the container service and the container.
(Hint: use the podman and systemctl commands).

::: {style="page-break-before: always;"}
:::

[]{#chapter0685.html}

## Lab 22-7: Build Custom Image Using Containerfile {.style3}

\

As conadm on server10, write a containerfile to use the latest version
of ubi8 and create a user account called user-in-container in the
resultant custom image. Test the image by launching a container in
interactive mode and verifying the user. (Hint: use the podman command).

::: {style="page-break-before: always;"}
:::

[]{#chapter0686.html}
