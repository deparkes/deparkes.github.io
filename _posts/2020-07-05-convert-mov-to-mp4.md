---
layout: post
title: Convert mov to mp4
date: 2020-07-05 15:25:14.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Video
tags:
- bash
- convert
- ffmpeg
- film
- movie
- open source
- powershell
- video
author: deparkes
permalink: "/2020/07/05/convert-mov-to-mp4/"
---
This post shows you how you can use the free ffmpeg tool to convert files: mov to mp4, either single files or whole folders. These days if you make a video with your phone or camera, the chances are it records it as an mp4. Older devices might store videos in mov format, which is not always compatible with modern software - particularly on windows machines.
<h2>Get ffmpeg</h2>
<a href="https://ffmpeg.org/about.html">ffmpeg</a> is a free, open source tool for working with video files. Ffmpeg itself is <a href="https://ffmpeg.org/ffmpeg.html">command-line based</a>, so might take a bit of getting used to if you are not familiar with it. The ffmpeg documentation is dense, but comprehensive - you can read the generic file conversion documentation <a href="https://ffmpeg.org/ffmpeg.html#Video-and-Audio-file-format-conversion">here</a>.
<a href="https://ffmpeg.org/download.html">Download ffmpeg</a> for your platform
See how you can <a href="{{site.baseurl}}/2018/01/05/create-video-images-ffmpeg/">use ffmpeg to turn a series of still images into a movie</a>
<h2>Convert mov to mp4 - single file</h2>
To convert a single mov to mp4 you can use the commands described in this <a href="https://stackoverflow.com/questions/12026381/ffmpeg-converting-mov-files-to-mp4">stackoverflow</a> answer:

```bash
ffmpeg -i input.mov output.mp4
```

If you want to output to a different folder you can just include that in the output filename, like this:

```bash
ffmpeg -i input.mov mp4/output.mp4
```

This is fine if you only have a single file, but you may also have a whole folder full over mov-formatted movies that you want to convert. ffmpeg can help you with that too.
<h2>Convert mov to mp4 - many files</h2>
Converting one mov to mp4 at a time is fine for a few files, but if you have whole folder full (or more!) then it makes sense to batch process them in one go. The trick here is to associate the filename of the input file with the filename of the output file.
To do this we will use the scripting tools available on different platforms - <a href="https://en.wikipedia.org/wiki/Unix_shell">shell</a> for Linux/mac and <a href="https://en.wikipedia.org/wiki/Windows_PowerShell">Powershell</a> for windows.
<h3>Windows (Powershell)</h3>
This works by:
<ol>
<li>Listing the contents of the current directory</li>
<li>
Filtering the contents of that directory to only include mov files
</li>
<li>
For each one of those files, convert with ffmpeg and change the filename's extension from 'mov' to 'mp4' (note this is case-sensitive, so you may need to swap 'mov' with 'MOV' for example)
</li>
</ol>

```powershell
ls | Where { $_.Extension -eq ".mov" } | ForEach { ffmpeg -i $_.FullName $_.Name.Replace(".mov", ".mp4") }
```

With a small modification we can output to a specified folder:

```powershell
ls | Where { $_.Extension -eq ".mov" } | ForEach { ffmpeg -i $_.FullName "output_folder/$($_.Name.Replace(".mov", ".mp4"))" }
```

For Linux/mac users, you can <a href="https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-7">install powershell for linux</a>, if you like, or check the commands for linux below.
<h3>Linux/Mac</h3>
For Linux or mac it is probably easier to use shell scripting rather than powershell:

```bash
for i in *.mov; do ffmpeg -i "$i" "mp4/${i%.*}.mp4"; done
```

If you are a windows user you can use this method if you install the <a href="https://docs.microsoft.com/en-us/windows/wsl/about">Windows Subsystem for Linux</a>.
You can read more discussion of batch processing on this <a href="https://stackoverflow.com/questions/5784661/how-do-you-convert-an-entire-directory-with-ffmpeg">StackOverflow answer</a>.
