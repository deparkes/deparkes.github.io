---
layout: post
title: Python Simple Logging
date: 2021-12-11 08:54:23.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- logging
- python
- simple
- software
author: deparkes
permalink: "/2021/12/11/python-simple-logging/"
---
There are lots of options for logging in python. In this post I wanted to write down one way to do python simple logging. This method should be fairly flexible across different
<a href="{{site.baseurl}}/2017/02/17/simple-python-logging/">Read more about some more simple logging in python</a>
<h2>Some General Principles</h2>
These aren't always going to be right, but you'll see these are the general principles I have used.
<ul>
<li>Use <a href="https://docs.python.org/3/library/logging.html#logging.basicConfig">basicConfig</a>
</li>
<li>Only call basicConfig once</li>
<li>Use a separate logger for each module</li>
<li>Use the same logging configuration across each logger</li>
</ul>
<h2>Python Simple Logging Example</h2>
<h3>Main script</h3>
The following it the code for the 'main' script in your application.
basicConfig is called once to configure logging including:
<ul>
<li>Specify the <a href="https://docs.python.org/3/howto/logging.html#when-to-use-logging">logging level</a>
</li>
<li>Set a reasonable <a href="https://docs.python.org/3/library/logging.html#formatter-objects">format</a>
</li>
<li>Output to a file and command line using <a href="https://docs.python.org/3/library/logging.handlers.html">handlers</a>
</li>
</ul>
This main script calls functions in modules which will be responsible for their own logging. We do not need to separately pass in a logger object or do additional configuration per module.
The logging module handles the behind the scenes details and each module, including the 'main' one can do a logging.getLogger() call.
Passing in the <strong>name</strong> variable means, along with the %(name)s format option, that the logging lines will show the name of the file that generated the logs. This can make interpreting log outputs much easier.

```python
import logging
import my_module
import my_other_module
"""Suggested minimal approach to logging in python
"""
logging.basicConfig(level=logging.DEBUG,
                    format="%(asctime)s %(name)s %(levelname)s:%(message)s",
                    handlers=[
                              logging.StreamHandler(),
                              logging.FileHandler('log.log')
                             ]
                   )
logger = logging.getLogger(__name__)
logger.debug("Debug message")
logger.info("Info message")
logger.warning("Warning message")
logger.error("Error message")
my_module.function_in_module()
my_other_module.function_in_module()
```

<h3>One Separate Module</h3>
We can now use this configured-once-only logger in a separate module.
In one module file:

```python
import logging
logger = logging.getLogger(__name__)
def function_in_module():
    logger.error("Error message in my_module")
```

<h3>Another Separate Module</h3>
The same approach applies in the other module file:

```python
import logging
logger = logging.getLogger(__name__)
def function_in_module():
    logger.info("Info log from my_other_module")
```

<h3>The resulting logs</h3>
The following shows how the log messages appear in the command line (and also in the 'log.log' file specified in the basicConfig).
The formatting is the same across each logging line, and the filename of each module is listed.

```
2021-10-20 19:30:10,659 __main__ DEBUG:Debug message
2021-10-20 19:30:10,669 __main__ INFO:Info message
2021-10-20 19:30:10,669 __main__ WARNING:Warning message
2021-10-20 19:30:10,669 __main__ ERROR:Error message
2021-10-20 19:30:10,669 my_module ERROR:Error message in my_module
2021-10-20 19:30:10,677 my_other_module INFO:Info log from my_other_module
```

<h2>Further Reading</h2>
<a href="https://realpython.com/python-logging/">https://realpython.com/python-logging/</a>
<a href="https://docs.python.org/3/library/logging.html">https://docs.python.org/3/library/logging.html</a>
