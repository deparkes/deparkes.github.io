---
layout: post
title: What is Docker?
date: 2017-10-13 15:00:40.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- container
- docker
- virtual machine
- virtualisation
author:
  display_name: deparkes
permalink: "/2017/10/13/what-is-docker/"
---
<h1>What is docker?</h1>
Docker is a technology for <a href="https://en.wikipedia.org/wiki/Operating-system-level_virtualization">software containers</a> - small virtual systems that can be used to support lightweight system virtualization. A <a href="https://www.docker.com/what-docker">Docker container</a> is a bit like a <a href="https://en.wikipedia.org/wiki/Virtual_machine">virtual machine</a>. Rather than being an entire standalone operating system, the container shares some elements of its host operating system.

Containers <a href="https://mspmentor.net/technologies/docker-vs-virtual-machines-understanding-performance-differences">can </a>have big benefits in terms of performance vs conventional virtual machines, so are popular with  developers and operations specialists who use them to help standardize software production and deployment.

<a href="https://en.m.wikipedia.org/wiki/Docker_(software)">Docker</a> containers are designed to function like a distributable, lightweight operating system. Bundling elements of the operating system and other packages into the container can remove many of the dependency issues associated with sharing applications, and stop the problem of well, it works on my machine.

To help keep docker containers lightweight and quick, they are not usually packaged with the entire operating system. Only the minimum libraries and dependencies to make an application work. The high-performance, low-footprint nature of docker containers mean that host machines often <a href="https://sysdig.com/blog/sysdig-docker-usage-report-2017/">run several containers at once</a> without problems.

Docker has become hugely <a href="https://containerjournal.com/2017/05/09/understanding-why-docker-popular/">popular </a>in recent years, but it actually builds on a <a href="https://blog.aquasec.com/a-brief-history-of-containers-from-1970s-chroot-to-docker-2016">fairly</a> <a href="https://opensource.com/resources/what-are-linux-containers">long history of Linux containers</a>, which first came about in the early 2000s. Docker itself  arrived in 2013, but took several years to reach maturity.

