---
layout: post
title: Anaconda Python Environments
date: 2016-10-21 15:00:49.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- anaconda
- conda
- python
- virtual env
author: deparkes
permalink: "/2016/10/21/anaconda-python-environments/"
---
Have multiple versions of Python on the same system with <a href="https://www.continuum.io/downloads">Anaconda P</a>ython environments. It can be good to have multiple versions of python on the same system for testing, development, or just to use packages only available in <a href="https://www.python.org/download/releases/2.7/">Python 2.7</a>. If you try to do a conventional install of multiple python versions, you will probably have problems with compatability and conflict between the versions. To get around this you can use Anaconda Python environments to manage your different python versions.
<h1>Create a new environment</h1>
A conda python environment can have its own packages and version of python, which you can keep separate from the system default, and other environments. To create a new environment just run:

```bash
conda create -n myenv python
```

This will create a new environment with the default python version, into which you can install packages as you need them.
<h1>Swapping Between Environments</h1>
To enter a virtual environment you have created you need to 'activate' it:
In windows this is done with

```bash
activate myenv
```

And in Linux/OSX:

```bash
source activate myenv
```

And similarly to deactivate:
In windows this is done with

```bash
deactivate myenv
```

And in Linux/OSX:

```bash
source deactivate myenv
```

<h1>Installing Packages Into An Environment</h1>
The above code will install a bare-bones python installation into the new environment. To install more than that you can either use a single line to install the package at the same time as creating the virtual environment:

```bash
conda create -n myenv python scipy
```

Or you can install the package into an existing virtual environment:

```bash
conda create -n myenv python scipy
```

You can also use pip in the new environment:

```bash
conda install -n myenv pip
source activate myenv
pip install my_package
```

<h1>Multiple python versions</h1>
One of the most powerful uses of multiple environments is being able to have multiple python versions installed and available on one systems. For this you need to specify the python version you wish to use in an environment. For example you might want to have a Python 2.7 environment available for using/testing python 2 scripts:

```bash
conda create -n py27 python=2.7
```

<h3><a href="https://conda.pydata.org/docs/faq.html#creating-new-environments">Find out more in the Conda docs </a></h3>
