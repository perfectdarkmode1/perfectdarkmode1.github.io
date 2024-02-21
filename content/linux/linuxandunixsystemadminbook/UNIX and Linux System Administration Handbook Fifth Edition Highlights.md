


### Controlling access

creates accounts for new users, removes the accounts of inactive users, and handles all the account-related issues that come up in between

process of actually adding and removing accounts is typically automated by a configuration management system or centralized directory service


### Adding hardware

### Automating tasks

 increases your efficiency, reduces the likelihood of errors caused by humans, and improves your ability to respond rapidly to changing equirements

### Overseeing backups

Backups must be executed on a regular schedule and restores must be tested periodically to ensure that they are functioning correctly.

### Installing and upgrading software

As patches and security updates are released, they must be tested, reviewed, and incorporated into the local environment without endangering the stability of production systems

software delivery” refers to the process of releasing updated versions of software

Continuous delivery” takes this process to the next level by automatically releasing software to users at a regular cadence as it is developed

### Monitoring

detecting problems and fixing them before public failures occur.

monitoring tasks include ensuring that web services respond quickly and correctly, collecting and analyzing log files, and keeping tabs on the availability of server resources such as disk space

### Troubleshooting


### Maintaining local documentation

Thorough and accurate documentation is a blessing for team members who would otherwise need to reverse-engineer a system to resolve problems in the middle of the night


## Vigilantly monitoring security

must implement a security policy and set up procedures to prevent systems from being breached

might include only a few basic checks for unauthorized access, or it might involve an elaborate network of traps and auditing programs, depending on the context

### Tuning performance
tailor systems for optimal performance in accord with the needs of users, the available infrastructure, and the services the systems provide

 When a server is performing poorly, it is the administrator’s job to investigate its operation and identify areas that need improvement.

### Developing site policies

most sites need policies that govern the acceptable use of computer systems, the management and retention of data, the privacy and security of networks and systems, and other areas of regulatory interest

develop sensible policies that meet the letter and

intent of the law and yet still promote progress and productivity

### Working with vendors

### Fire fighting

your response to these issues affects your perceived value as an administrator far more than does any actual technical skill you might possess a single well-handled trouble ticket scores more brownie points than five hours of midnight debugging

### Vim
Mastering vim is perhaps the single best productivity enhancement available to administrators
Use the vimtutor command for an excellent, interactive introduction.

### Programming
Capable administrators are usually polyglot programmers who don’t mind picking up a new language when the need arises

we recommend Bash (aka bash, aka sh), Ruby, or Python

We also suggest that you learn expect, which is not a programming language so much as a front end for driving interactive programs. It’s an efficient glue technology that can replace some complex scripting and is easy to learn.

### Distributions

A Linux distribution comprises the Linux kernel, which is the core of the operating system, and packages that make up all the commands you can run on the system

All distributions share the same kernel lineage, but the format, type, and number of packages
differ quite a bit

distributions derived from the Debian and Red Hat lineages will predominate in production environments in the years ahead

Virtually all leading distributions are cluttered with scores of unused software packages; security vulnerabilities and administrative anguish often come along for the ride






> By adopting a distribution, you are making an investment in a
> particular vendor’s way of doing things. Instead of looking only at
> the features of the installed software, it’s wise to consider how your
> organization and that vendor are going to work with each other. Some
> important questions to ask are:






> 1.  Is this distribution going to be around in five years?
> 2.  Is this distribution going to stay on top of the latest security
>     patches?






> Does this distribution have an active community and sufficient
> documentation






> If I have problems, will the vendor talk to me, and how much will that
> cost






> A comprehensive list of distributions, including many non-English
> distributions, can be found at lwn.net/Distributions or
> distrowatch.com






> Debian GNU/Linux, Ubuntu Linux, Red






> Hat Enterprise Linux (and its dopplegänger CentOS), and FreeBSD






> Debian defines three releases that are maintained simultaneously:
> stable, targeting production servers; unstable, with current packages
> that may






> have bugs and security vulnerabilities; and testing, which is
> somewhere in between.






> Ubuntu version numbers derive from the






> year and month of release, so version 16.10 is from October, 2016.
> Each release also has an alliterative code name such as Vivid Vervet
> or Wily Werewolf.






> Two versions of Ubuntu are released annually: one in April and one in
> October. The April releases






> in even-numbered years are long-term support (LTS) editions that
> promise five years of maintenance updates. These are the releases
> recommended for production use






> RHEL is open source but requires a license. If you’re not willing to
> pay for the license, you’re not going to be running Red Hat.






