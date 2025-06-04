---
layout: post
title: Python Networkx Load Graphs From File
date: 2018-04-09 16:00:34.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- graph analytics
- graphs
- network analytics
- networkx
- python
author: deparkes
permalink: "/2018/04/09/python-networkx-load-graphs-from-file/"
---
<a href="https://networkx.github.io/documentation/latest/tutorial.html">Networkx</a> is a python package for working with graphs and networks. Networkx is capable of <a href="https://wp.me/p4DE9r-13s">creating a graph from within a python script</a>, but you may also want to load a graphs from file. This post looks at some of the ways networkx allows you to load graphs from file, and gives some simple examples to help you get started.

If you have automatically produced a graph, such as from analysis of social media, then you may have a graph file format in mind. If you are making a graph from scratch you may prefer to write it into a separate file rather than having it saved along side your networkx python code.
<h1>Simple Load Graphs From File</h1>
Networkx node lists are just lists of python objects. Edge lists are lists of <a href="https://www.tutorialspoint.com/python/python_tuples.htm">tuples</a> representing the connections between nodes. If your graph nodes are just names then you can use simple methods to read them from a file.
First let's create a node file which we will think of as a list of node labels (I called it 'nodes.txt').

```
node_1
node_2
node_3
node_x
```

I am including an extra node in here that does not feature in the file containing edges. This is to show how you can include unconnected nodes. If all of your nodes are connected, you can actually just use a list of edges as networkx will add all the nodes it needs.
Since networkx will create any nodes in the edges file, you can use the node list to only include isolated nodes, like this:

```
node_x
```

And here's the corresponding edge file - 'edges.txt'. Notice how 'node_x' does not feature in this list.

```
node_1 node_2
node_2 node_3
node_3 node_1
```

We can now load these two files into network x:

```python
import networkx as nx
my_graph = nx.Graph()
edges = nx.read_edgelist('edges.txt')
nodes = nx.read_adjlist("nodes.txt")
my_graph.add_edges_from(edges.edges())
my_graph.add_nodes_from(nodes)
nx.draw(my_graph, with_labels=True, font_weight='bold')
```

This should draw a graph similar to this:

| ![Load Graphs From File - list and tuple]({{site.baseurl}}/assets/2018/04/simple_graph_list_and_tuple.png) |
|:--:|
| *Load Graphs From File - list and tuple* |

<h1>Use Graph Modelling Language</h1>
You may also want to load your graph saved in <a href="https://en.wikipedia.org/wiki/Graph_Modelling_Language">GML</a> format - a way of representing a graph in a plain text file. Networkx can <a href="https://networkx.github.io/documentation/stable/reference/readwrite/gml.html">read and write gml files</a> which contain both node and edge information. This might be a more attractive option if you also want to record additional attributes about the nodes and edges.
Here is a simple example gml file which I have saved as 'gml_graph.gml' (slightly modified from <a href="https://en.wikipedia.org/wiki/Graph_Modelling_Language">here</a>):

```
graph
[
 comment "This is a sample graph"
 directed 0
 label "Hello, I am a graph"
 node
 [
 id 1
 label "node 1"
  ]
 node
 [
 id 2
 label "node 2"
 ]
 node
 [
 id 3
 label "node 3"
 ]
 node
 [
 id 4
 label "node x"
 ]
 edge
 [
 source 1
 target 2
 label "Edge from node 1 to node 2"
 ]
 edge
 [
 source 2
 target 3
 label "Edge from node 2 to node 3"
 ]
 edge
 [
 source 3
 target 1
 label "Edge from node 3 to node 1"
 ]
]
```

We can easily load this into networkx with

```python
import networkx as nx
my_graph = nx.Graph()
gml_graph = nx.read_gml('./gml_graph.gml')
nx.draw(gml_graph, with_labels=True, font_weight='bold')
```

Which should draw a graph like the one below. This is essentially the same as the graph in the previous example: nodes 1, 2 and 3 are connected together, while node x is on its own.
<img class="aligncenter wp-image-4073 size-full" src="{{site.baseurl}}/assets/2018/04/simple_graph_gml.png" alt="Load Graphs From File - gml" width="481" height="322">
<h1>Other Methods</h1>
Networkx has a range of other <a href="https://networkx.github.io/documentation/stable/tutorial.html">methods to load graphs</a> from file which you may want to consider. Networkx is also <a href="https://networkx.github.io/documentation/stable/tutorial.html#creating-a-graph">quite flexible</a> in which python object types can be used as nodes, so you may be able to work beyond the methods included with the package, such as with <a href="https://stackoverflow.com/questions/26665799/networkx-adding-edges-to-a-graph-from-a-dictionary-with-lists-as-values">dictionaries</a>.
