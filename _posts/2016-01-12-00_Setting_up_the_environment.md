---
layout: post
title: 00 Installing the environment
---

<!--
  SETUP
  Delete irrelevant sections from the setup instructions.  Each
  section is inside a 'div' without any classes to make the beginning
  and end easier to find.
  This is the other place where people frequently make mistakes, so
  please preview your site before committing, and make sure to run
  'tools/check' as well.
-->

The instructions were taken from [Software Carpentry](http://software-carpentry.org/), in particular
[David Dotson's recent workshop at ASU](http://smallerthings.org/2016-01-07_asu_physics/).

You will need to install

1. [The Bash Shell](#shell)
2. [Git](#git)
3. a [text editor](#editor) (by default, `nano`)
4. [Python](#python) (including a number of additional packages
required for scientific computing)

## Setup

<p>
  To participate in a the class, you will need
  access to the software described below. In addition, you will
  need an up-to-date web browser.
</p>
<p>
  SoftwareCarpentry maintains a list of common issues that occur during installation as a reference for instructors
  that may be useful on the
  <a href = "https://github.com/swcarpentry/workshop-template/wiki/Configuration-Problems-and-Solutions">Configuration Problems and Solutions wiki page</a>.
</p>

<div id="shell"> <!-- Start of 'shell' section. -->
  <h3>The Bash Shell</h3>

  <p>
    Bash is a commonly-used shell that gives you the power to do simple
    tasks more quickly.
  </p>

  <div class="row">
    <div class="col-md-4">
      <h4 id="shell-windows">Windows</h4>
      <ol>
        <li>Download the Git for Windows <a href="https://git-for-windows.github.io/">installer</a>.</li>
        <li>Run the installer and follow the steps bellow:
          <ol>
            <!-- Git 2.6.1 Setup -->
            <!-- Welcome to the Git Setup Wizard -->
            <li>Click on "Next".</li>
            <!-- Information -->
            <li>Click on "Next".</li>
            <!-- Select Destination Location -->
            <li>Click on "Next".</li>
            <!-- Select Components -->
            <li>Click on "Next".</li>
            <!-- Select Start Menu Folder -->
            <li>Click on "Next".</li>
            <!-- Adjusting your PATH environment -->
            <li>
              <strong>
                Select "Use Git from the Windows Command Prompt" and click on "Next".
              </strong>
                If you forgot to do this programs that you need for the workshop will not work properly.
                If this happens rerun the installer and select the appropriate option.
            </li>
            <!-- Configuring the line ending conversions -->
            <li>
              Click on "Next".
              <strong>
                Keep "Checkout Windows-style, commit Unix-style line endings" selected.
              </strong>
            </li>
            <!-- Configuring the terminal emulator to use with Git Bash -->
            <li>
              <strong>
                Select "Use Windows' default console window" and click on "Next".
              </strong>
            </li>
            <!-- Configuring experimental performance tweaks -->
            <li>Click on "Next".</li>
            <!-- Installing -->
            <!-- Completing the Git Setup Wizard -->
            <li>Click on "Finish".</li>
          </ol>
        </li>
      </ol>
      <p>This will provide you with both Git and Bash in the Git Bash program.</p>
    </div>
    <div class="col-md-4">
      <h4 id="shell-macosx">Mac OS X</h4>
      <p>
        The default shell in all versions of Mac OS X is Bash, so no
        need to install anything.  You access Bash from the Terminal
        (found in
        <code>/Applications/Utilities</code>). You may want to keep
        Terminal in your dock for this workshop.
      </p>
    </div>
    <div class="col-md-4">
      <h4 id="shell-linux">Linux</h4>
      <p>
        The default shell is usually Bash, but if your
        machine is set up differently you can run it by opening a
        terminal and typing <code>bash</code>.  There is no need to
        install anything.
      </p>
    </div>
  </div>
</div> <!-- End of 'shell' section. -->

<div id='git'> <!-- Start of 'Git' section. GitHub browser compatability
           is given at https://help.github.com/articles/supported-browsers/-->
  <h3>Git</h3>

  <p>
    Git is a version control system that lets you track who made changes
    to what when and has options for easily updating a shared or public
    version of your code
    on <a href="https://github.com/">github.com</a>. You will need a
    <a href="https://help.github.com/articles/supported-browsers/">supported</a>
    web browser (current versions of Chrome, Firefox or Safari,
    or Internet Explorer version 9 or above).
  </p>

  <div class="row">
    <div class="col-md-4">
      <h4 id="git-windows">Windows</h4>
      <p>
        Git should be installed on your computer as part of your Bash
        install (described above).
      </p>
    </div>
    <div class="col-md-4">
      <h4 id="git-macosx">Mac OS X</h4>
      <p>
        <strong>For OS X 10.9 and higher</strong>, install Git for Mac
        by downloading and running the most recent "mavericks" installer from
        <a href="http://sourceforge.net/projects/git-osx-installer/files/">this list</a>.
        After installing Git, there will not be anything in your <code>/Applications</code> folder,
        as Git is a command line program.
        <strong>For older versions of OS X (10.5-10.8)</strong> use the
        most recent available installer labelled "snow-leopard"
        <a href="http://sourceforge.net/projects/git-osx-installer/files/">available here</a>.
      </p>
    </div>
    <div class="col-md-4">
      <h4 id="git-linux">Linux</h4>
      <p>
        If Git is not already available on your machine you can try to
        install it via your distro's package manager. For Debian/Ubuntu run
        <code>sudo apt-get install git</code> and for Fedora run
        <code>sudo yum install git</code>.
      </p>
    </div>
  </div>
</div> <!-- End of 'Git' section. -->

<div id="editor"> <!-- Start of 'editor' section. -->
  <h3>Text Editor</h3>

  <p>
    When you're writing code, it's nice to have a text editor that is
    optimized for writing code, with features like automatic
    color-coding of key words.  The default text editor on Mac OS X and
    Linux is usually set to Vim, which is not famous for being
    intuitive.  if you accidentally find yourself stuck in it, try
    typing the escape key, followed by <code>:q!</code> (colon, lower-case 'q',
    exclamation mark), then hitting Return to return to the shell.
  </p>

  <div class="row">
    <div class="col-md-4">
      <h4 id="editor-windows">Windows</h4>
      <p>
        nano is a basic editor and the default that is used in the class.
        To install it,
        download the <a href="{{site.swc_installer}}">Software Carpentry Windows installer</a>
        and double click on the file to run it.
        <strong>This installer requires an active internet connection.</strong>
      </p>
      <p>
        Others editors that you can use are
        <a href="http://notepad-plus-plus.org/">Notepad++</a> or
        <a href="http://www.sublimetext.com/">Sublime Text</a>.
        <strong>Be aware that you must
          add its installation directory to your system path.</strong>
        Please ask your instructor to help you do this.
      </p>
    </div>
    <div class="col-md-4">
      <h4 id="editor-macosx">Mac OS X</h4>
      <p>
        nano is a basic editor and the default that instructors use in the workshop.
        It should be pre-installed.
      </p>
      <p>
        Others editors that you can use are
        <a href="http://www.barebones.com/products/textwrangler/">Text Wrangler</a> or
        <a href="http://www.sublimetext.com/">Sublime Text</a>.
      </p>
    </div>
    <div class="col-md-4">
      <h4 id="editor-linux">Linux</h4>
      <p>
        nano is a basic editor and the default that instructors use in the workshop.
        It should be pre-installed.
      </p>
      <p>
        Others editors that you can use are
        <a href="https://wiki.gnome.org/Apps/Gedit">Gedit</a>,
        <a href="http://kate-editor.org/">Kate</a> or
        <a href="http://www.sublimetext.com/">Sublime Text</a>.
      </p>
    </div>
  </div>
</div> <!-- End of 'editor' section. -->

<div id="python"> <!-- Start of 'Python' section. Remove the third paragraph if
           the workshop will teach Python using something other than
           the IPython notebook.
           Details at http://ipython.org/ipython-doc/2/install/install.html#browser-compatibility -->
  <h3>Python</h3>

  <p>
    <a href="http://python.org">Python</a> is a popular language for
    scientific computing, and great for general-purpose programming as
    well.  Installing all of its scientific packages individually can be
    a bit difficult, so we recommend
    <a href="https://www.continuum.io/anaconda">Anaconda</a>,
    an all-in-one installer.
  </p>

    <p>
      Regardless of how you choose to install it,
      <strong>please make sure you install Python version 3.x</strong>
      (e.g., 3.4 is fine).
    </p>

    <p>
      We will teach Python using the IPython notebook, a programming environment
      that runs in a web browser. For this to work you will need a reasonably
      up-to-date browser. The current versions of the Chrome, Safari and
      Firefox browsers are all <a
      href='http://ipython.org/ipython-doc/2/install/install.html#browser-compatibility'>supported</a>
      (some older browsers, including Internet Explorer version 9
      and below, are not).
    </p>

  <div class="row">
    <div class="col-md-4">
      <h4 id="python-windows">Windows</h4>
      <ol>
        <li>Open <a href="http://continuum.io/downloads">http://continuum.io/downloads</a> with your web browser.</li>
        <li>Download the Python 3 installer for Windows.</li>
        <li>Install Python 3 using all of the defaults for installation <em>except</em> make sure to check <strong>Make Anaconda the default Python</strong>.</li>
      </ol>
    </div>
    <div class="col-md-4">
      <h4 id="python-macosx">Mac OS X</h4>
      <ol>
        <li>Open <a href="http://continuum.io/downloads">http://continuum.io/downloads</a> with your web browser.</li>
        <li>Download the Python 3 installer for OS X.</li>
        <li>Install Python 3 using all of the defaults for installation.</li>
      </ol>
    </div>
    <div class="col-md-4">
      <h4 id="python-linux">Linux</h4>
      </p>
      <ol>
        <li>Open <a href="http://continuum.io/downloads">http://continuum.io/downloads</a> with your web browser.</li>
        <li>Download the Python 3 installer for Linux.</li>
        <li>Install Python 3 using all of the defaults for installation.
        (Installation requires using the shell. If you aren't
        comfortable doing the installation yourself
        stop here and request help at the workshop.)</li>
        <li>
          Open a terminal window.
        </li>
        <li>
          Type <pre>bash Anaconda-</pre> and then press
          tab. The name of the file you just downloaded should
          appear.
        </li>
        <li>
          Press enter. You will follow the text-only prompts.  When
          there is a colon at the bottom of the screen press the down
          arrow to move down through the text. Type <code>yes</code> and
          press enter to approve the license. Press enter to approve the
          default location for the files. Type <code>yes</code> and
          press enter to prepend Anaconda to your <code>PATH</code>
          (this makes the Anaconda distribution the default Python).
        </li>
      </ol>
    </div>
  </div>
</div> <!-- End of 'Python' section. -->

## Testing

### Bash shell

Open a *terminal* (Mac OS X, Linux) or open *Git Bash* (under
*All Programs/Git/Git Bash*) in Windows.

Type
```
echo $SHELL
```

Should show */usr/bin/bash* (or similar).

We use "shell" and "terminal" (and "console") pretty
interchangeably.

### Git

In the shell, type
```
git --version
```
which should show something like

```
git version 2.7.0
```

### Python

In the shell, type

```
python -c 'import sys; print(sys.version)'
```

which should give something similar to 

```
3.5.1 |Anaconda 2.4.1 (64-bit); (default, Dec  7 2015, 15:00:12)
```

(and more stuff). Important: you should have Python 3, i.e., a version
like 3.4. or 3.5.


