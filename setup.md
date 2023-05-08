---
title: Setup
---

## Installing Python Using Anaconda

[Python][python] is great for general-purpose programming and is a popular language
for scientific computing as well. Installing all of the packages required for this
lessons individually can be a bit difficult, however, so we recommend the all-in-one
installer [Anaconda][anaconda].

Regardless of how you choose to install it, please make sure you install Python
version 3.x (e.g., Python 3.6 version). Also, please set up your Python environment at
least a day in advance of the workshop. If you encounter problems with the
installation procedure, ask your workshop organizers via e-mail for assistance so
you are ready to go as soon as the workshop begins.

### Windows - [Video tutorial][video-windows]

1. Open [anaconda.com/download][anaconda-dl]
  with your web browser.

2. Download the Python 3 installer for Windows.

3. Double-click the executable and install Python 3 using *MOST* of the
  default settings. The only exception is to check the
  **Make Anaconda the default Python** option.

### macOS - [Video tutorial][video-mac]

1. Open [anaconda.com/download][anaconda-dl]
  with your web browser.

2. Download the Python 3 installer for macOS.

3. Install Python 3 using all of the defaults for installation.

### Linux

Note that the following installation steps require you to work from the shell.
If you run into any difficulties, please request help before the workshop begins.

1. Open [anaconda.com/download][anaconda-dl] with your web browser.

2. Download the Python 3 installer for Linux.

3. Install Python 3 using all of the defaults for installation.
  
  a.  Open a terminal window.
  
  b.  Navigate to the folder where you downloaded the installer
  
  c.  Type
  
  ```bash
  $ bash Anaconda3-
  ```
  
  and press tab.  The name of the file you just downloaded should appear.
  
  d.  Press enter.
  
  e.  Follow the text-only prompts.  When the license agreement appears (a colon
  will be present at the bottom of the screen) hold the down arrow until the
  bottom of the text. Type `yes` and press enter to approve the license. Press
  enter again to approve the default location for the files. Type `yes` and
  press enter to prepend Anaconda to your `PATH` (this makes the Anaconda
  distribution the default Python).

## Starting Python

We will teach Python using [Spyder][spyder]. If you installed Python using Anaconda, Spyder should already be on your system. If
you did not use Anaconda, use the Python package manager pip
(see the [Spyder website][spyder-install] for details.)

To start Spyder, open a terminal or Git Bash and type the command:

```bash
$ spyder
```

To start the Python interpreter without Spyder, open a terminal
or Git Bash and type the command:

```bash
$ python3
```

[python]: https://python.org
[anaconda]: https://www.anaconda.com/distribution
[video-windows]: https://www.youtube.com/watch?v=xxQ0mzZ8UvA
[anaconda-dl]: https://www.anaconda.com/download/
[video-mac]: https://www.youtube.com/watch?v=TcSAln46u9U
[spyder]: https://www.spyder-ide.org/
[spyder-install]: https://docs.spyder-ide.org/installation.html



