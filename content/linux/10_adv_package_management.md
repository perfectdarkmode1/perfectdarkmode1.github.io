  
Describe package groups
Understand application streams and modules
Software repositories and how to access them
Review module streams and module profiles
Perform software management operations using dnf
List, install, update, and delete individual packages, package groups, and modules
Show package information, determine provider, and search metadata
Exhibit package group and module information
Install module from alternative stream

RHCSA Objectives:

44.Install and update software packages from Red Hat Network, a remote repository, or from the local file system 
45.Work with package module streams

dnf command (the yum command
- performs automatic dependency checks and marks any identified extra packages for installation

## Package Groups
### package group
- Collection of correlated packages designed to serve a common purpose. 
- Provides the convenience of querying, installing, and deleting as a single unit rather than dealing with packages individually.
- Two types of package groups: _environment groups_ and _package groups_. 
	- environment groups available in RHEL 8 are server, server with GUI, minimal install, workstation, virtualization host, and custom operating system. 
	- Listed on the software selection window during RHEL 8 installation. 
	- Package groups include container management, smart card support, security tools, system tools, network servers, _etc._

## Application Streams and Modules

_Application Streams_ is a 
- new concept introduced in RHEL 8. It 
- employs a modular approach to organize multiple versions of a software application alongside its dependencies to be available for installation from a single repository. A _module_ can be thought of as a logical set of application packages that includes everything required to install it, including the executables, libraries, documentation, tools, and utilities as well as dependent components. Modularity gives the flexibility to choose the version of software based on need.

* In older RHEL releases, each version of a package would have to come from a separate repository. (This has changed in RHEL 8.)
* Now modules of a single application with different versions can be stored and made available for installation from a common repository. 
* The package management tool has also been enhanced to manipulate modules.

- RHEL 8 is shipped with two core repositories called _BaseOS_ and _Application Stream_ (AppStream).

BaseOS repository
- includes the core set of RHEL 8 components
- kernel, modules, bootloader, and other foundational
software packages.
- lays the foundation to install and run software applications and programs. 
- BaseOS repository components are
available in the traditional rpm format.

AppStream repository
- comes standard with core applications,
- as well as several add-on applications
- many of them in the traditional rpm format and
- some in the new modular format. These 
- add-ons include web server software, development languages, database software, *etc.* 

Benefits of Segregation

Benefits to a segregation of the BaseOS components from other applications:

(1)  separates application components from the core operating system elements.  
(2) allows publishers to deliver and administrators to apply application updates more frequently. 

In previous RHEL versions, an OS update would update
all installed components including the kernel, service, and application
components to the latest versions by default. 

This could result in an unstable system or a misbehaving application due to an unwanted upgrade
of one or more packages. 

By detaching the base OS components from the applications, either of the two can be updated independent of the other.

This provides enhanced flexibility in tailoring the system components
and application workloads without impacting the underlying stability of
the system.

### Module Streams

- collection of packages organized by version. 
- Each module can have multiple streams, and 
- each stream receives updates independent of the other streams. A 
- stream can be enabled or disabled.
enabled stream
- allows the packages it contains to be queried or
installed.
- Only one stream of a specific module can be enabled at a
time.
- Each module has a default stream, which provides the latest or the
recommended version.i

### Module Profiles

- a list of recommended packages organized for purpose-built, convenient deployments to support a variety of use cases
such as
- minimal, development, common, client, server, *etc.* 
- A profile may also include packages from the BaseOS repository or the dependencies
of the stream. Each module stream can have zero, one, or more profiles
associated with it with only one of them marked as the *default*.

### dnf yum Repository

A *dnf repository* (*yum repository* or a *repo*) is a 
- digital library for storing software packages. A 
- repository is accessed for package retrieval, query, update, and installation, and it 
- The two repositories---
	- BaseOS and AppStream---
		- come preconfigured with the RHEL 8 ISO image. There are a 
		- number of other repositories available on the Internet that are maintained by software publishers
such as Red Hat and CentOS. 
- can build private custom repositories for internal IT use for stocking and delivering software.
- may prove to be a good practice for an organization with a large Linux server base, as it manages dependencies automatically and aids in maintaining software consistency across the board. T
- can also be used to store in-house developed packages.

- It is important to obtain software packages from authentic and reliable
sources such as Red Hat to prevent potential damage to your system and
to circumvent possible software corruption.

- There is a process to create repositories and to access preconfigured repositories. 
- there are two pre-set repositories available on the RHEL 8 image. You will configure access to them via a definition file to support the exercises and lab environment.

Sample repo definition file and key directives:

```
[BaseOS_RHEL_8]
name= RHEL 8 base operating system components
baseurl=file://*mnt*BaseOS
enabled=1
gpgcheck=0
```


**EXAM TIP:** 
- Knowing how to configure a dnf/yum repository using a URL plays an important role in completing some of the RHCSA exam tasks successfully. 
- Use two forward slash characters (//) with the baseurl directive for an FTP, HTTP, or HTTPS source.

Five lines from a sample repo file:
Line 1 defines an exclusive ID within the square brackets. 
Line 2 is a brief description of the repo with the "name" directive. 
Line 3 is the location of the repodata directory with the "baseurl" directive. 
Line 4 shows whether this repository is active. 
Line 5 shows if packages are to be GPGchecked for authenticity.

- Each repository definition file must have:
	- a unique ID, 
	- a description, and 
	- a baseurl directive defined 
	- other directives are set as required. 
	
- The baseurl directive for a local directory path is defined as file:///local_path (
	- the first two forward slash characters represent the URL convention, and the third forward slash is for the absolute path to the destination directory), and 
	- FTP and HTTP(S) sources as ftp://hostname/network_path and http(s)://hostname/network_path, respectively.
		- network path must include a resolvable hostname or an IP address.

### Software Management with dnf

- RH and Centos offer tools to work with individual packages as well as package groups and modules. 
- *rpm* command is limited to managing one package at a time.
- has an associated configuration file that can define settings to control its behavior.

#### dnf Configuration File

- key configuration file: /etc/dnf/dnf.conf
- "main" section
		- sets directives that have a global effect on dnf operations. You 
- can define separate sections for each custom repository that you plan to set up on the
system.
- preferred location to store configuration for each custom repository in their own definition files is in /etc/yum.repos.d
	- default location created for this purpose.
	
Default content of this configuration file:
```
cat /etc/dnf/dnf.conf

[main]
gpgcheck=1
installonly_limit=3
clean_requirements_on_remove=True
best=True
skip_if_unavailable=False
```

The above and a few other directives that you may define in the file:
Directive Settings in dnf.conf File:

| Directive                    | Description                                                                                                         |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| best                         | Whether to install (or upgrade to) the latest available version.                                                    |
| clean_requirements_on_remove | Whether to remove dependencies during a package removal process that are no longer in use.                          |
| debuglevel                   | Sets debug from 1 (minimum) and 10 (maximum). Default is 2. A value of 0 disables this feature.                     |
| gpgcheck                     | Whether to check the GPG signature for package authenticity. Default is 1 (enabled).                                |
| installonly_limit            | Count of packages that can be installed concurrently. Default is 3.                                                 |
| keepcache                    | Defines whether to store the package and header cache following a successful installation. Default is 0 (disabled). |
| logdir                       | Sets the directory location to store the log files. Default is **var*log.*                                          |
| obsoletes                    | Checks and removes any obsolete dependent packages during installs and updates. Default is 1 (enabled).             |
  ------------------------------ ------------------------------------------------------------------------------------------------------------------------------------------------------------


For other directives: `man 5 dnf.conf`

## The dnf Command

- introduced in RHEL 8 
- can use interchangeably with yum in RHEL
	 - yum is a soft link to the *dnf* utility. 
- requires the system to have access to either:
	- a local or remote software repository
	- a local installable package file. 

Subscription Management* (RHSM) service 
- available in the Red Hat Customer Portal 
- offers access to official Red Hat software repositories.

- Other web-based repositories that host packages are available 
- You can also set up a local, custom repository on your system and add packages of your choice to it.

Promary benefit of using *dnf* over *rpm*: 
- Resolve dependencies automatically 
	- by identifying and installing any additional required packages 
-  With multiple repositories set up, *dnf* extracts the software from wherever it finds it.

- Perform abundant software administration tasks. 
- Invokes the *rpm* utility in the background. *dnf* 
- can perform a number of operations on individual packages, package groups, and modules:
	- listing
	- querying
	- installing
	- removing them
	- enabling and disabling specific module streams.

Software handling tasks that dnf can perform on packages: 
- (clean and repolist) that are specific to repositories. 
- Refer to the manual pages of *dnf* for additional subcommands, operators, options, examples, and other details.

| **Subcommand** | **Description**                                                      |
| -------------- | -------------------------------------------------------------------- |
| check-update   | Checks if updates are available for installed packages               |
| clean          | Removes cached data                                                  |
| history        | Display previous dnf activities as recorded in /var/lib/dnf/history/ |
| info           | Show details for a package                                           |
| install        | Install or update a package                                          |
| list           | List installed and available packages                                |
| provides       | Search for packages that contain the specified file or feature       |
| reinstall      | Reinstall the exact version of an installed package                  |
| remove         | Remove a package and its dependencies                                |
| repolist       | List enabled repositories                                            |
| repoquery      | Runs queries on available packages                                   |
| search         | Searches package metadata for the specified string                   |
| upgrade        | Updates each installed package to the latest version                 |

dnf subcommands that are intended for operations on package
groups and modules:

| **Subcommand** | **Description**                                                         |
| -------------- | ----------------------------------------------------------------------- |
| group install  | Install or updates a package group                                      |
| group info     | Return details for a package group                                      |
| group list     | List available package groups                                           |
| group remove   | Remove a package group                                                  |
| module disable | Disable a module along with all the streams it contains                 |
| module enable  | Enable a module along with all the streams it contains                  |
| module install | Install a module profile including its packages                         |
| module info    | Show details for a module                                               |
| module list    | Lists all available module streams along with their profiles and status |
| module remove  | Removes a module profile including its packages                         |
| module reset   | Resets a module so that it is neither in enable nor in disable state    |
| module update  | Updates packages in a module profile                                    |

For labs, you'll need to create a definition file and configure access to the two repositories available on the RHEL 8 ISO
image.

### Lab: Configure Access to Pre-Built Repositories

Set up access to the two dnf repositories that are available on RHEL 8 image. (You should have already configured an
automatic mounting of RHEL 8 image on */mnt*.) Create a definition file for the repositories and
confirm.

1. Verify that the image is currently mounted:

`df -h | grep mnt`

2. Create a definition file called local.repo in /etc/yum.repos.d/ using the *vim* editor and define the
following data for both repositories in it:

```
[BaseOS] 
name=BaseOS 
baseurl=file:///mnt/BaseOS 
gpgcheck=0 

[AppStrean] 
name=AppStream 
baseurl=file:///mnt/AppStream 
gpgcheck=0
```

3. Confirm access to the repositories:

`sudo dnf repolist`

- Ignore lines 1-4 in the output that are related to subscription and
system registration. 
- Lines 5 and 6 show the rate at which the command read the repo data. 
- Line 7 displays the timestamp of the last metadata check.
- last two lines show the repo IDs, repo names, and a count of packages they hold.
- AppStream repo consists of 4,672 packages
- BaseOS repo contains 1,658 packages. 
- Both repos are enabled by default and are ready for use.

## individual packages, package groups, and modules:

### Individual Package Management

List, install, query, and remove packages.

#### Listing Available and Installed Packages

 - dnf lists available packages as well as installed packages.
### Lab: list all packages available for installation from all enabled repos,

`sudo dnf repoquery`

### Lab: list of packages that are available only from a specific repo:

`sudo dnf repoquery --repo "BaseOS"`
### Lab: grep for an expression to narrow down your search. 
For example, to find whether the BaseOS repo includes the *zsh* package.

`sudo dnf repoquery --repo BaseOS | grep zsh`
### Lab: list all installed packages on the system:

`sudo dnf list installed`

Three columns: 
	- package name
	- package version
	- repo it was installed from. 
	- \@anaconda means the package was installed at the time of RHEL installation.

List all installed packages and all packages available for installation from all enabled repositories:

`sudo dnf list`

- @ sign identifies the package as installed.

List all packages available from all enabled repositories that should be able to update:

`sudo dnf list updates`

List whether a package (*bc*, for instance) is installed or available for installation from any enabled repository:

`sudo dnf list bc`

List all installed packages whose names begin with the string "gnome" followed by any number of characters:

`sudo dnf list installed gnome`

List recently added packages:

`suod dnf list recent`

Refer to the *repoquery* and *list* subsections of the *dnf* command
manual pages for more options and examples.

### Installing and Updating Packages

Installing a package:
- creates the necessary directory 
- installs the required files
- runs any post-installation steps. 
- If already installed, *dnf* command updates it to the latest available version.

Attempt to install a package called *ypbind*, proceed to update if it detects the presence of an older version:

`sudo dnf install ypbind`

Install or update a package called *dcraw* located locally at /mnt/AppStream/Packages/

`sudo dnf localinstall /mnt/AppStream/Packages/dcraw*`

Update an installed package (*autofs*, for example) to the latest available version. Dnf will fail if the specified package is not already installed:

`sudo dnf update autofs`

Update all installed packages to the latest available versions:

`sudo dnf -y update`

Refer to the *install* and *update* subsections of the *dnf* command manual pages for more options and examples.

### Exhibiting Package Information

Show:
- name
- architecture it is built for
- version
- release
- size
- whether it is installed or available for installation
- repo name it was installed or is available from
- short and long descriptions
- license
- so on

dnf info subcommand

View information about a package called *autofs*:

`dnf info autofs`

- Determines whether the specified package is installed or
not.

Refer to the *info* subsection of the *dnf* command manual pages.

### Removing Packages

Removing a package:
- uninstalls it and removes all associated files and directory structure. 
- erases any dependencies as part of the deletion process. 

Remove a package called *ypbind*:

`sudo dnf remove ypbind`

Output 
- resolved dependencies
- list of the packages that it would remove. 
- disk space that their removal would free up. 
- After confirmation, it erased the identified packages and verified their removal. 
- list of the removed packages

Refer to the *remove* subsection of the *dnf* command manual pages for more options and examples available for removing packages.

### Lab: Manipulate Individual Packages

Perform management operations on a package
called *cifs-utils*. Determine if this package is already installed and if it is available for installation. Display its information before installing it. Install the package and exhibit its information. Erase the package along with
its dependencies and confirm the removal.

1. Check whether the *cifs-utils* package is already installed:

`dnf list installed | grep cifs-utils`

2. Determine if the *cifs-utils* package is available for installation:
`dnf repoquery cifs-utils`

3. Display detailed information about the package:
`dnf info cifs-utils`

4. Install the package:
`dnf install -y cifs-utils`

5. Display the package information again:
`dnf info cifs-utils`

6. Remove the package:
` dnf remove -y cifs-utils`

7. Confirm the removal:
`dnf list installed | grep cif`

### Determining Provider and Searching Package Metadata

- You can determine what package a specific file belongs to or which package comprises a certain string.

Search for packages that contain a specific file such as /etc/passwd/, use the *provides* or the *whatprovides* subcommand with dnf:
`dnf provides /etc/passwd`

- indicates file is part of a package called *setup*, installed during RHEL installation
- second instance, setup package is part of the BaseOS repository.

- can also use a wildcard character for filename expansion.

List all packages that contain filenames beginning with "system-config" followed by any number of characters:
`dnf whatprovides /usr/bin system-config*`

To search for all the packages that match the specified string in their
name or summary:
`dnf search system-config`

## Package Group Management

- group subcommand 
- list, install, query, and remove groups of packages.

### Listing Available and Installed Package Groups

group list subcommand:
- list the package groups available for installation from either or both repos
- list the package groups that are already installed on the system.

List all available and installed package groups from all repositories:
`dnf group list`

output:
- two categories of package groups: an 
	- environment group
	- group. An 
	- 
environment group
- larger collection of RHEL packages that provides all necessary software to build the
operating system foundation for a desired purpose.

group
- small bunch of RHEL packages that serve a common purpose. 
- saves time on the deployment of individual and dependent packages. 
- output shows installed and available package groups.

Display the number of installed and available package groups:
`sudo dnf group summary`

List all installed and available package groups including those that
are hidden:
`sudo dnf group list hidden`

Try *group list* with \--installed and \--available options to narrow
down the output list.
```
sudo dnf group list --installed
sudo dnf group list --available
```

List all packages that a specific package group such as Base contains:
`sudo dnf group info Base`

-v option with the group info subcommand for more
information. 

Review group list and group info subsections of the *dnf* man pages.

### Installing and Updating Package Groups

- creates the necessary directory structure for all the packages included in the group and all dependent packages
- installs the required files
- runs any post-installation steps.
- attempts to update all the packages included in the group to the latest available versions. 

Install a package group called Emacs. Update if it detects the presence of
an older version.
`sudo dnf -y groupinstall emacs`

Update the *smart card support* package group to the latest version:
`sudo dnf -y groupinstall emacs`

Refer to the *group install* and *group update* subsections of the *dnf* command manual
pages for more details.

### Removing Package Groups

- Uninstalls all the included packages and deletes all associated files and directory structure.
- erases any dependencies

Erase the *smart card support* package group that was installed:

`sudo dnf -y groupremove 'smart card support'`

Refer to the *remove* subsection of the *dnf* command manual pages for
more details.

### Lab: Manipulate Package Groups

Perform management operations on a package group called *system tools*. Determine if this group is already installed and if it is available for installation. List the packages it contains and install it. Remove the group along with its dependencies and confirm the removal.

1. Check whether the *system tools* package group is already installed:
`dnf group list installed`

2. Determine if the *system tools* group is available for installation:
`dnf group list available`

The group name is exhibited at the bottom of the list under the
available groups.

3. Display the list of packages this group contains:
`dnf group info 'system tools'`

- All of the packages will be installed as part of the group
installation.

4. Install the group:
`sudo dnf group install 'system tools'`

5. Remove the group:
`sudo dnf group remove 'system tools' -y`

6. Confirm the removal:
`dnf group list installed`


## Module Management

**Modules** are special package groups usually representing an application, a language runtime, or a set of tools. They are available in one or **multiple streams** which usually represent a major version of a piece of software, giving you an option to choose what versions of packages you want to consume.
https://docs.fedoraproject.org/en-US/modularity/using-modules/

Modules are a way to deliver different versions of software (such as programming languages, databases, or web servers) independently of the base operating system's release cycle.

Each module can contain multiple streams, representing different versions or configurations of the software. For example, a module for Python might have streams for Python 2 and Python 3.

 *module* dnf subcommand 
 - list, enable, install, query, remove, and disable
modules.

### Listing Available and Installed Modules

List all modules along with their stream, profile, and summary
information available from all configured repos:
`dnf module list`

Limit the output to a list of modules available from a specific
repo such as AppStream by adding \--repo AppStream:
`dnf module list --repo AppStream`

Output: 
- default (d)
- enabled (e)
- disabled (x)
- installed (i)

List all the streams for a specific module such as *perl* and display their status:
`dnf module list perl`

Modify the above and list only the specified stream (5.24) for the module *perl*:
`dnf module list perl:5.24`

List all enabled module streams:
`dnf module list --enabled`

Similarly, you can use the \--installed and \--disabled options with
**dnf module list** to output only the installed or the disabled
streams.

Refer to the *module list* subsection of the *dnf* command manual pages.

### Installing and Updating Modules

Installing a module 
- creates directory tree for all packages included in the module and all dependent packages
- installs required files for the selected profile
- runs any post-installation steps. 
- If module being loaded or a part of it is already present, the command attempts to update all the packages included in the profile to the latest available versions. 

Install the *perl* module using its default stream and default
profile:
`sudo dnf -y module install perl`

Update a module called *squid* to the latest version:
`sudo dnf module update squid -y`

Install the profile "common" with stream "rhel9" for the *container-tools* module: (module:stream/profile)
`sudo dnf module install container-tools:rhel9/common`

### Displaying Module Information

- Shows 
	- Name, stream, version, list of profiles, default profile, repo name module was installed or is available from
	- Summary, description, and artifacts. 
- Can be viewed by supplying module info with dnf. 

List all profiles available for the module ruby:
`dnf module info --profile ruby`

Limit the output to a particular stream such as 3.1:
`dnf module info --profile ruby:3.1`

Refer to the *module info* subsection of the *dnf* command manual pages for more details.

### Removing Modules

Removing a module will:
- uninstall all the included packages and 
- delete all associated files and directory structure. 
- erases any dependencies as part of the deletion process.

Remove the ruby module with "3.1" stream:
`sudo dnf module remove ruby:3.1

Refer to the *module remove* subsection of the *dnf* command manual pages: 

### Lab: Manipulate Modules

- Perform management operations on a module called *postgresql*. 
- determine if this module is already installed and if it is available for installation
- show its information and install the default profile for stream "10".
- remove the module profile along with any dependencies
- confirm the removal.

1. Check whether the *postgresql* module is already installed(i):
`dnf module list postgresql`

2. Display detailed information about the default stream of the
module:
`dnf module info postgresql:15`

3. Install the module with default profile for stream "15":
`sudo dnf -y module install --profile postgresql:15`

4. Display the module information again:
`dnf module info postgresql:15`

5. Erase the module profile for the stream:
`dnf module remove -y postgresql:15`

6. Confirm the removal (back to (d)):
`dnf module info postgresql:15`

### Switching Module Streams

- Typically performed to upgrade or downgrade the version of an installed module. 

process:
- uninstall the existing version provided by a stream alongside any dependencies that it has, 
- switch to the other stream
- install the desired version. 
- Installing a module from a stream automatically enables the stream if it was previously disabled
- you can manually enable or disable it with the *dnf* command.
- Only one stream of a given module enabled at a time.
- Attempting to enable another one for the same module automatically
disables the current enabled stream.

- dnf module list and dnf module info expose the enable/disable status of the module stream. 

### Lab: Install a Module from an Alternative Stream

- Downgrade a module to a lower version. 
- Remove the stream *perl* 5.26 and 
- Confirm its removal. 
- manually enable the stream *perl* 5.24 and confirm its new status. 
- install the new version of the module and display its information.

1. Check the current state of all *perl* streams:
`dnf module list perl`

2. Remove perl 5.26:
`sudo dnf module remove perl -y`

3. Confirm the removal:
`dnf module list perl`

4. Reset the module so that neither stream is enabled or
disabled. This will remove the enabled (e) indication from perl 5.26.
`sudo dnf module reset ruby`
(perl not available)

5. Install the non-default profile "minimal" for perl stream
5.24. This will auto-enable the stream.

--allowerasing 
- Will instruct the command to remove installed packages for dependency resolution.
`sudo dnf module install perl:5.24/minimal --allowerasing`

6. Check the status of the module:
`dnf module list perl`

## Review Questions

Q. A module profile is a list of recommended packages organized for purpose-built deployments. True or False?
A. True.

---

Q. What would the *dnf group info Base* command do?
A. The command provided will list all packages in the specified package group.


---

Q: What would you run to list all available profiles for the module postgresql?
A. To view *postgresql* module profiles, you would run `dnf module info \--profile postgresql`

---

Q. Which *dnf* subcommand can be used to list all available repositories?
A. The *repolist* subcommand.

---

Q. What is the use of the -y option with the *dnf group install* and *dnf module remove* commands?
A. dnf will not prompt for user confirmation if the -y option is used with it.

---

Q. What is the main advantage of using *dnf* over *rpm*?
A. dnf resolves and installs dependent packages automatically.

---

Q. What would be the command to install *perl* 5.26?
A. It would be `dnf module install perl:5.26`

---

Q. What *dnf* subcommand would we use to check available updates for installed packages?
A. The check-update subcommand.

---

Q. What is the concept of module in RHEL 8?
A. A module is a collection of packages, including the dependent packages, that are required to install an application.

---

Q. What must be the extension of a yum repository file?
A. The extension of a yum repository configuration file must be .repo in order to be recognized as a valid repo file.

---

Q. A module stream is a group of packages organized by version. True or False?
A. True.

---

Q. What would the `dnf list zsh` command do?
A. The command provided will display installed and available *zsh* package.

---

Q. What would the `dnf list installed gnome` command do?
A. The command provided will display all installed packages that contain gnome in their names.

---

Q. How many package names can be specified at a time with the dnf install command?
A. There is no limit.

---

Q. Name the two default yum repositories that contain all the packages for RHEL 8?
A. The two yum repositories the BaseOS and AppStream.

---

Q. We can update all the packages within a package group using the `groupupdate` subcommand with dnf. True or False?
A. True.

---

Q. What would you run to reset a module so that it is neither enabled nor disabled?
A. You would run `dnf module reset` to reset a module.

---

Q. What would the `dnf info zsh` command do?
A. The command provided will display the header information for the *zsh* package.

---

## Labs:

1. Configure Access to RHEL 8 Repositories (Make sure the RHEL 8 ISO image is attached to the VM and mounted.)  Create a definition file under /etc/yum.repos.d/, and define two blocks (one for BaseOS and another for AppStream). 

`vim /etc/yum.repos.d/local.repo`

```
[BaseOS]
name=BaseOS 
baseurl=file:///mnt/BaseOS 
gpgcheck=0 

[AppStrean]
name=AppStream 
baseurl=file:///mnt/AppStream 
gpgcheck=0
```

4. Verify the configuration with dnf repolist. You should see numbers in thousands under the Status column for both repositories. 
`dnf repolist`

### Lab:  Install and Manage Individual Packages

1. List all installed and available packages separately. 
`dnf repoquery && dnf list installed`

2. Show which package contains the /etc/group file. 
`dnf provides /etc/group`

3. Install the package *httpd*. 
`dnf -y install httpd`

4. Review /var/log/yum.log/ for confirmation. (/var/lib/dnf/history)
`dnf history`

5. Perform the following on the httpd package: 
1. Show information 
`dnf info httpd`

2. List dependencies
`dnf repoquery --requires httpd`

3. Remove it
`dnf remove httpd`

### Lab Install and Manage Package Groups

1. List all installed and available package groups separately. 
`dnf group list available && dnf group list installed`

2. Install package groups *Security Tools* and *Scientific Support. 
`dnf group install 'Security Tools'`

3. Review /var/log/yum.log for confirmation. 
`dnf history`

4. Show the packages included in the Scientific Support package group, and delete this group.
`dnf group info 'Scientific Support' && dnf group remove 'Scientific Support'`


### Lab: Install and Manage Modules

1. List all modules. Identify which modules, streams and profiles are installed, default, disabled, and enabled from the output. 
`dnf module list`

2. Install the default stream of the development profile for module *php*, and verify. 
`dnf module install php && dnf module list`

3. Remove the module. 
`dnf module remove php`
### Lab Switch Module Streams and Install Software

1. List *postgresql* module. This will display the streams and profiles, and their status. 
`dnf module list postgresql`

2. Reset both streams
`dnf module reset postgresql`

3. enable the stream for the older version, and install its client profile.
`dnf module install postgresql:15
 `