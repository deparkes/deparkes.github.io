---
layout: post
title: 'OOMMF Tutorial Part 8: OOMMF on HPC'
date: 2015-02-05 15:24:41.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- HPC
- oommf
author: deparkes
permalink: "/2015/02/05/oommf-on-hpc/"
---
<h1>OOMMF on HPC</h1>
HPC facilities can be very useful for<a href="{{site.baseurl}}/2014/10/16/oommf-tutorial-part-5-oommf-tips/"> speeding up OOMMF calculations</a>, both in terms of number of cores you can throw at the problem, and the number of <strong>simultaneous calculations</strong> you can run at once.
This post is a few tips and tricks I've picked up as I've been using OOMMF on HPC.
<h1>Installing OOMMF on an HPC</h1>
You almost certainly <strong>don't have root access</strong> on your HPC account. To install <strong>OOMMF without root</strong>, I suggest you read this <a title="Install OOMMF 1.2a5 without root" href="{{site.baseurl}}/2013/06/24/install-oommf-1-2a5-without-root/">guide</a>.
<h1>Check your mif files</h1>
For the most part your desktop and HPC mif files will be identical, but <strong>be careful</strong> about setting the scripts to automatically display on mmDisp or mmGraph. This will almost certainly cause your job to hang, probably without any error being reported - very frustrating!
<h1>Be clever about automatic saving</h1>
If space allows, set your mif file to <a href="{{site.baseurl}}/2015/02/05/oommf-automatic-output/">automatically</a><strong> save the omf</strong> magnetisation output every 1000 steps or so, this means that if you do happen to reach your <strong>computation time limit</strong>, you won't have to go back to the start when you re-run your calculation.
But do keep in mind the point above - <strong>don't try to automatically display</strong> the data on the HPC.
<h1>Use a master script</h1>
For large jobs I like to use a python master script - like this one <a href="https://github.com/bauhuasbadguy/Running-many-oommf-scripts">here</a>. This helps me <a title="Organising Computational Projects" href="{{site.baseurl}}/2013/06/25/organising-computational-projects/">organise </a>my submissions and outputs, and allows me to quickly and easily iterate through various parameters I might be interested in.

<a href="{{site.baseurl}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.baseurl}}/assets/2015/02/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
