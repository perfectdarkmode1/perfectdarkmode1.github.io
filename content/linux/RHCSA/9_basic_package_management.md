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
		- 