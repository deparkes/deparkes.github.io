---
layout: post
title: How to use rsync
date: 2014-02-14 14:53:30.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- backup
- cygwin
- install
- linux
- rsync
- ssh
- ssh keys
- synchronise
- synchronize
- ubuntu
- windows
author:
  display_name: deparkes
permalink: "/2014/02/14/keeping-in-sync-with-rsync/"
---
<h1>rysnc - for keeping remote folders synchronised</h1>
<a href="https://en.wikipedia.org/wiki/Rsync">rsync </a>is really good for keeping folders synchronised across two computers. With one command new or changed files can be sent over a network. It is even possible to compress and send the data securely via <a href="https://en.wikipedia.org/wiki/Secure_Shell">ssh</a>.
The procedures for using it are a little different for linux and Windows. There are already quite a few good guides on the internet for this,  and I have tried to bring some of them together here.
<h1><strong>Installing</strong></h1>
<h2><em>Installing - Ubuntu/Linux</em></h2>
On ubuntu it is easy to install rsync. From a terminal type:

```bash
sudo apt-get install rsync
```

similar commands will exist for other flavours of Linux.
<h2><em>Installing - Windows</em></h2>
In windows we need to use cygwin to access rsync. This is easy enough: just run the cygwin setup file. Search for 'rsync' and install it.


| ![rsync screenshot]({{site.baseurl}}/assets/2014/02/rsync-screen-shot.png) |
|:--:|
| *You can install rsync in windows using cygwin.* |


If you haven't done so already I'd also recommend setting up <a href="https://en.wikipedia.org/wiki/OpenSSH">openssh </a>on <a href="https://www.cygwin.com/">cygwin </a>at the same time (I've covered this <a title="Configuring Windows 7 ssh server with cygwin" href="https://deparkes.wordpress.com/2014/02/13/configuring-windows-7-ssh-server-with-cygwin/">here</a>).
<h1><strong>How to use rsync
</strong></h1>
Once installed on windows or linux, the usage of rsync should be pretty much the same.

```bash
rsync -avz -e ssh --exclude "*Trash*/" --exclude "*gconf*/" ~/ user@host:~/cygdrive/c
```

where the `-e ssh` indicates that we will connect via ssh - with ssh keys set up we won't need a password everytime we run this command. There are also <code>'--exclude'</code> commands to ignore certain files or folders. This can be useful if there are temporary files that you don't care about moving.
I like to have rysnc commands in a script to make it quicker and easier to synchronise my folders. rsync commands can also be scheduled with cron.
<h2>rsync and ssh</h2>
Using SSH keys can make synchronising between computers a bit more straightforward as you don't have to type your password in each time to connect to the remote computer. This is something I've written about <a title="Configuring Windows 7 ssh server with cygwin" href="deparkes.co.uk/2014/02/13/configuring-windows-7-ssh-server-with-cygwin/">previously</a>.
Further information on setting up rsync is available <a href="https://kvz.io/blog/2007/08/16/synchronize-files-with-rsync/">here</a> or on the rsync website, and some more examples are available <a href="https://www.thegeekstuff.com/2010/09/rsync-command-examples/">here</a>.