> Fedora, a community-based distribution that serves as an incubator for
> bleeding-edge software not considered stable enough for RHEL






> Fedora is used as the initial test bed for software and configurations
> that later find their way to RHEL






> CentOS is an excellent choice for sites that want to deploy a
> production-oriented distribution without paying tithes to Red Hat. A
> hybrid approach is also feasible: front-line servers can run Red Hat
> Enterprise






> Linux and avail themselves of Red Hat’s excellent support, even as
> nonproduction systems run CentOS






> This arrangement covers the important bases in terms of risk and
> support while also minimizing cost and administrative complexity






> CentOS aspires to full binary and bug-for-bug compatibility with Red
> Hat Enterprise Linux






> Apple’s macOS has a BSD heritage






> FreeBSD






> commands a 70% market share among BSD variants






> Unlike Linux, FreeBSD is a complete operating system, not just a
> kernel






> We use $ to denote the shell prompt for a normal, unprivileged user,
> and # for the root user






> 1.  A star (\*) matches zero or more characters.
> 2.  A question mark (?) matches one character.
> 3.  A tilde or “twiddle” (~) means the home directory of the current
>     user






> ~user means the home directory of user.






> one “megabyte” of memory is really 220 or 1,048,576 bytes






> RAM is always denominated in powers of 2, but network bandwidth






> is always a power of 10. Storage space is usually quoted in
> power-of-10 units, but block and page sizes are in fact powers of 2






> Unit decoding examples






> see wiki.ubuntu.com/UnitsPolicy for some additional details






> Man pages and other on-line documentatio






> consult man pages as an authoritative resource because they are
> accessible from the command line






> details on a program’s options, and show helpful examples and related
> commands






> concise descriptions of individual commands, drivers, file formats, or
> library routines






> FreeBSD and Linux divide the man pages into sections.






> Sections of the man pages






> be aware of the section definitions when a topic with the same name
> appears in multiple sections






> man title formats a specific manual page and sends it to your terminal
> through more, less, or whatever program is specified in your PAGER
> environment variable






> title is usually a command, device, filename, or name of a library
> routine






> sections of the manual are searched in roughly numeric order, although
> sections that describe commands (sections 1 and 8) are usually
> searched first.






> man section title gets you a man page from a particular section






> man sync gets you the man page for the sync command, and man 2 sync
> gets you the man page for the sync system call






> man -k keyword or apropos keyword prints a list of man pages that have
> keyword in their one-line synopses






> The keywords database can become outdated. If you add additional man
> pages to your system






> you may need to rebuild this file with makewhatis (Red Hat and
> FreeBSD) or mandb (Ubuntu).






> nroff input for man pages (i.e., the man page source code) is stored
> in directories under /usr/share/man and compressed with gzip to save
> space






> man maintains a cache of formatted pages in /var/cache/man or
> /usr/share/man if the appropriate directories are writable; however,
> this is a security risk. Most systems preformat the man pages once at
> installation time (see catman) or not at all.






> The man command can search several man page repositories to find the
> manual pages you request. On Linux systems, you can find out the
> current default search path with the manpath command. This path (from
> Ubuntu) is typical






> If necessary, you can set your MANPATH environment variable to
> override the default path






> Some systems let you set a custom system-wide default search path for
> man pages, which can be useful if you need to maintain a parallel tree
> of man pages such as those generated by OpenPKG






> Where to find OS






> Pro Git from git-scm.com/book make the hunt worthwhile






> Many pieces of software have both a man page and a long-form article






> Most software projects have user and developer mailing lists and IRC
> channels






> if you have questions






> 
> Request for Comments documents describe the protocols and procedures
> used on the Internet






> The phrase “reference implementation” applied to software






> usually translates to “implemented by a trusted source according to
> the RFC specification






> When stuck, search the web.






> Resources for keeping up to date






> <div>
> <div>
> <div></div>
> </div>
> </div>
> 
> Social media are also useful. Twitter and reddit in particular have
> strong, engaged communities with a lot to offer, though the
> signal-to-noise ratio can sometimes be quite bad. On reddit, join the
> sysadmin, linux, linuxadmin, and netsec subreddits.






> Task-specific forums and reference sites






> Stack Overflow and Server Fault






> It’s worth creating an account and joining this large community






> Conferences relevant to system administrators






> Meetups (meetup.com) are another way to network and engage with
> like-minded people. Most urban areas in the United States and around
> the world have a Linux user group or DevOps meetup that sponsors
> speakers, discussions, and hack days.






