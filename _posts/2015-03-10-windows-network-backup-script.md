---
layout: post
title: Windows Network Backup Script
date: 2015-03-10 17:29:55.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- backup
- windows
author: deparkes
permalink: "/2015/03/10/windows-network-backup-script/"
---
A simple<strong> Network Backup Script</strong> for windows.
This script uses <a title="Synctoy Automatic Backup" href="{{site.baseurl}}/2015/01/07/automatic-backup-synctoy/">synctoy </a>to backup data from your<strong> local computer</strong> to a <strong>remote network drive</strong>.
<strong>Run this script</strong> every time you want to <strong>backup your data</strong> to your remote drive.
<h3><a title="Synctoy Automatic Backup" href="{{site.baseurl}}/2015/01/07/automatic-backup-synctoy/">Find out more about using synctoy</a></h3>
<h1>Network Backup Script</h1>
Copy the below script into a text editor and save as a .bat file, e.g. "backup.bat".
Change the example path from "\\ad\data\Research\spintronics" to the one on your remote network drive.

```
net use P: \\ad\data\Research\spintronics
REM You should be prompted for password
REM For your user name use ad\<your username>
"C:\Program Files\SyncToy 2.1\SyncToyCmd.exe" -R
net use P: /delete
```

The first line <strong>maps the network drive</strong> specified in your network path to the drive letter P. I've picked P, but you can use any spare drive letter.
You can just use this part of the script, and <strong>manually copy across your files</strong> to the remote directory, but I think it makes much more sense to <strong>automate the process</strong>.
The second command does a<a title="Synctoy Automatic Backup" href="{{site.baseurl}}/2015/01/07/automatic-backup-synctoy/"> backup using synctoy</a>, a synchronisation program from Microsoft. This will<strong> synchronise</strong> your<strong> local folder</strong> with a remote one on the <strong>network drive</strong>.
Make sure you have downloaded and installed <a href="https://www.microsoft.com/en-gb/download/details.aspx?id=15155">synctoy </a>for this script to work properly.
Finally, the script <strong>closes your connection</strong> to the network drive.
