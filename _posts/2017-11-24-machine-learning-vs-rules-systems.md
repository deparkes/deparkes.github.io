---
layout: post
title: Machine Learning vs Rules Systems
date: 2017-11-24 15:00:33.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- ai
- artificial intelligence
- data science
- machine learning
- rules engine
author:
  display_name: deparkes
permalink: "/2017/11/24/machine-learning-vs-rules-systems/"
---
Machine learning and rules-based systems are widely used to make inferences from data. The two approaches have their <a href="https://www.forbes.com/sites/teradata/2015/12/15/data-science-machine-learning-vs-rules-based-systems/#41fab19d2119">strengths and weaknesses</a>, and it is useful to have a grasp of both. Although not as <a href="https://www.brianmadden.com/opinion/Machine-learning-hype-is-growing-but-theres-no-need-for-IT-to-worry">hyped </a>at the moment, <a href="https://tabbforum.com/opinions/6-big-trading-problems-that-are-easily-solved-with-a-rules-engine">rules-based systems do still have their place</a> and it is worth understanding the distinction between these methods and where they might be valuable. This post looks at machine learning and rule-based approaches and suggests which you may want to consider using.
<h1>Rules-Based Systems</h1>
Rules-based systems  are a simple <a href="https://link.springer.com/chapter/10.1007/978-3-642-21004-4_7">kind of artificial intelligence</a>, which use a series of IF-THEN statements that guide a computer to reach a conclusion or recommendation.
<h2>Two Key Components</h2>
A rules-based system is built on two main components: a set of facts about a situation, and a set of rules for how to deal with those facts:
<ol>
<li>
<strong>A set of facts.</strong> Also known as the knowledge base.  These facts are a combination of data, such as income and a condition such as 'is zero', or 'is greater than £10k'.</li>
<li>
<strong>A set of rules.</strong> Also known as the rules engine. It's the rules that describe the relationship between the IF and the THEN statements. For example a rule might be "IF a loan applicant has an income of zero THEN refuse the loan".</li>
</ol>
With these two basic concepts, it is possible to build a basic AI system such as a tool to recommend clothing choice on a particular day. The facts used in this case could include "It's a weekday", "It's cold", "It's raining". We could construct some rules so an AI concludes that the appropriate clothing choice might be warm work wear and an umbrella.
<h2>Expert-based Rules</h2>
Full rules-based systems are typically built from the combined knowledge of human experts in the problem domain. The domain experts specify all the steps taken to make a decision and how to handle any special cases and this full knowledge of the experts is incorporated into the system. This involvement of human experts means that rules system as re sometimes called <a href="https://stackoverflow.com/questions/1687734/rules-engine-vs-expert-systeM">expert systems</a>.
Since the knowledge of the world has been learned by humans, this involvement of experts in the details of decision making distinguishes rules systems from 'machine-learning' techniques.
<h2>Rules are Easy to Write</h2>
One of the key benefits of a rules system is that writing and implementing rules is quite easy. If we know about the situation of interest, we can create rules based on simple IF-THEN statements.
It is lucky that rules are generally easy to write. If you wanted to account for 100 possible outcomes or reactions for your AI, you would need to write 100 rules to cover them. If, having written the 100 rules you discover a special case you hadn't considered before, you will need to write an additional rule to account for it.
<h2>But Need to Account for Special Cases</h2>
If we look again at the example of deciding what clothes to where on a particular day, a little more thought about situation uncovers many other situations that we would want to include in the system.
A few situations which might break the simple rules might include: public holidays, vacation days, rain not heavy enough to warrant an umbrella, wind strong enough to make an umbrella impractical, the amount of time available to get ready in the morning, an important meeting on a particular day. This list could go on.
<h2>So Rules Systems Can Become Unwieldy</h2>
Rules based systems are deterministic in nature. Not having the right rule in place can result in false positives and false negatives, so system of rules can start of quite simple, but can become rather unwieldy over time as more and more exceptions and rule changes are added. While non-experts may understand individual rules, the complex interactions of a full rules engine may be more difficult to grasp.

Another challenge faced by rules-based systems is when the data and scenarios change faster than you can update the rules. You can reach a point when you lose track of what is going on and how many exceptions there are. As your rules system comes further adrift from the realities of the input data, the false positive and false negative rates can rise to a point that your system is no longer useful.
<h1>Machine Learning</h1>
<a href="https://en.wikipedia.org/wiki/Machine_learning">Machine learning</a> is an alternative approach which can help to address some of the issues with <a href="https://en.wikipedia.org/wiki/Rule-based_system">rules-based</a> methods. Rather than attempt to fully emulate the decision process of an expert or best practice, machine learning methods typically only take the outcomes from the experts.