> When adding software, don your security hat and remember that
> additional software creates additional attack surface






> Most software is developed by independent groups that release the
> software in the form of source code. Package repositories then pick up
> the source code, compile it appropriately for the conventions in use
> on the systems they serve, and package the resulting






> binaries. It’s usually easier to install a system-specific binary
> package than to fetch and compile the original source code. However,
> packagers are sometimes a release or two behind the current version.






> two systems use the same package format doesn’t necessarily mean that
> packages for the two systems are interchangeable






> Red Hat and SUSE both use RPM






> When the packaged format is insufficient, administrators must install
> software the old-fashioned way: by downloading a tar archive of the
> source code and manually configuring, compiling, and installing it.
> Depending on the software and the operating system, this process can
> range from trivial to nightmarish






> use the shell’s which command to find out if a relevant binary is
> already






> reveals that the GNU C compiler has already been installed on this
> machine






> If which can’t find the command you’re looking for, try whereis; it
> searches a broader range of system directories and is independent of
> your shell’s search path






> locate command, which consults a precompiled index






> the filesystem to locate filenames that match a particular pattern.






> FreeBSD includes locate as part of the base system. In Linux, the
> current implementation of locate is in the mlocate package






> On Red Hat






> and CentOS, install the mlocate package with yum; see this page.






> locate can find any type of file; it is not specific to commands or
> packages. For example, if you weren’t sure where to find the signal.h
> include file, you could try






> locate’s database is updated periodically by the updatedb command (in
> FreeBSD






> locate.updatedb), which runs periodically out of cron.






> Therefore, the results of a locate don’t always reflect recent changes
> to the filesystem






> you can also use your system’s packaging utilities to check directly
> for the package’s presence



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#45|1713)



> checks for the presence (and installed version) of the Python
> interpreter



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#45|1828)



> find out which package a particular file belongs to:
> 



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#46|557)



> installation of the tcpdump command on each of our example systems.
> tcpdump is a packet capture tool that lets you view the raw packets
> being sent to and from the system on the network.
> 
> <div>
> <div></div>
> </div>
> 
> <div>
> <div></div>
> </div>
> 
> Debian and Ubuntu use APT, the Debian Advanced Package Tool:



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#46|931)



> The Red Hat and CentOS version is



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#46|1016)



> The package manager for FreeBSD is pkg.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|75)



> build a version of tcpdump from the source code.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|150)



> identify the code.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|169)



> Software maintainers sometimes keep an index of releases on the
> project’s web site that are downloadable as tarballs. For open source
> projects, you’re most likely to find the code in a Git repository.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|373)



> The tcpdump source is kept on GitHub. Clone the repository in the /tmp
> directory, create a branch of the tagged version you want to build,
> then unpack, configure, build, and install it:



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|590)



> configure/make/make install sequence is common to most software
> written in C and works on all UNIX and Linux systems.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|736)



> check the package’s INSTALL or README file for specifics



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|798)



> must have the development environment and any package-specific
> prerequisites installed. (In the case of tcpdump, libpcap and its
> libraries are prerequisites.)



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#47|960)



> You’ll often need to tweak the build configuration, so use ./configure
> --help to see the options available for each particular package.
> Another useful configure option is --prefix=directory, which lets you
> compile the software for installation somewhere other than /usr/local,
> which is usually the default.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|34)



> Cross-platform software bundles increasingly offer an expedited
> installation process that’s driven by a shell script you download from
> the web with curl, fetch, or wget.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|204)



> These are all simple HTTP clients that download the contents of a URL
> to a local file or, optionally, print the contents to their standard
> output. For example, to set up a machine as a Salt client, you can run
> the following commands:
> 
> <div>
> <div></div>
> </div>



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|465)



> The bootstrap script investigates the local environment, then
> downloads, installs, and configures an appropriate version of the
> software. This type of installation is particularly common in cases
> where the process itself is somewhat complex, but the vendor is highly
> motivated to make things easy for users. (Another good example is RVM;
> see this page.)



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|908)



> This installation method



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|1030)



> leaves no proper record of the installation for future reference. If
> your operating system offers a packagized version of the software,
> it’s usually preferable to install the package instead of running a
> web installer.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|1249)



> Packages are easy to track, upgrade, and remove. (On the other hand,
> most OS-level packages are out of date. You probably won’t end up with
> the most current version of the software.)



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|1511)



