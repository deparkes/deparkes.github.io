---
layout: post
title: Use Tox With Anaconda
date: 2018-06-04 15:30:17.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- anaconda
- python
- tox
- virtualenv
author: deparkes
permalink: "/2018/06/04/use-tox-with-anaconda/"
---
<a href="https://tox.readthedocs.io/en/latest/">Tox</a> is a tool for building and running a matrix of test environments. This is useful when, for example, you need to support several different versions of python. You don't want to have to manually run tests againsts each of your supported versions. This post shows you how you can use tox with anaconda.

If, <a href="{{site.baseurl}}/2016/10/21/anaconda-python-environments/">like me</a>, you like to use the anaconda python distribution, you will find that it is not obvious how you can incorporate Tox into your workflow. Tox relies on the concept of the virtualenv, and as an anaconda user, I am more familiar with creating and using <a href="https://conda.io/docs/user-guide/tasks/manage-environments.html">conda environments</a>. Tox does not currently support conda so we cannot just tell it to create conda environments rather than virtualenvs. Thankfully, it is possible to use anaconda to create the python versions that tox needs.
<h1>How Tox Works</h1>
Tox is controlled via the 'tox.ini' file. This file tells tox which versions of python you are interested in, and the tests you would like to run for each version - the 'test environment'.

```ini
[tox]
envlist = py27,py36
[testenv]
deps = pytest
commands = pytest
```

<h2>Tox Creates 'virtualenv' Virtual Environments</h2>
For each one of the python versions in 'envlist' Tox will create a 'virtualenv' - an isolated python environment.
Without going into too much detail, a virtualenv creates a link to an existing python installation - e.g. C:\python 2.7 in windows or /usr/bin/python in Linux - and makes a new folder for installed modules. The virtualenv (with its link to an existing install) can sit inside a project folder.

| ![Tox With Anaconda - virtualenv example]({{site.baseurl}}/assets/2018/06/virtual_env_example-213x300.png) |
|:--:|
| *Tox With Anaconda - virtualenv example* |

<h4><a href="https://pyvideo.org/pycon-us-2011/pycon-2011--reverse-engineering-ian-bicking--39-s.html">Learn more about how virtualenv creates an isolated virtual environment.</a></h4>
<h2>Tox Finds Python Installations on Your System</h2>
Tox interprets the 'envlist' elements pyxy as python 'major'.'minor' on your system. For example 'py27' becomes python 2.7. How exactly Tox finds the corresponding python installation on your system depends on your operating system.
<h3>Non-windows</h3>
On non-windows machines, Tox uses <a href="https://py.readthedocs.io/en/latest/path.html#py._path.local.LocalPath.sysfind">py.path.local.sysfind()</a> to look in your system PATH for 'pythonx.y'.
For example, I have 'ffmpeg' installed on my machine. Running py.path.local.sysfind('ffmpeg') returns the following.
local('usr/bin/ffmpeg')
<h3>Windows</h3>
On windows machines, Tox tries the 'sysfind' approach first, but also checks the common python install location 'C:\pythonx.y'. At the time of writing these are the only places Tox will look (so you will have problems if you have installed python elsewhere, such as 'D:\pythonx.y').
For example, I have 'ffmpeg' installed on my machine. Running py.path.local.sysfind('ffmpeg') returns the following.
local('C:\Program Files\ffmpeg\bin\ffmpeg.EXE')
<h4>See exactly how Tox implements this by looking at the method '<span class="pl-en">tox_get_python_executable</span>' in '<a href="https://github.com/tox-dev/tox/blob/ff7143e7c991b1a80e7ec1ea6836ef3a21b5a812/tox/interpreters.py">interpreters.py</a>'</h4>
<h1>Tox With Anaconda</h1>
We can use anaconda to manage the python installations (and other packages) that Tox needs to work. It might feel a bit unnatural at first to be using a virtualenv <em>within</em> a conda environment (it does to me anyway), but it does seem to get the job done.

| ![Tox With Anaconda]({{site.baseurl}}/assets/2018/06/tox_and_virtualenv-300x251.png) |
|:--:|
| *Tox With Anaconda* |

We will create conda environments and make sure tox/virtualenv can find them.
<h3>Configure your conda environment</h3>
We will work within a conda environment. This doesn't need to be anything special, other than making sure that virtualenv is installed in it.
Run these commands:

```conda install virtualenv```

and

```
pip install tox
```

You need to install virtualenv with 'conda install virtualenv', because of how virtualenv needs to interact with the underlying conda python install.
<h2>Make Sure Tox Can Find Your Python Installs</h2>
We have some different options for how we can make sure tox finds the right python distribution installed by conda. Things are a little different depending on whether or not we are using Windows.
<h3>Windows</h3>
<h4>Install To Particular Locations</h4>
One option with windows is to install the conda environment to a location already searched by Tox. Tox already looks for e.g. C:\python27, so we can create a python environment there using anaconda.

```
conda create -p=C:\python27 python=2.7
```

Tox will now be able to find the python binary it needs.
This is probably the the simplest solution for windows users, but I am somehow uneasy about the python environment being installed to C:\python27. You could easily find yourself in trouble if you installed a fresh version of python 2.7 outside of Anaconda for instance.
Instead, I like the tidiness of having all anaconda environments installed to the same 'anaconda' directory.
<strong><a href="https://fizzylogic.nl/2017/11/01/how-to-setup-tox-on-windows-with-anaconda/">Read more about tox with windows</a></strong>
<h4>Create Batch Files to Redirect Tox</h4>
This is probably my preferred solution for windows. Rather than setting the conda environment to be on the path, we can do something that is a bit more nuanced, and also <a href="https://tox.readthedocs.io/en/latest/developers.html">suggested by tox itself</a>.
Pick a good directory to hold your batch scripts - these will be 'pointers' to the python binaries needed by tox. I use the anaconda install directory.
Create bash scripts called e.g. python2.7.bat like this:

```@C:\Users\your_user_name\Anaconda3\pkgs\python-2.7.15-0\python.exe %*```

I found that tox / virtualenv failed unless this was the only line in the batch scripts - i.e. no comments - but your experience may differ.
You will need to add the location of these batch scripts to your <a href="https://stackoverflow.com/questions/9546324/adding-directory-to-path-environment-variable-in-windows">PATH environment variable:</a>
E.g. setx PATH "%PATH%;C:\Anaconda3"
Now tox will find 'pythonx.y' on your system path (in the directory you have just added to the path) and execute your batch files, which you have directed at the appropriate python installs.
<h3>Non-windows</h3>
On non-windows systems, the only option open to us is to create executable scripts in a particular location. This works in basically the same was as windows bash scripts.
Pick a directory to hold you bash scripts - e.g. ~/anaconda3
<a href="https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix">Add this directory to the path</a> (it needs to go at the front of the path otherwise tox will pick up your system installs in e.g. /usr/bin/python).
Create a bash script for the python versions you need. For example if we wanted to run with conda's python3.5 install we could create a bash script called 'python3.5'. This script would contain.

```bash
#!/bin/sh
~/miniconda3/python3.5 $*
```

we will need to make this file executable by running

```
chmod u+x python3.5
```

The '#!/bin/sh' is essential, as it lets the system know which interpreter to use.
Tox should now be able to find the versions of python you need it to.
<a href="https://blog.ionelmc.ro/2015/04/14/tox-tricks-and-patterns/">Read more about tox</a>
