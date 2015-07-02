# Git for Type Designers

#### What is Version Control?

Version Control means keeping logical snapshots of a project. There are multiple options to consider for version control: The simplest approach is just duplicating and dating files, or adding version numbers, but that can get quite messy and confusing.

Version control is a very common workflow for anyone working with code. But also type designers can use version control, since they work with UFO files.

The UFO file format is text-based; this means that each glyph in a font has its own little XML-file. A UFO could theoretically be created and modified in a text editor. This opens it up for version control tools normally used only by software developers.

Version Control has the the following benefits:

* arbitrary snapshots of a project
* project log
* possibility of server-based backup

Version Control with Git adds the following:

* commits can be made even when offline
* complete project history is available to anyone with access to the repository (e.g. a Github user)
* popular web-based repo storage


#### About this Guide

This guide was first presented at TypeLab of Typographics conference New York. For the sake of better presentability and easier updates, it has been moved to a Git repository itself.

This guide is in no way complete; there are many guides to git out there, and it cannot possible compete with any of them. Instead, this guide tries to focus on the simple aspects of Git, which are needed by a type designer.

There are many UI applications available for Git. Since those are likely to 
change, and this guide would have a hard time keeping up. Therefore, the focus is on the easier 


## Using Git locally

### Start a new Repository
Version Control can start at any point in your project. No matter if you are 
just starting out or have worked on a project for years.
In the root level of your project folder, simply type:

```bash
git init
```

This will _initialize_ a new repository; and make the current folder (and its subfolders)
ready for version control with Git.


### Add files to the Repository

Git uses a three-level approach of looking at files. 

* the project folder, in which all the changes are made
* the “stage”, on which snapshots of files can be tracked
* the commit history, in which all the previous versions are

When the files in the project folder are modified, git recognizes there is a
difference.

```bash
git add fileName.txt
# add one specific file to stage

git add .
#add all files of the current folder (and its subfolders) to stage

git add -A
#add all files in the project to stage (even when not in root folder)
```


### Commit to the Repository

```bash
git commit -m 'New Small Caps'  
# the -m option allows adding the commit message immediately.  

git commit -am 'rounder bowl for b'
# the -a option adds all modified files to the commit.
# this only works for files that have been commited before.
```


### Helpers
```bash
git status
# see which files have been changed, which have been added, or deleted.

git log
# commit history with commit messages and changed files

git diff
# see what actually has changed

```


## Using Git with a Remote Server

Git repositories can be mirrored to a server very easily.
In GitSpeak, the online storage is called “Remote”.

Hosting Git repositories online has been popularized by services like
[GitHub](http://www.github.com) and [Bitbucket](http://www.bitbucket.com).

* [GitHub]: Free for open projects, $$$ for private projects.
* [BitBucket]: Free for open and private projects, $$$ for team projects.


```bash
git remote add origin https://github.com/user/repo.git
git remote add origin https://user@bitbucket.org/user/repo.git
# add connection to remote server

git push origin master
# push latest commits to server. the order is server-local.
# origin is the standard server name

git clone https://user@bitbucket.org/user/repo.git
# get a repo from github

git status
see current status of modified files

git pull
update local repo with new data from server
```

## Little Helpers

### The `.gitignore` file
It can be a good idea to exclude some files from ever being added to a Git repository. This is done with an invisible `.gitignore` file, which can contain single folder-or file names; and also wildcard search strings.
An example:

```bash
*.vfbak
*.pyc
.DS_Store

test/*

``` 
In the repository containing a `.gitignore` file like this, `vfbak` (FontLab backup) and `pyc` (compiled Python modules) files are never tracked.
Also, the `.DS_Store` (created by Finder) is omitted.
Finally, there might be a folder `test`, of which the contents are not important. It will not be added to the commit.

### The `--amend` command
Some

