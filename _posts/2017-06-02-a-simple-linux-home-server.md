---
layout: post
title: A Simple Linux Home Server
date: 2017-06-02 15:30:24.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- home server
- linux
- netowrk
- putty
- security
- server
- ssh
- windows
author:
  display_name: deparkes
permalink: "/2017/06/02/a-simple-linux-home-server/"
---
This post shows you how to set up a simple linux <a href="http://www.quepublishing.com/articles/article.aspx?p=1692557">home server</a>, and how you can use it to share files across your home network. This simple process will help get you going with a basic home server system which will be flexible enough for you to extend and develop.
<h1>1. Select Your Hardware</h1>
Almost any desktop or laptop made in the last 10 years should suffice, unless you are planning to run some intensive programs for many users (unlikely on a home network). Storage is more likely to be an issue with older systems, particularly if you want to store and share photos, videos and music at home. If that is a concern you may want to get a new hard drive.
I like to re-purpose old laptops to use as servers - once they stop being useful for day-to-day use, they can still be powerful enough for use as a server. On the whole, <a href="http://smallbusiness.chron.com/laptop-vs-pc-power-consumption-79347.html">laptops also use less energy than desktops</a>, which is good if you intend to leave your server on for extended periods of time.
If you don't have some old hardware available, or would prefer something new, you could also try a relatively inexpensive home server solution from Dell or HP, or start with a 'bare bones' system and add your own components.
<h1>2. Install An Operating System</h1>

| ![linux home server - operating system]({{site.baseurl}}/assets/2017/06/VirtualBox_Lubuntu_install_20_05_2017_11_07_49.png) |
|:--:|
| *linux home server - operating system* |

I like <a href="https://www.ubuntu.com/">Ubuntu </a>as an operating system - it is built on the power of <a href="https://www.debian.org/">Debian</a>, but is generally <a href="https://www.youtube.com/watch?v=qHGTs1NSB1s">easier to install</a>. You will also find <a href="https://askubuntu.com/">a wealth of resources </a>to help you if you get stuck with Ubuntu, which is in itself a benefit.
Ubuntu comes in a few <a href="https://www.ubuntu.com/about/about-ubuntu/flavours">different flavours</a>, and there is also <a href="https://www.ubuntu.com/download/server">Ubuntu specifically for servers</a>, which doesn't come with a desktop as standard. The Ubuntu server edition is just <a href="https://askubuntu.com/questions/31081/whats-the-difference-between-the-server-version-and-the-desktop-version">the same as the desktop editions</a>, so we could go with that as our operating system if we wanted. If like me, however, you are not completely confident working in a purely command-line environment, a good middle ground is to install the light-weight '<a href="http://lubuntu.net/">Lubuntu</a>'. This installs a light-weight desktop environment that you can use if you get stuck, and then add in the server components as you need them.
If you are using older, less powerful hardware, you may wish to use the '<a href="https://help.ubuntu.com/community/Lubuntu/Documentation/AlternateInstall">alternate install'</a> method which is suitable for lower-spec machines. Otherwise you can use the standard <a href="https://help.ubuntu.com/community/Lubuntu/InstallingLubuntu">Graphical install</a> via a Live CD.
If you are using a laptop, you may also wish to configure how Ubuntu behaves when you close the laptop lid. For me it made sense to <a href="https://askubuntu.com/questions/15520/how-can-i-tell-ubuntu-to-do-nothing-when-i-close-my-laptop-lid/372616#372616">turn the screen off, but not put the machine to sleep or hibernation mode</a>.
<h1>3. Allow Remote Access</h1>

| ![linux home server - remote access]({{site.baseurl}}/assets/2017/06/open_ssh_server.png) |
|:--:|
| *linux home server - remote access* |

