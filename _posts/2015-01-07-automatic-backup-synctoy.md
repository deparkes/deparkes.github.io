---
layout: post
title: Synctoy Automatic Backup
date: 2015-01-07 17:58:26.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- backup
- synchronise
- windows
- windows 7
author:
  display_name: deparkes
permalink: "/2015/01/07/automatic-backup-synctoy/"
---
<blockquote>"Backing up is easy, the hard part is remembering to do it" - a wise man</blockquote>
With that in mind this post shows you how to <strong>automatically backup your files</strong> on your windows computer.
For information on backing up a linux computer checkout this <a title="Keeping in sync with rsync" href="{{site.baseurl}}/2014/02/14/keeping-in-sync-with-rsync/">post on rsync</a>.
<h1>Microsoft Synctoy</h1>
There are no doubt scores of different synchronising and backup programs for windows, but the best I've found is synctoy. It's made by microsoft, and works well.
Get synctoy <a href="http://www.microsoft.com/en-gb/download/details.aspx?id=15155">here.</a>
Using it is simple enough. You just pick the source and target directories and run it.
There are different modes you can run your synchronisation in. For backup purposes I recommend setting your folder pairs to "<strong>Contribute</strong>" which prevents your local deletions from propagating through to your backup. If you're really sure you don't want a file, just delete both the local and backup versions.
<h2>Automatic Backup With Synctoy</h2>
Synctoy becomes really powerful if you use it to <strong>automate your backups</strong>.
We do this by using the <strong>task scheduler</strong>.
There's a good guide to doing this <a href="http://www.howtogeek.com/howto/25046/schedule-synctoy-to-run-automatically-with-task-scheduler-in-windows-7/">here.</a>
<h1>Network Drives</h1>
If you're lucky enough to have a mapped network drive to back your work up to, then you need to be a bit more clever.
The windows task scheduler doesn't know about your local drive names (like C:\, Z:\, etc.). Instead you need to use the '<a href="http://en.wikipedia.org/wiki/Path_%28computing%29#UNC_in_Windows">UNC</a>' path: something like "<code>\\host\directoryname</code>".
You can find the unc path for all your mapped network drives by running
```
net use
```
at the command line.
Use the entry under the Remote heading for the drive you would like to backup to.
<div id="yui_3_16_0_1_1423943112907_11688" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to David Zellaby's photostream" href="https://www.flickr.com/photos/toymaster/" data-rapid_p="25" data-track="attributionNameClick">Image: David Zellaby; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-nc-nd/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="29">Some rights reserved</a><a class="owner-name truncate" title="Go to David Zellaby's photostream" href="https://www.flickr.com/photos/toymaster/" data-rapid_p="25" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1423943112907_11919" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
