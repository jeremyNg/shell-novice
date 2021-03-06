---
title: "File structure in linux"
teaching: 5
exercises: 0
questions:
- "How are files organized in linux system?"
objectives:
- "Explain file structure in Linux system."
- "Introduce different types of files."
keypoints:
- "Generally, everything is a file in Linux system."
- "Directories in Linux system are organized in tree-like structure."
- "Different types of files in Linux system."

---

# Overview of the Linux file system

## General

A simple description of the UNIX system, also applicable to Linux, is this:

"On a UNIX system, everything is a file; if something is not a file, it is a process."

This statement is true because there are special files that are more than just files
(named pipes and sockets, for instance), but to keep things simple, saying that
everything is a file is **an acceptable generalization**. A Linux system, just like UNIX,
makes no difference between a file and a directory, since a directory is just a file
containing names of other files. Programs, services, texts, images, and so forth, are all
files. Input and output devices, and generally all devices, are considered to be files,
according to the system.

In order to manage all those files in an orderly fashion, man likes to think of them in
an ordered **tree-like structure** on the hard disk, as we know from MS-DOS (Disk
Operating System) for instance. The large branches contain more branches, and the
branches at the end contain the tree's leaves or normal files. For now we will use this
image of the tree, but we will find out later why this is not a fully accurate image.



## How does it look like?

For convenience, the Linux file system is usually thought of in a tree structure.
On a standard Linux system you will find the layout generally follows the scheme
presented below.


![The file system](../fig/Linux-FileSystem-layout.png)


> ## Notice
> This is a layout from a RedHat system.
>Depending on the system admin, the operating system and the mission of the UNIX machine, the structure may vary,
>and directories may be left out or added at will. The names are not even required;
>they are only a convention.
{: .callout}

## Path in Linux system

The tree of the file system starts at the trunk or slash, indicated by a forward slash **"/"**.
This directory, containing all underlying directories and files, is also called the **root directory** or **"the root"** of the file system.

Now the next level of the directories are often preceded by a slash, like this:

> /home/jeremy

If we go to the fourth level of the file system, it would look like this:

> /usr/share/doc

The paths shown here are **absolute path** which start from the root. There is another kind of path called **relative path**, which we will learn about later.

## Sort of files
Most files are just files, called regular files; they contain normal data, for example
text files, executable files or programs, input for or output from a program and so on.

While it is reasonably safe to suppose that everything you encounter on a Linux system is
a file, there are some **exceptions**.

* *Directories*: files that are lists of other files.
* *Special files*: the mechanism used for input and output. Most special files are in /dev.
* *Links*: a system to make a file or directory visible in multiple parts of the system's file tree.
* *Sockets*: a special file type, similar to TCP/IP sockets, providing inter-process networking protected by the file system's access control.
* *Named pipes*: act more or less like sockets and form a way for processes to communicate with each other, without using network socket semantics.
