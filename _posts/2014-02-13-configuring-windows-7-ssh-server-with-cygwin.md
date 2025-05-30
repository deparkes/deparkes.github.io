---
layout: post
title: Windows ssh server cygwin setup
date: 2014-02-13 17:18:09.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- connection
- cygwin
- remote
- server
- setup
- ssh
- ssh keys
- symbolic links
- windows
- windows 7
author:
  display_name: deparkes
permalink: "/2014/02/13/configuring-windows-7-ssh-server-with-cygwin/"
---
<h1>How to set up a Windows ssh Server With Cygwin</h1>
Connecting to your Windows computer is useful for transferring data over a network. I don't have to always remember to keep a usb stick handy.
<h1>Bitvise: A personal use alternative to cygwin</h1>
For personal use I've found <a href="https://www.bitvise.com/winsshd">bitvise</a>  to be really useful, but unfortunately the free license doesn't extent to computers in an organisation, so it is good to know how to set up a windows server using the cygwin, which emulates a linux environment in windows.
<h1>Setting up Cygwin as an ssh server</h1>
How to Geek have a <a href="https://www.howtogeek.com/howto/41560/how-to-get-ssh-command-line-access-to-windows-7-using-cygwin/">good guide</a> to setting up an ssh server using openssh on cygwin.
You can then connect to your windows computer using your normal login with a program like putty, or for file transfer winscp.
Setting up <strong>symbolic links</strong>: Connecting to the cygwin server will drop you into the cygwin home directory. To make it quicker to navigate around I like to set up symbolic links (shortcuts) to my windows folders.

```
ln -s -v target link_name
```
e.g.

```
ln -s -v /cygdrive/c c
ln -s -v /cygdrive/c/<<user>>/Documents and Settings Documents
```
<strong>SSH keys</strong> are another way that we can make our life a little easier. I followed this <a href="https://www.digitalocean.com/community/articles/how-to-set-up-ssh-keys--2">guide </a>to setting them up. This helps you to set up the ssh keys and transfer the public key to a remote computer (also with . This remote computer will now have permission to connect to your computer.
