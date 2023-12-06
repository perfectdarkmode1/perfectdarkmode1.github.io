# Chapter 9 RHCSA Notes - Basic Package Management

## RPM (Redhat Package Manager)
- also refers to a file(s) packaged together in a special format with the .rpm extension. 
- Each package included or available for RHEL is in rpm format.
- Metadata info also gets updated whenever a package gets updated.

### rpm command
- Query, install, upgrade, freshen, remove, or decompress packages.
- Validate package integrity and authenticity.

### Packages
Two types of packages :: binary (or installable) and source.

#### binary packages
- installation ready
- bundled for distribution.
- Have .rpm extension.
- Contain:
	- install scripts (pre and post)
	- Executables
	- Configuration files
	- Library files
	- Dependency information
	- Where to install files
	- Documentation
		- How to install/uninstall
		- Man pages for config files/commands
		- other install and usage info
	- Metadata
		- stored in central location
		- includes:
			- Package version
			- Install location
			- Checksum values
			- List of included files and their attributes
- Package intelligence
	- used by package administration toolset for successful completion of the package installation process. 
	- May include info on:
		- prerequisites
		- User account setup
		- Needed directories/ soft links
	- Includes reverse process for uninstall.

## Package Naming
5 parts to a package name:
	1. Name
	2. Version
	3. release (revision or build)
	4. Linux version 	
	5. Processor Architecture
		- noarch
			- platform independant
		- src
			- Source code packages
- Always has .rpm extension
- .rpm is removed after install
Example:
	openssl-1.1.1-8.el8.x86_64.rpm,

## Package Dependency
- Dependency info is in the metadata
	- Read by package handling utilities

## Package Database
- Metadata for installed packages and package files is stored in /var/lib/rpm/
	- Package database
	- Referenced by package manipulation utilities to obtain:
		- package name and version data
		- Info about owerships, permissions, timestamps, and file sizes that are part of the package.
		- Contain info on dependencies.
		- Aids management commands in:
			- listing and querying packages
			- Verifying dependencies and file attributes.
			- Installing new packages.
			- Upgrading and uninstalling packages. 
		- Removes and replaces metadata when a package is replaced. 
		- Can maintain multiple version of a single package. 

## Package Management Tools
- rpm (redhat package manager)
	- Does not automatically resolve dependencies.
- yum (yellowdog update, modified)
	- Find, get, and install dependencies automatically.
	- softlink to dnf now.
- dnf (dandified yum)

## Package management with rpm
rpm package management tasks:
	- query
	- install
	- upgrade
	- freshen
	- overwrite
	- remove
	- extract
	- validate
	- verify
- Works with installed and installable packages.

### rpm command
###### Query options
Query and display packages\
`-q (--query)` \
\
List all installed packages\
`-qa (--query --all)`\
\
List config files in a package\
`-qc (--query --config-files)`\
\
List documentation files in a package\
`-qd (--query --docfiles)` \
\
Exhibit what package a file comes from\
`-qf (--query --file)` \
\
Show installed package info (Version, Size, Installation status, Date, Signature, Description, etc.)	
`-qi (--query --info)` 
	
Show installable package info (Version, Size, Installation status, Date, Signature, Description, etc.)
`-qip (--query --info --package)`

List all files in a package.\
`-ql (--query --list)`

List files and packages a package depends on. \
`-qR (--query --requires)`

List packages that provide the specified package or file.\
`-q --whatprovides`

List packages that require the specified package or file.\
`-q --whatrequires`

###### Package installation options
Remove a package\
`-e (--erase)`

Upgrades installed package. Or loads if not installed.\
`-U (--upgrade)`

Display detailed information\
`-v (--verbose or -vv)`

Verify integrity of a package or package files\
`-V (--verify)`

## Querying packages
Query packages in the package database or at a specified location. 

## Installing a package



---
## Labs

### Lab: Mount RHEL 8 ISO Persistently
1. Go to the VirtualBox VM Manager and make sure that the RHEL 8 image is attached to RHEL8-VM1 as depicted below:

![Alt text](/images/isomount.png)

2. Open the /etc/fstab file in the vim editor (or another editor of your choice) and add the following line entry at the end of the file to mount the DVD image (/dev/sr0) in read-only (ro) mode on the /mnt directory.

	```
	/dev/sr0 /mnt iso9660 ro 0 0
	```

Note: sr0 represents the first instance of the optical device and iso9660 is the standard format for optical file systems.

3. Mount the file system as per the configuration defined in the /etc/fstab file using the mount command with the -a (all) option:

	```
	sudo mount -a
	```

4. Verify the mount using the df command:

	```
	df -h | grep mnt
	```

Note: The image and the packages therein can now be accessed via the /mnt directory just like any other local directory on the system.

5. List the two directories—/mnt/BaseOS/Packages and /mnt/AppStream/Packages—that contain all the software packages (directory names are case sensitive):

	```
	ls -l /mnt/BaseOS/Packages |more
	```

### Lab: Query Packages
1. query all installed packages:
	`rpm -qa`

2. query whether the perl package is installed:
	`rpm -q perl`

3. list all files in a package:
	`rpm -ql iproute`

4. list only the documentation files in a package:
	`rpm -qd audit`

5. list only the configuration files in a package:
	`rpm -qc cups`

6. identify which package owns the specified file:
	`rpm -qf /etc/passwd`

7. display information about an installed package including version, release, installation status, installation date, size, signatures, description, and so on:
	`rpm -qd audit`

8. list only the configuration files in a package:
	`rpm -qc cups`

9. identify which package owns the specified file:
	`rpm -qf /etc/passwd`

10. display information about an installed package including version, release, installation status, installation date, size, signatures, description, and so on:
	`rpm -qi setup`

11. list all file and package dependencies for a given package:
	`rpm -qR chrony`

12. query an installable package for metadata information (version, release, architecture, description, size, signatures, etc.):
	`rpm -qip /mnt/BaseOS/Packages/zsh-5.5.1-6.el8.x86_64.rpm`

13. determine what packages require the specified package in order to operate properly:
	`rpm -q --whatrequires lvm2`
	