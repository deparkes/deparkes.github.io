---
layout: post
title: How to create Origin Subplots
date: 2015-04-23 18:55:03.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Origin
tags:
- data
- plotting
author: deparkes
permalink: "/2015/04/23/how-to-create-origin-subplots/"
---
<h1>How to Create Subplots in Origin</h1>
Subplots can be  a useful way to display data clearly. In this post I show you how to use Origin to plot data as subplots.
This guide was made using Origin 8, but I imagine something similar should work with other origin versions.
<h2>Plot Your Multiple Data Sets</h2>
We begin by plotting our multiple data sets on a single axis. In this example I'm simply plotting the sine, cosine and tangent of an angle.

| ![origin subplots - same axis]({{site.baseurl}}/assets/2015/04/Graph1-1024x724.png) |
|:--:|
| *origin subplots - same axis* |

As you can see, it's a bit messy. Definitely a candidate for converting into subplots.
<h2>Extract to Layers</h2>
With your data displayed on the same plot, select this graph and find the "Extract to Layers" button on your toolbar:

| ![origin subplots - extract to layers]({{site.baseurl}}/assets/2015/04/extract_to_layers.png) |
|:--:|
| *origin subplots - extract to layers* |

this will bring up a dialogue asking you to select the number of rows and columns you would like to generate. For this example we will use 3 rows and 2 column.

| ![origin subplots - grid setup]({{site.baseurl}}/assets/2015/04/GridSetup.png) |
|:--:|
| *origin subplots - grid setup* |

Click 'OK' to bring up a further dialogue to set various margins and and spacings. For now we can just stick with the defaults.

| ![origin subplots - margins]({{site.baseurl}}/assets/2015/04/Margins.png) |
|:--:|
| *origin subplots - margins* |

Click 'OK' to generate  your three subplots:

| ![origin subplots - generate subplots]({{site.baseurl}}/assets/2015/04/subplot_output.png) |
|:--:|
| *origin subplots - generate subplots* |

If you like, you can leave things here: this is definitely much clearer than plotting all three curves on the same axes.
<h2>Tidy Up Your Subplots</h2>
The default subplot output doesn't look too bad, but I prefered to make some adjustments:

| ![origin subplots - final graph]({{site.baseurl}}/assets/2015/04/Graph2-1024x724.png) |
|:--:|
| *origin subplots - final graph* |

<h3><a href="{{site.baseurl}}/2015/04/23/origin-linked-axis/">Find out how to make a linked axis in origin</a></h3>
