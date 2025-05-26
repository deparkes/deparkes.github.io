---
layout: post
title: Improve Your Python Code With pylint
date: 2015-08-11 09:00:53.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- anaconda
- code
- improve
- spyder
author:
  display_name: deparkes
permalink: "/2015/08/11/improve-your-python-code-with-pylint-2/"
---
The myriad recommendations and requirements of the <a href="https://www.python.org/dev/peps/pep-0008/">Python Style Guide</a> can be bewildering and difficult to remember for the uninitiated.  <a href="http://www.pylint.org/">Pylint </a>is a Python application that analyses your code and suggests where you could make it more readable and more inline with the <a href="https://www.python.org/dev/peps/pep-0008/">Python style guide</a>.
Pylint takes much of the hard work out of using these conventions, by pointing out things like:
<ul>
<li>Missing docstrings in classes/functions</li>
<li>Checking variable, class and function names</li>
<li>Checking your code's line length</li>
</ul>
As you work through Pylint's list of suggestions it will update its 10-point evaluation to let you know how well-styled and readable your code is.
<a href="{{site.baseurl}}/assets/2015/08/pylint-window.png">


| ![improve your python code - pylint window]({{site.baseurl}}/assets/2015/08/pylint-window.png) |
|:--:|
| *improve your python code - pylint window* |

These are all things that we should ideally be keeping on top of as we go along, but of course we will always slip at some point. The more you use pylint, the more familiar you will become with the python style conventions, and before long you'll find you are writing much better and more readable code first time, without having to run pylint first.
Pylint is <a href="http://www.pylint.org/#install">easy to install</a> and <a href="http://docs.pylint.org/ide-integration">readily integrated</a> into commonly used Python IDEs such as <a href="https://pythonhosted.org/spyder/">Spyder/</a><a href="https://store.continuum.io/cshop/anaconda/">Anaconda</a>, <a href="http://www.pydev.org/">Eclipse/PyDev</a>, or <a href="https://www.jetbrains.com/pycharm/">PyCharm </a>so it's easy to use Pylint as you write.
<a href="{{site.baseurl}}/assets/2015/08/pylint-in-spyder.png">

| ![improve your python code - pylint in spyder]({{site.baseurl}}/assets/2015/08/pylint-in-spyder.png) |
|:--:|
| *improve your python code - pylint in spyder* |
