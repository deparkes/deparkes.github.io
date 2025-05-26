---
layout: post
title: Basic Vagrant - A Few Commands and Concepts To Get You Started
date: 2018-01-12 15:00:56.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- vagrant
- vagrant box
- virtual machine
- virtualisation
author:
  display_name: deparkes
permalink: "/2018/01/12/basic-vagrant/"
---
<a href="https://www.vagrantup.com/">Vagrant</a> is a command line tool for managing virtual machines. Vagrant commands are generally quite sensible and often a guess at what the command might be gives the rights of others<i> you</i> answer, but there are rather a lot of them. This post picks out some basic vagrant commands and works through the installation and basic usage of vagrant.
<h1>What Is Vagrant?</h1>
Vagrant is a <a href="https://www.hashicorp.com/?_ga=2.262092173.1492085936.1513440507-1414396871.1506457055">Hashicorp</a> tool for building and managing virtual machines, whicih acts like a wrapper around different virtual machine <a href="https://www.vagrantup.com/docs/providers/configuration.html">providers</a> to allow a consistent interface. Vagrant is configured using simple plain text files, which are easy to share and put under version control.
<h1>Installation and Setup</h1>
<h2>Installing Vagrant</h2>
Vagrant itself is <a href="https://www.vagrantup.com/docs/installation/">easy to install</a> on Windows, OSX and Linux systems.
<h2>Installing a Virtual Machine Provider</h2>
Vagrant does not work with virtual machines directly - it is more of a wrapper or interface to different virtual machine '<a href="https://www.vagrantup.com/docs/providers/">providers</a>' which actually run and control the virtual machines. You will need to install a provider on your machine to allow vagrant to work with it.
A good provider to start with is <a href="https://www.virtualbox.org/">Virtualbox</a>. Virtualbox is available for many different systems, and there are many Vagrant boxes available for it.
<h1>Working With Vagrant Boxes</h1>
<h2>Add A Box</h2>
Vagrant uses its own versions of virtual machines, known as '<a href="https://www.vagrantup.com/docs/boxes.html">boxes</a>' which have already been configured to allow vagrant to work with them. Hashicorp, who created Vagrant, maintain <a href="https://app.vagrantup.com/boxes/search">a repository of vagrant boxes</a>. The '<a href="https://www.vagrantup.com/docs/cli/box.html#box-add">vagrant box add</a>' command is used to select and download boxes from this repository. Boxes are identified by the account name in the repository and the name of the box.

```bash
vagrant box add USER/BOX

```

For example:

```bash
vagrant box add ubuntu/trusty64

```

Which will add the 'trusty64' box from the user 'ubuntu' to your system.
<h2>Add a Particular Version of Box</h2>
Some boxes are regularly updated, so to be sure you are using the right version (such as for compatibility reasons) you may want to <a href="https://www.vagrantup.com/docs/boxes/versioning.html">specify an exact version</a>. You can do this with:

```bash
vagrant box add USER/BOX --box-version VALUE
```

For example:

```bash
vagrant box add ubuntu/trusty64 --box-version 20171205.0.1

```

<h2>List Boxes Available on Your Machine</h2>
By default, vagrant will look on your local machine for boxes. You can see which boxes are available with this command:

```bash
vagrant box list
```

<h2>Remove A Box</h2>
If you download the wrong box, or just want to remove an old one, you can do this with:

```bash
vagrant box remove
```

For example:

```bash
 vagrant box remove ubuntu/trusty64
```

<h2>Where To Find New Boxes</h2>
Hashicorp maintains a <a href="https://app.vagrantup.com/boxes/search">repository</a> of pre-built vagrant boxes, and you will probably find the box you need on there. The Hashicorp repository has boxes from many different users, and Hashicorp recommend either using one of their official boxes, or boxes made as part of the <a href="https://app.vagrantup.com/bento">Bento</a> project. You may find, however, that you need to look around if you are not using one of the more popular operating systems providers.
<h1>Working With Vagrant Virtual Machines</h1>
This section is a whistle-stop tour of working with vagrant from setting up the vagrant machine to stopping and removing it.
<h2>Initialise Vagrant</h2>
The essential part of working with vagrant is the 'Vagrantfile' which describes the type of machine to build, and how to configure it. The presence of a vagrant file in a folder gives vagrant enough to work from to build and manage virtual machines.
You can create a template vagrant file by running

```bash
vagrant init
```

which will create a 'Vagrantfile' in the current directory, containing a number of commented out options.
Using 'vagrant init' isn't strictly necessary for creating a vagrantfile, and you may prefer to create one yourself. An example of the contents of a simple Vagrantfile is below:

```ruby
Vagrant.configure("2") do |config|
config.vm.box = "hashicorp/precise64"
end
```

Vagrantfiles are written using <a href="https://www.ruby-lang.org/en/">ruby</a> syntax, but a deep knowledge of ruby is not essential. This kind of basic Depending on your requirements you may need to make some adjustments, such as making sure the provider is correct and so on.
<h2>Start The Vagrant Virtual Machine</h2>
Once you have a Vagrantfile in your project folder you can start the Vagrant virtual machine. This is as simple as running:

```bash
vagrant up
```

Vagrant virtual machines are typically started in the background, so there may not be obvious indications that the machine is running.
<h2>Connect to a Running Vagrant Machine</h2>
Once your vagrant machine is running then it is possible to connect to it using this command:

```bash
vagrant ssh
```

which will connect to your machine via ssh using vagrant's default user 'vagrant'. You can logout from this session with the 'logout' command.
<h2>Stop a Running Vagrant Machine</h2>
Once you are finished with a running machine you can stop it with this command:

```bash
vagrant halt
```

which is similar to manually shutting down the machine. If you want to start the machine again, you can run 'vagrant up' again.
<h2>Remove a Vagrant Machine</h2>
If you no longer need your vagrant machine at all, you can remove it with:

```bash
vagrant destroy
```

The Vagrantfile for your project will still exist, and you can create it again by running 'vagrant up'
