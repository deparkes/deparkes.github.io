---
layout: post
title: Python Packaging
date: 2019-10-20 14:57:19.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- deployment
- distribution
- packaging
- python
- software engineering
author:
  display_name: deparkes
permalink: "/2019/10/20/python-packaging/"
---
Python packaging can be difficult to navigate. At some point in your python development career you will want to share your project or library with someone else, or deploy it to another location. While it is possible to send the python files individually, anything more than a very simple project will run into difficulties with installation and dependencies.

Thankfully, Python has some nice tools for helping you with packaging your code for distribution. This post looks into how you can build and test a "source distribution" which can easily be shared and installed elsewhere.
<h2>Python Packaging</h2>
The topic of python packaging is <a href="https://xkcd.com/1987/">famously complicated</a>, and this this post I'm going to look at just one aspect of it.  I don't claim that this will suit all use cases, but it should be enough to get you going and be a starting point for other packaging techniques.
If you want to get a better sense of how python packaging fits within a wider packaging possibilities, I recommend <a href="https://www.youtube.com/watch?v=Q3LyPTTb81w">this talk by Mahmoud Hashemi</a>.
<h2>An Example</h2>
As an example let's imagine a situation where we have a written some python functions which we think our friends or colleagues would find useful.
Our functions only use 'pure Python', for example they don't use any of the heavy-lifting graphics or numerical libraries which we would otherwise need to share as well.
Our package has some tests which we don't want to include in the installed package.
To be clear, our goal will be to get to a point where we can:
<ul>
<li>Build a package we can share with friends and colleagues</li>
<li>Be able to install the package with pip</li>
<li>Be able to uninstall the package with pip</li>
<li>Be able to easily test the package during development</li>
<li>Not include development/test tools or code with the installed package</li>
</ul>
<a href="https://github.com/deparkes/python-packaging-example">See a simple example of a project using this structure.</a>
<h2>Project Structure</h2>
The first thing we will do is make sure the project structure is in a good way for putting in a package. I am going to follow the structure described in <a href="https://blog.ionelmc.ro/2014/05/25/python-packaging/#the-structure">this post</a>, which has benefits for both <a href="https://doc.pytest.org/en/latest/goodpractices.html">testing</a> and packaging.
```
├─ src
│  └─ my_package
│     ├─ __init__.py
│     └─ ...
├─ tests
│  └─ ...
└─ setup.py
```
The three main features here are
<ol>
<li>A separate tests directory</li>
<li>Actual package code is in 'src/my_package'</li>
<li>setup.py - this is the python file which will contain packaging metadata.</li>
</ol>
There are a few general goals with this structure:
<ol>
<li>Have clear separation of code to be packaged and code to do the packaging</li>
<li>To encourage you to test the code as it would appear if you had installed it,</li>
<li>Head off some of the other common <a href="https://blog.ionelmc.ro/2014/06/25/python-packaging-pitfalls/">python packaging pitfalls</a>
</li>
</ol>
<h2>Alternative Project Structures</h2>
If you <a href="https://stackoverflow.com/questions/193161/what-is-the-best-project-structure-for-a-python-application">look around online</a> you will find alternatives to this structure, and some <a href="https://disq.us/p/n7fbt7">robust discussion</a> about pros and cons. Python does allow quite a bit of flexibility in its packaging structure, and does not have quite the same widely held standards as in, say, <a href="https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html">the Java community</a>. That being the case it is fine to have a read around and consider what works best for you.
One thing to consider however, is that there many blog posts and question responses which are rather old, and the Python packaging landscape has moved on in that time. One way to keep current is to review the GitHub pages of some of the major python projects.
<h2>Building The Package</h2>
<h3>Setup.py</h3>
The essential part of python packaging is setup.py read more about it <a href="https://docs.python.org/3.7/distutils/setupscript.html">here.</a> Note, it doesn't have to be called setup.py, but it is by convention.
The setup.py file is what defines the python package building process. In this example I have tried to keep the setup.py file simple.
```python
from setuptools import setup
from setuptools import find_packages
setup(name='my_package',
      version='0.1.0',
      description='Simple python packaging example',
      license='GPL', packages=find_packages('src'),
      package_dir={'': 'src'}  # Specifies that the 'root' directory for the build is 'src'
)
```
Once we have the basic setup.py in place we can build a source distribution with the command
```
python setup.py sdist
```
This will create a tar.gz file of the the 'src' directory. If we open the file up we can see the <a href="https://docs.python.org/3/distutils/sourcedist.html">files that are included by sdist as default</a>, along with some other metadata created.
<h3>Bundling the Tests Directory</h3>
One of the reasons for using this package structure was to keep a clearer separation of what should and should not be distributed.
By keeping 'tests' and 'src' separate and using <em>package_dir={'': 'src'} </em>in the setup.py file means that tests will not, by default, be included in the distributed package. Whether this is a good idea or not is another point of <a href="https://disq.us/p/n7fbt7">some discussion</a>, with <a href="https://stackoverflow.com/questions/32390705/should-i-include-tests-and-pyc-files-when-building-package-with-setuptools/32391295">no clear consensus</a>.
Nevertheless it is possible to include the tests directory in the distribution, but <em>not actually install them</em>, using a 'manifest' file. To use one we can simply add a 'MANIFEST.in' file into the top level project directory.
For example, to include the tests directory in what gets distributed we add the line:
```graft tests```
Now when we build the distribution the tests will also get bundled, but not in the same files that actually get installed when a user does a pip install of the package. We can use a similar technique for, say, license files or documentation.
<h2>Testing</h2>
<h3>Testing With Tox</h3>
We want to be confident our built package will work when we share it. Testing our code using the same directory structure we develop with is fine up to a point, but has the downside that its easy for the packaged/installed behaviour to be different from our local behaviour - for example if we got the import paths wrong.
One way around this is to create a new virtualenv to install the package into and then run the tests in. Rather than have to do this manually, we can use '<a href="https://tox.readthedocs.io/en/latest/">tox</a>' which will create a test virtualenv for us to use. If you are conda user, <a href="{{site.baseurl}}/2018/06/04/use-tox-with-anaconda/">read this to see how to get tox and conda to play nicely</a>.
Tox will build your package with 'python setup.py sdist' just as you would in your own environment, then check that it can be run in a separate test environment.
Once installed we can define a tox.ini file to specify how it should run. In this case we specify that we want to test with both Python 2.7 and Python 3.7, and that the tests need some additional dependencies.

