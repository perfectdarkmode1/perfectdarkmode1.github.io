---
title: Packages and Their Management
date: 2023-11-06T06:20:36-07:00
draft: true
---
Software Distribution

Packages such as internet browsers, text editors, media players, etc. are  managed via package managers that install and maintain the software on the system. Packages can be installed using sources code instead of by a package manager.

Packages are really just lot and lots of files compiled into one.

The people who write them are called upstream providers. They send updates to package maintainers who get the software into the hands of the users. Package maintainers review, manage, and distribute this software in the form of packages.

Packages Repositories

Central storage location for packages. Machine doesn't know where to look for repositories on the internet unless you tell them.

Pre-approved sources for repositories are located in /etc/apt/sources.list

tar and gzip

Compressing files with gzip

end in a .gz extension

$ gzip mycoolfile - compresses the file

$ gunzip mycoolfile.gz - decompresses the file

Creating archives with tar

Used for multiple files.

will have a .tar extension

$ tar cvf mytarfile.tar mycoolfile1 mycoolfile2 - compresses 2 files.

c - create

v - tell the program to be verbose and let us see what it's doing

f - the filename of the tar file has to come after this option, if you are creating a tar file you'll have to come up with a name.

Unpacking archives with tar

$ tar xvf mytarfile.tar - extracts the file

x - extract

v - tell the program to be verbose and let us see what it's doing.

f - the file you want to extract

Compressing/ uncompressing archives with tar and gzip

Used if a file has a .tar.gz extension.

You can do them one at a time from the end ext first or use z option with tar.

$ tar czf myfile.tar.gz - Create a compressed tar file

$ tar xzf file.tar - uncompress and unpack

eXtract all Zee Files (xzf)

\* other compression utilities will require different commands.

Package dependencies

Packages don't usually work alone. They need dependencies to help them run. Packages run code from other libraries so they don't have to have all of the code themselves.

If the dependencies cannot be accessed or they are broke then the package will not run.

rpm and dpkg

.deb (on Debian) and .rpm (on red hat) are executable files just like .exe.

To install these packages use rpm and dpkg (package management commands used to install package files)

These will not install package dependencies.

Install a package

Debian: $ dpkg -i some\_deb\_package.deb

RPM: $ rpm -i some\_rpm\_package.rpm

The i stands for install

Remove a package

Debian: $ dpkg -r some\_deb\_package.deb

RPM: $ rpm - e some\_rpm\_ package.rpm

Debian: r for remove

RPM: e for erase

List installed packages

Debian: $ dpkg -l

RPM: $ rpm -qa

Debian: l for list

RPM: q for query and a for all

yum and apt

Used for easy package installation, removal, and changes. Can also install package dependencies. Yum is exclusive to the red hat family and apt is exclusive to the Debian family.

Install a package from a repository

Debian: $ apt install package_name

RPM: $ yum install package_name

Remove a package

Debian: $ apt remove package_name

RPM: $ yum erase package_name

Updating packages for a repository

You should update your package repositories so they are up to date before you install and update a package.

Debian: apt update; apt upgrade

RPM: yum update

Get information about an installed package

Debian: apt show package_name

RPM: yum info package_name

Compile source code

Software to install tools that will allow you to compile source code.

$ sudo apt install build-essential

Extract the contents of the package file (most likely a .tar.gz file)

$ tar -xzvf package.tar.gz

Inside the package contents will be a configure script, this script checks for dependencies on your system and if you are missing anything, you'll see an error and you'll need to fix those dependencies.

$ ./configure

The ./ allows you to execute a script in the current directory.

$ make

Inside of the package contents is a file called Makefile that contains rules to building the software. The make command looks at this file to build the software.

$ sudo make install

This command actually installs the package, it will copy the correct files to the correct locations on your computer.

$ sudo make uninstall

To uninstall the package.

Use the checkinstall file instead of the make command. It can be hard to uninstall packages installed with the make command.

$ sudo checkinstall

This will essentially "make install" and build a .deb package and install it. It makes it easier to remove the package later on.
