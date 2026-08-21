---
title: Setup
---

## Installing Python Using Miniforge

[Python](https://python.org) is a popular language for scientific computing, and great for general-purpose programming as well. 
For this workshop we use Python version 3.x.
Installing all of its scientific packages individually can be a bit difficult, so we provide an environment file to help you take care of them all together.
We will use the _Miniforge_ distribution of Python.

Please refer to the [Python section of the workshop website for installation instructions](https://carpentries.github.io/workshop-template/install_instructions/#python).

## JupyterLab
We will teach Python using JupyterLab, a part of a family of [Jupyter][jupyter] tools that includes Jupyter Notebook and JupyterLab, both of which provide interactive web environments where you can write and run Python code. 
If you followed the instructions linked above, JupyterLab is installed on your system. 
Alternatively, you can [install JupyterLab][jupyter-install] on its own using conda, pip, or other popular package managers.

## Download the data

1. Download [this zip file][dataset] and save it to your Desktop. 
2. Unzip the ```data.zip``` file, which should create a new folder called ```data```.
3. Create a new folder on your Desktop called ```lc-python``` and put the ```data``` folder in this folder.

This lesson uses circulation data in multiple CSV files from the Chicago Public Library system. The data was compiled from records shared by the Chicago Public Library in [the data.gov catalog](https://catalog.data.gov/dataset/?q=chicago+%22circulation+by+location%22). Please do not download the circulation data from data.gov since the dataset you downloaded following the steps above has been altered for our purposes.

[python]: https://python.org/downloads
[video-windows]: https://www.youtube.com/watch?v=xxQ0mzZ8UvA
[video-mac]: https://www.youtube.com/watch?v=TcSAln46u9U
[jupyter]: https://docs.jupyter.org/en/latest/
[jupyter-install]: https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html
[dataset]: episodes/files/data.zip
