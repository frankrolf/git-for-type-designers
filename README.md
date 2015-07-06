# Git for Type Designers

#### What is Version Control?

Version control is keeping snapshots of a project at arbitrary points in time. There are multiple options to consider for version control: The simplest approach is just duplicating and dating files, or adding version numbers, but that can get quite messy and confusing.

Version control is a very common workflow for anyone working with code, and those people use dedicated version control systems like __Git__.
Some aspects of Git make is similar to a backup system like TimeMachine, but with much more actual control.

Any creative job on a computer could make use of version control, but type design especially is an ideal candidate for version control; since type designers work with [UFO][] files.

The [UFO file format][ufo] is perfect for version control, since it is text-based. A UFO is basically just a folder with many little XML-files in it. A UFO file could theoretically be created and modified in a text editor. This opens the field of digital type design for version control tools normally used only by software developers.



#### Glossary

If we imagine our whole project as a single drawing on paper, the mechanisms of version control (and Git) can easily be explained:

* __working directory:__ desk, the drawing is on it
* __repository:__ filing cabinet; contains previous copies of same drawing
* __stage:__ the hand while holding a copy of the drawing, ready to file
* __commit:__ the act of filing a copy of the latest drawing in the cabinet
* __remote:__ a 2nd filing cabinet of drawings in the attic
* __push:__ copy the contents of our filing cabinet (next to the desk) to the 2nd (attic) filing cabinet
* __pull:__ copy the latest drawings from the cabinet in the attic, and add them to the cabinet next to the desk.
* __fork:__ somebody makes a copy of the complete filing cabinet; or you make a copy of the filing cabinet in somebody else’s attic. A fork can transform into something totally different, or not continue its development at all.
* __pull request:__ Somebody has copied my whole cabinet, done some work on my drawing, and suggests that work might be interesting to me. I might accept or reject the suggestion.
* __clone:__ I don’t have a filing cabinet. Let’s get one from the store, where they have many.



#### Benefits of a Version Control System

* snapshots of a whole project can be created whenever needed
* frequent commit messages can create a project log
* possibility for server-based backup

Version Control with Git adds the following aspects:

* commits can be made even when offline (not dependent on server)
* complete project history is available to anyone with access to the repository (e.g. a Github user)
* there are popular platforms for storing and exploring repositories



#### About this Guide

A condensed version of this guide was first presented at the _TypeLab_ of the _Typographics_ conference in New York. For the sake of better presentability and easier updates, it has been moved to a Git repository itself.

This guide is in no way complete. There are many general guides on git out there, and this guide cannot possibly compete with any of them. Instead, this guide tries to focus on the simple aspects of Git which are needed by a type designer. 

Many UI applications are available for Git. Those are likely to 
change, and this guide would have a hard time keeping up. Therefore, the focus is on the bare-bones terminal commands.

If you have never used a terminal before: don’t worry – it’s easy!



## Using Git locally


### Start a New Git Repository
Version Control can start at any point in your project. No matter if just starting out, or if you have worked on a project for years. In the root level of your project folder, simply type:

```bash
git init
```

This command will _initialize_ a new repository; and make the current folder (and its subfolders) ready for version control with Git.



### Add files to the Repository

Git uses a three-level approach of looking at files. 

* the working directory, in which all the changes are made
* the _stage_, on which snapshots of files can be temporarily stored
* the commit history, in which all the previous versions are (all of which went through the stage). (See also the Glossary above).

When files in the project folder are modified, git recognizes they have changed. Git also notices when files are added or removed. To make those files eligible for the next commit, you have to add them to the stage like this:

```bash
git add fileName.txt
# add one specific file to stage

git add .
#add all files of the current folder (and its subfolders) to stage

git add -A
#add all files in the project to stage (even when not in root folder)
```

Adding files to the stage is usualy immediately followed by a commit:


### Commit to the Repository
A commit to a repository can mean _“This completes a logical step (add first iteration of Small Caps, for instance), let’s make a note of it.”_. Alternatively, it can also be _“I am scared of what comes next! Let’s save what we have, just in case anything breaks.”_

Commiting is crucial to keeping a history and log of your project. I usually commit after logical steps, several times during the day. The commit frequency depends on the working style, but it usually does not hurt making a commit to many.
There have been experiments with commiting after every save ([for the purpose of making a video][JeremieHornus]), but for a day-to-day workflow this is probably too extreme.

