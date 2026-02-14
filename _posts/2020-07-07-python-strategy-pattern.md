---
layout: post
title: Python Strategy Pattern
date: 2020-07-07 20:45:03.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- design pattern
- pattern
- python
- strategy
author: deparkes
permalink: "/2020/07/07/python-strategy-pattern/"
---
The strategy pattern is all about being able to swap complex functionality in and out, without needing to change large amounts of code. This post summarises the strategy pattern in python. Formal, traditional <a href="https://www.toptal.com/python/python-design-patterns">design patterns</a> are not found in python as often as in other languages such as C# or Java. It can still help to know the general principles and when to look out for opportunities to use them.

Another common design pattern is the command pattern - <a href="{{site.url}}/2020/06/21/command-pattern/">read about the command pattern in python</a>.
<h2>Python Strategy Pattern</h2>
The flexibility of python as a language means that you can approach the strategy pattern in different ways. In this post I've got an example of a simpler version that uses <a href="https://dbader.org/blog/python-first-class-functions">functions</a> for the strategies, and a less simple version which uses classes for the strategies.
This simple example has two possible strategy functions and a separate function for implementing the strategies.

```python
print("Using first-class function objects")
def string_printer(strategy):
    return strategy
def print_lower(input_string):
    print(input_string.lower())
def print_upper(input_string):
    print(input_string.upper())
```

We can pass the strategy function is as an object into the 'string_printer' function. This function immediately returns the strategy object, which is then called with the "Hello, World!" argument.

```python
string_printer(print_lower)("Hello, World!")
>>> hello, world!
string_printer(print_upper)("Hello, World!")
>>> HELLO, WORLD!
```

This might seem like an odd thing to do, and introducing unnecessary complexity. The benefit comes as it means that the 'string_printer' implementer can remain the same, while the strategies can change independently or new strategies can be developed.
<h2>Less Simple Implementation</h2>
It is also possible to implement the strategy pattern in a more 'traditional' way, using classes for the strategies. This is akin to how it might be implemented in languages like <a href="https://refactoring.guru/design-patterns/strategy/java/example">Java</a> or <a href="https://refactoring.guru/design-patterns/strategy/csharp/example">C#</a>.
By using classes rather than functions we extend the options for encapsulating data and methods in a class, which may be beneficial in some cases.

```python
print("Using classic classes")
class LowerCase:
    def execute(self, input_string):
        print(input_string.lower())
class UpperCase:
    def execute(self, input_string):
        print(input_string.upper())
class FancyCase:
    def execute(self, input_string):
        for i, letter in enumerate(input_string):
            if i % 2 == 0:
                print(letter.upper(), end="")
            else:
                print(letter, end="")
                print("")
class StringPrinter:
    def __init__(self, strategy):
        self._strategy = strategy
    def execute(self, input_string):
        self._strategy.execute(input_string)
    def change_strategy(self, new_strategy):
        self._strategy = new_strategy
```

Now we can use the specific strategies as plugins for the main operation. We can extend functionality without needing to change the StringPrinter code.

```python
printer = StringPrinter(UpperCase())
printer.execute('Hello, World!')
>>> HELLO, WORLD!
printer.change_strategy(LowerCase())
printer.execute('Hello, World!')
>>> hello, world!
printer.change_strategy(FancyCase())
printer.execute('Hello, World!')
>>> HeLlO, WOrLd!
```

