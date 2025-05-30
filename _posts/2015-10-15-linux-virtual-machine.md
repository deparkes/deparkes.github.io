---
layout: post
title: Try Out Linux With a Linux Virtual Machine
date: 2015-10-15 11:10:46.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- Linux
tags:
- linux
- virtual machine
author:
  display_name: deparkes
permalink: "/2015/10/15/linux-virtual-machine/"
---
This post shows you how to set up a virtual machine so you can try out Linux without having to do a full install on your physical system.
A virtual machine simulates the computer hardware such as the storage, memory and processor and let's you install an operating system directly to it.
So if you've heard about Linux, but aren't sure you're ready to install it on your system, then a virtual machine could be the thing for you.
<h1>VirtualBox</h1>
<h2>Download and Install Virtual Box</h2>
My preferred virtual machine software is VirtualBox which is available for Windows, OSX, Linux, and Solaris, and is relatively lightweight, and simple enough to install.
<h3><a href="https://www.virtualbox.org/wiki/Downloads">Download VirtualBox</a></h3>
<h2>Set Up The Virtual Machine</h2>
Once you have VirtualBox installed, you need to set up a virtual machine by setting its hardware and allocating resources.
Load up virtual box and hit "New" to create a  new machine. For now, just stick to the default settings.
<h3><a href="https://www.virtualbox.org/manual/ch01.html">Read a more detailed VirtualBox manual.</a></h3>

| ![For now you can probably get away with accepting the default settings for your new virtual machine]({{site.baseurl}}/assets/2015/10/VirtualBox-screen7.png) |
|:--:|
| *For now you can probably get away with accepting the default settings for your new virtual machine* |

<h1>Pick your Operating System</h1>
<h2>Light Weight Linux</h2>
You can install any operating system onto your new virtual machine, but as it will be relatively low-powered, it normally makes sense to go with a light-weight Linux distribution such as <a href="https://lubuntu.net/">Lubuntu </a>(a light weight version of Ubuntu)
<h3><a href="https://lubuntu.net/">Download Lubuntu</a></h3>
<h3><a href="https://www.linux.com/news/enterprise/systems-management/846633-best-lightweight-linux-distros">Check out more light-weight Linux distribtutions</a></h3>
<h1>Install The Virtual Operating System</h1>
Once you've picked the Linux distribution you want to try out you will need to download the disk image (usually a ".iso" file).
Click on the virtual machine's optical drive to load your Linux install disk image file and then just follow the normal install procedure of the operating system.

| ![Click on the virtual machine's optical drive to load the disk image]({{site.baseurl}}/assets/2015/10/VirtualBox-screen8.png) |
|:--:|
| *Click on the virtual machine's optical drive to load the disk image* |

<h3><a href="https://help.ubuntu.com/community/Installation">Get Help on Installing Lubuntu</a></h3>

| ![Just follow the normal install procedure for your operating system]({{site.baseurl}}/assets/2015/10/VirtualBox-screen9.png) |
|:--:|
| *Just follow the normal install procedure for your operating system* |


<h1>Try Out Your New Linux Virtual Machine</h1>
Your new virtual machine should now be working just like a physical one - give it a go!

| ![Try out your new Linux Virtual Machine]({{site.baseurl}}/assets/2015/10/VirtualBox-screen15-1024x768.png) |
|:--:|
| *Try out your new Linux Virtual Machine* |

<h1>Setting Up A More Advanced Virtual Machine</h1>
I first encountered virtual machines for learning Linux on a Software Carpentry course, where it is used to make sure all the students on the course have the same system and software. You can find some excellent instructions for setting up the kind of virtual machine used in a software carpentry course <a href="https://gist.github.com/benmarwick/11204658">here </a>which includes instructions for how to create virtual machine with a shared clipboard and shared folders with your physical machine, as well as automatically installing a number of useful programming tools and utilities.
<h3><a href="https://gist.github.com/benmarwick/11204658">Find out how to setup a more advanced virtual machine.</a></h3>

