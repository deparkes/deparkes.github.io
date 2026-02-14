---
layout: post
title: Plot the Publications in Your Thesis
date: 2015-10-20 16:21:48.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- Latex
- python
tags:
- data
- latex
- pandas
- python
- references
author: deparkes
permalink: "/2015/10/20/plot-the-publications-in-your-thesis/"
---
<h1><strong>How recent are the references in your thesis or dissertation?</strong></h1>
Have you only cited papers from the last few years? Or have you gone back to find dozens of pre-war publications?
I thought it would be interesting to find out, so I made a python script to plot the publications in your thesis.
In my case the output came out looking like this:
<h3>Have a Go Yourself</h3>

| ![Plot the Publications in Your Thesis]({{site.url}}/assets/2015/10/RefCountThesis.png) |
|:--:|
| *Plot the Publications in Your Thesis* |

In principle this script should work on pretty much any latex document with references (or at least those that generate a .bbl file - see below). My initial thought was that this would be for long documents such as theses or dissertations, but it could also work for papers
The first step is to:
<h2><a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">Download the Python Script</a></h2>
To run the <a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">RefCount.py</a> script you will need these packages:
<ul>
<li>re</li>
<li>pandas</li>
<li>collections</li>
<li>matplotlib</li>
</ul>
I normally use <a href="https://www.continuum.io/downloads">Anaconda </a>to help me manage my python packages
<h1>Search Through Your .bbl File</h1>
The script "<a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">RefCount.py</a>" works by searching through the .bbl file generated when you build your latex document.
<a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">RefCount.py </a>will need to be in the same folder as the .bbl file, so you could save RefCount.py into your latex build folder.
I would recommend making a copy of your .bbl file and putting it together with RefCount.py in a separate folder, e.g. "RefCount".
<h2>Regular Expressions - some assembly required</h2>

| ![Regular expressions - some assembly required]({{site.url}}/assets/2015/10/RegEx.png) |
|:--:|
| *Regular expressions - some assembly required* |

The actual searching through the .bbl file is done using a <a href="https://en.wikipedia.org/wiki/Regular_expression">regular expression</a>, which searches for matches to a particular string.
In <a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">RefCount.py</a> the regular expression is looking for years, such as 1985, 2010, 1908, etc., within the .bbl file. Of course these can be found in different ways, such as at the end of a sentence e.g. '1985.' or inside brackets '(1985)'.
For RefCount.py to work you will have to set the regular expresssion so that it can find the dates in your .bbl file.
<h3>Some Sample Regular Expressions</h3>
Regular expressions can be a bit tricky, so here are a couple of expressions that I've found to work on some common .bbl
4-digit numbers in parentheses e.g. '(1985)'.

```
"\(([0-9]{4})\)"
```

4-digit numbers (with or without a close-parenthesis), followed by a full stop, and end of line.

```
"([0-9]{4})\)*\.|$"
```

Hopefully these will be sufficient for most situations, but if you do need to build your own then <a href="https://pythex.org/">pythex.org</a> is a useful site for testing out regular expressions - just copy in the text from your .bbl file as "Your test string:".
<h3>If you're still having problems extracting the date from your .bbl file - leave a comment below and I'll see if I can help you out.</h3>
<h1>Some Example Graphs</h1>
Here are some examples of the kind of output you can expect from <a href="https://gist.github.com/deparkes/f51b5eaf35bdde3a0c00">RefCount.py</a>.


<a href="{{site.url}}/assets/2015/10/RefCountRobin1.png"><img class="aligncenter wp-image-2206" src="{{site.url}}/assets/2015/10/RefCountRobin1-1024x736.png" alt="Plot the Publications in Your Thesis" width="360" height="259"></a> <a href="{{site.url}}/assets/2015/10/RefCountJames.png"><img class="aligncenter wp-image-2204" src="{{site.url}}/assets/2015/10/RefCountJames-1024x736.png" alt="Plot the Publications in Your Thesis" width="360" height="259"></a> <a href="{{site.url}}/assets/2015/10/RefCountDuncan.png"><img class="aligncenter wp-image-2202" src="{{site.url}}/assets/2015/10/RefCountDuncan-1024x736.png" alt="Plot the Publications in Your Thesis" width="360" height="259"></a>
