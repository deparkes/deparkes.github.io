---
layout: post
title: Python Simple Networkx Example
date: 2018-04-02 16:45:41.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- analytics
- datascience
- graph
- networkx
- python
author:
  display_name: deparkes
permalink: "/2018/04/02/python-simple-networkx-example/"
---
<a href="https://networkx.github.io/">Networkx</a> is a python package for creating, visualising and analysing <a href="https://en.wikipedia.org/wiki/Graph_theory">graph</a> networks. This post gives a simple networkx example to show how it works.
<h1>A simple Networkx Example</h1>
A graph network is built from nodes - the entities of interest, and edges - the relationships between those nodes. To create a graph we need to add nodes and the edges that connect them.
Networkx is <a href="https://en.wikipedia.org/wiki/NetworkX">capable</a> of operating on graphs with up to 10 million rows and around 100 million edges, but for now we will just create a small example graph.
If we try to create an edge with a node that does not yet exist, networkx will create that node. This means that we can make a simple networkx example with the following code.

```python
import networkx as nx
# Create a networkx graph object
my_graph = nx.Graph()
# Add edges to to the graph object
# Each tuple represents an edge between two nodes
my_graph.add_edges_from([
                        (1,2),
                        (1,3),
                        (3,4),
                        (1,5),
                        (3,5),
                        (4,2),
                        (2,3),
                        (3,0)])
# Draw the resulting graph
nx.draw(my_graph, with_labels=True, font_weight='bold')
```

This will produce this output

| ![Simple networkx example]({{site.baseurl}}/assets/2018/04/simple_graph.png) |
|:--:|
| *Simple networkx example* |

<h1>Taking Things Further</h1>
To take things further, there are some extensions and additions you could try, such as:
<ul>
<li>Add new edges between existing nodes</li>
<li>Add new edges between existing nodes and new nodes</li>
<li>Add <a href="https://networkx.github.io/documentation/stable/tutorial.html#nodes">new nodes</a> without edges</li>
</ul>