One of the <a href="https://www.zdnet.com/article/what-is-docker-and-why-is-it-so-darn-popular/">attractions </a>of Docker is that it made it easy to develop and share containers, provides tools and <a href="https://docs.docker.com/get-started/">guides </a>to get you started with containerisation, and has worked with <a href="https://www.opencontainers.org/about/members">other companies</a> to bring standardisation to the container landscape.
<h1>How Can Docker Help?</h1>
The low-overhead virtualization provided by containers has proven popular among developers and system administrators. The use of containers can reduce dependency problems, as well as helping support the deployment of <a href="https://martinfowler.com/articles/microservices.html">micro-services</a>.
<h2>Developers</h2>
Docker containers can help developers by bringing standardization to their development environments. This standardization can help in a number of ways:
<ul>
<li>Simplified <a href="https://devops.com/continuous-delivery-pipeline/">code pipelines</a>: Once an app is created in a container, the container can easily be passed between development, testing and production. The physical machines may change, but the application environment can be kept the same</li>
<li>Reduced <a href="https://en.wikipedia.org/wiki/Dependency_hell">dependency problems</a>: Containers can help solve the 'it works on my machine' problem. Rather than just sharing your application, you can share the entire environment it needs to run.</li>
<li>
<a href="https://www.citrix.com/blogs/2008/08/19/application-isolation-what-does-that-really-mean/">Application isolation</a>: Containers make it easy to run multiple versions of an application or a library on the same machine, without getting in each others' way.</li>
<li>
<a href="https://stackify.com/measuring-software-development-productivity/">Productivity</a>: If your code is in a container it's possible to automate the process of setting up your working environment, and easy to pass this on to a new developer when they start on a project. No more spending ages getting new developers up and running.</li>
</ul>
<h2>Ops</h2>
Lightweight containers can also benefit ops and software delivery.
<ul>
<li>
<a href="https://en.wikipedia.org/wiki/Deployment_environment">Environment </a>consistency: Containers make it possible to carry the same application environment from development through to production, and avoid many of the dependency issues that using a purely physical system would have.</li>
<li>Rapid <a href="https://en.wikipedia.org/wiki/DevOps#Deployment">deployment</a>: Containers <a href="https://mspmentor.net/technologies/docker-vs-virtual-machines-understanding-performance-differences">can be started up and shutdown in seconds</a>, allowing application infrastructure to be scaled rapidly. This compares to virtual machines which can take minutes, and physical hardware which can take days.</li>
<li>Streamlined <a href="https://en.wikipedia.org/wiki/Continuous_delivery">delivery</a>: The speed with which containers can be deployed can also streamline the delivery of updates, bug fixes and new features.</li>
</ul>
<h2>Enterprise</h2>
The benefits to developers and ops also have potential to be carried over to enterprise users, although the uptake of Docker at an enterprise level, <a href="https://www.theregister.co.uk/2017/09/11/container_adoption_still_low_says_cloud_foundation/">has not been huge</a>. Many enterprise customers are <a href="https://www.theregister.co.uk/2016/03/04/docker_dumbest_move_you_make/">still getting to grips</a> with conventional virtual machines and are unlikely to move away from those right away. It may be that newer products and services, not burdened by legacy IT procurement will be the early adopters of containerization.
<h1>Alternatives To Docker</h1>
Since Docker has <a href="https://www.contino.io/insights/beyond-docker-other-types-of-containers">yet to saturate the market</a> for containers, it pays to be aware of some of the alternatives and <a href="https://www.infoq.com/articles/container-landscape-2016">competitors in the virtualization world</a>.
Some other approaches to containerization include:
<ul>
<li>
<a href="https://unikernel.org/">Unikernels</a>
<ul>
<li>
<a href="https://stackoverflow.com/questions/30392261/docker-container-compared-with-unikernel">Very specialised</a>, lightweight virtual machines.</li>
<li>Can reduce complexity and improve portability and security</li>
<li>However development and deployment tooling is still emerging (but may be helped by the <a href="https://www.linuxjournal.com/content/unikernels-docker-and-why-you-should-care">recent acquisition</a> of Unikernels by Docker)</li>
</ul>
</li>
<li>
<a href="https://www.ubuntu.com/containers/lxD">LXD</a>
<ul>
<li>Developed by <a href="https://www.canonical.com/">Canonical </a>(the company behind Ubuntu)</li>
<li>
<a href="https://unix.stackexchange.com/questions/254956/what-is-the-difference-between-docker-lxd-and-lxc">Focussed more on deploying VMs</a> than apps.</li>
<li>Built and operated with the same tools as traditional VMs, but can have runtime performance similar to containers.</li>
</ul>
</li>
<li>
<a href="https://openvz.org/Main_PagE">OpenVZ</a>
<ul>
<li>A container platform for running complete operating systems</li>
<li>Shares the host OS (like Linux containers), so much faster and more efficient than traditional virtual machines</li>
<li>One of the oldest container platforms still in use today (goes back to 2005)</li>
</ul>
</li>
<li>
<a href="https://coreos.com/blog/rocket.html">Rkt</a>
<ul>
<li>Originally emerged to <a href="https://bobcares.com/blog/docker-vs-rkt-rocket/">tackle security concerns</a> with early versions of Docker</li>
<li>An open source, lightweight operating system based on the Linux kernel</li>
<li>Designed for providing infrastructure to clustered deployments</li>
<li>Builds on the original premise of the container that Docker popularised</li>
</ul>
</li>
<li>
<a href="https://en.wikipedia.org/wiki/Virtual_machine">Conventional virtual machines</a>
<ul>
<li>Containers <a href="https://www.itworld.com/article/2915530/virtualization/containers-vs-virtual-machines-how-to-tell-which-is-the-right-choice-for-your-enterprise.html">won't always be the right answer</a>, to it pays to remember that conventional virtual machines are still an option.</li>
</ul>
</li>
</ul>
