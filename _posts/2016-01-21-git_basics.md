---
layout: post
title: Git Basics
---

Before we resume our
[Introduction to Python]({{site.baseurl}}/2016/01/19/02_Introduction_to_Python/),
we will start with a short introduction to
[version control systems](http://swcarpentry.github.io/git-novice/reference.html#version-control)
and in particular [git](https://git-scm.com/).

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
provide free repositories in the cloud.



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
  
