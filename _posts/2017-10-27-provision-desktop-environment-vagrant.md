---
layout: post
title: Provision a desktop environment with vagrant
date: 2017-10-27 15:00:50.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- desktop
- provision
- ubuntu
- vagrant
- virtual machine
author: deparkes
permalink: "/2017/10/27/provision-desktop-environment-vagrant/"
---
<h1>Provision a Desktop Environment With Vagrant</h1>
Vagrant base boxes often do not come with a desktop environment installed. Rather than hunting around to find <a href="https://github.com/rgl/xfce-desktop-vagrant/blob/master/provision.sh">one that does</a>, you can use vagrant's <a href="https://stackoverflow.com/questions/29687222/what-does-it-mean-to-provision-a-virtual-machine">provisioning </a>capabilities to add a desktop to your base box of choice.
If you are running an Ubuntu system without a desktop environment, such as <a href="https://www.ubuntu.com/download/server">Ubuntu server</a>, you can <a href="https://askubuntu.com/questions/53822/how-do-you-run-ubuntu-server-with-a-gui">install a desktop environment</a> by running:

```
sudo apt-get install ubuntu-desktop
```

which will install the full Ubuntu desktop to your system.
It's possible to do something similar with Vagrant's provisioning functionality. Vagrant can work with external provisioning tools, but in this case we will just incorporate a <a href="https://www.vagrantup.com/docs/provisioning/shell.html">shell script</a> into a vagrant file.
To do this we can add the following to the vagrantfile:

```
config.vm.provision "shell",
    inline: "sudo apt-get install --no-install-recommends lubuntu-desktop -y"
```

To keep the virtual machine relatively light weight I have selected to install the lxde-based lubuntu-desktop. I have also used --no-install-recommends to leave out some of the larger packages that are installed by default. Note that even a lightweight ubuntu desktop is likely to take a while to install.
It is essential that we include the '-y' flag to make sure the installation is approved (it's equivalent to us typing 'y').
Your final vagrantfile should look something like this:

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provision "shell",
    inline: "sudo apt-get install --no-install-recommends lubuntu-desktop -y"
end
```

Running

```bash
vagrant up
```

with this vagrant file should also run the new provision script.
If you encounter problems you may need to run

```bash
vagrant provision
```

or

```bash
vagrant up --provision
```

to re-run the provisioning.
You will need to tell your vagrant file that you want to provision your machine, and where to find the provisioning script.
Now when you run vagrant up, the resulting virtual machine should have a desktop environment.
