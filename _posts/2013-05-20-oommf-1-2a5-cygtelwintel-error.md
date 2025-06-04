---
layout: post
title: OOMMF 1.2a5 cygtel/wintel error
date: 2013-05-20 11:18:54.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- OOMMF
tags:
- cygwin
- error
- install
- issue
- oommf
- problem
author: deparkes
permalink: "/2013/05/20/oommf-1-2a5-cygtelwintel-error/"
---
My windows installation of OOMMF 1.2a5 was giving an error* about my platform not being 'cygtel', and then failing to run.
To get around this error and allow OOMMF to actually run I just changed the filename of  'cygtel.tcl' (found in '/oommf/config/names/') to 'wintel.tcl'. I left the contents of the file the same.
Since there already exists a file called 'wintel.tcl' I renamed this to wintelOLD.tcl. (If you want to keep an 'old' version of 'cygtel.tcl' you will need to put it in a different folder, as OOMMF seems to get confused otherwise.)
* I don't know exactly why this error was occuring. Possibly something to my having cygwin installed on my computer.
