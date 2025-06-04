---
layout: post
title: 'OOMMF Tutorial Part 6: OOMMF scripting with python'
date: 2014-10-28 20:33:33.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- oommf tutorial
- oommf tutorial part 6
- python
- scripting
author: deparkes
permalink: "/2014/10/28/oommf-tutorial-part-6-oommf-scripting-python/"
---
<h1 class="attribution-info">Introduction</h1>
This tutorial will show you how you can setup up OOMMF scripting with python. It will guide you through setting up your mif files for scripting and using python scripts to run OOMMF from the command line.
The examples will show you enough to get up and running with basic scripting, and point you in the right direction for more advanced sripting tasks.
<h1 class="attribution-info">Before you start</h1>
Automating your OOMMF simulations with python scripts can be a great way to improve your efficiency. You can queue up a range of simulations and loop through various different parameters, all without having to continuously check the progress of individual  simulations.
OOMMF can generate a large number of files at the best of times, and once you start automating you may find you generate so many files that this can become overwhelming.
Your best defense against this is to have a little think about how you want to organise your project. We can use our scripts to automatically save our output files where we want and with sensible names, so we should use this to our advantage.
For more information about organising computational projects (particularly OOMMF), you can read this post <a title="Organising Computational Projects" href="{{site.baseurl}}/2013/06/25/organising-computational-projects/">here</a>.
<h1 class="attribution-info">Setting up python</h1>
There plenty of good guides to downloading and installing python, both online [<a href="https://docs.python-guide.org/en/latest/">1</a>,<a href="https://wiki.python.org/moin/BeginnersGuide">2</a>,<a href="https://www.python.org/about/gettingstarted/">3</a>], and in print[<a href="https://amzn.to/1zmgFSz">1</a>,<a href="https://amzn.to/1uKOBQI">2</a>,<a href="https://amzn.to/ZJqGsy">3</a>], so I won't really dwell on it here.
For this tutorial vanilla <a href="https://www.python.org/download/">python 2.7</a> will be enough, but you might want to consider using one of the scientific distributions of python which are now available such as:
<ul>
<li><a href="https://store.continuum.io/cshop/anaconda/">Anaconda</a></li>
<li><a href="https://www.enthought.com/products/canopy/">Enthought Canopy</a></li>
<li><a href="https://code.google.com/p/spyderlib/">spyder</a></li>
</ul>

<h2>OOMMF scripting: Boxsi</h2>

The oommf scripting tool is called <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/OOMMF_eXtensible_Solver_Bat.html">boxsi</a>. You can get the full details in the user manual, but for our purposes we just need to know that we can run oommf with a mif file and a list of parameters thusly:

```bash
oommf.tcl boxsi -parameters "param1 value1 param2 value2" filename.mif
```

We'll be using a version of this line in our python scripts to launch oommf.

<h1>Preparing OOMMF mif files for scripting</h1>

OOMMF already comes with tools for running it as a script from the command line interface, so scripting with it is quite straight forward. There are however a few things we'll want to do to set up our mif files so we can get th emost out of scripting.

Oh, and if you haven't done so already, make sure you get a<a title="Notepad2-mod for editing OOMMF Files" href="{{site.baseurl}}/2014/05/13/notepad2-mod-for-editing-oommf-files/"> sensible text editor</a> with syntax highlighting so you can see what you're doing more easily.

<h2>Setting up parameters</h2>
We need to tell the mif file to allow certain variables to be changed from the command line.
Rather than use 'set xxx yyy' to define variables we use 'parameter xxx yyy', where xxx is the variable name. When we use 'set' yyy is the variable value, whereas when we use 'parameter' yyy is the default value which will be used if no further value is supplied from the command line.

<h2>Setting up variable substitution</h2>

Our parameters aren't worth much unless we can use them in our OOMMF specify blocks.
It's not immediately obvious how to do this (to me at least), so I've included it here. We just need to include our specify block in square brackets and a 'subst' command, like so:

```tcltk
# Divide image file into mesh, periodic in x direction
Specify Oxs_PeriodicRectangularMesh:mesh [ subst {
cellsize {$xcell $ycell $zcell}
atlas :atlas
periodic x
} ]
```

