---
layout: post
title: Elements of Software Testing
date: 2020-07-09 17:37:26.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- software
tags:
- development
- qa
- software engineering
- testing
author:
  display_name: deparkes
permalink: "/2020/07/09/elements-of-software-testing/"
---
Software testing is an important part of software development, this post has a few points to consider when developing tests for your own software.
<a href="https://www.guru99.com/software-testing-career-complete-guide.html">Read more about the profession of software testing
</a>
<h3>Existent</h3>
I wanted to put this one first. Before worrying about getting the testing automated, or comprehensive or whatever, the most important thing is just to have some level of testing. Tests will give you more confidence to build and enhance your software and that you can safely make releases.
<h3>Easy To Run</h3>
I've included 'automation' on this list, but I wanted to emphasise that automation is not the be all and end all. Having tests that are easy to run will mean that they actually are run. 'Easy' is a spectrum - try to find ways to make it easier to run your existing tests. This could involve some automation, but just adding some better documentation could help too.
<h3>Not Just the Happy Path</h3>
It is tempting to use testing to demonstrate that something works, without testing to see what happens in less than ideal conditions. This is sometimes referred to as testing the 'happy path'. Try to think of ways to break your software. When writing tests you may want to consider including cases for:
<ul>
<li>Valid data with correct outcome - the '<a href="https://en.wikipedia.org/wiki/Happy_path">happy path</a>'</li>
<li>Exceptions and errrors</li>
<li>Naughty data - such as the <a href="https://github.com/minimaxir/big-list-of-naughty-strings">big list of naughty strings</a>
</li>
<li>Extremely large or small values</li>
</ul>
Projects such as the can help you with breaking your software.
<h3>Automated</h3>
Automating your tests will make it much easier to run them at all and to run them regularly. Tests are only valuable if they are run.
<h3>Independent</h3>
Keeping tests independent will make it much easier to find out what is going on when there are problems or errors. If a test behaves differently depending on which tests ran before it, it is not independent. This is related to the point on 'isolation'
<h3>Isolated</h3>
You should try as far as possible to isolate your tests and testing environment from external factors. At the level of individual unit tests this is relatively easy, where you can provide data or mocks for individual units. You may find you need to work harder to keep the whole process isolated from external dependencies.
This can be challenging for integration tests, or data-tests which require the use of a database. Isolation (and independence) can break down if there is assumed access to a particular test database or schema. Improving independence and isolation are ways that tests can be made easier to run.
<h3>Quick</h3>
The longer tests run, the less likely it is that they will actually be run. As a rule of thumb you don't want your unit tests to take more than a few seconds to run, and ideally integration tests would run in more like a few minutes.

Reality often gets in the way of theory and it is not unheard of for integration test suites to take hours or even over night to complete.
One way to keep test run times down is to <a href="https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html">resist the temptation to add more and more 'end to end' tests</a> and instead focus on quick-running, well isolated unit tests.
<h3>End to End</h3>
You should aim to test your software from start to finish. Try to avoid just testing individual components on their own (although you should do that too). It is all to easy to have a broken system made up of 'perfectly working' sub-systems and components.

Testing in an end to end fashion like this helps flush out any issues with integration between components. That said, you should <a href="https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html">resist the temptation to add more and more 'end to end' tests</a>, as they will slow down your testing to the point that tests will not be run as often.
<h3>Reproducible</h3>
It should be possible for you to run your tests today and then in a week or a month and be confident that you will get the same results. This will be made much easier if you have suitably isolated your code and environment for testing.

For example if you software relies on external data or services, you should try to isolate your software from these. This also means nailing down any random seeds or implied randomness such as sort-orders etc.
<h2>Further Reading</h2>
<a href="https://madeintandem.com/blog/five-factor-testing/" target="_blank" rel="noopener">Five Factor Testing</a>
