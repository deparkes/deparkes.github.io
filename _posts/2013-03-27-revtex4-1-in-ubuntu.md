---
layout: post
title: How to install revtex4-1 in Ubuntu
date: 2013-03-27 15:43:45.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- Latex
tags:
- latex
- linux
- linux mint
- revtex
- ubuntu
author:
  display_name: deparkes
permalink: "/2013/03/27/revtex4-1-in-ubuntu/"
---
<h1>How to install revtex4-1 in Ubuntu...</h1>
I was having trouble installing <a href="https://journals.aps.org/revtex">revtex4-1</a> in <a href="https://www.ubuntu.com/">Ubuntu </a>(well, actually <a href="https://www.linuxmint.com/">Linux Mint</a>, but it's based on Ubuntu...). Suggestions to use revtex4-1.zip did not seem to work for me.
<h1>...use the 'texlive-publishers' package</h1>
In the end I found the solution to be a package "texlive-publishers" (<a href="https://ubuntuforums.org/archive/index.php/t-995840.html">https://ubuntuforums.org/archive/index.php/t-995840.html</a>)
To get revtex4-1 to work I just ran this in the terminal:

```bash
$ sudo apt-get install texlive-publishers
```
Simple.