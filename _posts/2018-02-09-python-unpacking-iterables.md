---
layout: post
title: Python - Unpacking Iterables
date: 2018-02-09 15:30:49.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- arguments
- iterators
- python
- unpacking
author: deparkes
permalink: "/2018/02/09/python-unpacking-iterables/"
---
Python iterables are lists, tuples, dictionaries and other similar objects - in other words things that can be <em>iterated</em> over. Python provides a way to 'unpack' these iterables which can be a useful shortcut in some situations. This post looks at unpacking iterables, and how it can also be used to make functions functions take a variable number of arguments.
<h1>Unpacking Iterables<strong>
</strong>
</h1>
An iterator in python is an object like a list or a tuple - in other words, things you can iterate over. There are times when you you want to separate out the elements in an iterator. For example a list may contain elements that you want to fit into a print statement:

```python
x = ['one', 'two', 'three']
print("{0}, {1}, {2}".format(x[0], x[1], x[2]))
```
or there may be a function which takes certain values which you have stored in a list:

```python
def func_test(one, two, three):
    print(one)
    print(two)
    print(three)
x = ['one', 'two', 'three']
func_test(x[0], x[1], x[2])
```
Accessing the individual elements in this way works up to a point, but it can be cumbersome under some circumstances such as where you don't know how many items there are in your iterator, or there are many items and writing our x[i] many times is repetitive.

For these situations, python has a short-hand - the '*' - to unpack an iterator of any length, without needing repetition.

Taking the two examples above again, we can use the * operator to unpack the iterator. In this first example *x 'unpacks' the elements of 'x' into the argument of the format function - it is almost like the list object becomes a series of comma-separated values.

```python
x = ['one', 'two', 'three']
print("{0}, {1}, {2}".format(x[0], x[1], x[2]))
print("{0}, {1}, {2}".format(*x))
```
The effect of the * operator is similar in the function example. *x 'unpacks' the elements of the x list and places those into the argument of the func_test function.

```python
def func_test(one, two, three):
    print(one)
    print(two)
    print(three)
x = ['one', 'two', 'three']
func_test(*x)
```
<h2>Unpacking Dictionaries</h2>
It is also possible to unpack dictionaries using a similar shortcut. For dictionaries, however we use the double asterisk: '**' to unpack.

This can be useful you have a function with some known arguments you need to pass in. You can construct your argument list as a dictionary and pass that dictionary as an argument. This may be useful to you as you can then create the dictionary programmatically.

```python
def func_test(one, two, three):
    print(one)
    print(two)
    print(three)
y = {'one': 1, 'two': 2, 'three': 3}
func_test(**y)
```