<div class="view attribution-view clear-float"></div>
<div class="view attribution-view clear-float">You can see this and other OOMMF tips in a previous post, <a title="OOMMF Tutorial Part 5: OOMMF Tips" href="{{site.baseurl}}/2014/10/16/oommf-tutorial-part-5-oommf-tips/">here</a>.</div>
<h2 class="view attribution-view clear-float">Automatic outputs</h2>

The final major thing we'll need to do to our mif files is make sure oommf automatically saves the outputs we want. Full details are available in the user manual, or you can check out another <a href="{{site.baseurl}}/2014/05/27/oommf-tutorial-part-3-mif-examples/">tutorial </a>in this series here which talks about some of the OOMMF example files and setting automatic output.
You will also need to be careful about naming your output files. If you are not careful you can easily over write all but the final simulation.

```tcltk
# Set a formatting string to prepend to the output, so we don't over-write
# output data
set outname [format "SquareCubic_xsize%.0fnm_ysize%.0fnm_zsize%.0fnm" $xsize $ysize $zsize]
```

We'll be putting code similar to this in our mif files to customise the output file name and destination.

<h1>OOMMF Scripting with Python: some examples</h1>

Ok, let's modify some of the examples that come with OOMMF to show what we can do with scripting. The files used in this tutorial are available for download <a href="https://github.com/deparkes/OOMMFpython">here</a>.

We'll start with a relatively simple script to just loop through a range of parameter numbers defined by the python script.
Then we'll try something more complicated by having the output of one simulation iteration go into the input of the next.
This tutorial really just covers the basics, but I've also included some ways you might want to improve the script to further unlock the power of scripting.
<h2>Example 1: Looping through parameters with squarecubic.mif</h2>

<h3>Set up squarecubic.mif</h3>
For this example we'll be modifying squarecubic.mif which comes with OOMMF 1.2a5. You can also find the original and the modified mif file (squarecubicscripted.mif) <a href="https://github.com/deparkes/OOMMFpython">here</a>.

First we'll set things up so we can accept some variables. Let's imagine we liked what squarecubic.mif did, but we'd also like to investigate how the simulation behaves for a range of different x and y dimensions. We think we might like to vary the z dimension at some point to, so we'll make a parameter for that too.

Once we've set up the variables, we also need to enable variable substitution so the script can have access.

We use the `$` to access the data stored in the variables. e.g. `$variable`.

```tcltk
parameter xsize 310e-9
parameter ysize 310e-9
parameter zsize 40e-9
Specify Oxs_BoxAtlas:atlas [ subst {
  xrange {0 $xsize}
  yrange {0 $ysize}
  zrange {0 $zsize}
}
]
```

We'll also enable automatic output of our scalar and vector data, like so:

```tcltk
# Create destinations
Destination my_graph mmGraph
Destination my_archive mmArchive
Destination my_display mmDisp
# Specify what should be saved
Schedule DataTable my_graph Step 1
Schedule DataTable my_archive Step 1
Schedule Oxs_TimeDriver::Magnetization my_archive Stage 1
Schedule Oxs_TimeDriver::Magnetization my_display Step 1
```

<h3>Write the python script</h3>
Now that our oommf mif file is ready to accept parameters and configured to automatically save the output, we can write our python script to run it.
In this case our script is going to be quite simple. It will:
<ul>
<li>Loop through the variables we specify</li>
<li>Run the oommf boxsi batch program using those variables as parameters</li>
</ul>

```python
import subprocess
import os
# define the path to your oommf install
path_oommf = 'C:/oommf-1.2a5bis/oommf.tcl'
# the name of the mif file
mif_file = os.path.abspath('../examples/squarecubic_scripted.mif')
# make our list of sizes that we will loop through
# in nm as our mif file converts to metres.
sizes = [100, 200, 300, 400]
for size in sizes:
	oommf_string = 'tclsh85' + ' ' + path_oommf + \
	' boxsi -parameters "xsize %s ysize %s" -- %s' % \
	 (size, size, mif_file)
	print oommf_string
	subprocess.call(oommf_string, shell=True)
```

