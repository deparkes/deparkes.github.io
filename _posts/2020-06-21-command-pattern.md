---
layout: post
title: Python Command Pattern
date: 2020-06-21 11:58:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- command pattern
- design patterns
- python
- software engineering
author:
  display_name: deparkes
permalink: "/2020/06/21/command-pattern/"
---
The <a href="https://en.wikipedia.org/wiki/Command_pattern">command pattern</a> bundles functionality into an object which can be passed around. This way the object can be executed when needed as a well defined command. In a sense a '<a href="https://en.wikipedia.org/wiki/Macro_(computer_science)">macro</a>' is an implementation of the command pattern: it abstracts more complex functionality into a single command or series of commands. This post shows a couple of ways to implement the command pattern in python.
<h2>Python Command Pattern</h2>
There is a good description of a python command pattern implementation at the <a href="https://refactoring.guru/design-patterns/command/python/example">refactoring Guru site</a>.
As with other software design patterns, when it comes to implementing patterns in Python it pays to <a href="https://www.youtube.com/watch?v=G5OeYHCJuv0">be a bit wary</a>:  since in many cases the classic design patterns have already been absorbed into the language such that they are not needed.
I find it useful to remember that the goals of the command pattern can be achieved with python without necessarily needing to implement a 'full' pattern. At the same it is valuable to know how to do the full implementation as it can provide more flexibility.
<h3>Classic Pattern</h3>
The Refactoring Guru site suggests a <a href="https://refactoring.guru/design-patterns/command/python/example">classic implementation of the command pattern</a>, similar to what would be used in a language like Java. We create a 'Command' class which can contain a 'do' method for executing the command, as well as an 'undo' method for reversing the command execution.
In my example below, I am have already simplified things over the classic example as there is no necessity in python to define an interface or abstract base class (although <a href="https://www.python-course.eu/python3_abstract_classes.php">you can if you would like to</a>). The 'ExampleCommand' class does not need to inherit from a base 'Command' class.

```python
class ExampleCommand:
    def __init__(self, payload):
        self._payload = payload
    def do(self):
        print("Doing operation on payload: " + self._payload)
    def undo(self):
        print("Undoing operation on payload: " + self._payload)
command = ExampleCommand("Example payload")
command.do()
command.undo()
```

<h3>A More Pythonic Command Pattern</h3>
A simple way to implement the command pattern in python is to just use a function.  We can do this because functions are '<a href="https://www.geeksforgeeks.org/first-class-functions-python/">first class objects</a>' in python. See more about this in <a href="https://codereview.stackexchange.com/questions/51003/implementing-command-pattern-in-python">this stackoverflow response</a>.

```python
def simple_command():
    print("Doing something")
simple_command()
def simple_undo_command():
    print("Undo something")
simple_undo_command()
```

This function-based implementation is limited compared to the 'classic' implementation of the command pattern as we cannot provide a payload for the function, since we need to keep the function objects.
We can pass the commands around as objects to be invoked when we need them. If we need to also provide a payload for the function at runtime, we can do that with separate class (similar to the 'classic' pattern) or
We can take this further by returning a function.

```python
# Example with functions with payloads
payload = 'example payload'
def payload_command(payload):
    def command():
        print("Doing command with payload within function: " + payload)
    # Returning the command function means that we can 'execute' when we need at run time
    return command
command = payload_command(payload) # The command ready to execute
command() # Executing the command
```

It's less clear how we can use this pythonic way to easily couple the 'do' and the 'undo' commands.
We could of course just have a do_function(payload) and an undo_function(payload), but it may be good to keep the functions together in a single command object, more like the 'classic' version.