```bash
git commit -m 'New Small Caps'  
# the -m option allows adding the commit message immediately

git commit -am 'DIAGONALS!!'
# the -a option adds all modified files to the commit
# new files are not added; only works with files that have been commited earlier
```

Commit messages: I keep them brief but specific.
I also add the commit message right with the commit command, because otherwise an external editor opens. The external editor is _Vim_; many casual users will be confused by Vim.



### Helpers

Those commands all exist for use on the command line. In reality, I use them very rarely. That’s where a UI tool (like [SourceTree][]) comes in handy. Looking at the log of a specific file; seeing which files are currently changed; reverting a file to a specific commit. Nevertheless, here they are:


```bash
git status
# see which files have been changed, which have been added, or deleted.

git status --short
# same as above, but in a more compact notation

git log
# show the commit history with time stamps and commit messages

git log specificFile.txt
# show the commit for specificFile.txt

git diff
# see what actually has changed

```


## Using Git with a Remote Server

Git repositories can be mirrored to a server very easily. 
Hosting Git repositories on a server has been popularized by services like
[GitHub][] and [Bitbucket][].

* [GitHub][]: Free for open projects, $$$ for private projects.
* [BitBucket][]: Free for both open and private projects, $$$ for team projects.

Both hosting services require creating a user account. Once the account is created, repositories can either be started directly on the site, and then “cloned” to the local machine; or an already existing, local repository can be connected to the service.

For the sake of simplicity, the username assumed here is _user_; the repository is called _repo_.

```bash
git remote add origin https://github.com/user/repo.git
# add connection to remote server, Github-style

git remote add origin https://user@bitbucket.org/user/repo.git
# add connection to remote server, Bitbucket-style

# both commands connect to the URL of a remote git repository
# the server name "origin" is standard, but we could also write:
git remote add myFavoriteServer https://github.com/user/repo.git

```

To copy (backup) our work to the remote repository, the __push__ command (and an internet connection) is needed:

```bash
git push origin master
# push the latest commits
# from ”master” branch to the server called “origin” 

```

If the contents of a hosted git repository are needed, you can either download the .zip file from the site (boring!) or just clone the repo with `git clone`. The cloned repository will include all its history, logs, and previous revisions of itself.

```bash
git clone https://github.com/user/repo.git
# get a repo from github

```

To get the latest non-local changes of a repository, and make the local version equal to what is available online:

```bash
git pull
# update local repository with latest changes from server

```

## Little Helpers

### The `.gitignore` file
It might be a good idea to exclude some files from ever being added to a Git repository. This is done with an invisible `.gitignore` file, which can contain single folder-or file names; and also wildcard search strings.
An example:

```
*.vfbak
*.pyc
.DS_Store

test/*

``` 

The repository containing this `.gitignore` file will not track `.vfbak` (FontLab backup) and `.pyc` (compiled Python modules) files. Also, the `.DS_Store` file (created by Finder) is ignored.
Finally, there might be a folder `test`, of which the contents are not important. It will not be added to the commit.

The `.gitignore` file will be visibile as a new file the next time `git status` is run. One can decide if it is useful to have it be part of the repository or not – in this case, the `.gitignore` file itself can also be ignored.

### The `--amend` flag
Sometimes, mistakes happen. Typo in the commit message. Forgotten file.

```bash
git commit --amend -m 'Superior Petite Caps IPA'
# Replaces previous commit with a new commit (and a new commit message).
# In case there are any staged files, those are also committed.

```

## Advanced Git Operations

As mentioned above, this guide on Git is very simple. It only covers the necessities of someone who just wants versioning and a backup.

One very powerful operation which is not mentioned here is __branching__. 
Branching is great, good for collaboration or new departures; but it comes with its own set of problems. None of those problems I feel equipped to cover here. Look it up when you get there.


[bitbucket]: http://www.bitbucket.com
[github]: http://www.github.com
[SourceTree]: https://www.sourcetreeapp.com/
[UFO]: http://www.unifiedfontobject.org
[JeremieHornus]: https://twitter.com/JeremieHornus/status/612370888785285120/
