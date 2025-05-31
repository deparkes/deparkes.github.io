---
layout: post
title: Immutable Objects In Python
date: 2020-01-25 10:44:57.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- data types
- immutability
- python
- tuple
author:
  display_name: deparkes
permalink: "/2020/01/25/immutable-objects/"
---
Immutable objects are useful for making sure the data they contain cannot be changed after they are created. Immutable objects can be useful for <a href="{{site.baseurl}}/2019/12/08/simple-python-pipes-and-filters/">passing messages</a> between components, and when working with <a href="https://en.wikipedia.org/wiki/Thread_safety">multiple threads</a>. Immutable objects can also be easier to work with and reason about, because once they are created they cannot be changed. This post describes some of the immutable objects available in python.
<h2>Immutable Objects In Python</h2>
The important thing about <a href="https://en.wikipedia.org/wiki/Immutable_object">immutable objects</a> is that once they have been instantiated, they cannot be modified (or 'mutated', hence the name).
In python, immutability can be <a href="https://realpython.com/courses/immutability-python/">slightly tricky</a> because it does not make a clear distinction between private and public attributes or methods in an object, making 'protecting' against mutation a challenge. There are thankfully some built in data types that you can use for immutability:
<ul>
<li>Tuples</li>
<li>Named tuples</li>
<li>Data Classes</li>
</ul>
<h2>Tuples</h2>
The simplest of the immutable objects in this list. <strong>Tuples</strong> are probably the most well known and widely used immutable data type available in python. Tuples are often used in a similar way to a list, that is as a series of elements, but they can also be used as a single value.
<a href="https://www.geeksforgeeks.org/tuples-in-python/">Read more about tuples</a>.
<h3>Example:</h3>

```python
message = ('Message header', 'Message data')
print(message)
print('Header: ', message[0])
print('Content: ', message[1])
```

which outputs:

```
('Message header', 'Message data')
Header:  Message header
Content:  Message data
```

If we try to modify one of the values in the tuple we get this error

```
Traceback (most recent call last):
  File "immutable_types.py", line 8, in &lt;module&gt;
    message[1] = 'New data'
TypeError: 'tuple' object does not support item assignment
```

<h2>Named Tuples</h2>
A big drawback to using a tuple is that values stored in the tuple can only be accessed by position, rather than a key or label. An extension to the concept of a 'tuple', <strong>named tuples</strong> help get around the restriction that data in tuples can only be accessed by position, rather than by a key.
<a href="https://pymotw.com/3/collections/namedtuple.html">Read more about named tuples</a>.
<h3>Example:</h3>

```python
import collections
Message = collections.namedtuple('Message', 'header content')
message = Message(header='Message header', content='Message data')
print(message)
print('Header: ', message.header)
print('Content: ', message.content)
```

which outputs:

```
Whole object:
Message(header='Message header', content='Message data')
Header:  Message header
Content:  Message data
```

If we try to change one of the values in the named tuple, we get an error:

```
Traceback (most recent call last):
  File "immutable_types.py", line 20, in &lt;module&gt;
    message.content = 'New data'
AttributeError: can't set attribute
```

<h2>Data Classes</h2>
Data classes were introduced in <a href="https://www.python.org/dev/peps/pep-0557/">python 3.7</a> as a shortcut for making 'data objects' - i.e. objects designed to hold data only, and no methods. To make a <strong>data class</strong> (<a href="https://www.python.org/dev/peps/pep-0557/#frozen-instances">almost</a>) immutable it can be passed the argument '<em>frozen=True</em>' when it is created.
<a href="https://realpython.com/python-data-classes/">Read more about data classes</a>.
<h3>Example:</h3>

```python
from dataclasses import dataclass
@dataclass(frozen=True)
class Message:
    header: str
    content: str
message = Message('Message header', 'Message data')
print(message)
print('Header: ', message.header)
print('Content: ', message.content)
```

Which gives the output

```
Message(header='Message header', content='Message data')
Header:  Message header
Content:  Message data
```

Because we used the 'frozen=True' argument to the dataclass decorator, if we try to change on of the values in the data object, we get an error:

```
Traceback (most recent call last):
  File "immutable_types.py", line 35, in &lt;module&gt;
    message.header = 'New message header'
  File "&lt;string&gt;", line 3, in __setattr__
dataclasses.FrozenInstanceError: cannot assign to field 'header'
```

