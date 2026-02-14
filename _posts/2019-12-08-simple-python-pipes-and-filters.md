---
layout: post
title: Simple Python Pipes and Filters
date: 2019-12-08 16:46:42.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- architecture
- message
- messaging
- pipes and filters
- python
author: deparkes
permalink: "/2019/12/08/simple-python-pipes-and-filters/"
---
Inspired by the <a href="https://www.enterpriseintegrationpatterns.com/index.html">Enterprise Integration</a> pattern of '<a href="https://www.enterpriseintegrationpatterns.com/patterns/messaging/PipesAndFilters.html">pipes and filters</a>' I wanted to make a simple python pipes and filters example. With some digging I found this <a href="https://github.com/lumannnn/pypifi">GitHub repository</a>, which does an excellent job breaking down the message-based approach to Object Oriented Programming described in a series of blog posts: <a href="https://eventuallyconsistent.net/2013/08/12/messaging-as-a-programming-model-part-1/">1</a>, <a href="https://eventuallyconsistent.net/2013/08/14/messaging-as-a-programming-model-part-2/">2</a>, <a href="https://eventuallyconsistent.net/2013/08/19/messaging-as-a-programming-model-revisited/">3</a>.
To explore the idea of 'pipes and filters' I wanted to work through an even more simple python pipes and filters implementation. The implementation described here is probably over-simplified and doubtless has issues and limitations. I hope though it can be a useful tool for understanding, and perhaps even usable in some simple projects.
<h2>Simple Python Pipes and Filters</h2>
In overview, we'll set up a 'Pipeline' class which holds a list of filters, and a method for executing the pipeline against a message provided.

| ![Simple python pipes and filters - the filters mutate the dictionary message]({{site.url}}/assets/2019/12/pipes-and-filters-schematic-1.png) |
|:--:|
| *Simple python pipes and filters - the filters mutate the dictionary message* |

Executing the pipeline applies each of the filters to the message.

```python
class Pipeline:
    def __init__(self):
        self.filters = list()
    def add(self, filter):
        self.filters.extend(filter)
    def execute(self, message):
        print("Executing pipeline...")
        for message_filter in self.filters:
            message_filter(message)
def double_data(message):
    message['data'] = [x*2 for x in message['data']]
def update_header(message):
    message['header'] = 'this is the updated message'
pipeline = Pipeline()
pipeline.add([double_data,
              update_header]) # note we are adding the function object, not making a function call
message = {'header': 'this is the original message',
           'data': [1,2,3]}
for key, value in message.items():
    print(key + ' : ' + str(value))
```

Which prints the following output:

```
header : this is the original message
data : [1, 2, 3]
Executing pipeline...
header : this is the updated message
data : [2, 4, 6]
```

<h3>The Messages</h3>
The message itself is represented by a dictionary. Dictionaries are <a href="https://stackoverflow.com/questions/15078519/python-dictionary-passed-as-an-input-to-a-function-acts-like-a-global-in-that-fu">mutable</a> and each of the filters is actually modifying the original message dictionary. In a sense this violates one of the common principles of working with messages: that they should be immutable.
We could think of the messages in this case as '<a href="https://www.enterpriseintegrationpatterns.com/patterns/messaging/DocumentMessage.html">document messages</a>', which are permitted to be mutable. It also conceptually seems a bit odd that the message is not passed through the pipeline, so much as stays in the same place while a series of filters act on it.
In an attempt to reduce the number of concepts needed to understand this example, I have decided to stick with dictionaries as the message, and not attempt to address this in the filter/pipeline. See the section 'taking things further' for more discussion about some possible ways of handling immutability as well as some other topics.
<h3>The Filters</h3>
In this example filters are defined by functions. Each function takes a message as an argument and mutates the data in the message. Since the messages are mutable dictionaries there is no need to return the message itself in this implementation.
For more sophisticated filters, you may want to define the filters as classes rather than functions. See the 'Taking Things Further' for more about this.
<h3>The Pipeline</h3>
The pipeline itself is defined as an object with methods:
<ul>
<li>add - adds a filter to the pipeline. In our implementation this is a <a href="https://medium.com/python-pandemonium/function-as-objects-in-python-d5215e6d1b0d">function object</a>, where each function expects to be passed in a message dictionary as its single argument. The method has been implemented so a list of function objects can easily be added, rather than having to 'add' a filter one at a time.</li>
<li>execute - executes the pipeline against a target message. This is achieved by passing the input message as an argument to each of the functions provided in the 'add' method.</li>
</ul>
As mentioned elsewhere in this post, the use of a dictionary as the input message means that the effect of running the pipeline is to modify the message in place. The modified message can be read or used further once the pipeline has run.
<h2>Taking Things Further</h2>
This simple python pipes and filters example has deliberately taken a bare-bones approach, and there are several areas that could be refined or extended. Below are some examples:
<ul>
<li>
<strong>Immutability</strong> - this simple python pipes and filters relies on the mutability of dictionaries to allow the pipeline to do something. An alternative would be to enforce some degree of mutability in the message. This could be achieved by using <a href="https://realpython.com/python-data-classes/">Data Classes</a> or <a href="https://docs.python.org/3/library/collections.html#collections.namedtuple">Named Tuples</a> (which are both immutable types), or by changing how the filters are expected to work: modifying and returning a '<a href="https://www.geeksforgeeks.org/copy-python-deep-copy-shallow-copy/">deep copy</a>' of the input dictionary.</li>
<li>Define <strong>filters as classes</strong> rather than simple functions. Defining the filters as classes means that they can be more easily instantiated with other data or configuration information. For example you could have a filter which communicates with a database and needs connection details; or a filter which does processing by comparison against some reference data.</li>
<li>Adding <strong>more pipes</strong> - this example only has a single pipe, so it would be interesting to extend the functionality to chain pipes together. A pipe (a collection of filters) can itself be treated as a filter in a separate pipe, which helps make the pipes and filters pattern powerful and flexible.</li>
<li>Separating into <strong>multiple files</strong>. In this example the filters have been defined in the same file as the pipeline and the actual usage of the pipeline. An alternative would be to separate out the filters into a separate 'filters library', and the pipeline into its own pipeline definition file. This could be done whether the filters are functions or separate classes.</li>
<li>
<strong>Using generators</strong> - it is possible to implement pipes and filters using generators, which you may wish to explore. There is an example of this <a href="https://tech.stylight.com/pipes-and-filters-architectures-with-python-generators/">here</a>.</li>
</ul>
