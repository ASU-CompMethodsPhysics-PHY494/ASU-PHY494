---
layout: post
title: 02 Introduction to Python
---

The [Python](http://www.python.org) programming language is used
widely in the sciences, the computational physics, biology, and
economics/quantitative finance
communities, and in big companies such as Google and Facebook.

For this class we are using **Python 3** (e.g. Python 3.4 or Python
3.5), which is the current standard. A lot of older code is still only
available for Python 2.7 (and there are a number of sometimes subtle
incompatibilities between 2 and 3) but once you know Python 3 you will
have no problems dealing with Python 2 code.

1. [Resources](#resources)
2. [Starting Python](#starting-python)
3. [Tutorial](#tutorial)

# Resources

* Official [Beginner's Guide to Python](https://www.python.org/about/gettingstarted/)
* Official [Python 3 Tutorial](https://docs.python.org/3/tutorial/)
* [Python Scripting for Computational Science](http://www.springerlink.com/content/978-3-540-73915-9/), Hans Petter Langtangen. Texts in Computational Science and Engineering, Volume 3, 2008. Springer. DOI: [10.1007/978-3-540-73916-6](http://dx.doi.org/10.1007/978-3-540-73916-6) (free access to the [PDF](http://link.springer.com.ezproxy1.lib.asu.edu/book/10.1007%252F978-3-540-73916-6) through the ASU Library — requires ASU login)

Keep the [Python documentation](http://www.python.org/doc/) close by
and have a look at [Python questions on StackOverflow](http://stackoverflow.com/questions/tagged/python).

# Starting Python

## Starting the Python Interpreter

Python is an interpreted language and the Python interpreter is called
... `python`. In the shell, type

{% highlight bash %}
python
{% endhighlight %}

and you should see something similar

~~~
Python 3.5.1 (default, Dec  6 2015, 22:55:58)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
~~~

The symbol `>>>` is the standard input prompt. Type commands and
submit them to the interpreter with `Enter`.

To *exit*, type

{% highlight python %}
exit()
{% endhighlight %}

## Running a Python script

Create a simple Python program (or "script"), e.g. using `nano`, and
save it as `gutentag.py`.

{% highlight python %}
import os

homedir = os.environ['HOME']
print("Guten Tag, Dein Heimatverzeichnis ist ", homedir)
{% endhighlight %}

Let Python execute the command:

{% highlight bash %}
python gutentag.py
{% endhighlight %}

## Interactive Python with `ipython`

The [ipython](http://ipython.org) interpreter is like Python but with
*lots* of improvements such as `TAB`-completion, help with `command?`
(one question mark directly following a command) and source code with
`command??` (two question marks), commandline history, and many
additional shell-like commands (so-called "magic" commands such as
`%cd`, `%ls`, `%pwd`, `%run`, `%time` and `%timeit` --- see `%magic`
for help).

To exit, give the `exit()` command or `^D` (`Control` + `D`).

Just use `ipython` instead of `python` for interactive work.


## Interactive Python with the Jupyter notebook

Start the [Jupyter](http://jupyter.org) notebook interface (formerly
called *ipython notebook*) with

{% highlight bash %}
jupyter notebook
{% endhighlight %}

and open <http://localhost:8888> with a modern browser. (Note:
`ipython notebook` will also work but the name was recently
changed.)

We will often use the notebook interface to develop and demonstrate
code. It is perfect for prototyping and quick analysis tasks as well
as plotting.

To open a new notebook: Go to the *New* menu and choose under
*Notebooks: Python 3*. This will open a new browser window with an
empty notebook. Press `ESC` and then `H` for help.

A notebook has two modes, command mode and edit mode. 

* `ESC` enables **command mode** with the following useful commands:
  * `H` for help
  * cursor keys: move between cells
  * `B` for new cell below
  * `A` for new cell above
  * `X` to cut cell
  * `M` to turn a cell into a text cell for notes
  * `1` – `6` to make a text heading at level 1, 2, ... 6
* `Enter` enables **edit mode** (type in a cell)
* Cells can be executed by the Python "kernel" in either mode with
    * `Control + Enter`: execute a cell
    * `Shift + Enter`: execute cell and move one cell down
    * `Alt + Enter`: execute cell and create a new one
* Give the notebook a name by editing "Untitled" in the top bar.
* Save with `S` in command mode (or use the mouse)
* You can move between cells to edit code and rerun. As long as you
  don't quit or restart the Python kernel, you have information from
  all cells available in the whole notebook. If you open it new, you
  have to evaluate all cells again.


# Tutorial

The tutorial will be live-coded in a
[Jupyter notebook](#interactive-python-with-the-jupyter-notebook). Open
a new notebook and follow my lead. Type and run commands. Ask
questions (use red stickies when stuck).

After the class, this link to the [tutorial notebook](http://nbviewer.jupyter.org/github/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/02_python/02-intro-python.ipynb) will be
enabled. The notebook is stored in the git repository
[ASU-CompMethodsPhysics-PHY494/PHY494-resources](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources):
`git pull` to update and find [PHY494-resources/02_python/02-intro-python.ipynb](https://github.com/ASU-CompMethodsPhysics-PHY494/PHY494-resources/blob/master/02_python/02-intro-python.ipynb).





