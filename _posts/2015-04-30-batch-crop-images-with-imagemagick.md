---
layout: post
title: Batch Crop Images With Imagemagick
date: 2015-04-30 09:00:47.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- imagemagick
- images
author: deparkes
permalink: "/2015/04/30/batch-crop-images-with-imagemagick/"
---

<h1>How to Batch Crop Images With Imagemagick</h1>
<a href="https://www.imagemagick.org/">Imagemagick </a>is a powerful, command-line based program for manipulating images. In this post I'll show you how to use Imagemagick to crop several images with one command.
<h3><a href="{{site.url}}/2015/03/16/useful-imagemagick-commands/">Find some more useful Imagemagick commands</a></h3>

<h2>Crop a Single Image</h2>
We'll start by looking at how to <a href="https://www.imagemagick.org/Usage/crop/">crop </a>a single image using Imagemagick. First <a href="https://www.imagemagick.org/script/binary-releases.php">download Imagemagick</a> if you haven't already. First, <a href="{{site.url}}/2015/04/28/how-to-open-a-command-prompt-in-a-folder/">open a command window </a>in the folder containing the image(s) you want to crop.
The command we want to run looks like this:

```bash
convert -crop x_sizexy_size+x_offset+y_offset inputfile outputfile
```

the different dimensions in the image we want to crop are shown below

| ![batch crop - Batch Crop Images]({{site.url}}/assets/2015/04/CropLayout.png) |
|:--:|
| *batch crop - Batch Crop Images* |

let's try running the Imagemagick crop command on this image to crop away all of the blue area, leaving only the red.
I've measured the pixel dimensions in mspaint, so I know exactly the area that I want to crop to. So the command is:

```bash
convert -crop 300x200+150+150 CropLayout.png CroppedLayout.png
```

Which outputs the image 'CroppedLayout.png'

| ![batch crop - Batch Crop Images]({{site.url}}/assets/2015/04/CropLayout1.png) |
|:--:|
| *batch crop - Batch Crop Images* |

<h2>Batch Crop a Folder of Images</h2>
That was the basic usage, but we can also combine it with the Imagemagick batch processor <a href="https://www.imagemagick.org/script/mogrify.php">mogrify </a>to crop many images at the same time.
In this example we'll crop a whole folder full of images to the same dimensions as in the example above.
Here's what we're starting with:


| ![batch crop - Batch Crop Images]({{site.url}}/assets/2015/04/ToCropArray.png) |
|:--:|
| *batch crop - Batch Crop Images* |

First we'll make a new folder called 'cropped' to keep the cropped images in. Now we'll run the command with a couple of changes:

```bash
mogrify -crop 300x300+150+150 -path ./cropped *.png
```
firstly we've specified the output to go to the cropped folder using the '-path' flag. Secondly we've told mogrify to look for all .png files in the current folder.

If we look in the cropped folder once we've run this command we get this

| ![batch crop - Batch Crop Images]({{site.url}}/assets/2015/04/CroppedImages.png) |
|:--:|
| *batch crop - Batch Crop Images* |
