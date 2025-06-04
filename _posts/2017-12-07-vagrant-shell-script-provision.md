---
layout: post
title: Vagrant Shell Script Provision
date: 2017-12-07 20:00:01.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- bash
- install
- provision
- shell
- vagrant
- virtual machine
author: deparkes
permalink: "/2017/12/07/vagrant-shell-script-provision/"
---
<a href="https://www.vagrantup.com/">Vagrant</a> is a tool for quickly creating and starting <a href="https://en.wikipedia.org/wiki/Virtual_machine">virtual machines</a>. One of the powerful features of vagrant is its ability to '<a href="https://stackoverflow.com/questions/29687222/what-does-it-mean-to-provision-a-virtual-machine">provision</a>' the virtual machines it creates. Provisioning involves connecting to the virtual machine and making any necessary installations or config changes. Vagrant can provision a virtual machine in a number of ways, and one of the simplest is to use a <a href="https://en.wikipedia.org/wiki/Shell_script">shell script</a>. This post looks at how to provision a vagrant virtual machine with a <a href="https://www.vagrantup.com/docs/provisioning/shell.html">shell script</a>.
<h1>Shell Script Provision</h1>
<h2>Vagrantfile for Shell Script Provision</h2>
The <a href="https://www.vagrantup.com/docs/vagrantfile/">vagrantfile</a> controls the setup of a virtual machine. At it's most basic, your vagrant file needs to specify that it will use a shell script to provision the machine, and the path to the shell script (it is also possible to use<a href="{{site.baseurl}}/2017/10/27/provision-desktop-environment-vagrant/"> in-line shell commands</a> to provision).
This example specifies that a script 'script.sh' will be used to provision the vagrant machine. This script will be run by vagrant once the basic box is created.

```
# -*- mode: ruby -*-
# vi: set ft=ruby :
# encoding: UTF-8
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell",
    path: "script.sh"
end
```

<h2>Writing New Provisioning Scripts</h2>
In many cases the provisioning script will be capturing a series of commands that would otherwise be typed in at the command line.
I suggest logging in to an un-provisioned virtual machine to test out the commands and scripts. This will help reveal any major version, dependency or permissions problems as before you write your provisioning script.
There are a few differences between running a script from within the machine and running the script via the vagrant provisioning, including;
<h3><em>Passing Arguments</em></h3>
If you need to pass arguments to your provisioning script, you can do this with an additional parameter for the provisioner 'args', which takes a string of space-separated values, just like they would be supplied at the command line. For example args: "argument_1 argument_2".
In the following example I pass a url and a software version as arguments to the shell script.

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
# encoding: UTF-8
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell",
    path: "script.sh",
    args: "https://math.nist.gov/oommf/dist/oommf20a0_20170929.tar.gz 8.6"
    config.vm.provider "virtualbox" do |v|
  v.gui = true
end
end
```

<h3>Changing Permissions</h3>
By default, Vagrant provisions its virtual machines as <a href="https://stackoverflow.com/questions/22547575/execute-commands-as-user-after-vagrant-provisioning">root</a>. Unless you specify otherwise, other users of the virtual machine will not be able to access files and folders created by this user.
<h2>An Example Provisioning Script</h2>
The following is an example of a script for installing a desktop environment and then downloading and installing some additional software.

```bash
#!/bin/bash -e
# $1 = oommf source
# $2 = tcl/tk version e.g. 8.6
echo "Installing "$1
echo "With tcl/tk"$2
# Update apt
sudo apt-get update -y
# Install a desktop environments
sudo apt-get install --no-install-recommends lubuntu-desktop -y
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
# Change folder permissions
sudo chown -R vagrant /home/vagrant/oommf
```


<h2>Multiple Shell Scripts Provision</h2>
It can sometimes make sense to divide your provisioning up across multiple scripts. This is largely the same as for single script as you specify an starting or master script for vagrant to begin provisioning with. This script will then need to run the other scripts you need to provision your machine.
In following example I have separated the installation of a desktop environment into one script, and the installation of a piece of software into another.
<h3>'Master Script'</h3>
This simple 'master script'  executes two other scripts with separate functions.

```bash
#!/bin/bash -e
exec /vagrant/install_lubuntu.sh
exec /vagrant/install_oommf.sh $1 $2
```

<h3>Desktop Install Script</h3>
This script installs a lubuntu desktop on the virtual machine.

```bash
#!/bin/bash -e
echo "Installing Lubuntu Desktop"
# Update apt
sudo apt-get update -y
# Install a desktop environments
sudo apt-get install --no-install-recommends lubuntu-desktop -y
```

<h3>Software Download and Compile Script</h3>
This script deals with the downloading and installing of some software not in a package manager. It picks up the arguments passed through from the vagrantfile and the 'master script'.

```bash
#!/bin/bash -e
# $1 = oommf source
# $2 = tcl/tk version e.g. 8.6
echo "Installing "$1
echo "With tcl/tk"$2
# Update apt
sudo apt-get update -y
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
# Change folder permissions
sudo chown -R vagrant /home/vagrant/oommf
```

