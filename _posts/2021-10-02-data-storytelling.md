---
layout: post
title: Data Storytelling
date: 2021-10-02 10:18:20.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- Design
tags:
- data
- design
- graphics
- graphs
- plotting
- story telling
author:
  display_name: deparkes
permalink: "/2021/10/02/data-storytelling/"
---
Inspired by the <a href="https://www.storytellingwithdata.com/books">Storytelling With Data book</a> I wanted to try applying some of the techniques to some existing charts and graphs. In all the examples I have been limited in not having access to the original data, so re-plotting hasn’t really been possible. Instead, I have redrawn using <a href="https://inkscape.org/">Inkscape</a> or Excel and then focused on labels, <a href="https://daydreamingnumbers.com/blog/preattentive-attributes-example/">pre-attentive attributes</a> etc.
<h2>Data Storytelling Method</h2>
<strong>The method</strong>
Broadly speaking, the data storytelling method from the book is as follows:
<ol>
<li>Context – what is the ‘Big Idea’ you are trying to communicate?</li>
<li>Choose an appropriate display – think about the data and the message</li>
<li>Eliminate clutter – think about <a href="https://daydreamingnumbers.com/blog/preattentive-attributes-example/">pre-attentive attributes</a>
</li>
<li>Think like a designer – aesthetics and accessibility</li>
<li>Tell a story – How can you take the audience on a journey</li>
</ol>
I also considered a few up-front questions to consider when looking at the initial 'before' charts:
<ul>
<li>Where was my eye drawn?</li>
<li>Is there any misalignment?</li>
<li>Are any <a href="https://www.interaction-design.org/literature/topics/gestalt-principles">Gestalt principles</a> jumping out? Proximity, similarity, enclosure, closure, continuity</li>
<li>Visual order: alignment, use of diagonals, white space, use of colour</li>
<li>Where are the pre-attentive attributes: Shape, line length/width, size, curvature, added marks, enclosure, hue, intensity, spatial position</li>
</ul>
<h2>Data Storytelling Examples</h2>
For each of these examples I try to follow the general 'Data Storytelling' approach. Obviously this is somewhat contrived as I don't really know what the intended message or audience would be, or how the visualisation would be delivered.
<h3>Trump/Obama Economic Policies Reaction</h3>
This <a href="https://www.flickr.com/photos/7563356@N08/45292344782/">first example</a> comes from some political analysis of the Trump and Obama presidencies.

| ![data storytelling - trump and obama]({{site.baseurl}}/assets/2021/10/45292344782_a58f8ee15f_o-300x236.png) |
|:--:|
| *data storytelling - trump and obama* |

<h4>Initial thoughts</h4>
<ul>
<li>Chart doesn't start at zero</li>
<li>Labels talk about percentages, but axes are numbers</li>
<li>Multiple colours used</li>
<li>No obvious focal point - what is the main point this chart is trying make?</li>
<li>Axes have been made less prominent and are generally uncluttered</li>
<li>Title not clearly aligned</li>
<li>Diagonal lines</li>
</ul>
<h4>My Attempt</h4>

| ![data storytelling - trump obama my version]({{site.baseurl}}/assets/2021/10/TrumpVsObama-300x182.png) |
|:--:|
| *data storytelling - trump obama my version* |

<h4>Summary of changes</h4>
<ul>
<li>Aligned the title to the left</li>
<li>Made the title more clearly reflect the Big Idea</li>
<li>Put all elements to the background by using grey</li>
<li>Remove colours apart from a blue to emphasise the Trump period</li>
<li>Reduce size of labels so they are less attention grabbing</li>
<li>Align labels so the design seems more deliberate</li>
</ul>
On reflection there were also other things that could have been done
<ul>
<li>Re-scale the y-axis to start at zero or show change relative to a baseline</li>
<li>Add an enclosing box or region to further emphasise the Trump period</li>
</ul>
<h4>Summary thoughts</h4>
<ul>
<li>Interesting that despite the ‘Big Idea’, once the distractions had been removed the effect was less clear. This is perhaps unsurprising given the source and purpose of the original chart. It’s a good reminder that we need to be careful not to overstretch the data to tell a point, only emphasise what is there.</li>
<li>I wasn’t really able to do a re-scale of the data so it started at zero. One thing that might have been interesting to do if the raw data was available was to re-plot showing a change from a baseline or change per year. As it is the line graph is rather noisy and in the long-run doesn’t really show much difference in trend between the two presidents.</li>
</ul>
<h3>Medical Personnel in South Vietnam</h3>
Next is <a href="https://www.flickr.com/photos/navymedicine/49306295576/">an example</a> of a table taken from a Vietnam war status update.

