---
layout: post
title: Python Plugin Architecture
date: 2022-07-24 16:34:45.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- architecture
- code
- importlib
- patterns
- plugins
- python
- software design
- software engineering
author:
  display_name: deparkes
permalink: "/2022/07/24/python-plugin-architecture/"
---
A plugin architecture is a way of achieving flexiblity, encapsulation, extensibility as well as other principles of good software design. This post shows how you can achieve a python plugin architecture using the <a href="https://www.blog.pythonlibrary.org/2016/05/27/python-201-an-intro-to-importlib/">importlib</a> library.
There are some similarities with other concepts such as <a href="https://deparkes.co.uk/2019/12/08/simple-python-pipes-and-filters/">pipes and filters</a>.
<h2>'Project' Plugins vs 'External' Plugins</h2>
In this post I'm considering two situations:
<ol>
<li>'Project' Plugins - Plugins are held within the project folder hierarchy, and used by the developer to isolate and encapsulate functionality</li>
<li>'External' Plugins - Plugins are available at an arbitrary location in the file system. This approach potentially allows users to provide plugins in, say, their own home folder rather than needing access to the main code location.</li>
</ol>
<h3>'Project' Plugins</h3>
This approach is probably the easiest as python comes with functionality to help.
In this case I've made a simple project structured like this:

```
main.py
project_plugins/project_plugin.py
```

The 'plugin' file just contains some example functionality that we want to keep separate from the main code.

```python
# project_plugins/project_plugin.py
print('importing...')
def run():
    print("I'm " + __name__)
```

The 'main.py' script uses importlib to load that module at run time, and then execute the 'run' function it contains.

```python
# main.py
import importlib
plugin = importlib.import_module('project_plugins.project_plugin')
plugin.run()
```

And the resulting output is:

```python
importing...
I'm project_plugins.project_plugin
```


<h3>'External' Plugins</h3>
Allowing plugins to exist in an arbitrary location and not necessarily within the project hierarchy is more difficult. We still use the importlib library, but need to utilise some lower-level functionality to achieve what we want.
For this example we also have a 'plugins' folder outside the project hierarchy:

```
project/
   main.py
plugins/
   external_plugin.py
```

The 'external_plugin.py' file in the 'plugins' folder contains the following code:

```python
print('Importing...')
def run():
    print("I'm " + __name__)
```

The file 'main.py' contains the following code to load the plugin code at runtime and execute the 'run' function it contains.
The 'spec' says where to find the module code and how it should be loaded.
The <code>exec_module(plugin)</code> code is needed to actually run the code associated with the 'plugin' module object, which makes the run function available.

```python
from importlib import util
import os
plugin_directory = os.path.abspath('plugins')
plugin_name = 'external_plugin'
spec = util.spec_from_file_location(plugin_name, os.path.join(plugin_directory, plugin_name+'.py'))
plugin = util.module_from_spec(spec)
spec.loader.exec_module(plugin)
plugin.run()
```

The resulting output in this case is

```
Importing...
I'm external_plugin
```
