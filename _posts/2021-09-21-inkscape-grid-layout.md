---
layout: post
title: Inkscape Grid Layout
date: 2021-09-21 19:54:07.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Design
tags:
- design grid
- graphic design
- grid
- inkscape
- layout
- scribus
author: deparkes
permalink: "/2021/09/21/inkscape-grid-layout/"
---
<a href="https://www.canva.com/learn/grid-design/">Grid layouts</a> are an important technique in graphic design. This blog post shows how you can make an <a href="https://inkscape.org/">Inkscape</a> grid layout using another open source publishing tool <a href="https://www.scribus.net/">Scribus</a>.
<h2>Inkscape Grid Layout</h2>
Scribus is an open source desktop publishing application and comes with a nice tool for breaking a page up into grids. This is much easier than manually attempting to calculate and draw a grid in Inkscape.
<h3>Creating The Grid</h3>
New document - set page size to same as what you will be using in Inkscape, or at least same proportions.
<blockquote>Page -&gt; Manage Guides -&gt; Column/Row</blockquote>
You can use whichever settings you want here. I chose 6 rows and 4 columns, measured from the margins rather than the page itself and included both a horizontal and vertical gap.

| ![Scribus Guide Manager]({{site.baseurl}}/assets/2021/09/GuideManager.png) |
|:--:|
| *Scribus Guide Manager* |

The grid guides will be visible on the Scribus page, but as yet there is no way to export them to Inkscape.

| ![Scribus Grid Guides]({{site.baseurl}}/assets/2021/09/GridGuides-1024x546.png) |
|:--:|
| *Scribus Grid Guides* |

To make the guides exportable we are going to draw shapes over the grid. First we want to make sure we'll exactly match the grid by turning on 'Snap to Guides' (don't turn on 'Snap to Grid').
<blockquote>Page -&gt; Snap to Guides</blockquote>
And then select the square shape:
<blockquote>Insert -&gt; Shape -&gt; Default Shapes -&gt; &lt;square&gt;</blockquote>
Draw a square in one of the grid boxes. With 'Snap to Guides' activated it should easily snap to the guides we created. If it snaps to a different point, you may have 'Snap to Grid' also selected.

| ![Scribus grid - single square]({{site.baseurl}}/assets/2021/09/GridGuidesSquare-1024x546.png) |
|:--:|
| *Scribus grid - single square* |

Copy and paste that square to the other grid-squares on that row.

| ![Scribus grid row]({{site.baseurl}}/assets/2021/09/GridGuidesSquareRow-1024x546.png) |
|:--:|
| *Scribus grid row* |

And then copy that row to the remaining columns.

| ![Scribus grid whole page]({{site.baseurl}}/assets/2021/09/GridGuidesSquareWholePage-1024x546.png) |
|:--:|
| *Scribus grid whole page* |

Finally we can export the grid as an SVG file for Inkscape.
<blockquote>File -&gt; Export -&gt; Save as SVG...</blockquote>
<h3>Loading the Grid into Inkscape</h3>
Open the created SVG file in Inkscape

| ![Inkscape grid loaded]({{site.baseurl}}/assets/2021/09/GridExampleInkscape-1024x546.png) |
|:--:|
| *Inkscape grid loaded* |

First we will create a new layer to hold the grid. We want the grid on a separate layer so it doesn't get in the way of our design and we can easily turn the visibility on and off.
<blockquote>Layer -&gt; Add Layer...</blockquote>
Add a new layer called 'Grid'.
Select all the grid rectangles and go
<blockquote>Layer -&gt; Move Selection to Layer</blockquote>
And select the new 'Grid' layer.
We can just purely use the grid a guide to the eye, but it can be easier if we make use of the 'Handle to cusp node' option, so we can design shapes which quickly snap to and line up with the grid. The option for turning this on can be found in the Snap controls bar:
<blockquote>View -&gt; Show/Hide -&gt; Snap controls bar</blockquote>

| ![Inkscape handle to cusp node]({{site.baseurl}}/assets/2021/09/SnapToNodeCloseup.png) |
|:--:|
| *Inkscape handle to cusp node* |

Remember to move onto a new layer before starting work - we want to keep the 'grid' layer just for the grid.

| ![Inkscape example layout with grid lines]({{site.baseurl}}/assets/2021/09/SimpleGridUsageExample-1024x546.png) |
|:--:|
| *Inkscape example layout with grid lines* |

Because we put the grid on a separate layer we can easily hide it check on progress as we build up our grid-based design.

| ![Inkscape hide the grid layer]({{site.baseurl}}/assets/2021/09/HideTheGridLayer-1024x546.png) |
|:--:|
| *Inkscape hide the grid layer* |
