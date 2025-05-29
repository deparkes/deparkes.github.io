---
layout: post
title: Easy Notepad Journal
date: 2015-12-14 09:00:18.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- software
tags:
- journal
- logging
- notepad
author:
  display_name: deparkes
permalink: "/2015/12/14/easy-notepad-journal/"
---
<h3>In this post I show you how you can make easy notepad journal, using <a href="https://en.wikipedia.org/wiki/Notepad_%28software%29">Notepad.exe </a>- the default text editor for Windows.</h3>
I'll show you how you can get notepad to automatically append today's date to the end of a file which makes it easy to keep a track of notes or journal entries.
<h1>Add '.log' to your text file to make a Notepad Journal</h1>
All you have to do is put the line (note the upper case):

```
.LOG
```
into your text file, like so:

| ![Journal with notepad]({{site.baseurl}}/assets/2015/12/Log1.png) |
|:--:|
| *Journal with notepad* |

The next time you open your file, notepad will put a date and time stamp at the bottom of your file - something like this:
```
15:32 2014-12-11
```

| ![Journal with notepad]({{site.baseurl}}/assets/2015/12/Log2.png) |
|:--:|
| *Journal with notepad* |

<h1>Notepad will add a new timestamp each time you open your log</h1>
When you re-open your (saved) log file, notepad will insert a new date/time stamp for this new entry.

| ![Journal with notepad]({{site.baseurl}}/assets/2015/12/Log3.png) |
|:--:|
| *Journal with notepad* |

<h3>You can also use this trick to make a notepad journal my favourite text editor - <a href="https://xhmikosr.github.io/notepad2-mod/">notepad2-mod</a>
</h3>
