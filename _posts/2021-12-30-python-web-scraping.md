---
layout: post
title: Python Web Scraping
date: 2021-12-30 15:43:16.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- data
- data science
- pandas
- python
- requests
- webscraping
author:
  display_name: deparkes
permalink: "/2021/12/30/python-web-scraping/"
---
<a href="https://en.wikipedia.org/wiki/Web_scraping">Web scraping</a> is the process of automatically identifying and downloading data from a webpage. This blog post looks a a few python web scraping options.
Alternatives to web scraping include:
- <strong>Using an API</strong>. Usually a better option than web scraping if an API is available. <em>See also</em> <a href="https://deparkes.co.uk/2018/08/11/flask-restful-api-json/">Creating an API with flask</a>. <a href="https://deparkes.co.uk/2016/10/07/some-cool-open-data-api/">Open data APIs</a>.
- <strong>Manually copying data</strong> from a website. Can be a better option if there is a small number of target pages or if there is a lot of variation in website data. <em>See also</em> an <a href="https://deparkes.co.uk/2021/04/16/time-team-map-of-episodes/">example of manual copying used to 'scrape' Wikipedia data</a>.
<h2>Python Web Scraping Options</h2>
I've picked out a few different python web scraping options. There is some overlap in terms of concepts and packages used as the essential idea is the same: programmatically grab data from a webpage and then look for certain aspects within it.
Common python web scraping packages include <a href="https://realpython.com/python-requests/">requests</a>, <a href="https://realpython.com/beautiful-soup-web-scraper-python/">beautiful soup</a>, <a href="https://realpython.com/regex-python/">regex</a>.
<h3>Requests</h3>
Probably the core of modern python web scraping is the <a href="https://docs.python-requests.org/en/latest/">requests</a> library, which allows you to easily capture webpage data in a python script. Note that earlier approaches to python web scraping may have used the urllib library - <a href="https://stackoverflow.com/questions/2018026/what-are-the-differences-between-the-urllib-urllib2-urllib3-and-requests-modul">read about the differences between requests and urllib</a>.
The data from requests comes back 'raw', and is likely to contain lots of HTML tags around the actual information you are interested in.
In very simple cases, such as looking for occurrences of a particular name or phrase you could use standard python string functions. Here is an example

```python
import requests
url = "https://en.wikipedia.org/wiki/North_Atlantic_air_ferry_route_in_World_War_II"
data = requests.get(url).text
print("Nova Scotia" in data)
```

So the text back from requests can be used just like any other string.
<h3>Simple Regex</h3>
Introducing <a href="https://realpython.com/regex-python/">regex</a> is a good next step once beyond simply downloading the data with requests. Using an <a href="https://regex101.com/">online regex tool</a> can be helpful when writing regex.
Regex is powerful, but <a href="https://stackoverflow.com/questions/590747/using-regular-expressions-to-parse-html-why-not">it is not possible to fully parse HTML using regex</a>. For this reason regex is generally suited to simpler tasks such as picking out IP addresses, postcodes etc. from a webpage.
The following example uses regex to find latitude and longitude coordinates in the webpage.

```python
import requests
import re
url = "https://en.wikipedia.org/wiki/North_Atlantic_air_ferry_route_in_World_War_II"
data = requests.get(url).text
# Find find pairs of coordinates
pattern = re.compile( r"(\d{1,3}°{1}\d{1,3}′{1}\d{1,3}″{1}[N]).*(\d{1,3}°{1}\d{1,3}′{1}\d{1,3}″{1}[W])")
re.search(pattern, data).groups()
for match in pattern.finditer(data):
    print(match.groups())
```

<a href="https://pynative.com/python-regex-capturing-groups/">Read more about capturing multiple groups using finditer</a>.
<h3>Beautiful Soup</h3>
Beautiful Soup is probably the most popular python web scraping tool. It is powerful and flexible and I won't be able to cover it all here, but the examples below hopefully give a flavour of how it can be used.
The basic Beautiful Soup usage is as follows:

```python
from bs4 import BeautifulSoup
url = "https://en.wikipedia.org/wiki/North_Atlantic_air_ferry_route_in_World_War_II"
data = requests.get(url).text
soup = BeautifulSoup(data, 'html.parser')
```

