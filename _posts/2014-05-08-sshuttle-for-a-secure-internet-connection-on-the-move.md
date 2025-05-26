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
author:
  display_name: deparkes
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

Where user@domain.com are your login username (user) for your remote computer (domain.com). All your internet traffic will now be <strong>securely <a href="http://en.wikipedia.org/wiki/Tunneling_protocol">tunnelled</a></strong> through this remote computer.
You may need to <a href="http://www.wikihow.com/Change-Proxy-Settings"><strong>adjust your local proxy settings</strong></a> if the remote computer is normally set up for this.
For more details see:<a title="sshuttle github repository" href="//github.com/apenwarr/sshuttle"> https://github.com/apenwarr/sshuttle</a>, <a title="Video discussing sshuttle" href="https://hak5.org/episodes/hak5-1224">https://hak5.org/episodes/hak5-1224</a>, <a href="http://askubuntu.com/questions/45075/how-do-i-route-my-internet-through-a-ssh-tunnel">http://askubuntu.com/questions/45075/how-do-i-route-my-internet-through-a-ssh-tunnel</a>
<div id="yui_3_16_0_1_1423941869065_8092" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Brett Davies's photostream" href="https://www.flickr.com/photos/photosightfaces/" data-rapid_p="48" data-track="attributionNameClick">Image: Brett Davies; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-nc-sa/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="27">Some rights reserved</a><a class="owner-name truncate" title="Go to Brett Davies's photostream" href="https://www.flickr.com/photos/photosightfaces/" data-rapid_p="48" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1423941869065_8332" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
