---
layout: post
title: Notepad2-mod for editing OOMMF Files
date: 2014-05-13 09:42:50.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- how to
- notepad2-mod
- oommf
- useful
author: deparkes
permalink: "/2014/05/13/notepad2-mod-for-editing-oommf-files/"
---
I like using Notepad2-mod (see<a title="Useful software" href="{{site.baseurl}}/2014/05/08/useful-software/"> useful software</a>, <a href="https://xhmikosr.github.io/notepad2-mod/">notepad2-mod webpage</a>) to edit OOMMF mif files, but I do generally find it a lot easier to edit if the syntax is highlighted. Since mif files are essential tcl we can just tell notepad2 to treat mif files as tcl files for the purposes of highlighting:

- Open Notepad2-mod
- View -> Customize Schemes
- Scroll down to Tcl Script.
- In the "Associated filename extensions:" box add (without quotation marks) "; mif" to the existing entries.
- Click ok.
- Now when you open mif files in notepad2-mod you should find the syntax is highlighted by default.

