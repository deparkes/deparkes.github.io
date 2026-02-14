---
layout: post
title: Vagrant Ansible Provision
date: 2017-12-29 15:00:39.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- ansible
- provision
- vagrant
- virtual machine
author: deparkes
permalink: "/2017/12/29/vagrant-ansible-provision/"
---
<a href="https://www.vagrantup.com/">Vagrant</a> is able to provision its virtual machines in a number of ways, including using the '<a href="https://www.ansible.com/">ansible</a>' automation tool. This post looks at vagrant ansible provision and a simple example of how it could be used. As well as being a good tool for provisioning vagrant machines, using vagrant is also a good way to understand how ansible works.
<h1>Telling Vagrant To Use Ansible</h1>
We need to modify the <a href="https://www.vagrantup.com/docs/vagrantfile/">vagrantfile</a> to specify the provisioner, and where vagrant can find the provisioning configuration file. To keep things simple I am going to use '<a href="https://www.vagrantup.com/docs/provisioning/ansible_local.html">ansible_local</a>', a variant of the Vagrant's <a href="https://www.vagrantup.com/docs/provisioning/ansible.html">ansible provisioner</a> which installs ansible on the guest machine.

Ansible uses configuration files called '<a href="https://www.digitalocean.com/community/tutorials/how-to-create-ansible-playbooks-to-automate-system-configuration-on-ubuntu">playbooks</a>' and we need to tell vagrant where to find the playbook to provision a machine. A simple example of a vagrant file suitable for vagrant ansible provision is below:

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :
# encoding: UTF-8
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
  end
  config.vm.provider "virtualbox" do |v|
    v.gui = true
  end
end
```
<h1>Ansible Playbooks</h1>
The configuration file for ansible provisioning is called a '<a href="https://docs.ansible.com/ansible/latest/playbooks_intro.html">playbook</a>'. The playbook contains settings for running the ansible provisioning process. I go through an example playbook in the next section, but it is worth knowing a few general principles about playbooks first.
<h2>'Plays'</h2>
Ansible playbooks are broken down into a series of 'plays' - a series of tasks set to be run on a particular machine or group of machines.
<h2>'Hosts'</h2>
Ansible is capable of provisioning multiple machines from one playbook, and not all plays will apply to all host machines. The host option within a play specifies which machines should be affected by a play.
<h2>'Tasks'</h2>
The tasks carried out by a play are what really affect the host machine. A task runs different ansible modules to make changes to the host machine.
<h2>Ansible Modules</h2>
Ansible is designed to use different <a href="https://docs.ansible.com/ansible/latest/dev_guide/developing_modules.html">modules</a>. These modules are rather like a wrapper to functionality on the host machine. Ansible modules aren't 'magic', and you will still need to understand the host machine, such as package manager, file structure and so on to use them effectively.
<h2>White Space</h2>
Playbooks are written in '<a href="https://en.wikipedia.org/wiki/YAML">yaml</a>' - a markup language which is relatively easy for a human to read as it mostly does away with the requirement for opening and closing of tags. The downside to this readability is that it is very sensitive to white space. You may want to take a look at some of the guides out there about correctly formatting yaml files, at least so that you are aware of some of the problems
<h2>Different Notations</h2>
There is some <a href="https://www.jeffgeerling.com/blog/yaml-best-practices-ansible-playbooks-tasks">flexibility</a> in how playbooks can be written. On the one hand this is useful as you can write things in the way that makes the most sense for a given context. On the other hand it can make deciphering playbooks a challenge if you are not familiar with the different possible formats. There are guides to <a href="https://www.ansible.com/blog/ansible-best-practices-essentials">best practice</a> for writing playbooks to help.
<h1>An Example Vagrant Ansible Provision</h1>
The following example goes through pretty much the same steps as in my previous post about <a href="{{site.url}}/2017/12/07/vagrant-shell-script-provision/">provisioning a vagrant machine with a shell script</a>. (It is actually possible to use ansible to just run a shell script, but then you lose much of the power and flexibility it can bring.)

I use this example file to provision a virtual machine with some software unavailable in package managers. I use the ubuntu 'apt' package manager module to install a desktop environment and some dependencies (tcl/tk). I then use the 'file' and 'unarchive' to download and unpack an archive file from the web. I finally use the 'command' module to issue the commands needed to build my software. This example playbook uses a few different modules, and hopefully gives you a sense of how ansible works and how an ansible playbook fits together.
<h2>Using the 'apt' module</h2>
The first few plays use the '<a href="https://docs.ansible.com/ansible/latest/apt_module.html">apt</a>' module to <a href="{{site.url}}/2017/10/27/provision-desktop-environment-vagrant/">install lubuntu-desktop</a> and some other dependencies. The plays have a name which helps identify it within the playbook, as well as in the ansible reporting output. I have included the 'update_cache' option in each case - this is the equivalent of running '<a href="https://askubuntu.com/questions/222348/what-does-sudo-apt-get-update-do">apt-get update</a>' to update repository information. For simplicity I have set the 'hosts' to be all, although this can be configured to run only on particular machines or groups of machines.
<h2>Using the 'file' and 'unarchive' Modules</h2>
I use two more modules to download and unpack my software. Firstly the <a href="https://docs.ansible.com/ansible/latest/file_module.html">file</a> module checks that a directory exists, and creates it if not. Then the <a href="https://docs.ansible.com/ansible/latest/unarchive_module.html">unarchive</a> module gets an <a href="https://askubuntu.com/questions/25347/what-command-do-i-need-to-unzip-extract-a-tar-gz-file">tar.gz</a> at a remote location and unpacks it to the folder I just checked/created with file.
<h2>Using the 'command' module</h2>
My final play includes two tasks which use the <a href="https://docs.ansible.com/ansible/latest/list_of_commands_modules.html">command</a> module to run the commands needed to build the software. An important option to include is the <em>chdir</em> within <em>args</em>, to temporarily set the working directory to the one with my software in. Without this the command would be unable to find the scripts it needed, and would fail.

```yaml
---
# This is a 'play' to install lubuntu-desktop
- name: Install lubuntu-desktop
  hosts: all
  tasks:
    - name: Install tcl8.6-dev
      become: true
      apt:
        name: lubuntu-desktop
        install_recommends: no
        state: present
        update_cache: true
# This is a 'play' to install tcl/tk
- name: Install tcl/tk
  hosts: all
  tasks:
    - name: Install tcl8.6-dev
      become: true
      apt:
        name: tcl8.6-dev
        state: present
        update_cache: true
    - name: Install tk8.6-dev
      become: true
      apt:
        name: tk8.6-dev
        state: present
        update_cache: true
# This is a 'play' to download and unpack oommf
- name: Install oommf
  hosts: all
  tasks:
    - name: Ensure oommf directory exists
      become_user: vagrant
      file:
        path: ~/
        state: directory
    - name: Download and unpack OOMMF
      become_user: vagrant
      unarchive:
        src: https://math.nist.gov/oommf/dist/oommf20a0_20170929.tar.gz
        remote_src: yes
        dest: ~/
# This is a 'play' to download and unpack oommf
- name: Install oommf
  hosts: all
  tasks:
    - name: Run oommf distclean
      become_user: vagrant
      command: tclsh8.6 ./oommf.tcl pimake distclean
      args:
        chdir: ~/oommf
    - name: Run oommf distclean
      become_user: vagrant
      command: tclsh8.6 ./oommf.tcl pimake
      args:
        chdir: ~/oommf
```
