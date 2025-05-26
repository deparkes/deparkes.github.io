---
layout: post
title: Nifi Version Control with Nifi Registry
date: 2019-11-16 22:58:28.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- apache
- data engineering
- docker
- docker-compose
- NiFi
- nifi registry
- workflow tool
- zookeeper
author:
  display_name: deparkes
permalink: "/2019/11/16/nifi-version-control-with-nifi-registry/"
---
NiFi is a tool designed to support the flow of data between software systems. This post shows how you can achieve NiFi version control with NiFi Register and docker.
A note of caution: this post is about showing a little of what of possible with NiFi version control, and I suggest you read the <a href="https://nifi.apache.org/docs/nifi-docs/html/administration-guide.html#embedded-zookeeper">NiFi administrator guide</a> if you want to configure NiFi correctly.
<h2>The Components</h2>
In this post I'll be using docker compose along with three main components: NiFi, NiFi Registry, and Zookeeper.
<h3>NiFi</h3>
<a href="http://nifi.apache.org/index.html">NiFi</a> was created by the NSA as a tool for flowing data between software systems. Unfortunately NiFi version control isn't something that is available out of the box.
<a href="https://hub.docker.com/r/apache/nifi/">Find out more about the NiFi docker image.</a>
<h3>NiFi Registry</h3>
<a href="http://nifi.apache.org/registry.html">NiFi registry</a> is a complementary tool for NiFi. It provides a place for workflows to be 'deployed' and thus shareable between NiFi instances. NiFi Registry also provides a form of version control so that workflows can be checked in / out as needed.
<a href="https://hub.docker.com/r/apache/nifi-registry/">Find out more about the NiFi Registry docker image</a>
<h3>Zookeeper</h3>
<a href="https://zookeeper.apache.org/">Zookeeper</a> is a tool for coordinating distributed clusters. Zookeeper is needed by NiFi because NiFi is designed to operate as a cluster.
<a href="https://hub.docker.com/_/zookeeper">Find out more about the Zookeeper docker image</a>

<h2>Docker Compose Configuration</h2>
We'll use docker-compose to set up three containers. The base docker configuration used is from <a href="https://medium.com/@erbalvindersingh/running-nifi-in-docker-using-docker-compose-34032de853d2">this blog post</a>.

```yaml
version: "3"
services:
  zookeeper:  # the configuration manager
    hostname: zookeeper:3.5
    container_name: zookeeper
    image: zookeeper:3.5
    environment:
      - ALLOW_ANONYMOUS_LOGIN=yes
  nifi:
    image: apache/nifi:1.9.2
    ports:
      - 8181:8080 # Unsecured HTTP Web Port
    environment:
      - NIFI_WEB_HTTP_PORT=8080
      - NIFI_CLUSTER_IS_NODE=true
      - NIFI_CLUSTER_NODE_PROTOCOL_PORT=8082
      - NIFI_ZK_CONNECT_STRING=zookeeper:2181
      - NIFI_ELECTION_MAX_WAIT=1 min
  nifi-registry:
    image: apache/nifi-registry:0.5.0
    ports:
      - 18080:18080
```

To start the containers, run

```bash
docker-compose up
```

This may take a few minutes.
<h2>Create a New Bucket In NiFi Registry</h2>
With the above docker-compose configuration, we can access the nifi registry by navigating to http://localhost:18080/nifi-registry

| ![Empty Registry]({{site.baseurl}}/assets/2019/11/1-empty-registry.png) |
|:--:|
| *Empty Registry* |

Create a new bucket by clicking the spanner icon in the top left.

| ![Spanner - New Bucket]({{site.baseurl}}/assets/2019/11/2-create-a-new-bucket.png) |
|:--:|
| *Spanner - New Bucket* |

Hit 'Create' and you'll see a new bucket is visible in the NiFi registry.
<h2>Configure Version Control in NiFi</h2>
With the above docker-compose configuration, we can access NiFi by navigating to http://localhost:8181/nifi/
<h3>Connect to NiFi Registry</h3>
Firstly we need to configure the NiFi to know about the NiFi registry we just set up. We can do this via the <a href="https://en.wikipedia.org/wiki/Hamburger_button">hamburger button</a> in the top right of the main NiFi screen.

| ![Configure NiFi via the burger menu]({{site.baseurl}}/assets/2019/11/3-NiFi-controller-settings.png) |
|:--:|
| *Configure NiFi via the burger menu* |

Once in the controller settings, go to the 'Registry Clients' tab and click the plus symbol to add a registry client.

| ![Add registry client]({{site.baseurl}}/assets/2019/11/4-Add-registry-client.png) |
|:--:|
| *Add registry client* |

Something that threw me at first was the address of the registry client.
Unlike other guides online which suggest using 'localhost' because we have used docker compose which has its <a href="https://docs.docker.com/compose/networking/">own way of handling networking</a>, so instead we use the http://nifi-registry:18080. (Or instead of 'nifi-registry' use whatever you've called  your docker-compose thing for the registry).
<h3>Start Committing Changes</h3>
To commit changes to the registry we need to create a process group. Once created we can right right click and start tracking.
As you make changes inside the process group you can right click and commit your changes to the workflow.

| ![start version control on a process group]({{site.baseurl}}/assets/2019/11/5-Start-Version-Control-on-process-group.png) |
|:--:|
| *start version control on a process group* |

As you make changes within the the process group you can commit your local changes to the NiFi Registry.

| ![commit your changes to the NiFi registry]({{site.baseurl}}/assets/2019/11/8-Commit-local-changes.png) |
|:--:|
| *commit your changes to the NiFi registry* |

Once you've made a commit or two to the registry, if you go back to the NiFi registry (found at http://localhost:18080/nifi-registry in this example), you will be able to see those changes stored.

| ![check the different versions in the bucket]({{site.baseurl}}/assets/2019/11/9-Bucket-with-two-versions.png) |
|:--:|
| *check the different versions in the bucket* |

<h2>Retrieve an Existing Workflow</h2>
Once you have committed a version of your workflow to the NiFi registry you can go back to it if you need to.
Right click in the workflow window and go to 'version', then 'change version' to bring up list of available versions.

| ![right click to change versions]({{site.baseurl}}/assets/2019/11/10-right-click-change-version.png) |
|:--:|
| *right click to change versions* |

Select the previously committed version that you need from the 'Change Version' menu.

| ![select the previously committed version you need]({{site.baseurl}}/assets/2019/11/11-available-versions.png) |
|:--:|
| *select the previously committed version you need* |
