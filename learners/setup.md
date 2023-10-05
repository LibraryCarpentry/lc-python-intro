---
title: Setup
---

## Installing Python Using Anaconda

[Python][python] is a popular general-purpose programming language, one that is commonly used for academic and scientific computing applications. Rather than installing each of the different packages required for this lesson on their own, we recommend downloading and installing [Anaconda][anaconda], which packages together Python, JupyterLab, and many common Python libraries that we'll use in the lesson.

Regardless of how you choose to install it, please make sure you install Python version 3.x (e.g., Python 3.6 version). Also, please set up your Python environment at least a day in advance of the workshop. If you encounter problems with the installation procedure, ask your workshop organizers via e-mail for assistance so you are ready to go as soon as the workshop begins.

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

## JupyterLab

We will teach Python using JupyterLab, a part of a family of [Jupyter][jupyter] tools that includes Jupyter Notebook and JupyterLab, both of which provide interactive web environments where you can write and run Python code. If you installed Anaconda, JupyterLab should already be on your system. If you did not install Anaconda, you can [install JupyterLab][jupyter-install] on its own using conda, pip, or other popular package managers.

## Download the data

This lesson uses a dataset comprised of circulation data across multiple CSV files from the Chicago Public Library system. The data was compiled from datasets shared by the Chicago Public Library system in [the data.gov catalog](https://catalog.data.gov/dataset/?q=chicago+%22circulation+by+location%22). Please do not download the CSV files directly from data.gov since the dataset we'll use has been cleaned to make it easier to work with.

1. Create a new folder on your Desktop called ```lc-python```.
2. Download [this zip file][dataset] and save it in the ```lc-python``` folder you just created. 
3. Unzip the ```lc-python-circ.zip``` file, which should create a new folder called ```lc-python-circ```.

[python]: https://python.org
[anaconda]: https://www.anaconda.com/distribution
[video-windows]: https://www.youtube.com/watch?v=xxQ0mzZ8UvA
[anaconda-dl]: https://www.anaconda.com/download/
[video-mac]: https://www.youtube.com/watch?v=TcSAln46u9U
[jupyter]: https://docs.jupyter.org/en/latest/
[jupyter-install]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html
[dataset]: episodes/files/lc-python-circ.zip


