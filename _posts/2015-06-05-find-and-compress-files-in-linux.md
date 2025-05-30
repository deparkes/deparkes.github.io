---
layout: post
title: Find and Compress Files in Linux
date: 2015-06-05 12:24:26.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- Linux
tags:
- compress
- find
- script
- shell
author:
  display_name: deparkes
permalink: "/2015/06/05/find-and-compress-files-in-linux/"
---
If you need to free up some space you can use this script to find and compress files in linux.
In my case I had some simulation files that were not currently needed, but I didn't want to get rid of them completely.
<h1>A Simple Bash Script</h1>
This simple script just looks through the whole of the current directory for files of the type ".ohf".
I used this script to free up disk space, but if you <strong>just wanted to compress the files</strong> you can just delete or comment out that line.

```bash
#!/bin/bash
# Find all ohf files.
# Put them into a tar ball in the directory they were found
find ./ -type f -name "*.ohf" -execdir tar -rvf ohf_archive.tar {} \
# Find all ohf_archive.tar file
# compress them
find ./ -type f -name "ohf_archive.tar" -execdir gzip {} \;
# Find all ohf files again and delete them
find ./ -type f -name "*.ohf" -execdir rm -rf {} \;
```

<h1>A More Flexible Modification</h1>
In most cases I think a simple script like the one above will be enough, but it's easy to add a couple of changes to make it more flexible.
Here I've added the ability to <strong>specify the file type</strong> <a href="https://how-to.wikia.com/wiki/How_to_read_command_line_arguments_in_a_bash_script">from the command line</a>, and what the <strong>output file name</strong> should be.

```bash
#!/bin/bash
# Usage: myzip.sh filetype archive_name
# Find all ohf files.
# Put them into a tar ball in the directory they were found
files="*$1"
tarfile="$2.tar"
find ./ -type f -name "$files" -execdir tar -rvf  "$tarfile" {} \;
# Find all ohf_archive.tar file
# compress them
find ./ -type f -name $tarfile -execdir gzip {} \;
echo "Output to $tarfile"
# Find all ohf files again
find ./ -type f -name $1 -execdir rm -rf {} \;
```
<div class="attribution-info"></div>
