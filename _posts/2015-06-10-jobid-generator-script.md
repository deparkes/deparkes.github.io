---
layout: post
title: JOBID generator script
date: 2015-06-10 11:30:20.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- data
- python
tags:
- generator
- jobid
- script
author:
  display_name: deparkes
permalink: "/2015/06/10/jobid-generator-script/"
---
How you <a href="{{site.baseurl}}/2013/06/25/organising-computational-projects/">organise your computational projects</a> is important. If you're not  careful you can find yourself with hundreds of computer-hours worth of data,  without being exactly sure which parameters or scripts you used to generate it. One way to keep track of your scripts and your data is with a JOBID number, which you attach to records of input and output files, and lists of parameters you used for each job.
On server-type systems such as <a href="https://en.wikipedia.org/wiki/Portable_Batch_System">high-performance computers</a>, or research  facilities like the <a href="https://www.diamond.ac.uk/Home.html">Diamond Light Source</a> synchrotron, which uses <a href="https://www.opengda.org/">GDA</a>, there is often a system  set up to automatically generate a unique JOBID each time a job or script is run. This makes it much easier to keep track of exactly which simulation, calculation or operation was carried out. Inspired by these server-type systems, I've made a simple <a href="https://github.com/deparkes/jobid">jobid generator script</a> for running jobs on my own machine.
Each time you call the script it increments a log file with the JOBID, a time stamp, and records any comments you wish to make to the job. You can incorporate the JOBID output from this script into your own jobs.
Once you've got the JOBID it opens doors for you to make copies of your input scripts, your output files, and make a record of the parameters used for each job. It also makes it much easier and quicker to link your computational work to notes in a physical paper notebook, as one JOBID number immediately connects you to all work related to a particular calculation or experiment. I like to use the search program "<a href="https://www.voidtools.com/">Everything</a>" to quickly find files relating to a particular JOBID.
Once you've got your unique JOBID, here's a few things you could try.
<ul>
<li>automatically <strong>save output files</strong> with jobid in the filename</li>
<li>
<strong>save outputs in a directory</strong> named after the jobid</li>
<li>create a <strong>copy of your script</strong> file with the JOBID prepended to the filename</li>
<li>create a separate<strong> parameters file</strong>, named after the JOBID.</li>
</ul>
<h3><a href="https://github.com/deparkes/jobid">Download my JOBID generator script</a></h3>
