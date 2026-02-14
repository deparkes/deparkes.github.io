---
layout: post
title: Make a Grid of Images With Imagemagick
date: 2015-05-01 09:00:58.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- data
tags:
- grid
- image processing
- imagemagick
- images
- montage
- thesis tips
author: deparkes
permalink: "/2015/05/01/make-a-grid-of-images-with-imagemagick/"
---
<h1>How to Make a Grid of Images</h1>
Perhaps you've got a <strong>time-series</strong> of images that you want to examine, or you want to look for <strong>differences in images</strong> taken from different experiments. Presenting images next to each other in a grid can make it much easier to see, and convey, what is going on. In this post I'll show you how you can use <a href="https://www.imagemagick.org/">Imagemagick </a>to make a grid of images quickly and easily.
<h3><a href="https://www.imagemagick.org/script/binary-releases.php">Download Imagemagick</a></h3>
The Imagemagick command we're going to use is '<a href="https://www.imagemagick.org/script/binary-releases.php">montage</a>'. Montage is a powerful and flexible command, so I'll just use this simple example to show off some of the things it's capable of.
```bash
montage -density 300 -tile 2x0 -geometry +5+50 -border 10 *.png out.png
```
Which gives the output (to "out.png"):

| ![Make a Grid of Images - combine]({{site.url}}/assets/2015/05/combined1-473x1024.png) |
|:--:|
| *Make a Grid of Images - combine * |

The important options we've included are
"<strong>-tile 2x0</strong>" This specifies that we want to arrange the images into two columns, with as many rows as needed. Imagemagick automatically tries to arrange the images as 'nicely' as possible.
"<strong>-geometry +5+50</strong>" tells the montage command to set a 5 pixel boundary between the images in the x direction, and a 50 pixel boundary in the y direction.
"<strong>-border 2</strong>" puts a 2 pixel border around each of the images in the grid.
"<strong>-density 300</strong>", which sets the output pixels/inch. I found that the default resolution was too low.
<strong>"*.png out.png" </strong>sets the command to look for all png files in the current folder, with the output being set to a file 'out.png'.<strong>
</strong>
This example should get you up and running, but be sure to check out the<a href="https://www.imagemagick.org/Usage/montage/"> Imagemagick manual page</a> to see the full range of options for montage. Of course you can also combine it with some of the <a href="{{site.url}}/tag/imagemagick/">other Imagemagick commands</a> to help automate your image processing steps.
<h3><a href="https://www.imagemagick.org/Usage/montage/">Find out about more advanced montage usage</a></h3>
