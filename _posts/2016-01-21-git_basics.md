---
layout: post
title: Git Basics
---

Before we resume our
[Introduction to Python]({{site.baseurl}}/2016/01/19/02_Introduction_to_Python/),
we will start with a short introduction to
[version control systems](http://swcarpentry.github.io/git-novice/reference.html#version-control)
and in particular [Git](https://git-scm.com/).[^0]

A **version control system** (VCS) manages files and tracks changes to
those files. It stores the complete **history** and allows you to
recover files at any stage of the history (think "undo" to the
beginning). Any serious software project uses version control but its
uses go beyond software, e.g., documents and data can also be version
controlled.

![PhD Comics: "FINAL".doc (c) 2012 Jorge Charm](http://www.phdcomics.com/comics/archive/phd101212s.gif)

A set of changes is called a **commit**. It typically contains changes
to multiple files. It also contains a timestamp, information about
the user who made the changes, and a **commit message** that explains the
changes. The history consists of all the commits. The VCS stores the
history in a storage area called a **repository**.

Modern distributed VCS such as *Git* or *mercurial* make it easy for
multiple developers to work on the same project. They have support for
**merging changes** from different people into a single new file, and
for **resolving conflicts**, i.e., the case when the same part of a
file was changed (the changes "collided"). Online platforms such as
[GitHub](https://github.com) or [Bitbucket](https://bitbucket.org/)
provide free repositories in the cloud (but you don't need these
platforms to use a VCS!).

We will use [Git](https://git-scm.com/). For the class you should get
into the habit to version-control your work: in class notes, home
works, and projects. You will later use GitHub to submit code that you
develop as part of your assignments and projects.

1. [Tutorial](#tutorial)
2. [Set up your own GitHub repositories](#set-up-your-own-github-repositories)
3. [Class resources on GitHub](#class-resources-on-github)
4. [Additional resources](#more)

## Tutorial
Let's use `git` to manage what we have done so far.

### Configuring Git ###

The first time you use `git` you need to tell it who you are: this
information will be the user information in the commit history. (*Use
your own name and email address!*)

{% highlight bash %}
git config --global user.name "Darth Vader"
git config --global user.email "dvader@empire.gov"
git config --global color.ui "auto"
{% endhighlight %}

You also tell it how to color output and what editor to use to write
commit messages [^1].

{% highlight bash %}
# choose your favorite editor
# Windows users: First try without executing this command.
#                If you have problems with 'git commit' later, ask!
git config --global core.editor "nano -w"
{% endhighlight %}

You can see a list of all your configuration settings with `git config
--list`.


Git commands always follow the pattern `git <verb> [options]
[arguments ...]`. In particular, `--help` is always an option. Also
try `git help` and `git help tutorial`.


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

(Use `git reset FILENAME` to unstage any files that you might have
added accidentally.)

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
* After you wrote and saved the message (in `nano`, `^O`; in `vim`,
  `i` to write, `ESC :wq` to save and exit) and exited (`^X` in
  `nano`), your changes will be committed to the repository.
* You can also supply the message as an argument: `git commit -m "one
  line summary of changes"`.
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

If you haven't
[done so earlier]({{site.baseurl}}/2016/01/14/01_Unix_Shell/#using-git-to-get-data-for-the-class),
clone the repository where code and data will be posted:

~~~
cd ~
git clone https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources.git
cd PHY494-resources
~~~

Note:

* The local name of your repository can be any name you like but it is
  customary (and less confusing) if you go with the default, which is
  the remote repository name without the ".git" suffix, i.e.,
  *PHY494-resources* for us.
* For all other `git` commands you *must* be *inside* your local
  repository:

		cd ~/PHY494-resources


Update your local repository with any "upstream" changes:

~~~
git pull
~~~

Update the remote repository with you local changes (commits):

~~~
git push
~~~

(For "pushing" to work, you must be allowed to write to the remote
repository; this will not work for *PHY494-resources* but we will use
it below for
[your own GitHub repositories](#set-up-your-own-github-repositories)).

### Contributing to Open Source on GitHub

GitHub enables you to easily contribute to other projects. This
includes

* filing bug reports or feature requests (*raising issues*); for
  instance, if you do not agree with some of the Star Wars data from
  the previous lessons, raise an issue in the
  [issue tracker for the PHY494-auxilliary repository](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-auxilliary/issues).
* proposing to add your own code and changes through
  *[pull requests](https://help.github.com/articles/using-pull-requests/)*
  (but this is too advanced for a our short introduction today --- see
  the additional resources under [More...](#more)).


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

   You only need the `--set-upstream origin master` (or `-u origin
   master`) for the first time (it tells git which "branches" to
   associate with each other in local and remote) [^4]. All further
   push operations will then simply be

		git push

   Look at the web interface at
   https://github.com/USERNAME/PHY494-class and see your changes
   appear.

For the rest of the semester, commit what you did during each class
session to the repository.

## Class resources on GitHub

Notebooks and files are being made available on GitHub in the
repository
[ASU-CompMethodsPhysics-PHY494/PHY494-resources](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources). If
you have not done so already:

~~~
cd ~
git clone https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources.git
~~~

Update:

~~~
cd ~/PHY494-resources
git pull
~~~

You should get a new file, `02_python/02-intro-python.ipynb`. Copy it
to *your* class directory:

~~~
cp ~/PHY494-resources/02_python/02-intro-python.ipynb ~/PHY494/02_python/
~~~

and create a new commit with it:

~~~
cd ~/PHY494/02_python/
git add 02-intro-python.ipynb
git commit -m "Lesson 02 Intro to Python notebook"
~~~

Open the notebook (`jupyter notebook`) and then we will continue with
[02 Introduction to Python]({{site.baseurl}}/2016/01/19/02_Introduction_to_Python/).

At the end of today's class, commit your changes to the notebook and
push to your github repository.


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

[^0]:

     Acknowledgements: This lesson uses ideas from Software
     Carpentry's
     [Version Control with Git](http://swcarpentry.github.io/git-novice/)
     and includes an image from Jorge Cham's
     [PhD Comics](http://www.phdcomics.com/)
     ["FINAL".doc](http://www.phdcomics.com/comics.php?n=1531) (which is &copy; 2012 Jorge Cham).

[^1]:

     See also Software Carpentry's list of
     [git configuration options for different editors](http://swcarpentry.github.io/git-novice/02-setup.html).

	 For problems with setting up editors in Windows, see the
     StackOverflow question
     [How can I set up an editor to work with Git on Windows?](http://stackoverflow.com/questions/10564/how-can-i-set-up-an-editor-to-work-with-git-on-windows)
     as a starting point for various recipes.
	 
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

[^4]:

    *Branching* is a more advanced topic, which is explained in the
    materials linked under [More...](#more). We barely scratched the
    surface of Git but this will be sufficient to already make good
    use of this very powerful tool.
