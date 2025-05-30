---
layout: post
title: Python XML Libraries
date: 2016-12-16 15:00:44.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
tags:
- data
- data structures
- data types
- elementtree
- lxml
- python
- xml
author:
  display_name: deparkes
permalink: "/2016/12/16/python-xml-libraries/"
---
<a href="https://en.wikipedia.org/wiki/XML">XML</a>, or Extensible Mark-up Language, is a set of rules for encoding data and documents in a way that is both human and machine readable. <a href="https://www.quora.com/What-are-some-practical-uses-of-XML">XML excels</a> where you need to transfer data between different systems, as there is almost always going to be an <a href="https://www.w3schools.com/xml/xml_parser.asp">XML parser</a> available. In this post I take a quick look at two Python XML libraries to help you work with XML data.
For a more comprehensive look at python xml libraries visit <a href="https://eli.thegreenplace.net/2012/03/15/processing-xml-in-python-with-elementtree">here.</a>
<h1>Python XML Libraries</h1>
<h2>ElementTree</h2>
The <a href="https://docs.python.org/3/library/xml.etree.elementtree.html">ElementTree </a>module introduces the <a href="https://effbot.org/zone/element-index.htm">Element data type</a> to python. The Element type is a cross between a <a href="https://www.tutorialspoint.com/python/python_lists.htm">list </a>and a <a href="https://www.tutorialspoint.com/python/python_dictionary.htm">dictionary </a>and is designed to store <a href="https://en.wikipedia.org/wiki/Hierarchical_database_model">hierarchical data structures</a> (like XML) in memory. The ElementTree library can load xml files as trees of ‘Element’ objects within Python.
ElementTree can both read and write xml files, as well as being able to search for sub-elements within XML data. You can also use ElementTree to create new XML files, and comes with various helper functions such as <a href="https://effbot.org/zone/xml-writer.htm">SimpleXMLWriter </a>which helps you generate well-formed XML data. ElementTree comes packaged with Python (since version 2.5), so should work without trouble.
<a href="https://pymotw.com/2/xml/etree/ElementTree/parse.html">Read more about ElementTree </a>on Python Module of the Week.
<h2>Lxml</h2>
<a href="https://lxml.de/">Lxml </a> is a library that builds on, and extends the functionality of ElementTree. Lxml uses C libraries for parsing XML, and should be much faster than ElementTree for larger XML files. Lxml is largely <a href="https://lxml.de/1.3/compatibility.html">compatibile </a>with the ElementTree API so to some extent you can use whichever is more convenient. There <a href="https://blog.startifact.com/posts/older/lxml-and-c-elementtree.html">doesn’t seem</a> to be a tremendous amount of controversy between ElementTree and lxml, although for simpler tasks you may find little difference between Lxml and ElementTree.
Get started with the <a href="https://lxml.de/tutorial.html">lxml tutorial.</a>
<a href="https://www.diveintopython3.net/xml.html">Dive Into Python</a> has a crash course in xml, as well has how you can parse xml with both ElementTree and Lxml.
