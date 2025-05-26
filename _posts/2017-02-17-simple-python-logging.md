---
layout: post
title: Learn About Simple Python Logging
date: 2017-02-17 16:00:42.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- logging
- python
author:
  display_name: deparkes
permalink: "/2017/02/17/simple-python-logging/"
---
Logging can offer much <a href="http://stackoverflow.com/questions/6918493/in-python-why-use-logging-instead-of-print">more flexibility</a> than simply printing a message to the console but it can be difficult to know where to start. This post looks a some examples of simple python logging to get you started.
<h1>Why 'log' instead of 'print'?</h1>
<a href="https://en.wikipedia.org/wiki/%22Hello,_World!%22_program">Printing to the console</a> is usually one of the first things you learn with any language. It's easy to use '<a href="https://docs.python.org/3/library/functions.html#print">print()</a>' to give messages to your users, display debugging for you, and output error messages and warnings.
But it's also easy to get in a muddle with commenting and uncommenting print statements when you are trying to debug.
Instead of using print <a href="https://www.loggly.com/blog/4-reasons-a-python-logging-library-is-much-better-than-putting-print-statements-everywhere/">we can use logging</a> which allows us to:
<ul>
<li>specify different <a href="https://docs.python.org/3/library/logging.html#levels">levels </a>of message,</li>
<li>control when messages are logged</li>
<li>direct outputs to <a href="http://stackoverflow.com/questions/6386698/using-the-logging-python-class-to-write-to-a-file">files</a>, screen, and <a href="https://docs.python.org/3/library/logging.handlers.html">elsewhere</a>
</li>
</ul>
The standard module for logging in python is called '<a href="https://docs.python.org/3/library/logging.html">logging</a>'. Below are some simple examples of <a href="https://pymotw.com/2/logging/">how you could use logging</a> if you haven't used it before.
<a href="https://fangpenlin.com/posts/2012/08/26/good-logging-practice-in-python/">Read more about good logging practice in python </a>
<h1><b>Simple logging in python</b></h1>
<h2><b>A Simple Example</b></h2>
Logging can be very simple. This example shows how by just importing the logging module and setting the logging level you can do everything that you were previously doing with print, but with greater flexibility.

```python
import logging
# Set the logging level to log all messages 'debug' and higher
logging.basicConfig(level=logging.DEBUG)
# Write log messages at different levels
logging.debug("write this to the log - debug")
logging.info("write this to the log - info")
logging.error("write this to the log - error")
logging.warning("write this to the log - warning")
logging.critical("write this to the log - critical")
```

Which will print the following output:

```
DEBUG:root:save this to the log - debug
INFO:root:save this to the log - info
ERROR:root:save this to the log - error
WARNING:root:save this to the log - warning
CRITICAL:root:save this to the log - critical
```

For normal use, you will probably want the <a href="https://docs.python.org/3/library/logging.html#levels">logging level</a> set to 'info' or perhaps 'warning', and go to 'debug' when you want see debugging messages.
Now, rather than <a href="https://www.loggly.com/blog/4-reasons-a-python-logging-library-is-much-better-than-putting-print-statements-everywhere/">commenting and uncommenting</a> print statements, we can just use different levels of logging.
<h2>Logging Levels</h2>
When you send messages to the logger, you specify their level. This esssentially means that you can filter out messages depending on their logging level. For example it's unlikely that you would want to print out the results of each iteration of a loop during normal use, but this can be very useful for debugging.
<table>
<tbody>
<tr>
<td width="20%"><strong>Logging Level
</strong></td>
<td><strong>Use it for</strong></td>
</tr>
<tr>
<td>Debug</td>
<td>Instead of having a print statement that you comment out, you use the debugging logging level. Examples might include showing the index and values in a loop, or checking that a variable stores the value you expect.</td>
</tr>
<tr>
<td>Info</td>
<td>You can use this logging level for things like printing messages to the user, returning results of functions that the user will want to see (i.e. not debugging info).</td>
</tr>
<tr>
<td>Warning</td>
<td>You could I suppose just use 'info' for this. For important messages that the user may want to intervene on - e.g. incorrect login info, loading large files and so on</td>
</tr>
<tr>
<td>Error</td>
<td>Use this when something goes wrong - can also be combined with <a href="https://docs.python.org/3/library/logging.html#logging.Logger.exception">exception handling</a>.</td>
</tr>
<tr>
<td>Critical</td>
<td>There probably aren't all that many situations that warrant a 'critical' message over an 'error' message. This option is here nevertheless.</td>
</tr>
</tbody>
</table>
<h2><b>Output to file rather than the console</b></h2>
Often it is more useful to output the log to a separate log file, rather than to the console. This example will create a log file 'example.log', and save to it the same logging outputs as before.

