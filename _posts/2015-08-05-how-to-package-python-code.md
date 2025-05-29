---
layout: post
title: How to Package Python Code
date: 2015-08-05 20:51:04.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- open source
- package
- publish
- pypi
author:
  display_name: deparkes
permalink: "/2015/08/05/how-to-package-python-code/"
---
With <a href="{{site.baseurl}}/2015/02/28/python-alternatives-to-matlab/">Python distributions </a>such as <a href="https://www.enthought.com/">Enthought </a>and <a href="https://store.continuum.io/cshop/anaconda/">Anaconda</a>, its never been easier to create and install python packages. In this post I show you how to build your own python packages and publish them on the <a href="https://pypi.python.org/pypi">PyPI python package index</a>.
<h1>Step 1. Create PyPI Account</h1>
Before we can upload our package to the <a href="https://pypi.python.org/pypi">Python Package Index PyPI</a> we must first create an account.
Go to the <a href="https://pypi.python.org/pypi">PyPI website</a> and set up an account. Remember your user name and password as you will need these later to upload your files.
<h1>Step 2. Prepare your files</h1>
Before we build and upload your module, we need to organise our files in a particular way.
For this basic example we're assuming your project code is in a single python file "module_file.py". You will also need to create a file "setup.py" and "__init__.py".
Create the folder structure like this:

```
project_directory/
     setup.py
     module_name/
          __init__.py
          module_file.py
```
Everything in the directory 'module_name' will be packaged and uploaded to PyPI.
<h2>__init__.py</h2>
The file "__init.py__" tells Python that the folder it is in is a module folder. For now we'll just leave the file blank.
<h2>setup.py</h2>
The file "setup.py" is a setup script that defines important information and metadata for your project.
For our simple example we'll just include some basic information about the package and its author:

```python
from setuptools import setup
setup(name='texlog',
      version='0.2.0',
      description='Log the wordcount of tex files',
      url='https://github.com/deparkes/texlog',
      author='deparkes',
      author_email='deparkes@deparkes.co.uk',
      license='GPL',
      packages=['texlog'])
```

Have a look at the <a href="https://pythonhosted.org/setuptools/setuptools.html">setuptools documentation</a> or  <a href="https://github.com/trending?l=python">other python projects on github</a> to see what else you might include in setup.py.
<h1>Step 3. Build and Upload Your Package To PyPI</h1>
Having sorted out your project files and organisation, the next step is to build your package and upload it to PyPi.
We do this by running a series of commands from 'project_directory'.
<h2>1. setup.py register</h2>
Running the command

```python
setup.py register
```

registers your project on PyPI. Running this command will give you these options:

```
running register
We need to know who you are, so please choose either:
    1. use your existing login,
    2. register as a new user,
    3. have the server generate a new password for you (and email it to you), or
    4. quit
Your selection [default 1]:
```

At which point you can login using your PyPI username and password.
You will be given the option to save your username and password as a plaintext file on your computer. Since this is just an unsecure plaintext file you may wish to not do this - it just means you'll have to enter your login details each time you register or upload a package.
<h2>2. setup.py sdist</h2>
This is the step that actually builds your package. For now the default options will be enough, which should create a zip-file package in a directory "dist"
sdist refers to a "source distribution". You can find out more about different distribution types <a href="http://stackoverflow.com/questions/6292652/what-is-the-difference-between-an-sdist-tar-gz-distribution-and-an-python-egg">here</a>.
<h2>3. twine upload dist\*</h2>
Now we get to the stage of uploading our package to PyPI.
To upload all of the packaged files in the directory 'dist' run:

```
twine upload dist\*
```


If you didn't save your username and password for PyPI when you ran "setup.py register" you'll need to use the username and password flags:

```
twine -u USERNAME -p PASSWORD upload dist\*
```


Note: If you don't have twine you'll need to run

```
pip install twine
```


<h1>Install your package</h1>
With your project packaged and uploaded to PyPi you and others can now easily install it using the "pip install" command:

```
pip install jobid
```

