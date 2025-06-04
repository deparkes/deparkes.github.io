---
layout: post
title: Writing a Vagrantfile
date: 2018-04-30 16:30:51.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- DevOps
tags:
- devops
- vagrant
- virtual machine
- virtualbox
author: deparkes
permalink: "/2018/04/30/writing-a-vagrantfile/"
---
Vagrantfiles are used to configure vagrant virtual machines. This post goes a little beyond the <a href="{{site.baseurl}}/2018/01/12/basic-vagrant/">basics</a> of creating a Vagrantfile, and looks at some of the more advanced topics for writing a vagrantfile to make a more polished machine.

I have posted before about how you can <a href="{{site.baseurl}}/2017/12/29/vagrant-ansible-provision/">provision your virtual machine</a> via the vagrantfile - for example set which packages should be installed when the machine is created. This post shows how you can also use the vagrantfile to define characteristics of the machine itself including custom machine names, memory and cpu, networking and shared folders.
<h1>Naming the Vagrant Machine</h1>
When you create a vagrant virtual machine you will see that vagrant has given the virtual machine a fairly generic name. This might be fine for in some cases, but you may also want to have more control over the virtual machine name. There are actually <a href="https://stackoverflow.com/questions/17845637/how-to-change-vagrant-default-machine-name">a</a> <a href="https://stackoverflow.com/questions/17845637/how-to-change-vagrant-default-machine-name">few different ways</a> to interpret the 'machine name':
<ul>
<li>vagrant has its own name for the virtual machine created</li>
<li>the provider (e.g. virtualbox) will display a name for the virtual machine</li>
<li>the 'hostname' as it appears on the command line.</li>
</ul>
<h2>Vagrant's Own Name</h2>
Firstly, let's take a look at the name vagrant uses for the machine. Default is DIRECTORY_default_TIMESTAMP - this is often fine, but you may want to customise it. You can do this with:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
 config.vm.define "custom_vagrant_name"
end
```

<h2>Provider GUI Name</h2>
The name of the vagrant machine can also appear in the provider itself. You may also want to customise this too. This will be provider-specific, so you should check the details for your <a href="https://www.vagrantup.com/docs/providers/">provider</a>. If you are using virtual box you can use:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
  config.vm.provider "virtualbox" do |v|
   v.gui = true
   v.name = "custom_vm_name"
  end
end
```


<h2>The Hostname</h2>
The <a href="https://en.wikipedia.org/wiki/Hostname">hostname</a> is what your machine will appear as on a network, and what it will say on the command line when you log in.  The host name limited by soem rules or conventions of, mainly that it can be letters seprated by hypen or dot. Here's an example:

```ruby
Vagrant.configure("2") do |config|
 config.vm.box = "hashicorp/precise64"
 config.vm.hostname = "my-vagrant-machine"
end
```


<h1>Setting Memory and Number of Cores</h1>
Setting the hardware <a href="https://www.vagrantup.com/docs/virtualbox/configuration.html">configuration</a> can be really useful to do, particularly the memory and number of cores / CPUs. This is something else that is specific to the provider that you are using.
For example, the virtualbox provider can be configured like this:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise64"
 config.vm.provider "virtualbox" do |v|
   v.gui = true
   v.memory = 1024
   v.cpus = 2
  end
end
```

<h1>Opening / Forwarding Ports</h1>
You can open up ports / allow forwarding to allow you to access a port on your host machine and have all data forwarded to a port on the guest machine. You configure port forwarding with

```ruby
Vagrant.configure("2") do |config|
 config.vm.box = "hashicorp/precise64"
 config.vm.network "forwarded_port", guest: 80, host: 8080
end
```


<h1>Sharing Folders</h1>
Setting up a shared or synced folder makes working with a virtual machine much easier - you can share files between the host and the guest machine. You can do this in vagrant with the '<a href="https://www.vagrantup.com/docs/synced-folders/">synced_folder</a>' option:

```ruby
Vagrant.configure("2") do |config|
 config.vm.box = "hashicorp/precise64"
 config.vm.synced_folder "local_folder", "/guest/folder"
end
```

Which will sync a folder 'local_folder' in the same directory as your vagrantfile with a file in '/home/vagrant/guest/folder'. You can also explore more advanced folder syncing options such as NFS, rsync and samba shares.
<h1>Bringing It All Together</h1>
As an example of some of these more advanced vagrant file concepts here is an example - reference oommf vagrant build.

```ruby
Vagrant.configure("2") do |config|
 config.vm.box = "hashicorp/precise64"
 config.vm.network "forwarded_port", guest: 80, host: 8080
 config.vm.hostname = "my-vagrant-machine"
 config.vm.define "custom_vagrant_name"
 config.vm.synced_folder "local_folder", "/guest/folder"
 config.vm.provider "virtualbox" do |v|
 v.gui = true
 v.name = "custom_vm_name"
 v.memory = 1024
 v.cpus = 2
 end
end
```

