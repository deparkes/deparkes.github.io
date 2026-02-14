---
layout: post
title: Use Vagrant With Git
date: 2018-01-19 15:00:26.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- collaboration
- devops
- git
- vagrant
- version control
- virtual machine
author: deparkes
permalink: "/2018/01/19/use-vagrant-git/"
---
<a href="https://wp.me/p4DE9r-X5">Vagrant </a>is a tool for managing virtual machines. By combining vagrant with git (and shared git repositories like <a href="https://github.com/">github</a> or <a href="https://bitbucket.org/">bitbucket</a>) it is possible to share machine configurations. This post explores how using vagrant with git works and some possible challenges with <a href="{{site.url}}/2017/12/15/basic-git-simple-collaborative-working/">collaborating</a> with vagrant machines.
<h1>Sharing Virtual Machines</h1>
Sharing virtual machine images can be useful to provide a <a href="https://dzone.com/articles/works-on-my-machine">consistent</a> development or test environment, or to allow colleagues to run software not available on their usual operating system. Unfortunately, virtual machine images can be <a href="https://www.tintri.com/blog/2016/05/data-dive-vm-sizes-real-world">very large</a> - the base operating system alone can already be several gigabytes before any additional packages or software are installed. This large file size makes it impractical to share virtual machines directly.
An alternative is to use Vagrant, which uses small plain text '<a href="https://www.vagrantup.com/docs/vagrantfile/">vagrantfiles</a>' to hold the commands needed to configure a virtual machine. The vagrantfiles are small, easy to share, and lend themselves to version control with a tool like git.
Vagrantfiles specify how to build up from a 'base' operating system with additional software, packages, users and so on. The vagrantfile can be shared, rather than the full virtual machine image. Combining vagrant with git and collaboration services such as github or bitbucket are a powerful way to share virtual machine configurations for collaborators to use.
<h1>Software Requirements</h1>
So if collaborating with virtual machines using vagrantfiles is a good idea, what are the software requirements for this?
To be specific, I am thinking about using vagrant with git for :
a) version control of virtual machines
b) sharing of virtual machine configurations
To do this a user would need:
<ul>
<li>
<a href="https://www.atlassian.com/git/tutorials/install-git">Git installed</a> on their local machine</li>
<li>
<a href="https://www.vagrantup.com/docs/installation/">Vagrant installed</a> on their local machine</li>
<li>A virtualisation provider (such as <a href="https://www.virtualbox.org/">virtualbox</a>)</li>
<li>Access to a shared/remote git repository such as <a href="https://github.com/">github</a>
</li>
</ul>
<h1>An Example Of How Vagrant With Git Could Work</h1>
In theory using vagrant with git should be quite straightforward, but I wanted to think about an example situation. This hypothetical example explores the process of using vagrant with git and exposes some possible challenges.

Alice and Bob both run windows machines and are developing some Linux-based software. They decide to use virtual machines running Linux as a development environment so they can be sure that their shared code will work for both of them. Rather than starting from a Linux install disk to create a virtual machine, Alice decides to <a href="https://wp.me/p4DE9r-X5">configure a vagrant machine</a> which they can both use.

Alice and Bob collaborate on code development with github, using a <a href="{{site.url}}/2017/12/15/basic-git-simple-collaborative-working/">simple git collaboration approach</a>. Alice creates a git repository which she will use to hold the vagrantfile and any other configuration files needed to setup the virtual machine.

Alice creates a vagrantfile based on and <a href="https://app.vagrantup.com/bento/boxes/ubuntu-16.04">Ubuntu base box</a>. There are a few packages and configuration changes that she and Bob both need to develop with so she incorporates these into a <a href="{{site.url}}/2017/12/07/vagrant-shell-script-provision/">simple provisioning script</a> for the vagrant virtual machine. She makes a series of commits to her  local git repository and when she is happy with the machine she pushes her changes to the github repository.

Bob is now able to pull from this repository and have the same virtual machine configuration as Alice. While he is working on the virtual machine he realises that one of the packages is not configured correctly. He makes changes to the provisioning script they are using and pushes his changes to their shared repository. Alice can easily pull down these changes herself and re-provision her own machine.

A new collaborator, Cyril, joins Alice and Bob to help with their project. Alice updates the readme of their project to explain how to install vagrant and git, clone the github repository and initialise the vagrant box. Cyril can now easily work with the same system configuration as Alice and Bob.
<h1>Some Other Things To Consider</h1>
Collaborating with others introduces some other things to consider. I have identified a couple here, but there are probably others.
<h2>Provider Compatability</h2>
Vagrant relies on '<a href="https://www.vagrantup.com/docs/providers/">providers</a>' - such as <a href="https://www.virtualbox.org/">Virtualbox</a>, <a href="https://www.microsoft.com/en-us/cloud-platform/server-virtualization">HyperV</a> and <a href="https://www.vmware.com/">VMware</a> - to actually run the virtual machines it configures. Vagrant provides some level of standardisation across these different providers, but this situation can add complexity.

Not all boxes exist for all providers and not all providers exist for all systems (e.g. HyperV is specific to . Many boxes are only available for a few providers and if your system is unable to run one of those providers or you don't have access to it then you cannot run the machine.
Given these issues it is important to consider who your users or collaborators for a vagrant machine are when you select a base box for your system.
<h2>Box Versioning</h2>
To add to the complexities of selecting a base box for your vagrant virtual machine, boxes can have <a href="https://www.vagrantup.com/docs/boxes/versioning.html">different versions</a>. Some boxes are frequently updated, and it is possible that software or configuration that works in one version does not work in another.

Vagrant will default to selecting the most recent box version available. This can be good if you need the latest versions and patches, but you may find it better to be specific about exactly which version of a box should be used.
