---
title: Setup
---

This lesson is designed to be run on a personal computer.
All of the software and data used in this lesson are freely available online,
and instructions on how to obtain them are provided below.

# <a name=#setup>Setup</a>

To participate in this lesson, you will need a working Unix-like shell environment. We will be using Bash ([Bourne Again Shell](https://en.wikipedia.org/wiki/Bash_\(Unix_shell\))) which is standard on Linux and macOS. Some macOS users (Catalina or later) will have zsh (Z shell) as their default version. Even if you are a Windows user, learning Bash will open up a powerful set of tools on your personal machine, and familiarize you with the standard remote interface used on most servers and supercomputers.

For the workshop, we will use the Broad's [login servers](https://intranet.broadinstitute.org/bits/service-catalog/scientific-computing/login-servers). To access those machines, your laptop needs to be on the **Broad-Internal** wireless network when you are on-site OR on the Broad VPN if you have a non-Broad-issued computer or are off-site.

:::::::::::::::::::  prereq
:::::::::::::::::::::::::::::::::::::::::: spoiler

## Virtual Private Network (VPN) Access

To reach to the Broad login servers when you are off-site, you will connect to the Broad VPN to access internal Broad resources.

#### [VPN Installation](https://intranet.broadinstitute.org/bits/service-catalog/networking/vpn)

- Use Broad Self Service ([Mac](https://intranet.broadinstitute.org/bits/service-catalog/applications/self-service-software-mac) or [Windows](https://intranet.broadinstitute.org/bits/service-catalog/applications/software-center-windows-self-service)) to install the **Cisco AnyConnect Secure Mobility Client** software <p><p>
OR
- Visit <https://vpn.broadinstitute.org> and follow the prompts.

You will also need to [set up DUO two-factor authentication](https://broad.service-now.com/sp?id=kb_article&sys_id=7541196213ffe280df1955912244b0a2) or [Google 2FA](https://broad.service-now.com/sp?id=kb_article&sysparm_article=KB0011056) to use the Broad VPN. Contact [BITS](https://intranet.broadinstitute.org/bits) for troubleshooting if you have a Broad-issued machine.

If you can't access the documentation linked above or can't connect to the Broad VPN using your Broad credentials, please let the [workshop organizers](mailto:cb-admin@broadinstitute.org) know so we can assess whether you will be able to participate in the workshop.
::::::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::

:::::::::::::::::::  prereq
:::::::::::::::::::::::::::::::::::::::::: spoiler

## Terminal Setup

Bash is the default shell on most Linux distributions and older versions of macOS. Windows users will need to install WSL to provide a Unix-like environment.

::: tab

### Linux

The default shell is usually Bash, but if your machine is set up differently you can run it by opening a terminal and typing `bash` followed by the <kbd>enter</kbd> key. There is no need to install anything. Look for Terminal in your applications to start the Bash shell.

### Mac

Open Terminal from `/Applications/Utilities` or Spotlight Search. In versions before Catalina, Bash is the default shell, so you do not need to do anything further. In Catalina and onwards, the default shell is zsh, which is similar but may behave differently from Bash in some cases. To switch to Bash, enter the command `bash` in your terminal window followed by the <kbd>enter</kbd> key.

### Windows

On Windows, CMD or PowerShell are normally available as the default shell environments. These use a syntax and set of applications unique to Windows systems and are incompatible with the more widely used Unix utilities. However, a Bash shell can be installed on Windows to provide a Unix-like environment. For this lesson we suggest using [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install). Open PowerShell or Windows Command Prompt in administrator mode by right-clicking and selecting "Run as administrator", enter <kbd>wsl --install</kbd>, then restart your machine.

Alternatively, you can install Git Bash, part of the [Git for Windows](https://gitforwindows.org/) packagee

- Download the latest Git for Windows [installer](https://gitforwindows.org/).
- Double click the `.exe` file to run the installer (for example, `Git-2.42.0.2-64-bit.exe`) using the default settings.
- Once installed, open the shell by selecting Git Bash from the start menu (in the Git folder).

You can also run Bash commands on a remote computer or server that already has a Unix Shell from your Windows machine. This can be done through a Secure Shell (SSH) client. One client available for free for Windows is [PuTTY](https://www.putty.org/), which is also available through the [Microsoft store](https://apps.microsoft.com/detail/xpfnzksklbp7rj?hl=en-us&gl=US).

If you encounter issues, the Carpentries has a [Configuration Problems and Solutions wiki page](https://github.com/carpentries/workshop-template/wiki/Configuration-Problems-and-Solutions) that may help.

Broad recommends the SecurtCRT terminal application for Broad-issued Windows machines. Broadies can download through the [Windows 10 Software Center](https://intranet.broadinstitute.org/bits/service-catalog/applications/software-center-windows-self-service). :

1. Click on the Windows logo.
1. Click on All Programs > Microsoft System Center > Configuration Manager > Software Center
1. Locate and select SecureCRT, then click on “Install”.

For help with installation on Broad-issued Windows machines, check the [troubleshooting section](https://intranet.broadinstitute.org/bits/service-catalog/applications/software-center-windows-self-service) or contact [BITS](https://intranet.broadinstitute.org/bits).

:::

::::::::::::::::::::::::::::::::::::::::::::::::::
:::::::::::::::::::

## Testing Broad Login Server access

If you are on-site, connect to the **Broad-Internal** wireless network. If you are off-site, [connect](https://intranet.broadinstitute.org/bits/service-catalog/networking/vpn) to the Broad VPN.

::: tab

### Mac

1. Open Terminal from `/Applications/Utilities` or Spotlight Search.
1. Type <kbd>ssh \<username\>@login.broadinstitute.org</kbd> [Example: ssh jcase@login.broadinstitute.org ]
1. Enter your Broad password when prompted.

### Linux

1. Most Linux systems use Ctrl-Alt-T to start a Linux Terminal session.
1. On the command line, type <kbd>ssh \<username\>@login.broadinstitute.org</kbd> [Example: ssh jcase@login.broadinstitute.org ]
1. Enter your Broad password when prompted.

### Windows - WSL

1. Open WSL from the start menu item or by typing <kbd>wsl</kbd> from a command prompt or PowerShell.
1. Type <kbd>ssh \<username\>@login.broadinstitute.org</kbd> [Example: ssh jcase@login.broadinstitute.org ]
1. Enter your Broad password when prompted.

### Windows - SecureCRT

1. Launch [SecureCRT](https://broad.service-now.com/sp?sys_kb_id=072a3dc613eb0f80449fb86f3244b0e8&id=kb_article_view&sysparm_rank=1&sysparm_tsqueryId=f5b28afe47714e50a5d9a8ba216d43e9) from the Start menu
1. Go to the File menu and select "Connect". Select the "New Session"" button.
1. Within the New Session Wizard window, select SSH2 at the Protocol toggle and click Next.
1. Within the Hostname field, enter login.broadinstitute.org. Leave the Port and Firewall fields set to their defaults. Within the username field, enter your Broad username and click Next.
1. Leave the SecureFX protocol field as is (eg. SFTP), click Next.
1. Leave the session name field as it is, or rename it to something shorter. Click the Finish button.
1. X11 setup (for future reference, not needed for this workshop): Select the newly created connection entry and click the Properties icon button. The Session Options window will appear. Select Remote/X11 from the menu on the left, check Forward X11 packets. Click the OK button to close the window.
1. Finally, select your session and click the Connect button. Enter your password to log on.

:::

## Obtain lesson materials

1. Download [python-novice-inflammation-data.zip][zipfile1]
  and [python-novice-inflammation-code.zip][zipfile2].
2. Create a folder called `swc-python` in your home directory.
3. Move downloaded files to `swc-python`.
4. Unzip the files.

You should see two folders called `data` and `code` in the `swc-python` directory.

#### Show your successful access

1. Type <kbd>touch /broad/hptmp/computing_basics_python/\<username\>_was_here</kbd>
2. Type <kbd>ls /broad/hptmp/computing_basics_python</kbd> Did you leave your mark?
3. Type <kbd>exit</kbd> to leave the server.

If you were unable to access the Broad login servers, please let the [workshop organizers](mailto:cb-admin@broadinstitute.org) know so we can help you troubleshoot before the start of the workshop.

:::::::::::::::::::::::::::::::::::::::::: spoiler

## to be updated by cb-admins

## Launch Python interface

To start working with Python, we need to launch a program that will interpret and execute our
Python commands. Below we list several options. If you don't have a preference, proceed with the
top option in the list that is available on your machine. Otherwise, you may use any interface
you like.

## Option A: Jupyter Notebook

A Jupyter Notebook provides a browser-based interface for working with Python.
If you installed Anaconda, you can launch a notebook in two ways:

::::::::::::::::: spoiler

## Anaconda Navigator

1. Launch Anaconda Navigator.
  It might ask you if you'd like to send anonymized usage information to Anaconda developers:
  ![](fig/anaconda-navigator-first-launch.png){alt='Anaconda Navigator first launch'}
  Make your choice and click "Ok, and don't show again" button.
2. Find the "Notebook" tab and click on the "Launch" button:
  ![](fig/anaconda-navigator-notebook-launch.png){alt='Anaconda Navigator Notebook launch'}
  Anaconda will open a new browser window or tab with a Notebook Dashboard showing you the
  contents of your Home (or User) folder.
3. Navigate to the `data` directory by clicking on the directory names leading to it:
  `Desktop`, `swc-python`, then `data`:
  ![](fig/jupyter-notebook-data-directory.png){alt='Anaconda Navigator Notebook directory'}
4. Launch the notebook by clicking on the "New" button and then selecting "Python 3":
  ![](fig/jupyter-notebook-launch-notebook.png){alt='Anaconda Navigator Notebook directory'}

:::::::::::::::::::::::::

::::::::::::::::: spoiler

## Command line (Terminal)

1\. Navigate to the `data` directory:

::::::::::::::::: spoiler

## Unix shell

If you're using a Unix shell application, such as Terminal app in macOS, Console or Terminal
in Linux, or [Git Bash][gitbash] on Windows, execute the following command:

```bash
cd ~/Desktop/swc-python/data
```

:::::::::::::::::::::::::

::::::::::::::::: spoiler

## Command Prompt (Windows)

On Windows, you can use its native Command Prompt program.  The easiest way to start it up is
pressing <kbd>Windows Logo Key</kbd>\+<kbd>R</kbd>, entering `cmd`, and hitting
<kbd>Return</kbd>. In the Command Prompt, use the following command to navigate to
the `data` folder:

```source
cd /D %userprofile%\Desktop\swc-python\data
```

:::::::::::::::::::::::::

2\. Start Jupyter server

::::::::::::::::: spoiler

## Unix shell

```bash
jupyter notebook
```

:::::::::::::::::::::::::

::::::::::::::::: spoiler

## Command Prompt (Windows)

```source
python -m notebook
```

:::::::::::::::::::::::::

3\. Launch the notebook by clicking on the "New" button on the right and selecting "Python 3"
from the drop-down menu:
![](fig/jupyter-notebook-launch-notebook2.png){alt='Anaconda Navigator Notebook directory'}

:::::::::::::::::::::::::

  <!-- vertical spacer -->

## Option B: IPython interpreter

IPython is an alternative solution situated somewhere in between the plain-vanilla Python
interpreter and Jupyter Notebook. It provides an interactive command-line based interpreter with
various convenience features and commands.  You should have IPython on your system if you installed
[Anaconda][anaconda-instructions].

To start using IPython, execute:

```source
ipython
```

  <!-- vertical spacer -->

## Option C: plain-vanilla Python interpreter

To launch a plain-vanilla Python interpreter, execute:

```source
python
```

If you are using [Git Bash on Windows][gitbash], you have to call Python *via* `winpty`:

```source
winpty python
```

::::::::::::::::::::::::::::::::::::::::::

[anaconda-instructions]: https://carpentries.github.io/workshop-template/install_instructions/#python
[zipfile1]: data/python-novice-inflammation-data.zip
[zipfile2]: ../episodes/files/code/python-novice-inflammation-code.zip
[gitbash]: https://gitforwindows.org
