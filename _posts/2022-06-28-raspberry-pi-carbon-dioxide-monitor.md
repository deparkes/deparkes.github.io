---
layout: post
title: Raspberry Pi Carbon Dioxide Monitor
date: 2022-06-28 20:16:41.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- api
- dashboard
- environment
- flask
- home server
- plotly
- python
- raspberry pi
- sensor
- sql
- visualisation
author: deparkes
permalink: "/2022/06/28/raspberry-pi-carbon-dioxide-monitor/"
---
This post shows how to make a Raspberry Pi Carbon Dioxide Monitor using a raspberry pi connected to a USB carbon dioxide monitor. The project is deliberately bare bones and leaves several opportunities for refinement, improvement and general tinkering.
<h2>What we are aiming to make</h2>
The following schematic shows what we will be building up to:
<ul>
<li>The actual CO2 monitor hardware, which is just a commercial carbon dioxide monitor with USB interface.</li>
<li>Python script to <strong>query the monitor hardware</strong> and store results in a <strong>SQLite database</strong>
</li>
<li>A <strong>bash script</strong> to regularly run the hardware-querying python script</li>
<li>An <strong>API</strong> for the sqlite database using</li>
<li>A <strong>dashboard</strong> for the carbon dioxide monitor using flask and plotly</li>
</ul>

| ![Carbon Dioxide Monitor Schematic]({{site.url}}/assets/2022/06/Schematic_v3_small.png) |
|:--:|
| *Carbon Dioxide Monitor Schematic* |

The resulting dashboard looks like this:

| ![raspberry pi carbon dioxide monitor - dashboard]({{site.url}}/assets/2022/06/Screenshot-2022-06-28-at-20-21-03-Screenshot.png) |
|:--:|
| *raspberry pi carbon dioxide monitor - dashboard* |

<h2>Prerequisites</h2>
Before getting going with this project there are a few prerequisites you should check you have first:
<ul>
<li>Raspberry Pi</li>
<li>CO2 Meter device like <a href="https://www.co2meter.com/products/co2mini-co2-indoor-air-quality-monitor">this</a>
</li>
<li>Copy of <a href="https://github.com/heinemml/CO2Meter/blob/master/CO2Meter.py">this code</a>
</li>
<li>running on Linux - probably need sudo access</li>
<li>Python packages
<ul>
<li>flask</li>
<li>plotly</li>
<li>requests</li>
</ul>
</li>
</ul>
<h2>Quick Start</h2>
Follow these steps if you just want to try out the code without looking at it in detail.
Get the code from <a href="https://github.com/deparkes/carbon-dioxide-monitor/releases/tag/original_blog_post">GitHub</a>.


```bash
source venv/bin/activate
```

It's probably easier to run each of the following commands in a separate terminal window.
<h3>Setting up a SQLite Database</h3>
We configure a SQLite database so we can store data from the carbon dioxide meter.
The SQLite database is stored in a file 'co2meter.db'. <a href="https://database.guide/create-a-database-in-sqlite/">Read about how to create a sqlite database</a>.
And then we create a single table in that database called 'data'. <a href="https://database.guide/create-table-sqlite/">Read more about creating a table</a>.

```sql
CREATE TABLE data
( timestamp DATETIME,
co2 DOUBLE,
temperature DOUBLE);
```

We will write it to a sqlite database so we can easily query it later for what we have in mind.
<h3>Start collecting Data</h3>

```bash
bash runapp.sh
```

This assumes you have configured your user to have hidraw access as per the CO2Meter readme. If you have followed the instructions and it still isn't working, you may need to restart your machine/raspberry pi.

<h3>Start sharing data</h3>
Run

```bash
python3 api.py
```

<h3>Start visualising data</h3>

Run

```bash
python3 dashboard.py
```

