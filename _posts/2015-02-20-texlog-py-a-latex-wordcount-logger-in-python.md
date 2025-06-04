---
layout: post
title: texlog.py - A Latex Wordcount Logger in Python
date: 2015-02-20 21:02:45.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Latex
- python
tags:
- latex
- scripting
- software
- writing
author: deparkes
permalink: "/2015/02/20/texlog-py-a-latex-wordcount-logger-in-python/"
---
<h1>Log your wordcount in Latex</h1>
texlog.py is a <strong>simple python script </strong>for<strong> logging your wordcount</strong> in latex. The logging output put is saved as simple comma separated values which you can <strong>easily load into plotting software</strong>.
<strong><a href="https://github.com/deparkes/texlog">Download texlog.py from github</a></strong>
<h1>Building on texcount</h1>
If you use Latex for writing documents, you may well already be familiar with <a href="https://app.uio.no/ifi/texcount/">texcount</a>, a script for counting the number of words in a latex document. You can <a href="https://app.uio.no/ifi/texcount/">download </a>it as a stand-alone perl script, although it may also be bundled with your latex distribution, such as <a href="https://miktex.org/">Miktex</a>, or latex editor, like <a href="https://www.xm1math.net/texmaker/">Texmaker.</a>
This script is invaluable, particularly when writing large documents, or writing to a strict word limit. I thought it would be cool to be able to<strong> keep track of how many words</strong> I was writing on a particular document.
To do this I've made a <strong>python script</strong> that keeps a log of the output from the texcount script.
<h1>Texlog - a python script for wordcount logging</h1>
Texlog, available in a <a href="https://github.com/deparkes/texlog">github repository</a>, is a python script that calls texcount, and saves its output as text files that can be plotted in your favour plotting program.
This <strong>simple script</strong> can<strong> easily be edited</strong> to work on different files, and set different output files and directories.
If you are using a master file with included files, <a href="https://github.com/deparkes/texlog">texlog</a> can also output the word counts of those files separately, as well as the total count for the whole document.
<h2>Automated Logging</h2>
The most direct usage of the script is just to <strong>run it as a standalone</strong> python script. New data will be appended to the log files, so you <strong>won't have to worry</strong> about over-writing your log file.
You can <strong>automate your script</strong> using the standard scheduling approach for your software. On linux this will likely by <a title="crontab" href="{{site.baseurl}}/2014/05/17/crontab/">cron, </a>while on windows, you'll probably want to use the windows <a href="https://www.7tutorials.com/how-create-task-basic-task-wizard">task scheduler</a>.
<h2>Plotting the Data</h2>
The output files are just comma separated values with column headings, so you should have<strong> no problem plotting</strong> them in your favourite plotting software.
A date and time stamp is automatically included with each log write, so it is easy to <strong>build up a time-series</strong> of your writing progress.
<h2>Feature wish list</h2>
For the most part this little script is as I need it for now. If I get time in the future, these are a few things that I might work on:
<ul>
<li>Improved readme</li>
<li>Commandline usage</li>
<li>Optparser for setting input file, output file, usage options</li>
<li>Option for storing other stats e.g. number of chapters, sections, words per section</li>
</ul>
