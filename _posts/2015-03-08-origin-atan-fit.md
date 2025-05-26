---
layout: post
title: Origin atan Fit
date: 2015-03-08 00:41:17.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Origin
tags:
- data
- fitting
- graph
author:
  display_name: deparkes
permalink: "/2015/03/08/origin-atan-fit/"
---
One of the useful features of Origin is its ability to <strong>easily fit functions</strong> to data. Unfortunatly <strong>atan</strong> isn't one of the functions built in to origin.
In this guide show you how to make and fit your own <strong>Origin atan function</strong>.
<h1>Make and Fit Your Origin atan Function</h1>
This quick guide shows you how to make your own origin atan function.
<h2>Create a New Function</h2>
Select the data you wish to fit to and select <strong>Analysis</strong> -&gt; <strong>Non-linear Curve Fit</strong>. On the window that comes up, you'll need to click the "<strong>Create/Edit Fitting Function</strong>" button:

| ![create new origin atan function]({{site.baseurl}}/assets/2015/03/NewFunction-180x300.png) |
|:--:|
| *Create a new origin atan function* |

<h2>Input the atan Function Settings</h2>
In the "Fitting Function Organizer" click "New Function". Input the values as shown here:
One thing to be sure of is that you have <strong>set the initial values</strong> for your fitting parameters:

| ![Make origin atan function]({{site.baseurl}}/assets/2015/03/origin_atan-300x289.png) |
|:--:|
| *Make an origin atan function* |

```python
InitialValues = 1,1,1,1
```
With these you will have to manually set them each time you want to fit a function.
Save your function by hitting 'save'.
<h2>Check the Function By Simulating</h2>
To make sure that your function is behaving as you expect, you can simulate it by clicking 'simulate'.
Make sure that you have saved the function first, as changes are not always automatically incorporated into the simulation.
>Once you're happy that your function is correct, click 'ok' on the simulation window, and 'ok' on the simulation organizer. Save any changes.

| ![simulate origin atan function]({{site.baseurl}}/assets/2015/03/simulate_atan-300x209.png) |
|:--:|
| *Simulate origin atan function* |

<h2>Fit Your Origin atan Function</h2>
If you're happy with the function in the simulation, you can fit your function to your data:


| ![fit origin atan function]({{site.baseurl}}/assets/2015/03/Non-LinearFit-162x300.png) |
|:--:|
| *Fit origin atan function* |

<h2>View Your Fitted Data</h2>
Fit using your new origin atan function, and plot on the same axes as your data:

| ![Origin atan]({{site.baseurl}}/assets/2015/03/Graph1-300x210.png) |
|:--:|
| *Origin atan* |
