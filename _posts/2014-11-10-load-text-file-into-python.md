---
layout: post
title: 'Python tips: checking for updated input files'
date: 2014-11-10 22:41:23.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- python
- python tips
author: deparkes
permalink: "/2014/11/10/load-text-file-into-python/"
---
<h1>Introduction</h1>
Loading files from python scripts can have many benefits such as for data analysis or setting script parameters.

This article shows you how to not only load in a text file, line-by-line into a python list, but also how to keep checking for and loading updated versions of that file during a simulation run.

Loading files like this can be useful if you notice your list of parameters is incorrect before the simulation run is complete. You can just alter the input file and the script will pick up the new version on the next iteration.
You can find the files for this, and other posts from this series in my PythonTips <a href="https://github.com/deparkes/PythonTips" target="_blank">github repository</a>.
<h2>Things covered in this article:</h2>
<ul>
<li>loading a text file line by line into a python list</li>
<li>iterating through the list using a loop</li>
<li>using try and except to protect our script from errors</li>
</ul>
<h1>How to do it</h1>
<h2>Loading in a text file line-by-line</h2>
First we'll sort out loading our text file. Thankfully loading in a text file is rather straight forward in python. We can just use
```python
FileList = open('./FileList.txt').read().splitlines()
```

This will load each line in 'FileList.txt' as a different element in the list FileList.
<h2>Make some dummy simulation code</h2>
Now that we've got access to our list of parameters to act on we need to have python operate on it in some way.
To show what effect our file loader might have, lets add some dummy code to represent our simulation. This could be in the same script, a different python script, or a separate program called externally.
In this case we'll simply iterate through our list and display each element in turn. Of course for a real script this would use the list value as in input to the simulation or analysis.
This technique only really works, and is only really useful when our simulations take a long time. In these circumstances we don't want to interrupt our simulation, or wait for it to finish. Rather than waiting, our dummy simulation code just contains a pause, to give us enough time to modify the input file.
```python
print "Running script on %s" % (FileList[file_count])
print "Modify the file now, if you want"
a=raw_input()
```

Once we've made any alterations to our input file, we just press enter and the code continues.
<h2>Make our list of input parameters</h2>
Lets say that we want our simulation to work on a series of files. We can make list of these files in a text file, with each file name on a seprate line, like this:
```
File1
File2
File3
File5
```
Note the deliberately miscounted file names, missing out File4. We'll use our script to enable us to correct this 'on the fly'.
<h2>Using the most recent list for input</h2>
Finally, we can add in the code to our script to allow us check for updates to our file list in between simulation runs.

```python
try:
    file_list_new = open('./FileList.txt').read().splitlines()
    if FileList != file_list_new:
        FileList = file_list_new
        print(FileList)
        print('New list loaded successfully');
except IOError:
    print('Error loading new file\n')
```
The technique we use here is quite straight forward. Each time we run our simulation code as we iterate through the file names list we load the list and check to see if it has been changed. If it has, we use the mostly recent version of the list.
<h2>Protect your script with try...except</h2>
By using a try and except block we can anticipate any problems and tell the script what to do if there is a problem.
The script will first attempt to run the code in the 'try' block. If this is successful, then the try-except block is finished. If however there is an error, an exception, python will instead run the code in the except block. In this case here the except block just gives us more informative error information than the standard, but it could in principle be as complicated as we'd like.
In this script we've told it to watch out for an 'IOError' meaning that there are problems with loading the file.
We might also have added a 'finally' block. Code included in the finally block is run whether the try is error free or not.
<h1>Example Run</h1>
Here is an example run of this program, using an 'incorrect' list of files. We start by running the program through a few times.

| ![Initial run of FileLoadLoop.py. We have not yet noticed that our file list is incorrect]({{site.url}}/assets/2014/11/Screenshot3.png) |
|:--:|
| *Initial run of FileLoadLoop.py. We have not yet noticed that our file list is incorrect* |

Oh, no! The file list is incorrect. We need to change it before the next iteration. We just open up FileList.txt in our <a title="Notepad2-mod for editing OOMMF Files" href="{{site.url}}/2014/05/13/notepad2-mod-for-editing-oommf-files/">favourite text editor</a> and save it.

| ![Elements in this list.]({{site.url}}/assets/2014/11/Screenshot5.png) |
|:--:|
| *After the mistake in the intial file list, we load up the new list. The script continues to work on the list elements.* |

With the text file corrected we can keep running through the iterations and complete the analysis/simulation as planned.
<h1>Conclusion</h1>
So there it is. With this script you can load a text file a line at a time into a python list and keep checking to make sure that list is updated.
You can can also use a 'try-except' block to protect your code against exceptions which might otherwise cause your code to break.