> Be very suspicious if the URL of the boot script is not secure (that
> is, it does not start with https:). Unsecured HTTP is trivial to
> hijack, and installation URLs are of particular interest to hackers
> because they know you’re likely to run, as root, whatever code comes
> back. By contrast, HTTPS validates the identity of the server through
> a cryptographic chain of trust. Not foolproof, but reliable enough.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|1923)



> A few vendors publicize an HTTP installation URL that automatically
> redirects to an HTTPS version. This is dumb and is in fact no more
> secure than straight-up HTTP. There’s nothing to prevent the initial
> HTTP exchange from being intercepted, so you might never reach the
> vendor’s redirect



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|2213)



> However, the existence of such redirects does mean it’s worth trying
> your own substitution of https for http in insecure URLs. More often
> than not, it works just fine.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|2618)



> he root shell still runs even if curl outputs a partial script and
> then fails—say, because of a transient network glitch. The end result
> is unpredictable and potentially not good.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|2947)



> piping the output of curl to a shell has entered the collective
> sysadmin unconscious as a prototypical rookie blunder, so if you must
> do it, at least keep it on the sly.



          1.10 Ways to find and install software
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#48|3138)



> ust save the script to a temporary file, then run the script in a
> separate step after the download successfully completes.



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|326)



> The most practical choice, and our recommendation for new projects, is
> a public cloud provider. These facilities offer numerous advantages
> over data centers:
> 
> * No capital expenses and low initial operating costs
> * No need to install, secure, and manage hardware
> * On-demand adjustment of storage, bandwidth, and compute capacity
> * Ready-made solutions for common ancillary needs such as databases,
>   load balancers, queues, monitoring, and more
> * Cheaper and simpler implementation of highly available/redundant
>   systems



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1106)



> Our preferred cloud platform is the leader in the space: Amazon Web
> Services (AWS)



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1246)



> AWS is ten times the size of all competitors combined



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1301)



> AWS innovates rapidly and offers a much broader array of services than
> does any other provider.



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1510)



> free service tier to cut your teeth on, including a year’s use of a
> low powered cloud server.



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1607)



> Google Cloud Platform (GCP



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1805)



> reputation for dropping support for popular offerings.



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1873)



> customer-friendly pricing terms



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1959)



> DigitalOcean



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|1977)



> simpler service with a stated goal of high performance.



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|2037)



> target market is developers, whom it woos with a clean API, low
> pricing, and extremely fast boot times



          1.11 Where to host
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#49|2159)



> strong proponent of open source software, and their tutorials and
> guides for popular Internet technologies are some of the best
> available.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#50|347)



> Your goal as a system administrator, or as a professional working in
> any of these related areas, is to achieve the objectives of the
> organization. Avoid letting politics or hierarchy interfere with
> progress. The best administrators solve problems and share information
> freely with others.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#51|78)



> DevOps



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#51|163)



> aims to improve the efficiency of building and delivering software,
> especially at large sites that have many interrelated services and
> teams. Organizations with a DevOps practice promote integration among
> engineering teams and may draw little or no distinction between
> development and operations. Experts who work in this area seek out
> inefficient processes and replace them with small shell scripts or
> large and unwieldy Chef repositories.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#52|32)



> Site reliability engineers value uptime and correctness above all else



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#52|104)



> Monitoring networks, deploying production software, taking pager duty,
> planning future expansion, and debugging outages



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#52|282)



> Single points of failure are site reliability engineers’ nemeses.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#53|35)



> Security operations engineers



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#53|65)



> focus on the practical, day-to-day side of an information security
> program



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#53|153)



> install and operate tools that search for vulnerabilities and monitor
> for attacks on the network. They also participate in attack
> simulations to gauge the effectiveness of their prevention and
> detection techniques.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#54|28)



> Network administrators design, install, configure, and operate
> networks. Sites that operate data centers are most likely to employ
> network administrators; that’s because these facilities have a variety
> of physical switches, routers, firewalls, and other devices that need
> management. Cloud platforms also offer a variety of networking
> options, but these usually don’t require a dedicated administrator
> because most of the work is handled by the provider.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#55|2)



> Database administrators



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#55|83)



> experts at installing and managing database software.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#55|142)



> manage database schemas, perform installations and upgrades, configure
> clustering, tune settings for optimal performance, and help users
> formulate efficient queries.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#55|317)



> usually wizards with one or more query languages and have experience
> with both relational and nonrelational (NoSQL) databases.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#56|47)



> NOC engineers monitor the real-time health of large sites and track
> incidents and outages.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#56|143)



> troubleshoot tickets from users, perform routine upgrades, and
> coordinate actions among other teams. They can most often be found
> watching a wall of monitors that show graphs and measurements.



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#57|2)



