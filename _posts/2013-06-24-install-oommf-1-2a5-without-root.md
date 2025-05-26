---
layout: post
title: Install OOMMF 1.2a5 without root
date: 2013-06-24 11:03:49.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- linux
- oommf
author:
  display_name: deparkes
permalink: "/2013/06/24/install-oommf-1-2a5-without-root/"
---
Installing OOMMF in linux without root access can be difficult. The <a href="http://math.nist.gov/oommf/doc/userguide12a5/userguide/Basic_Installation.html">basic install procedure</a> for OOMMF is quite straight forward: check you have tcl/tk, download the oommf source then run oommf.tcl pimake. This is fine when you have root access and can easily run the package manager to install the dev versions of tcl and tk.
If we only have user level access it can be a bit more tricky. Without access to a package manager we must compile tcl and tk from source. In this post I will go through the full install of oommf, including compiling tcl/tk from source. The install guides for tcl, tk and oommf are all really good. They do still however require some decisions to be made, so hopefully spelling out what worked for me here can be of use.
<h2>1. Download tcl, tk.</h2>
We will be following the general compile instructions here: <a href="http://www.tcl.tk/doc/howto/compile.html" target="_blank">http://www.tcl.tk/doc/howto/compile.html</a>. These instructions are generally very good, but I will try to highlight any areas of uncertainty I had.
First download the tcl and tk source from <a href="http://www.tcl.tk/software/tcltk/download.html">http://www.tcl.tk/software/tcltk/download.html</a>
(wget can be useful for downloading things from the command line. Just type
`wget file_to_download.txt`.)
Extract the archives to your (a subdirectory of) your home folder.


```bash
mkdir ~/downloads
tar -zxvf tcl8.5.14-src.tar.gz -C ~/downloads/
tar -zxvf tk8.5.14-src.tar.gz -C ~/downloads/
```


We specify the install location during the compilation stage.

2. Make/configure/install tcl


```bash
cd ~/downloads/tcl8.5.14/unix
./configure --prefix=/home/user_name/tcl --enable-threads
make
make test
make install
```
A whole load of text will scroll by.
<h2>3. Make/configure/install tk.</h2>
The process is very similar to compiling tcl, but we also tell tk where to find our tcl installation.
Before configuring tk: If you are connected to your oommf machine via ssh it is important that X-11 forwarding is setup and that you have a suitable X server (e.g. Exceed) running on your system and your ssh connection allows <a title="X-forwarding" href="http://www.math.umn.edu/systems_guide/putty_xwin32.html">X forwarding</a>.
When configuring tk it is important to set the --prefix flag to be the same as you used to install tcl. If not then you will get version conflicts.

```bash
cd ~/downloads/tk8.5.14/unix
./configure --with-tcl=/home/user_name/tcl/lib --prefix=/home/user_name/tcl
make
make test
make install
```


Add the tcl install to the path, so you can easily access it (e.g. to run oommf):
<code> export PATH=/path/to/tcl/bin/:$PATH</code>
(Add these export command lines to your .bashrc so that they load automatically when you login.)
<h2>4. You might need to set environment variables for oommf.</h2>

```bash
export PATH=$PATH:/home/user_name/tcl/bin
export OOMMF_TCL_INCLUDE_DIR=/path/to/tcl/include
export OOMMF_TK_INCLUDE_DIR=/path/to/tcl/include
export OOMMF_TCL_CONFIG=/path/to/lib/tclConfig.sh
export OOMMF_TK_CONFIG=/path/to/lib/tkConfig.sh
```

If you have trouble at this stage please check the <a href="http://math.nist.gov/oommf/doc/userguide12a3/userguide/Basic_Installation.html#SECTION00032200000000000000">oommf basic installation</a> page.
<h2>5. Install/compile oommf.</h2>
Please see <a href="http://math.nist.gov/oommf/doc/userguide12a3/userguide/Basic_Installation.html"> OOMMF install guide</a> for full install details.
If you haven't already done so download and extract oommf from http://math.nist.gov/oommf/dist/oommf12a5rc_20120928.tar.gz
Extract archive to a separate folder

```bash
mkdir ~/oommf/
tar -zxvf oommf12a5rc_20120928.tar.gz -C ~/oommf/
```


Go to the oommf directory e.g. ~/oommf/oommf1-2a5/
Check that the tcl/tk install and oommf are compatible.

```bash
tclsh8.5 oommf.tcl +platform
```
If this is ok then run

```bash
path/to/tclsh8.5 oommf.tcl pimake upgrade
path/to/tclsh8.5 oommf.tcl pimake distclean
path/to/tclsh8.5 oommf.tcl pimake
```

Then you can just run oommf:
```bash
path/to/tclsh8.5 oommf.tcl
```

I like to make a script "oommf.sh" which has:

```bash
#!/bin/bash
/path/to/tclsh8.5 /path/to/oommf/oommf.tcl $@
```
The "$@" takes all command line arguments from the terminal. This is useful for having quick access to the various useful command line utilities built in to OOMMF, such as any2ppm.
