---
layout: post
title: Python Instrument Control
date: 2015-03-03 20:36:56.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
- software
tags:
- hardware
- instrumentation
- interfacing
- labview
- python
- VISA
author:
  display_name: deparkes
permalink: "/2015/03/03/python-instrument-control/"
---
Python is becoming <a title="3 Python Alternatives to Matlab" href="{{site.baseurl}}/2015/02/28/python-alternatives-to-matlab/">more established</a> for scientific <strong>data analysis</strong> and <strong>processing</strong>, but what python<strong> instrument control</strong> options are there?
For me the <strong>benchmark</strong> instrument control software has to be <a href="http://www.ni.com/labview/">LabView</a>. It's incredibly expensive and certainly has it's quirks, but I've found that it can often make interfacing with hardware <strong>relatively painless</strong>.
I've recently been exploring alternatives to Matlab for scientific analysis and processing, so I was curious to see what the state of affairs was for <strong>python instrument control.</strong>
<h3>Read about my <a title="3 Python Alternatives to Matlab" href="{{site.baseurl}}/2015/02/28/python-alternatives-to-matlab/">3 Python Alternatives to Matlab</a>.</h3>
<h1>My Requirements For Instrument Control</h1>
For me any python instrument control package would need:
<ul>
<li><strong>Standard hardware interfacing (E.g. GPIB, RS232, USB)</strong></li>
<li><strong>NIDAQ interfacing</strong></li>
<li>Ability to easily build a virtual rack</li>
<li>Easy live plotting of data</li>
</ul>
The <strong>most important</strong> of these of course is the <strong>ability to interface</strong> with the measurement hardware, so let's see what python instrument control packages are available.
In a <strong>future post</strong> I'll investigate the options for completely <strong>replacing LabVIEW with python</strong>.
<h1>Python Instrument Control Packages</h1>
The <strong>most important</strong> part of any python instrument control software has to be the packages for <strong>interfacing</strong> with the measurement equipment itself.
Thankfully there are a couple of fairly <strong>well maintained python packages</strong> that cover most of your interfacing needs.
<h2>PyVISA</h2>
<a href="http://pyvisa.readthedocs.org/en/master/">PyVISA</a> is a python package for the <a href="http://en.wikipedia.org/wiki/Instrument_control">Virtual Instrument Software Architecture</a> (VISA). It's actually a wrapper for the National Instruments VISA library, which you will have to <a href="http://pyvisa.readthedocs.org/en/master/getting_nivisa.html#getting-nivisa">install separately</a>.
PyVISA allows python to relatively painlessly interface with:
<ul>
<li>GPIB</li>
<li>RS232</li>
<li>USB</li>
<li>Ethernet</li>
</ul>
This example (taken from the PyVISA documentation) communicates with a Keithley multimeter on GPIB address 12:
```python
import visa
rm = visa.ResourceManager()
rm.list_resources()
('ASRL1::INSTR', 'ASRL2::INSTR', 'GPIB0::12::INSTR')
inst = rm.open_resource('GPIB0::12::INSTR')
print(inst.query("*IDN?"))
```
PyVISA seems to be an active, regularly updated package with fairly good <a href="http://pyvisa.readthedocs.org/en/master/">documentation</a> page. Unfortunately the VISA architecture does not include the popular NIDAQ card interface. For that we need PyDAQmx (below).
<h2>PyDAQmx</h2>
Whilst <a href="http://pyvisa.readthedocs.org/en/master/">PyVISA </a>will allow you to communicate with most hardware, it unfortunately is not capable of communicating with the popular and commonly found <a href="http://www.ni.com/data-acquisition/pci/">NI-DAQ card</a>.
Thankfully there is an additional package, <a href="http://pythonhosted.org/PyDAQmx%20">PyDAQmx</a>, which acts as a wrapper to the NI-DAQ driver and allows your python scripts to communicate with the the DAQ card.
<div id="yui_3_16_0_1_1425412730845_686" class="view attribution-view requiredToShowOnServer clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Matt Mets's photostream" href="https://www.flickr.com/photos/cibomahto/" data-rapid_p="26" data-track="attributionNameClick">Image: Matt Mets; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-sa/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="31">Some rights reserved</a><a class="owner-name truncate" title="Go to Matt Mets's photostream" href="https://www.flickr.com/photos/cibomahto/" data-rapid_p="26" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1425412730845_687" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