<h3>Basic interaction with the co2 meter</h3>
The <a href="https://github.com/heinemml/CO2Meter">co2meter.py</a> code conceals quite a bit of complexity, and the only commands you really need to worry about are
<ul>
<li>get_data</li>
<li>get_co2</li>
<li>get_temperature</li>
</ul>
I found that this code worked best for me if I ran the commands in 'sudo' mode, although you may find success if you follow the <a href="https://github.com/heinemml/CO2Meter">hidraw access instructions</a> and reset your raspberry pi before continuing.
<h4>Code overview</h4>
The following code creates a connection to the hardware carbon dioxide meter as well as the SQLite database we created.
A 'while' loop keeps trying to poll the carbon dioxide meter until a complete response is returned. Without this, it is possible for queries to the meter to return empty.
The code also prints out the same data so it could, in theory, be more easily captured directly within Linux.
Once a full, correct response from the carbon dioxide meter has been received, the code finishes.

```python
#!/bin/env python
import time
import sqlite3
from datetime import datetime
from CO2Meter import *
Meter = CO2Meter("/dev/hidraw0")
conn = sqlite3.connect("co2meter.db")
cursor = conn.cursor()
no_measurement = True
while no_measurement:
    measurement = Meter.get_data()
    measurement.update({'timestamp': datetime.now()})
    try:
        print(measurement['timestamp'].strftime("%Y-%m-%d %H:%M:%S"),
        measurement['co2'],
        measurement['temperature'],
        sep=","
        )
        cursor.executemany("INSERT INTO data VALUES (?,?,?)",
                [(measurement['timestamp'].strftime("%Y-%m-%d %H:%M:%S"),
                    measurement['co2'],
                    measurement['temperature'])]
                    )
        conn.commit()
        no_measurement = False
    except Exception as e:
        pass # not all calls result in data to display
```

<h3>Getting Regular Updates</h3>
I wanted to keep different elements of the project well separated so that, in theory at least, I could tweak and improve each one separately. Using a separate bash script to regularly run a python script is an example of this.
One of the decisions to make at the data collection stage is how frequently to collect it. I went for 5 minutes (300 seconds) as it seemed to capture variation in the data without massively oversampling.
<h4>Example Output</h4>

| ![Regular Updates]({{site.url}}/assets/2022/06/RegularUpdates.png) |
|:--:|
| *Regular Updates* |

<h4>Code Overview</h4>
This simple bash script runs until it is cancelled. Every 5 minutes (300 seconds) the script runs the main meter.py script.
As shown in an earlier section, the meter.py script itself handles writing the data to a sqlite database.
Alternatively, this bash script picks up the 'print' outputs from the python script and writes them to a separate 'data.dat' file.
Note the use of 'sudo' to get around issues with access to hidraw.

```bash
while true;
do
	sudo python3 meter.py
       	sleep 300;
done
```


<h3>Exposing the data with a Flask API</h3>
At this stage we have a python script which writes data to a sqlite database. To expose this data to other services or devices on a local network we will use a flask app to create an API.
We can use flask to make a <a href="{{site.url}}/2018/08/11/flask-restful-api-json/">simple rest api</a> for the data. More complexity would be possible, but for now we'll just keep it simple.
<h4>Example Output</h4>

| ![API raw data example]({{site.url}}/assets/2022/06/Screenshot-2022-06-28-at-20-43-32-Screenshot.png) |
|:--:|
| *API raw data example* |

<h4>Code Overview</h4>
Creates a single 'monitor' endpoint which will return the contents of the co2meter.db database in json format

```python
import sqlite3
from flask import Flask, request, make_response, jsonify
import io
import os
import csv
app = Flask(__name__)
database_name = 'co2meter.db'
def get_db():
    conn = sqlite3.connect(database_name)
    return conn
def get_data():
    db = get_db()
    cursor = db.cursor()
    statement = "SELECT * FROM data"
    cursor.execute(statement)
    return cursor.fetchall()
@app.route('/api')
def api():
    data = get_data()
    columns = ['timestamp', 'co2', 'temperature']
    result =  [{'timestamp': row[0], 'co2': row[1], 'temperature': row[2]}for row in data]
    return jsonify(result)
@app.route('/')
def myapp():
    message = "To use this app: %sapi" % request.base_url
    return message
if __name__ == '__main__':
    app.run(debug=True, port=5000, host='0.0.0.0')
```

