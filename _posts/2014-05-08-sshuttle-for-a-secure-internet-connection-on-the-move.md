---
layout: post
title: sshuttle Ubuntu Install Instructions
date: 2014-05-08 13:54:10.000000000 +01:00
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
- security
- ssh
- sshuttle
- ubuntu
author: deparkes
permalink: "/2014/05/08/sshuttle-for-a-secure-internet-connection-on-the-move/"
---
<h1>sshuttle Ubuntu Installation</h1>
You're on your way back home. You arrive at the airport and realise you need to check your emails. Helpfully this airport provides free wi-fi, but you've heard that using free wi-fi like that can be asking for trouble.
The solution to this problem could be <strong>sshuttle</strong> - a program which provides a way for you to <strong>safely tunnel your internet traffic through a remote computer</strong>. If you trust the internet connection of your remote computer, you can <strong>trust that your network activity is secure</strong>.
<h1>To install on ubuntu is simple</h1>
To install sshuttle ubuntu, just type this at the terminal:

```bash
sudo apt-get install sshuttle
```
Once installed just type this:


```bash
sshuttle --dns -vvr user@domain.com 0/0
```

Where user@domain.com are your login username (user) for your remote computer (domain.com). All your internet traffic will now be <strong>securely <a href="https://en.wikipedia.org/wiki/Tunneling_protocol">tunnelled</a></strong> through this remote computer.
You may need to <a href="https://www.wikihow.com/Change-Proxy-Settings"><strong>adjust your local proxy settings</strong></a> if the remote computer is normally set up for this.
For more details see:<a title="sshuttle github repository" href="https://github.com/apenwarr/sshuttle"> https://github.com/apenwarr/sshuttle</a>, <a title="Video discussing sshuttle" href="https://hak5.org/episodes/hak5-1224">https://hak5.org/episodes/hak5-1224</a>, <a href="https://askubuntu.com/questions/45075/how-do-i-route-my-internet-through-a-ssh-tunnel">https://askubuntu.com/questions/45075/how-do-i-route-my-internet-through-a-ssh-tunnel</a>