```ini
[tox]
envlist = py37, py27
[testenv]
deps = pytest
commands = pytest
```
<h2>Distributing The Package</h2>
We said originally that for this example we did not need to upload our package to PyPI (if you are interested what this process involves, read <a href="{{site.baseurl}}/2015/08/05/how-to-package-python-code/">this post</a>). Instead lets look at how we can share and test our newly build package.
The build step created a 'tar.gz' file in a 'dist' folder. This is an 'artifact' we can share with our friends and colleagues. If they want to install the package they can use pip:
<pre><span class="n">pip</span> <span class="n">install</span> <span class="o">./</span><span class="n">downloads</span><span class="o">/</span><span class="n">my_package</span><span class="o">-</span><span class="mf">0.1</span><span class="o">.</span><span class="mf">0.</span><span class="n">tar</span><span class="o">.</span><span class="n">gz
</span></pre>
and the package will be available for them to import and use.
<h2>Next Steps</h2>
With more confidence in building and working with python packages,we can look for ways to continue our journey through the python packaging universe:
<ul>
<li><a href="{{site.baseurl}}/2015/08/05/how-to-package-python-code/">Publish a package to a repository such as PyPI</a></li>
<li>Handling compiled C headers, which makes our code package independent</li>
<li>Including dependencies with the distribution to make it easier to install</li>
<li>Handling package versioning</li>
<li>Adding non-code files such as documentation</li>
</ul>
