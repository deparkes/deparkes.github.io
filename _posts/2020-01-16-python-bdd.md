---
layout: post
title: Python BDD
date: 2020-01-16 20:46:19.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- bdd
- behaviour-driven development
- python
- software engineering
- testing
author: deparkes
permalink: "/2020/01/16/python-bdd/"
---
Behaviour Driven Development, or <a href="https://en.wikipedia.org/wiki/Behavior-driven_development">BDD</a>, is a valuable collaboration technique for bridging the gap between developers and wider stakeholders. One part of BDD is the tools or frameworks that can be used to convert BDD statements into actual running tests. This post goes through a simple example using the pytest-bdd plugin.
<h1>Python BDD with pytest-bdd</h1>
There are different ways of implementing BDD in python and I have chosen to focus on <a href="https://github.com/pytest-dev/pytest-bdd">pytest-bdd</a>, a plugin for the popular <a href="https://docs.pytest.org/en/latest/">pytest</a> test framework.

For a more comprehensive run-down of different Python BDD frameworks you could use I suggest reading this <a href="https://automationpanda.com/2019/04/02/python-bdd-framework-comparison/">excellent blog post</a>.

For these examples I am going to use a simple example of a python 'Greeter' class which says hello. This example is <a href="https://github.com/deparkes/pytest-bdd-example">available on GitHub</a> if you just want to get stuck in.
<h2>The Gherkin Language</h2>
A big part of BDD is using the <a href="https://automationpanda.com/2017/01/26/bdd-101-the-gherkin-language/">Gherkin language</a> as a way of specifying expected behaviour in plain language. Here's an example.

```gherkin
Feature: Greeter
   As a user
   I want to be greeted nicely
   So that I feel welcomed.
Scenario: No name provided
  Given a Greeter
  When I don't provide a name
  Then the greeter says "Please provide a name"
```

Let's break this example down. The first line specifies the name of the feature being described, below which is a 'user story' style declaration of what the user expects of the feature.

The scenario is one aspect of this feature that we want to specify. In this case we want to specify what should happen when a name isn't provided.
At this stage we deliberately haven't said anything about any implementation details.

The 'given', 'when', 'then' language corresponds to the concepts of 'set up' -&gt; 'run code' -&gt; 'assert outcome'. This linguistic link between the world of the developer and customer or stakeholder is a key part of what makes BDD useful.
<h2>Linking Gherkin With Python</h2>
I am using the pytest-bdd framework (it's a plugin to pytest). By convention feature files are stored in a 'features' directory. The feature files contain the Gherkin that specify the expected behaviour.

To actually run the Gherkin as python tests we need to create some 'step definitions'. By convention these step definitions are created in a folder named 'step_defs'.
pytest-bdd is a pytest plugin, and we 'drive' it by having it pick up test scripts in the same way that pytest does.

```
src/
  L package_name
      L package.py
tests/
  L features
    L feature_file.feature
  L step_defs
    L test_feature.py
```

There are a few things we need to make sure our 'step_def' file has before we can get to actually implementing the tests.
Firstly the imports. Secondly, we need to specify where pytest-bdd can find the corresponding feature file for this step_def file.

```python
from pytest_bdd import given, when, then, scenarios
scenarios('../features)
```

With these pre-requisites in place we can actually implement the tests. The link to the 'given', 'when', 'then' in the feature file is achieved with decorators.
<h2>Running The Tests</h2>
Using pytest-bdd means that we can run the tests by running pytest as usual and our 'BDD' style tests should be run.