```python
import logging
LOG_FILENAME = 'example.log'
logging.basicConfig(filename=LOG_FILENAME,level=logging.DEBUG)
logging.debug("write this message to log file - debug")
```

Note: this will stop logging information being directed to the console. See below for how to have output to both the console and a file.
<h2><b>Adding a timestamp to the output</b></h2>
The basic logging does not include any date or timestamp of when the log was made. To add a timestamp was can set the formatting to the logging basicConfig:

```python
import logging
format_string = '%(levelname)s: %(asctime)s: %(message)s'
logging.basicConfig(level=logging.DEBUG, filename="example.log", format=format_string)
logging.debug("write this to the log - debug")
```

Which will output the log message with the log level, the date and time, along with our message.

```
DEBUG: 2017-02-14 20:38:01,457   write this to the log - debug
```

<h2><b>Output to a file and the console</b></h2>
In the simple examples above we have had to chose between either output to the console, or output to a file. It is also possible to output to both the console and to a file. We'll need to do a little be more set up for this, however.
The first difference is that we will create an instance of logging (called 'logger' in this case). Creating our logger object will give us the flexibility we need to set outputs for console and log files.

```python
import logging
logging_format = '%(levelname)s: %(asctime)s: %(message)s'
logging.basicConfig(level=logging.DEBUG, format=logging_format)
logger = logging.getLogger()
# create a file handler
handler = logging.FileHandler('console_and_file.log')
# create a logging format
formatter = logging.Formatter(logging_format)
handler.setFormatter(formatter)
# add the handlers to the logger
logger.addHandler(handler)
logger.info("save this to the log")
```

<h1><b>Customise the logger further</b></h1>
<h2>Change the logging level</h2>
It's quite common to want to be able to output a different level of detail to the console and the log file. It might be that we want all messages to go to the log file, but only the most important (say warning and above) to be directed to the screen. We may also want the log file to be timestamped, but the console output to not take a timestamp. We can do that by modifying the above example.

```python
import logging
#set different formats for logging output
console_logging_format = '%(levelname)s: %(message)s'
file_logging_format = '%(levelname)s: %(asctime)s: %(message)s'
# configure logger
logging.basicConfig(level=logging.DEBUG, format=console_logging_format)
logger = logging.getLogger()
# create a file handler for output file
handler = logging.FileHandler('console_and_file.log')
# set the logging level for log file
handler.setLevel(logging.INFO)
# create a logging format
formatter = logging.Formatter(file_logging_format)
handler.setFormatter(formatter)
# add the handlers to the logger
logger.addHandler(handler)
# output logging messages
logger.info("save this to the log - info logger")
logger.debug("save this to the log - debug logger")
logger.error("save this to the log - error - logger")
logger.warning("save this to the log - warning - logger")
logger.critical("save this to the log - critical - logger")
```

The file output is now:

```
INFO: 2017-02-12 15:10:52,325: save this to the log - info logger
ERROR: 2017-02-12 15:10:52,328: save this to the log - error - logger
WARNING: 2017-02-12 15:10:52,329: save this to the log - warning - logger
CRITICAL: 2017-02-12 15:10:52,330: save this to the log - critical - logger
```

Which has a timestamp, but is not capturing the debug and info level messages.
The console output on the other hand is:

```
INFO: save this to the log - info logger
DEBUG: save this to the log - debug logger
ERROR: save this to the log - error - logger
WARNING: save this to the log - warning - logger
CRITICAL: save this to the log - critical - logge
```

Which keeps the debug level info, but does not have a timestamp.