For example an insurance specialist may review a number of cases and decide whether they are fraudulent or not. Exactly how the expert arrived at their decision is not important for machine learning, only what their decision was. Focusing on the outcomes rather then entire decision making process can make machine learning more flexible and less susceptible to some of the problems encountered with rules-based systems.
<h2>Machine Learning is Based on 'Models'</h2>
Unlike rules-based methods, machine learning is <a href="https://yseop.com/blog/artificial-intelligence-machine-learning-vs-deterministic/">probabilistic</a> and uses statistical models rather than deterministic rules. The basic operation of a machine learning process is to say 'given what we know about these historic outcomes, what can we say about future outcomes'.
Machine learning approaches assume that the outputs (identified by historic outcomes data) can be described by a combination of input variables and other parameters.

The output could be a simple binary classification (e.g. 'should I take my umbrella today?'), or more complex (e.g. predicting fraudulent behaviour), or a predicted value (e.g. how much of a loan is a person likely to repay). The input variables can be numerous, and some models can use hundreds of inputs (also known as 'features').
<h2>Models Can Sometimes be Treated as Blackbox</h2>
The machine learning algorithm itself is often regarded as a '<a href="https://datascience.stackexchange.com/questions/22335/why-are-machine-learning-models-called-black-boxes">black box</a>' - the inputs and outputs are closely connected to the real world, but the internal works are more difficult to describe.
This black box nature of machine learning is both a curse and a blessing. In many business situations, <a href="https://www.inference.vc/accuracy-vs-explainability-in-machine-learning-models-nips-workshop-poster-review/">explaining</a> the decision made by an algorithm is important and some machine learning algorithms do not lend themselves to explanation. On the hand, the disconnect between the real world and the problem domain can help avoid getting caught up with complex rules arrangements.

There are many possible <a href="https://www.datasciencecentral.com/profiles/blogs/top-10-machine-learning-algorithms">machine learning algorithms</a> out there, but some models are easier to explain and provide an audit trail for than other. '<a href="https://en.wikipedia.org/wiki/Decision_tree">Decision tree</a>' methods can <a href="https://medium.com/@rnbrown/creating-and-visualizing-decision-trees-with-python-f8e8fa394176">visualise their decisions</a> in a way not unlike <a href="https://www.researchgate.net/post/comparison_of_rules_generated_by_decision_tree_vs_rules_of_rule-base_system">rule-systems</a>. You can put a single case in at the start of the model and easily follow through the decisions made. Although in some ways a decision tree may look similar to a rules-system, how the decisions were derived is rather different: the rules system comes from input from human experts, whereas the decisions in a decision tree are produced by the machine learning process.
<h2>Machine Learning Models Need to Be 'Trained'</h2>
A machine learning model is 'trained' on <a href="https://fastml.com/how-much-data-is-enough/">historic data</a> - outcomes already identified or labelled by human experts. In some cases this is not a problem - there may be large amounts of historic data available to train with. In other cases the <a href="https://machinelearningmastery.com/much-training-data-required-machine-learning/">lack of good training data</a> is a real problem. If your machine learning model is attempting to identify rare events - such as fraudulent activity - there may not be many examples to start with.
Highly specialised problems can also struggle with having <a href="https://rdcu.be/yJkg">sufficient labelled data</a> - you may struggle to sit enough doctors down to label thousands of x-ray images as showing cancer or not.  Even if you can, you may be missing out on large amounts of specialist knowledge held by the doctors.

<h2>Feature Engineering Replaces Rules Creation</h2>
In machine learning the creation of rules is largely replaced by the <a href="https://machinelearningmastery.com/discover-feature-engineering-how-to-engineer-features-and-how-to-get-good-at-it/">engineering of features</a>. Features are input variables related to trends in historic data. If our model was trying to predict appropriate clothing choices for a given day, a feature might be the average historic temperature on a particular day, or whether or not the day of interest is a weekday or a weekend.
The learning process involves trying to find parameters which give correct outputs most of the time. The resulting taught model is derived from the data itself rather than externally supplied information.
<h1>Which Method Should I Use?</h1>
The answer is 'It Depends'. To its detractors Rules-based systems can be seen as cumbersome and unweildy. On the other hand, machine learning models can be slow to implement.

Machine learning may be a better bet in the long-run as it is more amenable to continuous adaption and improvement through data preparation, algorithm selection and algorithm parameter tweaking. Machine learning algorithms tend to be one step away from human involvement in favour of optimisation for computers.

Rules-based systems can often offer quicker, tactical solutions and workarounds. The requirement for business expert input can help wider business buy-in and make it easier to explain how decisions were made. Many projects begin with an expert or rules-based system to explore and understand the system.
