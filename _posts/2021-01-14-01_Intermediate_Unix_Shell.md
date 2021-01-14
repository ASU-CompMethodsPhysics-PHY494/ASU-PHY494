---
layout: post
title: 01' Intermediate Shell Hacks (optional)
date: 2021-01-14 15:00:00
weight: 20
---

The real power of the [shell]({{ site.baseurl }}{% post_url
2021-01-14-01_Unix_Shell %}) lies in the fact that one can combine
multiple shell commands and in this way automate pretty much any task
that operates on files and directories. The two major ways to combine shell commands are

* pipes, filters, and redirection
* shell scripts

"Pipes" feed the output from one command to the input of another
command and in this way combine multiple tools for filtering data.

"Scripts" are text files that contain multiple commands (including
pipes). Executing the file will the nexecute all the commands, without
having to type them repeatedly. The bash shell is actually a complete
programming language and one can accomplish rather complicated tasks
with it.

The following is very useful but for right now not essential and is
*optional*. **You can work through the tutorial in your own time.**

* [Pipes and Filters](#pipes-and-filters)
* [Using `git` to get data for the shell example](#using-git-to-get-data-for-the-class) (we will do this again in the lesson on version control and `git`)
* [Shell scripts](#shell-scripts)


### Pipes and Filters ###

#### Commands ####

* `cat`
* `head`
* `tail`
* `less`
* `wc`
* `sort`
* `uniq`
* `cut` and `paste`
* `grep`

and special shell characters

* `|` ("pipe", joins commands together)
* `>` (redirects output to a file)
* `<` (redirects file to input)

#### Working with redirection and command pipelines ####

Download [planets.dat]({{site.baseurl}}/{{site.data}}/planets.dat)[^3]
and put it in the directory `data/`. You can do this with your web
browser or if you have the `curl` program installed, try

{% highlight bash %}
curl {{site.url}}{{site.baseurl}}/{{site.data}}/planets.dat -O
{% endhighlight %}

(all on one line).

Output the whole file to the screen:

{% highlight bash %}
cat planets.dat
{% endhighlight %}

Look at the first three lines of the file

{% highlight bash %}
head -3 planets.dat
{% endhighlight %}

should give

~~~
Alderaan             12500  grasslands/mountains
Yavin_IV             10200  jungle/rainforests
Hoth                  7200  tundra/icecaves/mountainranges
~~~
{: .output}

Count the number of planets

{% highlight bash %}
wc planets.dat
{% endhighlight %}

~~~
      60     180    2944 planets.dat
~~~
{: .output}

Make a file in which all planets are duplicated:

{% highlight bash %}
cat planets.dat planets.dat > planets_2.dat
{% endhighlight %}

(`cat` concatenates files and then you redirect it to a new file.)


##### Activity #####

1. Test that `wc -l` gives just the number of lines ("60").
2. What does `wc planets.dat planets_2.dat` do?
3. What happens when you do `wc < planets.dat`?
4. Run `wc` then type any number of lines of text (pressing enter
   to terminate each line) and when you get bored, press `^D`
   (control+D). What happened?

##### Pipes #####

Sort by name and look at the first five using a **pipes** and
**filters**:

{% highlight bash %}
sort planets.dat | head -5
{% endhighlight %}

Sort by diameter (`-k2,2` is column 2 and numeric sort `-n`), biggest
first (`-r` reverse sort), and write the top 3 to a file
`biggest_planets`:

{% highlight bash %}
sort -k2,2 -n -r planets.dat | head -3 > biggest_planets
{% endhighlight %}

Count the number of planets with unknown diameter:

{% highlight bash %}
grep "unknown" planets.dat | wc -l
{% endhighlight %}

Get the first letter of each planet name and sort alphabetically:

{% highlight bash %}
cut -b 1,1 planets.dat | sort
{% endhighlight %}

Get the terrain types

{% highlight bash %}
cut -b 29-  planets.dat
{% endhighlight %}

#### Activity ####

1. Count the number of planets in `planets_2.dat`.
2. Find planets where the rebel might have a base (hint: you know it's
   cold there... use `grep`). How many planets will you investigate
   more closely? Write the list to the file `bases`.
3. How many *unique* terrain types are there? (Hint: `uniq` needs a
   sorted list as input)
4. What is the most frequent and the least frequent first letter
   amongst these planets? (Hint: `uniq -c`)


#### Shell glob patterns ####

Use the character `*` to match "any part of a file name", e.g.

{% highlight bash %}
ls *.dat
{% endhighlight %}

will list all files ending in `.dat`.

The `?` character matches a single character. Neither of them matches
a leading `.` in a file name or a space.


## Using `git` to get data for the class ##

`git` is a version control software and we will come back to explain
its main functionality later. Right now we use it as a convenient tool
to get additional data. 

There is a "repository" at
<https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources>
that contains data and code to be used during the class. It will be
updated as we go along.

Get the data for today by **cloning** the repository:

~~~
cd ~
git clone https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources.git
~~~

(You only need to do this *once*.)

At any later time, **pull** in the latest updates from inside the
repository::

~~~
cd PHY494-resources
git pull
~~~

(This can be done as often as you like.)

Go into the `PHY494-resources/01_shell/data` directory.

### Activity

1. Read the `README` file (e.g. using `atom` or `cat` or `less` (for
the latter, use `h` to get help and `q` to quit)).

2. Count the number of entries in *all files ending in "csv"*. (Hint:
use a glob pattern)

3. Use `cut -f 1  -d ',' people.csv` to extract each name to a file
`names` and a similar command to extract weight to a file `weights`.

4. Use the `paste` command to generate a new list that contains
   "weight name" (reordered and separated by space):

        paste weights names

   Use this approach to sort the people in order of decreasing weight.

## Shell scripts

You can save commands in a file. This is called a **script**. A script
allows you to reuse commands (laziness is a programmer's virtue!)
without having to retype them over and over again. It also allows you
to solve a task once and then forget about how you did it in detail
because it is written in the script.

Make directory `~/bin` for your scripts in your home directory.

{% highlight bash %}
mkdir ~/bin
{% endhighlight %}

(I strongly suggest you do this really in your home directory because
in the following I will assume it; if you changed the path to
e.g. `~/classes/2016/PHY494/bin` then you will need to use that path
in all the following examples.)

Using`atom`, create the following script `~/bin/update_resources.sh`:

{% highlight bash %}
# PHY 494 script to update the resources repository

GIT_REPOSITORY="${HOME}/PHY494-resources"

cd "${GIT_REPOSITORY}"
git pull

echo "Updated resources in ${GIT_REPOSITORY}"
{% endhighlight %}

(You create the script by (1) `atom ~/bin/update_resources.sh` (opens
empty file if it does not exist), (2) type all the lines into the
editor (or copy & paste), (3) save the file and exit the editor.)

Notes:

* *All* the lines above should be in your file (first line will start
  with `# PHY 494` and the last line will begin with `echo`).

* The line starting with `#` is a *comment*: it is not a shell command
  and is ignored by the shell. However, adding comments to scripts is
  **a really, really good idea!**

* The shell has **variables**: Some like `HOME` are pre-defined,
  others you can define yourself (`GIT_REPOSITORY=...`). Using
  all-caps is a convention that you should follow.

  The contents (value) of variables is accessed with the dollar `$`
  sign in front of the variable name.

* `echo` prints to the standard output (typically, the screen)

Execute the script with

{% highlight bash %}
bash ~/bin/update_resources.sh
{% endhighlight %}

It should show output similar to 

~~~
Already up-to-date.
Updated resources in /Users/oliver/PHY494-resources
~~~

However, during the course of the year more data will be added to the
repository and then you can just run your update command to get the
data and you might see output like the following:

~~~
remote: Counting objects: 15, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 15 (delta 2), reused 15 (delta 2), pack-reused 0
Unpacking objects: 100% (15/15), done.
From https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources
   c3b5c04..23a4083  master     -> origin/master
Updating c3b5c04..23a4083
Fast-forward
 01_shell/bin/update_resources.sh | 8 ++++++++
 02_python/gutentag.py            | 4 ++++
 2 files changed, 12 insertions(+)
 create mode 100644 01_shell/bin/update_resources.sh
 create mode 100644 02_python/gutentag.py
Updated resources in /Users/oliver/PHY494-resources
~~~

------------------------------------------------------------

##### Footnotes #####

[^0]:

    You can also see if you have the [`tree`](https://manpages.debian.org/stretch/tree/tree.1.en.html) command installed, which
	shows you beautiful directory trees:
	
	    $ tree ~dvader
		/home/dvader/
		├── Documents
		│   ├── deathstar
		│   │   ├── electrical_bill.dat
		│   │   └── weaknesses.txt
		│   └── work
		└── data
			├── bases
			└── planets.dat
    			
    `tree` is typically *not* included with git-bash.


[^1]:

    If you *must* need spaces then enclose the string in single or
    double quotes, e.g., `'/c/Program Files/'` or `"/c/Program
    Files"`. Double quotes admit shell variable expansions, single
    quotes do not. Note that a tilde `~` within quotes will *not*
    expand to the home directory!


[^2]: 

    **Upgrading nano**: If you are using `nano` as your editor then you want to
    enable a few useful features including syntax highlighting. The
    easiest way is to download the config files as the zip file
    [nanoconfig.zip]({{site.baseurl}}/{{site.siteresources}}/nanoconfig.zip)
    and unpack them in your home directory (`curl` can be used to
    download a file directly instead of having to use the browser):

        cd 
        curl {{site.url}}{{site.baseurl}}/{{site.siteresources}}/nanoconfig.zip -O
        unzip nanoconfig.zip

	This should create the files `~/.nanorc` (which you can edit to
	customize further) and the directory `~/.nano`.

[^3]:

	Star Wars data courtesy of [SWAPI](https://swapi.dev/). See
	[PHY494-auxilliary/star_wars](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-auxilliary/tree/master/star_wars)
	for Python code to pull the data from SWAPI.

[^4]:

    If you cannot start `atom` from the commandline, go back to
	[Setting up the Environment: Testing: editor (atom)]({{ site.baseurl }}{% post_url
    2021-01-12-00_Setting_up_the_environment %}#from-the-shell) and follow
    the steps described there.
