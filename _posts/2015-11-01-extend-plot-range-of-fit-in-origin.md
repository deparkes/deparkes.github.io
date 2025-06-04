---
layout: post
title: Extend Plot Range Of Fit In Origin
date: 2015-11-01 14:45:52.000000000 +00:00
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
- extend
- fitting
- originlab
- plotting
author: deparkes
permalink: "/2015/11/01/extend-plot-range-of-fit-in-origin/"
---
In this post I show you how to extend the plot range of the fitted function in <a href="https://www.originlab.com/">Origin</a>, beyond that of your initial data.
Origin makes it easy to fit to your data, but how to extend the fit beyond the range of the original data isn't obvious.
Follow the steps below to find out how.
<h1>1. Select Your Fit Function</h1>
The first stage is to select your fit function as you would do normally.
In my case I have some data showing cooling over time, which I'll fit with a simple falling exponential, via the non-linear curve fitting tool.


| ![non-linear curve fit 2]({{site.baseurl}}/assets/2015/11/non-linear-curve-fit-2-1024x506.png) |
|:--:|
| *non-linear curve fit 2* |

<h1>2. Extend Plot Range</h1>

To extend the plot range of the fitted function, you need to select the '<strong>Fitted Curves</strong>' options on the '<strong>Settings</strong>' tab.

| ![FittedCurves]({{site.baseurl}}/assets/2015/11/FittedCurves.png) |
|:--:|
| *FittedCurves* |

Under the x-data type you can change the '<strong>Range</strong>'  from '<strong>Use Input Range</strong>' to '<strong>Custom</strong>', which allows you to set the <strong>Max</strong> and <strong>Min</strong> range for the fit.

| ![FittedCurves - Custom Range]({{site.baseurl}}/assets/2015/11/FittedCurves-CustomRange.png) |
|:--:|
| *FittedCurves - Custom Range* |

Hit '<strong>Fit Till Converged</strong>' and you'll see that the fit now extends beyond the original data range.
(I found that I sometimes had to click on some of the grey background of the settings window, near to the Min/Max numbers for them to be 'set'.)
If you don't have a definite range you need to show, you might need to play around with the maximum and  minimum values until you have a range you are happy with (make sure you hit 'Fit Till Converged' each time).
<h1>3. Output Plot</h1>
The fit function now extends beyond the original data, so you can predict behaviour higher and lower than your initial values.

| ![FittedCurves - Output plot]({{site.baseurl}}/assets/2015/11/Graph2-1024x719.png) |
|:--:|
| *FittedCurves - Output plot* |
