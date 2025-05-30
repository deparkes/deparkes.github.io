---
layout: post
title: Some Samba Basics
date: 2017-06-09 15:30:31.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- basics
- file sharing
- how to
- network
- samba
- server
author:
  display_name: deparkes
permalink: "/2017/06/09/some-samba-basics/"
---
<a href="https://en.wikipedia.org/wiki/Samba_(software)">Samba </a>is a protocol that makes file sharing across a network easy (great if you have your own home server). This post has a few samba basics - commands and operations to help you configure and run your samba shared folders.
<h1>Setting up samba</h1>
Read about <a href="{{site.baseurl}}/2017/06/02/a-simple-linux-home-server/">how you can setup and configure Samba</a> for a simple home server.
<h1>Restart samba</h1>
If something goes wrong, turning Samba off and on again can be a solution.
Read <a href="https://askubuntu.com/questions/79078/how-to-restart-samba-server">this response</a> for more details.
<h3>Start Samba Service</h3>

```
sudo service smbd start
```

<h3>Stop Samba Service</h3>

```
sudo service smbd stop
```

<h3>Restart Samba Service</h3>

```
sudo service smbd restart
```

<h1>Find the name of the Samba Service</h1>
If you're not sure of your Samba service name, you can list your services with this command:

```
service --status-all
```

<img class="aligncenter size-full wp-image-3406" src="{{site.baseurl}}/assets/2017/06/samba_service.png" alt="samba basics - samba service name" width="802" height="391">
<h1>List samba users</h1>
It can be useful to be able to <a href="https://superuser.com/questions/271034/list-samba-users">list current Samba users</a>. You can do this with:

```
sudo pdbedit -L -v
```

<a href="https://www.samba.org/samba/docs/man/manpages/pdbedit.8.html">pdbedit </a>is a tool for working with the database of Samba users. The -L flag lists users, and -v makes the output verbose.
<h1>Reset samba passwords</h1>
To <a href="https://ubuntuforums.org/showthread.php?t=1687199">reset the password of a samba user</a>, you can add the user name to samba again:
Code:

```
sudo smbpasswd -a user-name
```

If you aren't sure of the user names, see 'List Samba Users', above.
<h1>Clear windows connection cache</h1>
If you do change the password on a Samba user account, you may find you have trouble connecting via windows. One solution to this is to <a href="https://www.golinuxhub.com/2013/12/multiple-connections-to-server-or.html$or.html&gt;">clear the windows connection cache</a>.
First run <code>net use</code> to see what connections are stored. In this case I hvae a stored connection to my <a href="{{site.baseurl}}/2017/06/02/a-simple-linux-home-server/">Lubuntu file server</a>.

| ![samba basics - net use]({{site.baseurl}}/assets/2017/06/net_use.png) |
|:--:|
| *samba basics - net use* |

If I was having trouble with this connection I would <code>run net use /delete \\LUBUNTU\IPC$</code> to remove it. The output confirms this connection has been removed.

| ![samba basics - net use delete]({{site.baseurl}}/assets/2017/06/net_use_delete.png) |
|:--:|
| *samba basics - net use delete* |

If we try to list connections, we will be told there are none:

| ![samba basics - no entries]({{site.baseurl}}/assets/2017/06/net_use_no_entries.png) |
|:--:|
| *samba basics - no entries* |

A new connection will be added the next time we try to connect to our Samba folder via windows explorer.
