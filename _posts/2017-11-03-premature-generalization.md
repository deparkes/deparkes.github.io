---
layout: post
title: Premature Generalization
date: 2017-11-03 15:00:31.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- coding
- design
- design patterns
- generalization
- programming
- software design
author:
  display_name: deparkes
permalink: "/2017/11/03/premature-generalization/"
---
Premature generalization can happen when we incorrectly widen the scope of a problem, or try to anticipate use cases before they happen. It often comes about when we attempt to make a multi-purpose, or re-usable solutions before fully understanding what is really needed.
<a href="https://wiki.c2.com/?PrematureGeneralization">Premature generalization</a> is a trap we can fall into just about anywhere we are trying to solve problems: construction work, product design, and carpentry. Here I am mainly interested in how premature generalization can be a problem in programming and writing software.
<h1><b>Why Do We Generalize?</b></h1>
There are plenty of good reasons to generalize when designing and writing software - we often know that we have a number of similar cases to deal with so that it makes sense to build a framework or abstraction to help us.
At a high level, generalization can involve attempting to make solution that is not just specific to one exact problem, but that is extensible to more general problems. At a lower level, generalization may involve drawing together common features or classes into a library as<a href="https://wiki.c2.com/?BestPractice"> good practice</a> in software design often involves <a href="https://wiki.c2.com/?OnceAndOnlyOncE">avoiding duplication</a> and <a href="https://wiki.c2.com/?CouplingAndCohesion">reducing coupling</a> of code.
Sometimes, however, our reasons for generalizing are not so sensible:
<ul>
<li>we just want to make something cool or try out a new <a href="https://amzn.to/2gFltxt">design pattern</a>. It feels much more fun to be working on a project that can process any file type under the sun, rather than the two file types you know it will actually need to deal with.</li>
<li>Our enthusiasm gets the better of us - we have a great idea for our program and can see the potential applications beyond the immediate problem we are working on.</li>
<li>Our inexperience means we want to try out everything we can in our project - using every tool for the job rather than the right tool.</li>
</ul>
What ever the reason for generalization, doing it too soon can be problematic.
<h1><b>Premature Generalization Is Bad</b></h1>
Premature generalization <a href="https://solitum.net/premature-generalization/">often happens</a> because we are unfamiliar with the problem we are working on, or we over-estimate our ability to find a solution. Scott Wiersdorf has written that it's when working under these conditions that any solution he comes up with "is suboptimal in the best case and flat-out wrong in the common case".
Premature generalization is not necessarily the <a href="https://ryanfarley.com/blog/archive/2004/04/30/570.aspx">root of all evil</a>, and you will likely produce a working solution irrespective of when you generalize. The problem is that your code is likely to be more difficult to develop, and maintain than it needed to be. Once you have started down the path of a wide-spread, generalized solution, it can be difficult to change direction.
<h1><b>How to Avoid Premature Generalization</b></h1>
Knowing when it is appropriate to generalize can be difficult, but there are some principles you can try to keep in mind.
<h2><b>The Rule of Three</b></h2>
A good thing to <a href="https://dotev.blogspot.co.uk/2012/10/premature-generalization.html">remember</a> is that you can't make something reusable and generalized unless you have at least three examples to work with. A rough rule of thumb is to not attempt to generalize until you have at least three real use cases to work with. With these real-world cases you can identify the common traits and create genuinely useful abstractions of them. More real-world use cases will help you define and refine the abstractions you need. Of course if you try to gather too man use cases, you run the risk of delaying generalization too much.
<h2><b>You Ain't Gonna Need It</b></h2>
<a href="https://en.wikipedia.org/wiki/You_aren%27t_gonna_need_it">You Ain't Gonna Need It</a> (or YAGNI) is another principle you can try to keep in mind when your mind is racing about the possible features and abstractions you could implement. Implement things when you need them, and not before.
Even if you feel completely sure that you will need to implement something in the future, it still makes sense to wait: often you won't actually need it; even if you do it's likely you'll need something different from what you original envisioned.
Following YAGNI will help you by a) not having to write as much code b) Not cluttering your code with 'just in case' preparation for possible future uses.
<h2><b>The Simplest Thing That Could Possibly Work</b></h2>
Another way of approaching things is to build the <a href="https://en.wikipedia.org/wiki/Extreme_programminG">simplest thing that could possibly work</a>. This focus on simplicity is a philosophy borrowed from '<a href="https://en.wikipedia.org/wiki/Extreme_programming">Extreme Programming</a>' . When considering options for what your program, class or module might involve you should aim for simplicity at first, and only later modify your code when 'what works' changes to include more use cases.
<h2><b>Refactor: Code First Generalize Second</b></h2>
Being prepared to <a href="https://en.wikipedia.org/wiki/Code_refactoring">refactor</a> your code can also help you <a href="https://softwareengineering.stackexchange.com/questions/71206/when-to-write-abstract-code-and-when-to-be-more-specific">avoid generalizing at the wrong time</a>. You first write code to solve your specific, immediate problems, and only then do you look for the abstractions that can generalize your solution. By starting from a concrete example of useful code, you will have a much better idea of which generalizations will be beneficial.
<h2><b>Relax</b></h2>
Premature generalization <a href="https://solitum.net/premature-generalization/">can come about</a> from being too concerned with adherence to coding standards and getting things absolutely 'perfect'. Keeping things clear, explicit and concrete, even at the expense of repeating yourself occasionally may help you get a better grasp of the problem, and open your eyes to better, more optimal solutions.
So try to relax away from always being doing things perfectly, and write your solutions knowing that you will want to refactor them later.
