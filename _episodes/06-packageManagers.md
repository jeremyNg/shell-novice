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
---

Installing software packages is one of the most important tasks that one will undertake when using any computer. In Windows and Mac OSX, this process is relatively straight-forward: we simply download the installer, double-click, and *viola!*, the software is installed. However, this is not the case with Linux. 

## What is a software package? 


## Installing software packages
There are numerous methods that can be used to install software packages, depending on how the software package is distributed. These includes (in decreasing order of complexity):  

1. Compilation from source
2. Installation using package managers
3. Downloading pre-compiled binaries

The last method is what most people are familiar with: 'installers' downloaded from the internet (*.exe* and *.dmg* files) are in reality pre-compiled binaries for the specific platform (*.exe* for Windows and *.dmg* for Mac OSX). However, this is the most restrictive as it is *platform specific*. 

Compilation from source is the most flexible way of installing software packages. This is because the installation can be optimized to the specific platform in use. However, this can sometimes be tedious and be an extremely complex undertaking, especially if the software in question requires a large number of *dependencies*. Compiling from source is particularly tedious for software packages that have extremely complex dependency trees (more below). 

>##Dependencies 
>
> Some software packages require the installation of other packages in order to function properly. These 'other packages' are called *dependencies*. In turn, these dependencies might have their own dependencies, giving rise to an extremely complex *dependency tree*. In simpler terms, you can think of dependencies as being similar to the pre-requisites for modules you wish to take in your candidature. This analogy is imperfect though: these 'pre-requisites' are called dependencies because their installation is often non-negotiable. 

Not all software packages requiring installation from source is complicated though. At times, compilation from source represents the only way to install the software package of interest. For that reason, we will briefly discuss a common method used to install software packages from source at the end of this section. 

Installation from package managers represent a compromise between platform compatibility (offered by compilation from source) and ease (offered by pre-compiled binaries). These managers will download the software package from their package repositories, along with any additional dependencies that the package requires. The latter vastly simplifies the installation process by sparing us the need to manually find and install the dependencies of our software package of interest.

## Package managers 
Different flavors of linux uses different package managers, although they are broadly categorized as *RPM*-based or *Debian*-based systems. Our specific distrubution, Ubuntu, uses APT as the package manager. 

>## A matter of rights: sudo vs non-sudo
> 
> Similar to Windows and Mac OSX, there are three categories of users in Ubuntu (in decreasing order of access rights): administrators, standard users and guest. Installation of software packages *generally* require administrator rights, which is invoked (assuming you are added as a member of the administrator group, or 'sudo-ers' in Linux) by issuing the command with `sudo`. When a software is installed using `sudo`, the software is installed **system-wide** and anyone using the computer can use the software. This is contrasted to installations that are done without `sudo`, which are **local** and can only be used by the user who installed it.   For installation using `apt-get`, `sudo` is required. Otherwise, you will have to compile the software package from source.
 
## Compiling from sources using a Make file 
Although package managers greatly simplify the installation of software packages for us, there are at least two distinct instances wherein you will have to compile the software package from source: 

1. The software package is not available in the software repository, or
2. you do not have `sudo` rights

Often, software packages that require installation from source are downloaded as a *tar* file, which is an archive format (similar to *.zip* files in Windows).  





