---
layout: post
title: Python Variable Function Arguments
date: 2019-10-20 15:52:17.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- function
- iterable
- python
- software engineering
author: deparkes
permalink: "/2019/10/20/python-variable-function-arguments/"
---
Python variable function arguments are typically represented by the somewhat arcane-looking '*args' and '**kwargs' arguments in a function signature. Using python variable function arguments frees you from having to know in advance exactly how many arguments a function or method will take, which can be very useful.
<h2>Variable Function Arguments</h2>
There are two ways we can pass arguments to a function or method
<ul>
<li>Key word arguments ('kwargs') - we specify a key word to identify the variable to associate with the argument value. We can use a dictionary to represent key word arguments.</li>
<li>Positional arguments ('args') - we rely on the position of the argument in all provided arguments to identify which argument it is. We can use lists, tuples and sets to represent positional arguments.</li>
</ul>
Python variable function arguements make use of the concept of <a href="{{site.url}}/2018/02/09/python-unpacking-iterables/">packing and unpacking an iterable</a>.
The function definition can specify that the function expects an 'unpacked' iterable to be provided. The function also specifies the name of the variable that the corresponding packed iterables should be assigned to.
Let's see some examples.
<h3>Keyword Arguments</h3>
A dictionary contains key-value pairs which can be used to represent key word arguments. We define a function and say that we expect to be provided a series of key-value pairs, which will be packed into a dictionary.
By convention this dictionary is named 'kwargs'. We can access the dictionary name 'kwargs' just like any other argument.
```python
def func_kwargs(**kwargs):
    for i,j in kwargs.items():
        print(i,j)
```
When we use the function we can put in as many key-value pairs as we like:
For example
```
$ func_kwargs(one=1, two=2)
one 1
two 2
```
And
```
>>> func_kwargs(one=1, two=2, three=3)
one 1
two 2
three 3
```
If we try to provide an argument without its corresponding key word we'll get an error.
```
$ func_kwargs(one=1, two=2, 3)
  File "<stdin>", line 1
SyntaxError: positional argument follows keyword argument
$ func_kwargs(1, two=2, three=3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: func_kwargs() takes 0 positional arguments but 1 was given
```
<h3>Positional Arguments</h3>
For positional arguments our function definition expects a list-like object to be provided.
First let's look at
```python
def func_args(*args):
    for i in args:
        print(i)
```
When we use the function we can provide as many arguments as we like
```
$ func_args(1, '2', 'three')
1
2
three
```
But if we try to add a key word argument we'll get an error:
```
$ func_args(1, x='2')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: func_args() got an unexpected keyword argument 'x'
```
<h3>Args and Kwargs</h3>
Unless we provide both 'args' and 'kwargs' in the function definition, we are limited to <em>only </em>providing key word arguments or <em>only</em> providing positional arguments. It is for this reason that the 'args, kwargs' pattern is seen so frequently.
```python
def func_args_kwargs(*args, **kwargs):
    for i,j in kwargs.items():
        print(i,j)
    for i in args:
        print(i)
```
We can use this function with a mixture of positional and key word arguments.
```
$ func_args_kwargs(1, two=2)
two 2
1
```

<h3>Compulsory and Optional Arguments</h3>
For completeness, it is also worth noting that, the concepts of 'args' and 'kwargs' allow you to have variable function arguments, but you can also combine conventional, required arguments with optional arguments.
```python
def func_required_and_optional(required_argument, *args):
    print("This argument is required: ", required_argument)
    for i in args:
        print("This argument is optional: ", i)
```
```
$ func_required_and_optional('Required', 'Optional')
This argument is required:  Required
This argument is optional:  Optional
```
