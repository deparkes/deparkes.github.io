---
layout: post
title: Python Compare Wikipedia Pages
date: 2020-12-27 11:30:19.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- api
- data
- data science
- python
- rest api
- wikipedia
author: deparkes
permalink: "/2020/12/27/python-compare-wikipedia-pages/"
---
Wikimedia has an API which lets you compare Wikipedia pages, and in some cases modify pages and information within the Wikimedia group. The main page for all Wikimedia API information is <a href="https://www.mediawiki.org/wiki/API:Main_page">here</a>.

In this post I am most interested in the Wikipedia compare API, to show how you use it to see differences between versions of a Wikipedia page. The documentation for this part of the Wikipedia API is <a href="https://www.mediawiki.org/wiki/API:Compare">here</a>:
<h2>Compare Wikipedia Pages</h2>
Using the example on the Wikipedia page it is fairly easy to use the API to return the diff for two different pages. In this case for <a href="https://en.wikipedia.org/wiki/Gold">gold</a> and <a href="https://en.wikipedia.org/wiki/Silver">silver</a>.

```python
import requests
session = requests.Session()
api_url = "https://en.wikipedia.org/w/api.php"
PARAMS = {
    'action': "compare",
    'format': "json",
    'fromtitle': 'Gold',
    'totitle': 'Silver'
}
response = session.get(url=api_url, params=PARAMS)
response_json = response.json()
for key, value in response_json['compare'].items():
    print(key, ' : ', value)
```

This code will capture and print the whole of the API response json. The diff of the pages is stored in the '*' key of the 'compare' dictionary.
<h2>Comparing Page Versions</h2>
The API also makes it possible to compare between different revisions of the same (or different) pages. The use of the API is similar to comparing separate Wikipedia pages, only we specify individual revisions (which are unique ids across different pages) rather than page names.
An example of the comparison viewed via the webpage is <a href="https://en.wikipedia.org/w/index.php?title=Gold&amp;type=revision&amp;diff=989941568&amp;oldid=989715533">here.</a>

```python
import requests
session = requests.Session()
api_url = "https://en.wikipedia.org/w/api.php"
PARAMS = {
    'action': "compare",
    'format': "json",
    'fromrev': 989715533,
    'torev': 989941568
}
response = session.get(url=api_url, params=PARAMS)
response_json = response.json()
for key, value in response_json['compare'].items():
    print(key, ' : ', value)
```