Once you have installed the Lubuntu operating system, you should configure it to allow remote access. We will do this for within your home network only. It is possible to run your server as a webserver, but you do then have to <a href="https://www.thefanclub.co.za/how-to/how-secure-ubuntu-1604-lts-server-part-1-basics">be</a> <a href="http://www.datamation.com/open-source/how-to-secure-your-ubuntu-network.html">more</a> <a href="https://ubuntuforums.org/showthread.php?t=1258628">security</a> <a href="https://www.reddit.com/r/HomeServer/comments/5o909f/home_server_security/">conscious</a>.
<h3>a) Set up static IP address</h3>
Giving your server a static IP address means you will be able to connect to it using the same address each time (e.g. 192.168.0.19) . The simplest way to do this is probably at your router. The exact details of this will vary depending on the model of your router, but the steps should be similar to those in <a href="https://www.howtogeek.com/184310/ask-htg-should-i-be-setting-static-ip-addresses-on-my-router/">this guide</a> - you need to tell your router to always assign the same IP address to your server machine.
<h3>b) Install ssh server on Lubuntu</h3>
The ssh server allows you to securely connect to your server machine. There are plenty of<a href="https://help.ubuntu.com/community/SSH/OpenSSH/Configuring"> guides to install ssh server</a> on Ubuntu, and it is generally painless. Once ssh server is installed, it just operates as a service on your machine, and you can <a href="https://www.cyberciti.biz/faq/howto-start-stop-ssh-server/">start and stop the ssh server</a> as you see fit.
This <a href="https://help.ubuntu.com/community/SSH/OpenSSH/Configuring">guide</a>  also suggests setting up '<a href="https://en.wikipedia.org/wiki/Public-key_cryptography">ssh keys</a>'. This can make things easier, particularly for more advanced things, but is not essential. If you do decide to configure public / private keys, there are more detailed resources available, particularly for <a href="http://support.hostgator.com/articles/specialized-help/technical/ssh-keying-through-putty-on-windows-or-linux">ssh keys with Windows</a>. Use of ssh keys can also<a href="https://www.thefanclub.co.za/how-to/how-secure-ubuntu-1604-lts-server-part-1-basics"> make your home server more secure</a>, and is a step in <a href="https://superuser.com/questions/429383/hardening-a-home-server">'hardening' your server</a>.
<h3>c) Check the connection to your server</h3>
You should now be able to connect to your new home server from other machines on your network (using the static IP address you created). From a Windows machine I suggest using <a href="https://mediatemple.net/community/products/dv/204404604/using-ssh-in-putty-">Putty</a>. You will connect to your server using the same user name and password that you would do login in directly.
If you like, you can stop at this stage, and use something like <a href="https://winscp.net/eng/download.php">winscp</a> to transfer files between your machines. I like to go a step further and set up my server to share folders I can access from within Windows Explorer.
<h1>4. Configure File Sharing</h1>

| ![linux home server - windows samba]({{site.baseurl}}/assets/2017/06/WindowsSambaFolder.png) |
|:--:|
| *linux home server - windows samba* |

You can also allow the windows machines on your network to access shared folders on your linux home server.
You can <a href="https://help.ubuntu.com/community/How%20to%20Create%20a%20Network%20Share%20Via%20Samba%20Via%20CLI%20%28Command-line%20interface/Linux%20Terminal%29%20-%20Uncomplicated%2C%20Simple%20and%20Brief%20Way%21">set up file sharing over the command line</a>, using Putty to connect remotely if you need. If you would prefer, it is also possible to <a href="https://www.howtogeek.com/74459/how-to-create-samba-windows-shares-in-linux-the-easy-way/">configure the file sharing from with the Lubuntu desktop</a> - the steps are essentially the same, just with a graphical interface.
If you have done that correctly your windows machine should now show your new, shared folder as available to access. Double click on it and you will be prompted for the Samba username and password you configured on your server.
If you do have trouble seeing your shared folder, you can type \\ followed by the IP address for your server into the Windows Explorer address bar (e.g. \\192.168.0.24) which should then show you the shared folders available on your server.