| ![data storytelling - medical personnel]({{site.baseurl}}/assets/2021/10/49306295576_b0571e3a85_c-300x202.jpg) |
|:--:|
| *data storytelling - medical personnel* |


<h4>Initial thoughts</h4>
<ul>
<li>very noticeable black lines representing rows and columns.</li>
<li>Center-aligned title</li>
<li>Title is rather dominant</li>
<li>No clear purpose or ‘Big Idea’ to highlight.</li>
</ul>
<h4>My Attempt</h4>
| ![vietnam personnel - my attempt]({{site.baseurl}}/assets/2021/10/VietnamMedicalPersonnelWithTitle-300x122.png) |
|:--:|
| *vietnam personnel - my attempt* |

<h4>Summary of Changes</h4>
<ul>
<li>Rather than do anything fancy, just use it as an opportunity to apply some of the general principles of putting non-data to the background and adding a bit of breathing space to the numbers.</li>
<li>Changed to Arial font so as to be in line with the other graphics attempted in this post. An alternative might have been to move plot it as a bar chart. Using Arial lacks the aesthetic that the original had.</li>
<li>Use Arial Heavy for the title, but in grey so the title is bold, but sits somewhat in the background</li>
</ul>

<h3>Carbon Baseline</h3>
This <a href="https://www.flickr.com/photos/warrenpearce/4582620392/">final example</a> seems to be a carbon review carried out by a business.

| ![data storytelling - carbon baseline]({{site.baseurl}}/assets/2021/10/4582620392_f859d60dff_o-300x100.jpg) |
|:--:|
| *data storytelling - carbon baseline* |

<h4>Initial Thoughts</h4>
<ul>
<li>What’s the big idea? There isn’t much context to this chart, but it seems to be examining carbon generated by different areas. A possible way of expressing this is “Focus on contracted services to make the biggest impact on carbon emissions”.</li>
<li>Use of a 3d pie chart isn't great, although it does use labels rather than a legend</li>
<li>Uses a box around the chart</li>
</ul>

<h4>My Attempt</h4>

| ![data storytelling - carbon baseline - my attempt]({{site.baseurl}}/assets/2021/10/CarbonBaseline-300x180.png) |
|:--:|
| *data storytelling - carbon baseline - my attempt* |

<h4>Summary of changes</h4>
<ul>
<li>In this case I mainly just wanted to get away from using a pie chart.</li>
<li>Change to horizontal bar chart. Excel recommended this as the category label text is relatively long and there are only a few categories</li>
<li>Change the title to reflect the Big Idea</li>
<li>Highlight the main category of interest using blue</li>
</ul>
<h4>Other thoughts:</h4>
<ul>
<li>Does the book suggest other possible options?</li>
<li>What about x-axis tick labels?</li>
<li>What about showing proportions rather than absolute numbers?</li>
</ul>

<h2>Finding Charts for Practice</h2>
If you want to practice data storytelling on some existing charts then some possible sources include:
<ul>
<li><a href="https://commons.wikimedia.org/w/index.php?search=chart&amp;title=Special:MediaSearch&amp;go=Go&amp;type=image">Wikimedia charts</a></li>
<li><a href="https://www.flickr.com/search/?license=1%2C2%2C9%2C10&amp;text=chart%20graph">flickr</a></li>
<li>Just do an image search for 'chart' or 'graph'</li>
</ul>
