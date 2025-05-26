---
layout: post
title: Python Dashboard
date: 2021-01-09 01:17:47.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- dash
- dashboard
- datascience
- python
- visualisation
author:
  display_name: deparkes
permalink: "/2021/01/09/python-dashboard/"
---
This post shows you how to make a python <a href="https://www.betterevaluation.org/en/evaluation-options/data_dashboard">dashboard</a> using dash. Dash <a href="https://dash.plotly.com/introduction">combines</a> the <a href="https://plotly.com/">plotly</a> plotting library with the <a href="https://en.wikipedia.org/wiki/Flask_%28web_framework%29">flask server</a> to host the dashboard.
<h2>Python Dashboard with Dash</h2>
Dash is a powerful, flexible package and this short guide only scratches its surface. It will show how to make simple python dashboard consisting of three charts in a layout.
This guide builds on <a href="https://dash.plotly.com/dash-core-components/">the official dash documentation</a> and assumes you have already <a href="https://dash.plotly.com/installation">installed dash</a>.
<h3>A simple start</h3>
This is just a very minimal python dashboard implemented in dash. In this simple example we'll look at creating and adding charts to a grid layout dashboard. The general idea is to use python to build up <a href="https://dash.plotly.com/dash-html-components">html components</a> to represent your dashboard. It helps to have some rudimentary understanding of html layout, but it isn't essential.

The full code for this example is below, but I wanted to pick out some particular sections to explain in more detail.
<h3>Preparing Figures</h3>
Figures in dash are handled via the <a href="https://plotly.com/python/px-arguments/">plotly API</a>. You can read more in the documentation, but essentially you can select different plots such as bar, scatter or violin plots to represent your data.

```python
figure_1 = px.scatter(dataframe_1, x="x", y="y")
figure_2 = px.scatter(dataframe_2, x="x", y="y")
figure_3 = px.scatter(dataframe_3, x="x", y="y")
```

Plotly accepts pandas dataframes as inputs, which means you can easily load external data or prepare data in a different process for passing to your plotly dashboard. In the example below I have generated some random data for plotting, but you could equally load a csv file from disk or a remote location for example.

```python
dataframe_1 = pd.DataFrame({'x': np.random.rand(50), 'y': np.random.rand(50)})
dataframe_2 = pd.DataFrame({'x': np.random.rand(10), 'y': np.random.rand(10)})
dataframe_3 = pd.DataFrame({'x': np.random.rand(5), 'y': np.random.rand(5)})
```

<h3>Defining the Layout</h3>
The format and layout of the dashboard is set using the <a href="https://dash.plotly.com/dash-html-components">dash html components</a>. In the example below a mixture of '<a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div">divs</a>' and headings are used to create a simple layout.
In dash, elements can be passed into Divs as a list. For example:

```python
html.Div(['element1', 'element2', 'element3', 'element4'])
```

would result in:

```python
element1element2element3element4
```

Columns can be achieved with nested 'html.Div' statements. For example:

```python
html.Div([html.Div(['element1', 'element2']), html.Div([ 'element3', 'element4'])], style={'columnCount': 1})
```

yields:

```
element1element2
element3element4
```

<h2>The Full Code</h2>
The full code for this simple example is below and can be run with python app.py. The resulting dashboard will look like this:

| ![Python Dashboard]({{site.baseurl}}/assets/2021/01/plotly_dash.png) |
|:--:|
| *Python Dashboard* |

Try playing around with the code to change the dashboard layout.

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.express as px
import pandas as pd
import numpy as np
# Data is defined as pandas dataframes
# This could be from anywhere e.g. loaded from API, local csv file etc.
dataframe_1 = pd.DataFrame({'x': np.random.rand(50), 'y': np.random.rand(50)})
dataframe_2 = pd.DataFrame({'x': np.random.rand(10), 'y': np.random.rand(10)})
dataframe_3 = pd.DataFrame({'x': np.random.rand(5), 'y': np.random.rand(5)})
app = dash.Dash(__name__)
# figures are built up based on plotly API
# see https://plotly.com/python/px-arguments/ for more details
figure_1 = px.scatter(dataframe_1, x="x", y="y")
figure_2 = px.scatter(dataframe_2, x="x", y="y")
figure_3 = px.scatter(dataframe_3, x="x", y="y")
# Main dashboard layout is built up from html elements
app.layout = html.Div([
            html.H1('Example Dashboard Layout'),
            html.Div([
                    html.H2('Example Graph 1'),
                    dcc.Graph(
                            id='example-graph-1',
                            figure=figure_1
                            ),
                    ]),
                    html.Div([
                        html.Div([
                            html.H3('Example Graph 1'),
                            dcc.Graph(
                                    id='example-graph-2',
                                    figure=figure_2
                                    ),
                        ]),
                        html.Div([
                            html.H3('Example Graph 3'),
                            dcc.Graph(
                                    id='example-graph-3',
                                    figure=figure_3
                                    ),
                        ])
                    ], style={'columnCount': 2})
            ])
if __name__ == '__main__':
    app.run_server(debug=True)
```

