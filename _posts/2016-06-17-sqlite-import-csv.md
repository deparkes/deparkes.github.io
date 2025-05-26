---
layout: post
title: SQLite Import csv
date: 2016-06-17 15:00:30.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- software
tags:
- csv
- data
- data science
- import
- sql
- sqlite
- sqlitestudio
author:
  display_name: deparkes
permalink: "/2016/06/17/sqlite-import-csv/"
---
<a href="https://www.google.co.uk/url?sa=t&amp;rct=j&amp;q=&amp;esrc=s&amp;source=web&amp;cd=1&amp;cad=rja&amp;uact=8&amp;ved=0ahUKEwinvrvYvNLMAhWIExoKHUi1DZ4QFggdMAA&amp;url=http%3A%2F%2Fsqlitestudio.pl%2F&amp;usg=AFQjCNGXtzg1D_-yLsc0-Grag_DKOaSV1A&amp;sig2=7AfG0vFS-35Sb1pvUZMtIA">SQLiteStudio </a>is a free SQLite database manager. In this post I show you the SQLite import csv steps for SQLiteStudio.
<h1>1. Open or Create Your SQLite Database</h1>
In this case I had an existing, empty database called "postcodes"

| ![SQLite Import csv - SQLite Import csv - sqlitestudio]({{site.baseurl}}/assets/2016/06/sqlitestudio.png) |
|:--:|
| *SQLite Import csv - SQLite Import csv - sqlitestudio* |

<h1>2. Open "Import" Window</h1>
Bring up the "Import" dialogue window by going to Tools -&gt; Import.

| ![SQLite Import csv - tools_import]({{site.baseurl}}/assets/2016/06/tools_import.png) |
|:--:|
| *SQLite Import csv - tools_import* |

<h1>3. Select an existing table, or type the name of your new table</h1>
In this case I am going to create a new table called "new_table" to import csv data into.

| ![SQLite Import csv - new_table]({{site.baseurl}}/assets/2016/06/new_table.png) |
|:--:|
| *SQLite Import csv - new_table* |

<h1>4. Select Your Input CSV File</h1>
Once you've selected your destination table, click next, and you'll be taken to a dialogue to select your csv file to import. Select CSV as the data source type, and browse to your data file.
Depending on your data you may wish to tick the box "First line represents CSV column names" if your first row contains header information.

| ![SQLite Import csv - import_loading_screen]({{site.baseurl}}/assets/2016/06/select_input_file.png) |
|:--:|
| *SQLite Import csv - import_loading_screen* |

<h1>5. Import your data</h1>
Depending on the size of your csv file you may be shown a loading screen similar to this one. In my case I had a ~500MB csv to import which took around 5-10 minutes to import.

| ![SQLite Import csv - import_loading_screen]({{site.baseurl}}/assets/2016/06/import_loading_screen.png) |
|:--:|
| *SQLite Import csv - import_loading_screen* |

<h1>6. View Your Imported Data</h1>
If everything has gone to plan you should now be able to navigate to your table and explore your data.

| ![SQLite Import csv - data]({{site.baseurl}}/assets/2016/06/data.png) |
|:--:|
| *SQLite Import csv - data* |
