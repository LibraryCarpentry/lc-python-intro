---
title: Getting Started
teaching: 15
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Learners can launch JupyterLab
- Learners are able to use the Jupyter Lab interface
- Learners are able to write and run Python code in JupyterLab 
- Learners are able to save their code as an iPython notebook (.ipynb) file 
- Learners can use the different buttons and features in JupyterLab

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How do I use JupyterLab?
- How can I run Python code in JupyterLab?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use JupyterLab to edit and run Python code.
  
If you haven't already done so, see [the setup instructions](../learners/setup.md) for details on how to install JupyterLab and Python via Anaconda. The setup instructions also walk you through the steps you should follow to create an 'lc-python' folder on your Desktop, and to download and unzip the dataset we'll be working with inside of that directory. 

### Start JupyterLab
Once you have created the 'lc-python' directory on your Desktop, you can start JupyterLab by opening a shell (Terminal on Mac or Git Bash for Windows), navigating to your ```lc-python``` folder, and typing 'jupyter lab' on the command line.

```bash
$ cd Desktop/lc-python
$ jupyter lab
```

If you are unfamiliar with the command line,  you can also launch JupyterLab by opening the Anaconda Navigator app and choosing the "Launch" button underneath the JuypterLab icon. If you launch Jupyterlab from Anaconda you'll need to navigate the directory of folders visible in the left-hand column of the JupyterLab display to find your 'lc-python' folder.

### A first look at JupyterLab

Launching JupyterLab should open a new tab or window in your preferred web browser. While JupyterLab enables you to run code from your browser, it does not require you to be online. If you take a look at the URL in your browser address bar, you should see that the environment is located at your localhost, meaning it is running from your computer and not connecting to a URL that is online: ```http://localhost:8888/lab```.

When you first open JupyterLab you should see two main panels. In the left sidebar there is a file browser. You should see a folder in the file browser named 'lc-python-circ' that contains all of our data. If you double-clock on that folder, you will see a list of the CSV files we'll be working with. To get back to the working directory, choose the folder icon just above file browser pane. 

To the right you will initially see a Launcher tab. Here we have options to launch a Python 3 notebook, a Terminal (where we can use shell commands), text files, and other filetypes. For now, we want to launch a new Python 3 notebook, so click once on the 'Python 3 (ipykernel)' button underneath the Notebook header. 

Now you should see a new tab that is called Untitled.ipynb. You should also see it listed in the file browser to the left. Go ahead and right-click on the Untitled.ipynb file in the left hand panel and choose 'Rename' from the dropdown options. Let's call the notebook file, 'workshop.ipynb.'

### Running Python code 


## Python in the console

:::::::::::::::::::::::::::::::::::::::  challenge

Go to the IPython tab at the bottom right. What happens when you type a small calculation there?
For example, what happens when you type the following calculation and press enter?

```python
7 * 3
```

:::::::::::::::  solution

## Solution

Python returns the result of the calculation.

```python
21
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Python in the editor

The large panel on the left probably has some text in it that looks like this:

```
"""
Spyder Editor

This is a temporary script file.
"""
```

Write the following line below these lines and press run (the green 'play' button or f5). A window might pop up asking you to specify the run settings, leave the settings as they are and press 'Run'.
What happens?

```python
print('Hello world!')
```

:::::::::::::::  solution

## Solution

In the IPython console  Python tells you which files it ran and the result of this run

```python
runfile('/home/ylja/.config/spyder-py3/temp.py', wdir='/home/ylja/.config/spyder-py3')
Hello world!
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

- Code written in the editor can be saved, like any other file.

:::::::::::::::::::::::::::::::::::::::  challenge

## Saving the code

To save the code, press 'file' and then 'save as'. Now give the file a name, for example 'mycode.py' and save it in a directory/folder where you know how to find it.
Look into your file system the way you usually do it. Is the file where you expect it to be?

::::::::::::::::::::::::::::::::::::::::::::::::::

[anaconda]: https://docs.anaconda.com/anaconda/install/
[spyder]: https://www.spyder-ide.org/


:::::::::::::::::::::::::::::::::::::::: keypoints

- Use the Spyder IDE for editing and running Python
- The IPython console can be used to interact with Python directly
- The editor can be used to write code, run and save it

::::::::::::::::::::::::::::::::::::::::::::::::::


