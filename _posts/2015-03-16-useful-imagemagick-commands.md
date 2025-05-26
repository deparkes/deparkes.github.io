---
layout: post
title: Useful Imagemagick Commands
date: 2015-03-16 09:36:06.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- software
tags:
- image processing
- imagemagick
- images
author:
  display_name: deparkes
permalink: "/2015/03/16/useful-imagemagick-commands/"
---
<a href="http://www.imagemagick.org/">Imagemagick </a>is a command-line based image processing suite. It's hugely powerful with all kinds of <a href="http://www.imagemagick.org/script/examples.php">functions and features</a>, and I can never quite remember how to use my favourite commands.
There is a very good and comprehensive list of '<a href="http://www.imagemagick.org/Usage/basics/">basic</a>' commands, but I find it dwarfs the selection that I actually need, so here are some useful Imagemagick commands that I can never remember how to use.
<h3><a href="http://www.imagemagick.org/script/binary-releases.php">Download Imagemagick</a></h3>
<h1>Mogrify vs Convert</h1>
It's worth pointing out that Imagemagick has two main commands for modifying images. The main difference is that '<a href="http://www.imagemagick.org/Usage/basics/#convert">convert</a>' tends to be for working on individual images, whereas '<a href="http://www.imagemagick.org/Usage/basics/#mogrify">mogrify</a>' is for batch processing multiple files.
Another key distinction is that convert is designed to modify an image and output to a separate file. Mogrify on the other hand will quite happily change the original file, unless you specify a separate output location. Be careful not to modify images without a backup!
<h1>Processing Individual Images</h1>
The convert command is used to operate on single images and it's repertoire of functions is much greater than that of mogrify.
Add file name as label to image

```bash
convert input.jpg -gravity South -annotate 0 '%f' output.jpg
```

For a more advanced labelling method, see <a href="http://stackoverflow.com/questions/4106200/overlaying-an-images-filename-using-imagemagick-or-similar">here</a>.
<h1>Batch Process Images</h1>
Batch processing with mogrify is probably where Imagemagick comes into its own. In these examples, the script will operate on all png files within the current folder.
<strong>Change format to jpg</strong>:

```bash
mogrify    -format jpg   *.png
```

Save as a jpg and <strong>output to the directory 'new_folder'</strong>:

```bash
mogrify    -format jpg -path ./new_folder  *.png
```

Save as a jpg, output to 'new_folder', <strong>resize to 50%</strong>:

```bash
mogrify    -format jpg -resize 50% -path ./new_folder  *.png
```

For more complex processes, it is recommended that you <strong>write your own script</strong> that uses 'convert' rather than 'mogrify'.
Check out <a href="http://www.imagemagick.org/script/api.php#python">this list</a> of libraries, modules and packages for interfacing with your favourite scripting language.
