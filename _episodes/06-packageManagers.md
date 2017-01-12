---
title: "Installing software packages"
teaching: 10
exercises: 1
questions:
- "How are software packages installed on a Linux system?"
- "What are package managers?"
- "Software package installation made easy using package managers"
keypoints:
- "Software packages can be installed by compiling from source or via the use of package managers." 
- "Package managers are used in Linux systems to simplify the installation of software packages."
- "Different flavors of Linux might use different package managers. In Ubuntu, the package manager that is used is apt-get."
- "Superuser rights can be invoked by using `sudo`"
- "Make is used to install packages from source when the package is not available via the package manager or if one does not have `sudo` rights." 

---

Installing software packages is one of the most important tasks that one will undertake when using any computer. In Windows and Mac OSX, this process is relatively straight-forward: we simply download the installer, double-click, and *viola!*, the software is installed. However, this is not the case with Linux. 

## Installing software packages
There are numerous methods that can be used to install software packages, depending on how the software package is distributed. These includes (in decreasing order of complexity):  

1. Compilation from source
2. Installation using package managers
3. Downloading pre-compiled binaries

The last method is what most people are familiar with: 'installers' downloaded from the internet (*.exe* and *.dmg* files) are in reality pre-compiled binaries for the specific platform (*.exe* for Windows and *.dmg* for Mac OSX). However, this is the most restrictive as it is *platform-specific*. 

Compilation from source is the most flexible way of installing software packages. This is because the installation can be optimized to the specific platform in use. However, this can sometimes be tedious and be an extremely complex undertaking, especially if the software in question requires a large number of *dependencies*. Compiling from source is particularly tedious for software packages that have extremely complex dependency trees (more below). 

>## Dependencies 
>
> Some software packages require the installation of other packages in order to function properly. These 'other packages' are called *dependencies*. In turn, these dependencies might have their own dependencies, giving rise to an extremely complex *dependency tree*. In simpler terms, you can think of dependencies as being similar to the pre-requisites for modules you wish to take in your candidature. This analogy is imperfect though: these 'pre-requisites' are called dependencies because their installation is often non-negotiable. 

Not all software packages requiring installation from source is complicated though. At times, compilation from source represents the only way to install the software package of interest. For that reason, we will briefly discuss a common method used to install software packages from source at the end of this section. 

Installation from package managers represent a compromise between platform compatibility (offered by compilation from source) and ease (offered by pre-compiled binaries). These managers will download the software package from their package repositories, along with any additional dependencies that the package requires. The latter vastly simplifies the installation process by sparing us the need to manually find and install the dependencies of our software package of interest.

## Package managers 
Different flavors of linux uses different package managers, although they are broadly categorized as *RPM*-based or *Debian*-based systems. Our specific distribution, Ubuntu, uses APT as the package manager. The rest of our discussion using package managers will thus be focused on APT, although similar principles applies to other package managers. 

At its core, the following is done when you attempt to install a software package using the APT package manager, `apt-get`: 
1. Connects to the software repository and/or other sources,
2. Downloads the source file of the package, 
3. Read the dependency list of the package you are trying to install,
4. Check for missing dependencies, and if possible, download the dependencies, 
5. Compile the sources of the dependencies and the software package using default settings for your system. 

For that reason, an active internet connection is required for `apt-get` to work.  Information about repository sources (where software packages are to be found) is contained in the file */etc/apt/sources.list*. One may add more other repositories by editing said file. If the list of repositories is updated, one needs to run `sudo apt-get update` before using *apt-get* so that the newly added source will be searched when using *apt-get*. 

## Searching for packages from software repositories. 
The APT software repository contains thousands of packages, and package names can sometimes be cryptic. Fortunately, we can search for packages that match a regular expression using the following command:
~~~
apt-cache search <pattern>
~~~ 
{: .bash}

The output of the search, as with other outputs on **STDOUT**, can be redirected to a text file if desired. 

## Installing software packages using `apt-get` 
Installing packages using `apt-get` is simply accomplished using the following
~~~ 
$sudo apt-get install <package name>
~~~
{: .bash}

Note the presence of the command `sudo` preceding the `apt-get` command. `sudo` is the command that is used to run `apt-get` as a **super-user**, which means `apt-get` is run with administrator rights. The use of `sudo` has certain implications, and the absence of *sudo* rights substantially complicates installation of software packages (by design since non-*sudo-ers* are not supposed to be able to do anything that changes the system (below). 

>## A matter of rights: sudo vs non-sudo
> 
> Similar to Windows and Mac OSX, there are three categories of users in Ubuntu (in decreasing order of access rights): administrators, standard users and guest. Installation of software packages *generally* require administrator rights, which is invoked (assuming you are added as a member of the administrator group, or 'sudo-ers' in Linux) by issuing the command with `sudo`. When a software is installed using `sudo`, the software is installed **system-wide** and anyone using the computer can use the software. This is contrasted to installations that are done without `sudo`, which are **local** and can only be used by the user who installed it. Because **local** installations do not write to system-wide locations such as `/usr/bin`, the underlying operating system remains unchanged.   For installation using `apt-get`, `sudo` is required because `apt-get` automatically installs the software to system-wide directories such as */usr/bin* and */usr/share*. Otherwise, you will have to compile the software package from source.
 
## Compiling from sources using a Make file 
Although package managers greatly simplify the installation of software packages for us, there are at least two distinct instances wherein you will have to compile the software package from source: 

1. The software package is not available in the software repository, or
2. you do not have `sudo` rights

We will discuss the simplest cases of installation from source (which works in most cases), where we have downloaded the source file of the software package and its associated dependencies. 

Often, software packages that require installation from source are downloaded as a *.tar* or *.tar.gz* file, which is an archive format (similar to *.zip* files in Windows).  Unlike Windows where you need to download *WinZip* or equivalent to unpack these archives, unpacking in Linux is done at the command line using `tar -zxvf <file>.tar.gz`, where `tar` is the utility used to work with archives. The `-zxvf` arguments indicate that you need to decompress the archive first using gzip (`-z`), then extract (`-x`) a given file (`-f`) in a verbose manner (`-v`).  If the *.tar* file is not compressed with gzip, the `-z` option should be omitted.

After the archive is unpacked, you will need to change your working directory into the folder containing the binaries. Often, install instructions are found in a text file **README** found in the folder. Most commonly, only two commands that needs to be run for installation (using default settings): `make` and `make install`. 

>## make and makefiles
>
> When `make` is run, it reads the makefile, which is essentially a text-file containing configuration information (among a whole host of information), and compiles the sources according to the information contained in *makefile*. `make` thus accomplishes two things: (1) it simplifies the installation process because only 2 commands are needed, and (2) it allows control over the configuration of the software package. The latter allows **local** installation to be done by configuring the compiled binaries to be saved in a directory that one has write-access to, such as *~/bin*. 
 
## Exercise 
A software package that you will be using later in the course is `samtools`, which is used for the manipulation of SAM files (a specific format of file for next-generation sequencing data). `samtools` is not installed on Ubuntu by default, but is available using APT. Now, install `samtools` on your machine using `apt-get`.




