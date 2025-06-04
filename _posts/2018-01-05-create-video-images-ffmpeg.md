---
layout: post
title: Create a Video From Images With ffmpeg
date: 2018-01-05 15:00:52.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- convert
- ffmpeg
- images
- video
author: deparkes
permalink: "/2018/01/05/create-video-images-ffmpeg/"
---
Turning a sequence of images into a video can be useful for creating <a href="https://en.wikipedia.org/wiki/Stop_motion">stop-frame movies</a>, <a href="https://shallowsky.com/blog/2015/Oct/04/">scientific animations</a>, and simple slide shows. This post shows you how you can use the free command line tool <a href="https://www.ffmpeg.org/">ffmpeg</a> to create a video from images. ffmpeg is a powerful, versatile command line tool which is <a href="https://en.wikipedia.org/wiki/Category:Software_that_uses_FFmpeg">widely used</a> for other movie and animation manipulation tasks.
<h1>Prepare Your Image Files<strong>
</strong>
</h1>
It's actually quite easy to create a video from images using ffmpeg, as long as you prepare your image files in right way.
You need to make sure your sequence of images are in the same folder and named correctly. They should be named sequentially, for example img-00.png, img-01.png, img-02.png and so on. By default ffmpeg expects that images should be <a href="https://superuser.com/questions/624567/how-to-create-a-video-from-images-using-ffmpeg">numbered starting from zero</a>.

| ![video from images]({{site.baseurl}}/assets/2018/01/images_to_video.png) |
|:--:|
| *Video from images* |

<h1>Create a Video From Images</h1>
Once you have your source images named correctly and in the same directory, you can run this command at the command line (from inside your image directory):

```bash
ffmpeg -i img-%02d.png video_name.avi
```

In this example, ffmpeg will look for images with file names with 'img-' followed by a two-digit number and a .png file extension, and convert these images into a avi video file named 'video_name.avi'.
In this command you need to specify a <a href="https://en.wikibooks.org/wiki/FFMPEG_An_Intermediate_Guide/image_sequence#Filename_patterns">search pattern</a> for ffmpeg to find the image sequence it should use. This search pattern depends on what you named your images when preparing them.
<h2>Setting The Frame Rate</h2>
An important consideration when you create a video from images is the frame rate - the number of frames (images) per second (fps) in the video. The most appropriate frame rate will depend on your source images. If you are making a stop-frame animation for example, you may be happy with the default of 25 fps. If however you want something more like a slow moving slide show, you may want a slower frame rate such as 2 fps.
If you don't specify the frame rate, you may find some odd results in your output video file. For example, to set an output video with a frame rate of 5 fps, you would need to run:

```bash
ffmpeg -framerate 5 -i img-%02d.png video.avi
```

<h2>Changing the Video Format</h2>
In these examples I have used avi as the output video format. ffmpeg supports a range of <a href="https://www.ffmpeg.org/general.html#Supported-File-Formats_002c-Codecs-or-Features">different video formats</a> and you can change the format of your output video by changing the file extension of the output video file.
To see which output formats are available you can run:

```bash
ffmpeg -encoders
```