<h4>Finding All Links</h4>
Because Beautiful Soup incorporates an <a href="https://stackabuse.com/guide-to-parsing-html-with-beautifulsoup-in-python/">HTML parser</a>, it can be used to extract information from particular <a href="https://en.wikipedia.org/wiki/HTML_element"> HTML elements</a>.
In this simple example we use Beautiful Soup to list the href of all links (which use the 'a' tag).

```python
for table in soup.find_all('a'):
    print(table.get('href'))
```

We can combine finding links with regex or simple string functions to find particular links.

```python
for link in soup.find_all('a'):
    if 'wikimedia' in link.get('href', 'default_value') :
        print(link)
```

<h4>Finding all body text</h4>
Next, an example of getting all of the text found in the HTML 'body'.
could technically do<code>body = soup.find_all('body')[0]</code>, but typically there would only by one <code>body</code>.

```python
body = soup.body
for string in body.strings:
    print(string)
```

To be more focused in which text to capture we can also look for paragraphs (see next section). Note that here <a href="https://stackoverflow.com/questions/25327693/difference-between-string-and-text-beautifulsoup">we use 'string' rather than 'text'</a>.
<h4>Finding all Paragraphs</h4>
In a similar fashion we can find all text in a paragraph block.

```python
paras = soup.find_all('p')
    for para in paras:
        print(para.text)
```

<h4>Finding tables</h4>
This final example is more complex and shows how Beautiful Soup can be used to extract table data from a webpage.
Firstly we can find all the 'table' element in the target page.

```python
tables = soup.find_all('table')
```

To select particular types of table, it can be useful to list the class of all tables

```python
for table in soup.find_all('table'):
    print(table.get('class'))
```

Note that <a href="https://stackoverflow.com/questions/11041405/why-dict-getkey-instead-of-dictkey">here we use <code>get</code> rather than '<code>[]</code>' can be useful so we can provide a default if needed</a>.
The output of that gives some indication that the class of interest is 'wikitable'

```python
for table in soup.find_all('table', class_='wikitable'):
    print(table.text)
```

Once we have identified the tables we need to work through individual rows and columns.
It's not always obvious how to handle the data coming back from the webpage, so building up an understanding can help. In this case we can use a simple loop to print out what belongs in each row and column, and match it to the corresponding rows and columns on the target webpage.

```python
n = 1
for row in tables[1].find_all('tr'):
    print('Row: ', n)
    m = 1
    for column in row.find_all('td'):
        print('Column: ', m)
        print(column.text)
        m+=1
    n+=1
```

Once we have a better understanding of how the table is laid out in HTML we can transform it into a pandas dataframe. In this case we j

```python
names = []
locations = []
coordinates = []
notes = []
for row in tables[1].find_all('tr'):
    col_num = 1
    for column in row.find_all('td'):
        if col_num == 1:
            names.append(column.text.strip())
        if col_num == 2:
            locations.append(column.text.strip())
        if col_num == 3:
            coordinates.append(column.text.strip())
        if col_num == 4:
            notes.append(column.text.strip())
        col_num+=1
    n+=1
df = pd.DataFrame({'Name': names,
                   'Location': locations,
                   'Coordinates': coordinates,
                   'Notes': notes
                  })
```

One problem you may encounter is nested tables, i.e. tables within tables. One way to approach this challenge is to use <code>recursive=False</code> as an extra parameter to find_all().
<h3>pandas read_html</h3>
Finally I wanted to show how pandas has a function '<a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_html.html">read_html</a>', which can be used to parse html table data without directly working with Beautiful Soup. read_html is particularly suited for simpler pages with well-defined tables. You may find it doesn't have the flexibility to deal with with more challenging pages.

```python
import pandas as pd
import requests
url = 'https://en.wikipedia.org/wiki/North_Atlantic_air_ferry_route_in_World_War_II'
html = requests.get(url).content
df_list = pd.read_html(html)
```

In this case it works really well, apart from the first table it finds just being irrelevant.
<h2>A word on robots.txt</h2>
<a href="https://www.robotstxt.org/">Robots.txt</a> is a file that gives website owners the opportunity to specify what automated tools can access via their website. Wikipedia has a <a href="https://en.wikipedia.org/robots.txt">good example of a detailed robots.txt</a> which reveals that a big issue for wikipedia is requests coming in at too fast a rate
It is possible to ignore robots.txt, but generally speaking you should respect it.
