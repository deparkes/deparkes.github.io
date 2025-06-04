---
layout: post
title: Parse Wordpress Post Export With Python
date: 2021-02-06 13:18:34.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Wordpress
tags:
- parsing
- python
- rss
author: deparkes
permalink: "/2021/02/06/parse-wordpress-post-export-with-python/"
---
Within Wordpress<a href="https://codesteps.com/2018/10/11/wordpress-export-the-posts-pages-or-media-content/"> it is possible to export all historic posts</a> as an XML file. This XML file is a little unwieldy, but it is possible to parse the Wordpress post export with python. This post shows how you can use the python <a href="https://feedparser.readthedocs.io/en/latest/">feedparser</a> library to easily access the export elements.
When you do this Wordpress is keen to emphasise that this is not intended as a backup, so be warned.
<h2>Wordpress Post Export</h2>
One option for handling this exported XML file is to <a href="https://www.geeksforgeeks.org/xml-parsing-python/">manually parse</a> it to access the elements you are interested in.
As it happens however, the Wordpress export XML is close enough to the an <a href="https://www.w3schools.com/XML/xml_rss.asp">RSS feed</a>, that we can use the python package <a href="https://feedparser.readthedocs.io/en/latest/">feedparser</a>.
<h3>Parse With Feedparser</h3>
Feedparser can parse <a href="https://feedparser.readthedocs.io/en/latest/introduction.html#parsing-a-feed-from-a-remote-url">URLs</a> or <a href="https://feedparser.readthedocs.io/en/latest/introduction.html#parsing-a-feed-from-a-local-file">local files</a>. Once you have exported your Wordpress posts you can parse the the resulting xml file with this python code:

```python
import feedparser
data = feedparser.parse('./data/deparkes.WordPress.2021-01-23.xml')
```

Once you have loaded the parsed data, you can explore it following the principles described on <a href="https://waylonwalker.com/parsing-rss-python">this page</a>.
As a quick example, here is how you could extend that script to access the actual content of reach post.

```python
posts = []
for entry in data['entries']:
    posts.append(entry['content'][0]['value'])
```

In this case you may also want to clean up the html from within the posts, such as with this <a href="https://stackoverflow.com/questions/9662346/python-code-to-remove-html-tags-from-a-string">approach</a>:
