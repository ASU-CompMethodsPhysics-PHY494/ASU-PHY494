---
layout: post
title: Git Basics
---

Before we resume our
[Introduction to Python]({{site.baseurl}}/2016/01/19/02_Introduction_to_Python/),
we will start with a short introduction to
[version control systems](http://swcarpentry.github.io/git-novice/reference.html#version-control)
and in particular [Git](https://git-scm.com/).

A **version control system** (VCS) manages files and tracks changes to
those files. It stores the complete *history* and allows you to
recover files at any stage of the history (think "undo" to the
beginning). Any serious software project uses version control but its
uses go beyond software, e.g., documents and data can also be version
controlled.

A set of changes is called a *commit*. It typically contains changes
to multiple files. It also contains a timestamp, information about
the user who made the changes, and a *log message* that explains the
changes. The history consists of all the commits. The VCS stores the
history in a storage area called a *repository*.

Modern distributed VCS such as *Git* or *mercurial* make it easy for
multiple developers to work on the same project. They have support for
*merging* changes from different people into a single new file, and
for resolving *conflicts*, i.e., the case when the same part of a file
was changed (the changes "collided"). Online platforms such as
[GitHub](https://github.com) or [Bitbucket](https://bitbucket.org/)
provide free repositories in the cloud (but you don't need them to use
a VCS!).

We will use [Git](https://git-scm.com/). For the class you should get
into the habit to version control your work, both in class, home
works, and projects. You will later use GitHub to submit code that you
develop as part of your assignments and projects.

1. [Tutorial](#tutorial)
2. [Set up your own GitHub repositories](#set-up-your-own-github-repositories)
3. [Additional resources](#more)

## Tutorial
Let's use `git` to manage what we have done so far.

### Configuring Git ###

The first time you use `git` you need to tell it who you are: this
information will be the user information in the commit history. (*Use
your own name and email address!*)

~~~
git config --global user.name "Darth Vader"
git config --global user.email "dvader@empire.gov"
git config --global color.ui "auto"
git config --global core.editor "nano -w"
~~~

You also tell it how to color output and what editor to use to write
commit messages [^1]. You can see a list of all your configuration
settings with `git config --list`.


Git commands always follow the pattern `git <verb> [options]
[arguments ...]`. In particular, `--help` is always an option.


### Creating a repository ###

You alread should have a `PHY494` directory in your home directory
with a layout like the following (where `01_shell` might contain
other folders and documents):

~~~
~/PHY494/
        01_shell/
        02_python/
		         gutentag.py
~~~

Make the `PHY494` directory a **repository** with the `git init` command:

~~~
cd ~/PHY494
git init
~~~

That's it. Although, not much happened yet... except, check with

~~~
ls -la
~~~

A new hidden directory `~/PHY494/.git/` appeared. This is your actual
repository where Git stores all its information. **Do not change
anything in this directory** (unless you really know what you are
doing) and **do not delete the `.git`** directory. If you delete it,
your repository is irrevocably gone (and there is no undo for that!).

Now try the (possibly) most-used git command:

~~~
git status
~~~


### Adding files ###

Prepare the files to be committed to the repository: `git add` adds
files and directories to a "staging area":

~~~
git add .
git status
~~~

(Use `git rm --cached FILENAME` to unstage.)

The files are not committed yet. You can do more work, add more files...


### Committing ###

~~~
git commit
~~~

* When your editor pops up, enter a **commit message**: Convention:
  - first line (<60 char): one line summary
  - second line: blank
  - third and following lines: more details
  The first line is mandatory (you cannot have a commit without a
  message), the rest is optional.
* After you wrote the message (in `nano`, `^O`) and exited (`^X`),
  your changes will be committed to the repository.
* Check the status with `git status`...

For a new commit, [add files](#adding-files) and [commit](#committing)
again.

### History

Read the history with

~~~
git log
~~~


### Removing and renaming files

Removing files and directories via git allows you to get them back later.

~~~
git rm FILENAME
git rm -r DIRECTORY
~~~

Renaming is the same as removing the old file and adding the new one
but there is also a simple command

~~~
git mv OLD NEW
~~~

The `git rm` and `git mv` commands are similar to the `git add`
command in that they stage these changes; you still have to
[commit](#committing) them.


### Working with remote repositories

Initialize a local repository from a remote source:

~~~
git clone URL
~~~

Update your local repository with any "upstream" changes:

~~~
git pull
~~~

Update the remote repository with you local changes (commits):

~~~
git push
~~~

(For pushing to work, you must be allowed to write to the remote
repository.)

## Set up your own GitHub repositories

1. Go to <https://github.com> and create a new account. It is
   free.[^2] Remember your
   GitHub **username** and the **password**.
2. Create a new repository *PHY494-class*.
3. Note the repository URL
   https://github.com/USERNAME/PHY494-class.git
4. Add the remote repository to your repository (replace *USERNAME*
   with your GitHub username):

        git remote add origin https://github.com/USERNAME/PHY494-class.git

   We named the remote "origin", which is a common choice for the main
   repository. You can have many different remotes, just give them
   different names. You can list them with

		git remote -v

5. **push** your local history to the remote repository:

		git push --set-upstream origin master

   You need to enter your username and password [^3].

   You only need the `--set-upstream origin master` for the first time
   (it tells git which "branches" to associate with each other in
   local and remote). All further push operations will then simply be

		git push

   Look at the web interface at
   https://github.com/USERNAME/PHY494-class and see your changes
   appear.

For the rest of the semester, commit what you did during each class
session to the repository.


## More... ##

* For a longer introductory tutorial see the Software Carpentry lesson on
  [Version Control with Git](http://swcarpentry.github.io/git-novice/).
* Interactive in-browser lesson [Try Git](http://try.github.com/),
  takes 15 minutes.
* Blischak JD, Davenport ER, Wilson G
  (2016). [A Quick Introduction to Version Control with Git and GitHub](http://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004668). PLoS
  Comput Biol 12(1): e1004668. doi:10.1371/journal.pcbi.1004668 
* For in-depth discussion read the
  [Pro Git](https://git-scm.com/book/) book by Scott Chacon and Ben
  Straub.
  

#### Footnotes

[^1]:

     See also Software Carpentry's list of
     [git configuration options for different editors](http://swcarpentry.github.io/git-novice/02-setup.html).
	 
[^2]:

     An unlimited number of *public* (i.e., visible for everyone)
     repositories are free on GitHub but private repositories cost
     money. However, if you use your school email address
     (e.g. @asu.edu) you can get a limited number of private
     repositories for free(?) through the
     [GitHub educational discount](https://help.github.com/articles/discounted-private-accounts/).
	 
[^3]:

     There are ways to set up remote repositories so that you don't
     have to provide username and password for every push and which
     are also more secure. Namely one can use SSH keys instead of the
     HTTPS protocol, as described in the GitHub tutorial on
     [Generating SSH keys](https://help.github.com/articles/generating-ssh-keys/).