You can download this script <a href="https://github.com/deparkes/OOMMFpython">here</a>.
We'll set up the file and create a python script to allow us to change the size of the square we are simulating.
You will notice we have only passed parameters for xsize and ysize (in fact we've used the same number for both, to keep it a square). As we've specified a default zsize value in the mif file we can just use that if we want.
This is a very simple example, but you might actually find this useful to help gauge how long it takes your system to run simulations of various sizes.
<h3>Taking things further:</h3>
Here are a few things you might want to think about for taking this script further:
<ul>
<li>Have nested loops to loop through different parameters, such as varying xsize and ysize.</li>
<li>Try setting parameters for the value of K1, the cubic anisotropy constant.</li>
<li>You can modify this script to take a list of different file names to use in an ImageAtlas.</li>
</ul>
<h2>Example 2: Using the output of one iteration as the input of the next</h2>
We'll build on our previous example to allow us to vary the anisotropy in squarecubic.mif.
Let's say we have some process which allows us to vary the cubic anisotropy in the square and want to see how smoothly varying that anisotropy affects the behaviour of the system.
To do this we need to have someway of automatically taking the output of one OOMMF simulation and passing it as the input to the next.
OOMMF automatically names output files with the stage and step number that produced them. This is usually helpful since it tells us important information about our simulation and is a first line of defence against accidentally over-writing files.
In this case, however this is something of a hindrance as we want our script to know exactly which output file to feed into OOMMF as the input of the next iteration.
It is difficult to have total control over the output filename, but we do have much more control over the output destination folder. We can use this to allow us to find the output file we want.
<h3>Prepare the mif file</h3>
As in the previous example, we will also need to prepare the mif file with various parameters.
Download the file squarecubic_scripted2.mif from <a href="https://github.com/deparkes/OOMMFpython">here</a>.
Look through and you'll find we've made a number of changes from the original squarecubic.mif:
<ul>
<li>Made a parameter for K1 and substitution in the specify block.</li>
<li>Made a parameter for specifying the output folder</li>
<li>Made a parameter specifying the input omf file</li>
<li>Made an output format string so we can specify the name and output folder</li>
<li>Automatic output formatting so there is a standard output.</li>
<li>In Oxs_TimeDriver we have changed to using Oxs_FileVectorField and changed the output basename.</li>
<li>Only output after the final stage so we end up with only one omf file for each value of the cubic anisotropy. This just keeps it a bit simpler to find the omf output file we want.</li>
</ul>
You'll see that much of this is similar to the previous example of squarecubicscripted.mif
</div>
<div class="view attribution-view clear-float">
<h3>The python script</h3>
With the mif file suitably modified we can now look to the python script file.
For this python script (squarecubicscript2.py) we're going to have to use some more advanced features. If you're not that familiar with python, it may seem somewhat bewildering, but I'll try to walk through it and include plenty of comments in the script.
As with the other files for this tutorial, you can download the python script <a href="https://github.com/deparkes/OOMMFpython">here</a>.
For the most part however you won't need to worry about exactly what python is doing, and can just copy and paste the relevant sections of the scripts for your own use.
Here's what the python script does:
<ul>
<li>Specify an initial omf file</li>
<li>Set the output directory for the first anisotropy value</li>
<li>Find the omf file in the output directory using the function 'get_omf'</li>
<li>Use this output file as the input for the next anisotropy value</li>
<li>Repeat until the all anisotropies have been simulated</li>
</ul>
You'll see that by this method we can easily and automatically pass the output of one OOMMF simulation into the input of another.
<h3>Suggested improvements:</h3>
Here's a few things you might like to think about for taking this script further:
<ul>
<li>You don't need to keep the other parameters constant from one iteration to the next. You can modify them between each step to have a 'time-varying' parameter.</li>
<li>You can have more omf outputs per simulation, you'll just have to use a combination of python functions and formatting strings to enable you to find the right one automatically.</li>
</ul>
<h1>Analysis</h1>
Now that you know how to use scripts to automate your OOMMF simulations you'll no doubt be generating an abundance of data to analyse.
Analysing this data by hand can be a difficult and time consuming task, so check out my tutorial on <a title="OOMMF Tutorial Part 4: OOMMF Analysis Tools" href="{{site.baseurl}}/2014/06/10/oommf-tutorial-part-4-oommf-analysis-tools/">OOMMF analysis tools</a>.
<h1 class="attribution-info">Tutorial Files</h1>
If you've not done so already you can find all the files used in this tutorial <a href="https://github.com/deparkes/OOMMFpython">here</a>.
If you find any mistakes with the files please <a href="https://github.com/deparkes/OOMMFpython/issues/new">create an issue on github</a>.
</div>
<a href="{{site.baseurl}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.baseurl}}/assets/2014/10/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
