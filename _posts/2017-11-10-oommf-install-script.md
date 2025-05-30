---
layout: post
title: OOMMF Installation With An OOMMF Install Script
date: 2017-11-10 15:00:15.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- bash
- install
- oommf
- oommf install
- script
- ubuntu
author:
  display_name: deparkes
permalink: "/2017/11/10/oommf-install-script/"
---
Installing <a href="https://math.nist.gov/oommf/oommf.html">OOMMF </a>is a multi-step process which can be a bit fiddly, particularly on Linux systems. I would normally just work through the <a href="{{site.baseurl}}/2014/05/18/oommf-tutorial-part-1-install-oommf-and-tcltk/">installation steps </a>separately, but was inspired by the <a href="https://virtual-micromagnetics.readthedocs.io/en/development/">Virtual Micromagnetics</a> project to write an OOMMF install script.

This OOMMF install script is contains the steps needed to install OOMMF on a Debian / Ubuntu system (it uses apt-get). It's probably quite easy to trip it up (e.g. trying to install multiple versions of tcl/tk on the same system, using incorrect arguments e.g.), but I have tried to keep it very simple and easy to modify if needed.

```bash
#!/bin/bash
# $1 = oommf source
# $2 = tcl/tk version e.g. 8.6
echo "Installing "$1
echo "With tcl/tk"$2
# OOMMF compilation needs g++ from build-essential package
sudo apt-get install build-essential -y
# Install tcl/tk dev packages
sudo apt-get install tcl$2-dev -y
sudo apt-get install tk$2-dev -y
# need base tcl to be installed to run
sudo apt-get install tcl -y
# Download and unpack oommf version
wget -qO- $1 | tar xvz
# Build OOMMF
cd ./oommf
tclsh oommf.tcl pimake distclean
tclsh oommf.tcl pimake
```

Usage:

```bash
oommf_install.sh oommf_download_url tcl_tk_version
```

You can find the 'oommf_download_url' from the OOMMF website - the zipped tar source files available for each OOMMF version.
For example:

```bash
oommf_install.sh https://math.nist.gov/oommf/dist/oommf20a0_20170929.tar.gz 3.6
```

This will install OOMMF to a directory 'oommf' within your current directory. You should read any guidance on the <a href="https://math.nist.gov/oommf/oommf.html">OOMMF website</a> regarding compatibility of OOMMF versions with tcl/tk versions.
<a href="https://github.com/deparkes/oommf_install/blob/master/install_oommf.sh">Find this OOMMF install script on Github</a>.
