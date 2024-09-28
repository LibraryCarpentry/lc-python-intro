---
title: Setup
---

## Installing Python Using Anaconda
Python is a popular language for research computing, and great for general-purpose programming as well. Installing all of its research packages individually can be a bit difficult, so we recommend Anaconda, an all-in-one installer.

Regardless of how you choose to install it, please make sure you install Python 3.6 or above. The latest 3.x version recommended on [Python.org][python] is fine.

We will teach Python using JupyterLab, a programming environment that runs in a web browser (JupyterLab will be installed by Anaconda). For this to work you will need a reasonably up-to-date browser. The current versions of the Chrome, Safari and Firefox browsers are all supported (some older browsers, including Internet Explorer version 9 and below, are not).

::::::::::::::::: tab

### Windows 

[Watch a video tutorial for Windows][video-windows].

1. Open [anaconda.com/download][anaconda-dl] with your web browser.
2.  Download the Anaconda for Windows installer with Python 3. (If you are not sure which version to choose, you probably want the 64-bit Graphical Installer *Anaconda3-...-Windows-x86_64.exe*)
3. Install Python 3 by running the Anaconda Installer, using all of the defaults for installation except make sure to check *Add Anaconda to my PATH environment variable*.

### Mac

[Watch a video tutorial for Mac][video-mac].

1. Open [anaconda.com/download][anaconda-dl] with your web browser.
2. Download the Anaconda Installer with Python 3 for macOS (you can either use the Graphical or the Command Line Installer).
3. Install Python 3 by running the Anaconda Installer using all of the defaults for installation.

### Linux

Note that the following installation steps require you to work from the shell. If you aren't comfortable doing the installation yourself stop here and request help from the workshop organizers.

1. Open [anaconda.com/download][anaconda-dl] with your web browser.
2. Download the Anaconda Installer with Python 3 for Linux.
3. Open a terminal window and navigate to the directory where the executable is downloaded (e.g., `cd ~/Downloads`).
4. Type `bash Anaconda3` and press <kbd>Tab</kbd> to auto-complete the full file name. The name of file you just downloaded should appear.
5. Press <kbd>Enter</kbd> (or <kbd>Return</kbd> depending on your keyboard). You will follow the text-only prompts. To move through the text, press <kbd>Spacebar</kbd>. Type `yes` and press <kbd>Enter</kbd> to approve the license. Press <kbd>Enter</kbd> (or <kbd>Return</kbd>) to approve the default location for the files. Type `yes` and press <kbd>Enter</kbd> (or <kbd>Return</kbd>) to prepend Anaconda to your PATH (this makes the Anaconda distribution the default Python).
6. Close the terminal window.

:::::::::::::::::::::::::

## JupyterLab
We will teach Python using JupyterLab, a part of a family of [Jupyter][jupyter] tools that includes Jupyter Notebook and JupyterLab, both of which provide interactive web environments where you can write and run Python code. If you installed Anaconda, JupyterLab is installed on your system. If you did not install Anaconda, you can [install JupyterLab][jupyter-install] on its own using conda, pip, or other popular package managers.

## Download the data

1. Download [this zip file][dataset] and save it to your Desktop. 
2. Unzip the ```data.zip``` file, which should create a new folder called ```data```.
3. Create a new folder on your Desktop called ```lc-python``` and put the ```data``` folder in this folder.

This lesson uses circulation data in multiple CSV files from the Chicago Public Library system. The data was compiled from records shared by the Chicago Public Library in [the data.gov catalog](https://catalog.data.gov/dataset/?q=chicago+%22circulation+by+location%22). Please do not download the circulation data from data.gov since the dataset you downloaded following the steps above has been altered for our purposes.

[python]: https://python.org/downloads
[video-windows]: https://www.youtube.com/watch?v=xxQ0mzZ8UvA
[anaconda-dl]: https://www.anaconda.com/download/
[video-mac]: https://www.youtube.com/watch?v=TcSAln46u9U
[jupyter]: https://docs.jupyter.org/en/latest/
[jupyter-install]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html
[dataset]: episodes/files/data.zip
