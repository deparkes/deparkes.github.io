---
layout: post
title: Origin Linked Axis
date: 2015-04-23 19:26:35.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- Origin
tags:
- data
- origin
- plotting
author: deparkes
permalink: "/2015/04/23/origin-linked-axis/"
---
<h1>How to Create a Linked Axis in Origin</h1>
Right click on your graph to bring up the 'layer management' dialogue.

| ![origin linked axis - layer management]({{site.baseurl}}/assets/2015/04/layer_properties.png) |
|:--:|
| *origin linked axis - layer managements* |

<h2>Add layers if Needed</h2>
I'm going to be using the layers generated when I <a href="{{site.baseurl}}/2015/04/23/how-to-create-origin-subplots/">created subplots</a>, but you might need to add an extra layer to hold your new axes. You can set up your axes and new layers here.

| ![origin linked axes - add layers]({{site.baseurl}}/assets/2015/04/add_layers_if_needed.png) |
|:--:|
| *origin linked axes - add layers* |

<h2>Link Axes</h2>
With your new layers added as necessary, go to the 'Link' tab. Here you need to select which layer you would like to link the selected layer to.
In most cases you will probably need the 'Straight'(1 to 1)', as selected here.
<h3><a href="{{site.baseurl}}/2015/02/19/add-a-second-axis-in-origin/">Find out how to make more advanced additional axes</a></h3>
Click 'Link' for each of the layers you want to link from, so that the 'Link to' column is filled for them.
You do not need to change anything for the Layer you are linking to.

| ![origin linked axis - link]({{site.baseurl}}/assets/2015/04/Link_to_column_filled.png) |
|:--:|
| *origin linked axis - link* |

<h2>Make Adjustments to Your 'Linked-to' Layer</h2>
Now when you make changes to the layer you linked to, these changes should also be present in the layers you were linking from.
Here's an example of linked axes when <a href="{{site.baseurl}}/2015/04/23/how-to-create-origin-subplots/">making a subplot</a>. Notice the tick marks and scales are all identical.

| ![origin linked axis - adjust layer]({{site.baseurl}}/assets/2015/04/Adjust_layer1.png) |
|:--:|
| *origin linked axis - adjust layer* |
