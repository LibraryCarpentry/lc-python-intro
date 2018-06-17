---
title: "Getting Started"
teaching: 15
exercises: 0
questions:
- "How do I use the Spyder IDE?"
- "How can I run Python programs?"
objectives:
- "Learners can launch the Spyder IDE"
- "Learners are able to use the iPython console to interact with Python"
- "Learners are able to write code in the Spyder editor and run this code"
- "Learners are able to save their code in a *.py file"
- "Learners can use the different buttons and panels needed in the Spyder IDE"
keypoints:
- "Use the Spyder IDE for editing and running Python"
- "The iPython console can be used to interact with python directly"
- "The editor can be used to write code, run and save it"
---

## Use the Spyder IDE for editing and running Python.

*   The [Anaconda package manager][anaconda] is an automated way to install the [Spyder IDE][spyder].
    *   See [the setup instructions]({{ page.root }}/setup/) for Anaconda installation instructions.
*   It also installs all the extra libraries it needs to run.
*   Once you have installed Python and the Spyder IDE requirements, open a shell and type:
    ~~~
    $ spyder
    ~~~
    {: .python}

*   This will start The Spyder IDE.
*   This environment has several useful tools we can use, which you can see in different panels in the Spyder IDE. We will look into some of them. 
* You can change the positions and sizes of these panels to your preference, as you get to know them.

## Different ways of interacting with Python using Spyder

*   On the left, filling half of the screen is the editor. Here you can write and edit code, which can then be saved in a file (usually with a .py extension). We can run the code we wrote here by pressing the green 'play' button on top or press F5 on your keyboard.
*   On the bottom right, we find the iPython console. This is were we can talk directly to python. It will interpret what you have typed directly when you press Enter.

## Python in the console

> Go to the iPython tab at the bottom right. What happens when you type a small calculation there?
> For example, what happens when you type the following calculation and press enter?
> ~~~
> 7 * 3
> ~~~
> {: .python}
>
> > ## Solution
> >
> > Python returns the result of the calculation.
> > ~~~
> > 21
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Python in the editor
>
> The large panel on the left probably has some text in it that looks like this:
> ~~~
> """
> Spyder Editor
>
> This is a temporary script file.
> """ 
>~~~
> Write the following line below these lines and press run (the green 'play' button or f5). A window might pop up asking you to specify the run settings, leave the settings as they are and press 'Run'.
> What happens?
>
> ~~~
> print('Hello world!')
> ~~~
> {: .python}
>
> > ## Solution
> >
> > In the iPython console  Python tells you which files it ran and the result of this run
> > ~~~
> > runfile('/home/ylja/.config/spyder-py3/temp.py', wdir='/home/ylja/.config/spyder-py3')
> > Hello world!
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

* Code written in the editor can be saved, like any other file.

> ## Saving the code
>
> To save the code, press 'file' and then 'save as'. Now give the file a name, for example 'mycode.py' and save it in a directory/folder where you know how to find it.
> Look into your file system the way you usually do it. Is the file where you expect it to be?
> 
> {: .python}
{: .challenge}



[anaconda]: https://docs.anaconda.com/distribution/install
[spyder]: http://pythonhosted.org/spyder/