<h3>Viewing the Data with Flask and Plotly</h3>
The final step is to actually make the data available for a user to easily view and interpret. The Flask API serving JSON data provides quite a bit of flexibility for how to do that.
I opted to make a dashboard using a plotly along with a separate flask app. Plotly can play nicely with pandas dataframes, but since I wanted to keep the dependencies for this project relatively light, I implemented the plotly chart without pandas.
This section borrows from this blog post which shows how you can <a href="https://towardsdatascience.com/web-visualization-with-plotly-and-flask-3660abf9c946">create a dashboard using plotly without dash</a>. I found that dash could not install onto my raspberry pi.
<h4>Example Output</h4>
| ![raspberry pi carbon dioxide monitor - dashboard]({{site.url}}/assets/2022/06/Screenshot-2022-06-28-at-20-21-03-Screenshot.png) |
|:--:|
| *raspberry pi carbon dioxide monitor - dashboard* |

<h4>Code Overview</h4>
Does a get request from the api created earlier
Uses plotly to create a simple dashboard (without using '<a href="{{site.url}}/2021/01/09/python-dashboard/">dash</a>')
Makes the dashboard available on port 3000

```python
from flask import Flask, render_template
import json
import requests
import plotly
import plotly.graph_objects as go
from plotly.subplots import make_subplots
app = Flask(__name__)
@app.route('/')
def notdash():
    r = requests.get('localhost:5000/api')
    data = r.json()
    co2 = [x['co2'] for x in data]
    temperature = [x['temperature'] for x in data]
    timestamp = [x['timestamp'] for x in data]
    fig = make_subplots(specs=[[{'secondary_y': True}]])
    fig.add_trace(go.Scatter(x=timestamp,
                             y=co2,
                             name="CO2 (ppm)"),
                             secondary_y=False
                )
    fig.add_trace(go.Scatter(x=timestamp,
                             y=temperature,
                             name="Temperature (deg. C)"),
                             secondary_y=True)
    graphJSON = json.dumps(fig, cls=plotly.utils.PlotlyJSONEncoder)
    return render_template('dashboard.html', graphJSON=graphJSON)
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=3000, debug=True)
```

This flask app for the dashboard also needs a file 'dashboard.html' in a 'templates' directory. This html file is a template into which a 'graphJSON' object can be passed.

```html
&lt;html&gt;
	&lt;body&gt;
		&lt;h1&gt;Carbon Dioxide Monitor&lt;/h1&gt;
		&lt;div id='chart' class='chart'&gt;&lt;/div&gt;
	&lt;/body&gt;&lt;script src='https://cdn.plot.ly/plotly-latest.min.js'&gt;&lt;/script&gt;
	&lt;script type='text/javascript'&gt;
		var graphs = {{graphJSON | safe}};
		Plotly.plot('chart', graphs, {});
	&lt;/script&gt;
&lt;/html&gt;
```


<h2>Possible refinements</h2>
This example raspberry pi carbon dioxide monitor is deliberately rough and leaves lots of areas for development or refinement, such as:
<ul>
<li>Use cron rather than bash script with timer -&gt; blog post on cron vs regular bash script</li>
<li>Host a dashboard to view and explore data rather than just an api to pick up with Excel -&gt; blog post on flask data dashboard / plotting</li>
<li>Make a virtualenv - quick post on creating a virtualenv (and alternatives?). Maybe reference conda?</li>
<li>Use pyusb rather than hidraw? I think this would require some rework of the co2meter.py code</li>
<li>Implementing using a different pattern other than database + api e.g. pub/sub</li>
<li>Query by date range - min and max, need update the api</li>
<li>Higher frequency polling of co2 meter, then just sampling from the stream</li>
</ul>
There are many options for what to do with the data once captured e.g.
<ul>
<li>csv</li>
<li>json</li>
<li>database</li>
<li>queue?</li>
<li>pub/sub?</li>
</ul>
Again, there are multiple options for how to view the data, such as:
<ul>
<li>Load and process the data with python</li>
<li>Point Excel at the api</li>
<li>Use a tool such as power bi</li>
<li>Plot the data in a browser with javascript</li>
</ul>
<h2>Related Projects and Posts</h2>
A <a href="https://github.com/vfilimonov/co2meter">more comprehensive co2meter approach</a>
Background on <a href="https://hackaday.io/project/5301-reverse-engineering-a-low-cost-usb-co-monitor">reverse engineering the co2 meter </a>