> Data center technicians



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#57|53)



> work with hardware. They receive new equipment, track equipment
> inventory and life cycles, install servers in racks, run cabling,
> maintain power and air conditioning, and handle the daily operations
> of a data center



          1.12 Specialization and adjacent disciplines
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#58|16)



> Systems architects have deep expertise in more than one area. They use
> their experience to design distributed systems. Their job descriptions
> may include defining security zones and segmentation, eliminating
> single points of failure, planning for future growth, ensuring
> connectivity among multiple networks and third parties, and other
> site-wide decision making. Good architects are technically proficient
> and generally prefer to implement and test their own designs.



          1.13 Recommended reading
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#59|30)



> Abbott, Martin L., and Michael T. Fisher. The Art of Scalability:
> Scalable Web Architecture, Processes, and Organizations for the Modern
> Enterprise (2nd Edition). Addison-Wesley Professional, 2015.
> 
> Gancarz, Mike. Linux and the Unix Philosophy. Boston: Digital Press,
> 2003.
> 
> Limoncelli, Thomas A., and Peter Salus. The Complete April Fools’ Day
> RFCs. Peer-to-Peer Communications LLC. 2007. Engineering humor. You
> can read this collection on-line for free at rfc-humor.com.
> 
> Raymond, Eric S. The Cathedral &amp; The Bazaar: Musings on Linux and
> Open Source by an Accidental Revolutionary. Sebastopol, CA: O’Reilly
> Media, 2001.
> 
> Salus, Peter H. The Daemon, the GNU &amp; the Penguin: How Free and
> Open Software is Changing the World. Reed Media Services, 2008. This
> fascinating history of the open source movement by UNIX’s best-known
> historian is also available at groklaw.com under the Creative Commons
> license. The URL for the book itself is quite long; look for a current
> link at groklaw.com or try this compressed equivalent:
> tinyurl.com/d6u7j.
> 
> Siever, Ellen, Stephen Figgins, Robert Love, and Arnold Robbins. Linux
> in a Nutshell (6th Edition). Sebastopol, CA: O’Reilly Media, 2009.



          1.13 Recommended reading
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#60|2)



> 
> Kim, Gene, Kevin Behr, and George Spafford. The Phoenix Project: A
> Novel about IT, DevOps, and Helping Your Business Win. Portland, OR:
> IT Revolution Press, 2014. A guide to the philosophy and mindset
> needed to run a modern IT organization, written as a narrative. An
> instant classic.
> 
> Kim, Gene, Jez Humble, Patrick Debois, and John Willis. The DevOps
> Handbook: How to Create World-Class Agility, Reliability, and Security
> in Technology Organizations. Portland, OR: IT Revolution Press, 2016.
> 
> Limoncelli, Thomas A., Christina J. Hogan, and Strata R. Chalup. The
> Practice of System and Network Administration (2nd Edition). Reading,
> MA: Addison-Wesley, 2008. This is a good book with particularly strong
> coverage of the policy and procedural aspects of system
> administration. The authors maintain a system administration blog at
> everythingsysadmin.com.
> 
> Limoncelli, Thomas A., Christina J. Hogan, and Strata R. Chalup. The
> Practice of Cloud System Administration. Reading, MA: Addison-Wesley,
> 2014. From the same authors as the previous title, now with a focus on
> distributed systems and cloud computing.



          1.13 Recommended reading
        ](https://reader.bookfusion.com/books/4031036-unix-and-linux-system-administration-handbook-fifth-edition?type=epub_reflowable#61|2)



> 
> Blum, Richard, and Christine Bresnahan. Linux Command Line and Shell
> Scripting Bible (3rd Edition). Wiley, 2015.
> 
> Dougherty, Dale, and Arnold Robins. Sed &amp; Awk (2nd Edition).
> Sebastopol, CA: O’Reilly Media, 1997. Classic O’Reilly book on the
> powerful, indispensable text processors sed and awk.
> 
> Kim, Peter. The Hacker Playbook 2: Practical Guide To Penetration
> Testing. CreateSpace Independent Publishing Platform, 2015.
> 
> Neil, Drew. Practical Vim: Edit Text at the Speed of Thought.
> Pragmatic Bookshelf, 2012.
> 
> Shotts, William E. The Linux Command Line: A Complete Introduction.
> San Francisco, CA: No Starch Press, 2012.
> 
> Sweigart, Al. Automate the Boring Stuff with Python: Practical
> Programming for Total Beginners. San Francisco, CA: No Starch Press,
> 2015.



