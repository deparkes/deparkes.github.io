---
layout: post
title: Simple NiFi Dataflow
date: 2019-11-17 20:31:23.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- docker
- docker-compose
- NiFi
- workflow
author: deparkes
permalink: "/2019/11/17/simple-nifi-dataflow/"
---
This post shows a simple NiFi dataflow and tries to demonstrate some of the elements of creating a NiFi workflow including adding and connecting processors, attributes and properties. This simple NiFi dataflow takes files from an input directory and routes them to different folders depending on the file name.
<h2>Configure NiFi and Docker Compose</h2>
In this example I'm using NiFi with docker compose to configure NiFi, and set up a volume mount so we can easily see and manipulate files visible to NiFi.
This is the docker-compose file I'm using:

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
    volumes:
      - .:/home/nifi
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

<pre></pre>
This <a href="https://docs.docker.com/compose/">docker-compose</a> configuration includes a volume mount from the current directory to '/home/nifi'. We'll be using this directory for input and output of files.
For the example to work, create an 'input' file inside the same directory as the docker-compose file.
Run this configuration with this command:

```bash
docker-compose up
```

<h2>Create a simple NiFi dataflow</h2>
<h3>Get file and put file</h3>
To start with this simple NiFi dataflow example will just move any file placed in an 'input' directory to an 'output' directory.
We'll use '<a href="https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.5.0/org.apache.nifi.processors.standard.GetFile/index.html">getFile</a>' and '<a href="https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.5.0/org.apache.nifi.processors.standard.PutFile/index.html">putFile</a>' processors to move a file between two locations.
<a href="https://nifi.apache.org/docs/nifi-docs/html/user-guide.html#building-dataflow">Read the NiFi documentation on processors</a> if you are not sure about how to add one to a dataflow.

| ![get file and put file]({{site.baseurl}}/assets/2019/11/1-GetFile-and-PutFile.png) |
|:--:|
| *get file and put file* |

The 'get File' and the 'put File' processors have been joined with a queue. To get the processors to work, we need to update their configuration.
<h4>GetFile Configuration</h4>
For get file we need to specify the input directory. In this case it is the 'input' directory we created when we were setting up the example. If you haven't done this already, you need to make an 'input' directory in the same location as the 'docker-compose.yaml' you are using.

| ![getfile properties]({{site.baseurl}}/assets/2019/11/2-getFile-properties.png) |
|:--:|
| *getfile properties* |

<h4>PutFile Configuration</h4>
For the PutFile processor we need to specify where the files should be moved to. In this example we set it to an 'output' directory in the same location as the docker-compose file.
The properties are also set to replace any files where there is a naming clash, and to create any missing output directories.

| ![putfile configuration]({{site.baseurl}}/assets/2019/11/3-putFile-properties.png) |
|:--:|
| *putfile configuration* |

<h4>Try Out the Dataflow</h4>
The GetFile and PutFile processors should now be configured so that if you add a file to the 'input' directory, it will be moved to the 'output' directory.
Right click on the background of the data flow and click 'Start' to make sure that all the processors are running, and try to add a file to the 'input' directory.
<h3>Route On attribute</h3>
To add some more sophistication to this simple NiFi dataflow, we will use the NiFi processor '<a href="https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.6.0/org.apache.nifi.processors.standard.RouteOnAttribute/index.html">route on attribute</a> to route files differently depending on file name. We will route 'green files', 'red files' to different folders. We will also set up a default route for files which don't fit the either 'red' or 'green'.
This is where we are headed:

| ![Simple NiFi Dataflow - route on attribute]({{site.baseurl}}/assets/2019/11/4-More-route-red-and-green-files-differently.png) |
|:--:|
| *Simple NiFi Dataflow - route on attribute* |

Using the Route on Attribute processor is a good example of where it is good to use the NiFi documentation to figure out what is going on. Searching for processors within NiFi can get you started, but it is not always obvious which is the right one to use, and how to correctly use it.
To set the routing rules for the Route on Attribute processor, right click on it go to configuration -&gt; properties and click the plus symbol to add a new property.

| ![route on attribute properties]({{site.baseurl}}/assets/2019/11/5-route-on-attribute-properties.png) |
|:--:|
| *route on attribute properties* |

The 'value' here is pretty much lifted straight from the <a href="https://nifi.apache.org/docs/nifi-docs/components/org.apache.nifi/nifi-standard-nar/1.6.0/org.apache.nifi.processors.standard.RouteOnAttribute/additionalDetails.html">NiFi documentation for Route on Attribute</a>. In this example each routing option is connected up to its own 'PutFile' processor, which is in turn configured to send the file to an appropriate directory.

| ![Examples of connections available]({{site.baseurl}}/assets/2019/11/6-Example-of-connections.png) |
|:--:|
| *Examples of connections available* |

In this case there are the three options available from the Route on Attribute processor: match on green, match on red, and unmatched.
I'll leave it as an exercise to finalise the configuration and connections for this extension to the original example. When you are finished you should be able to route files with 'green' in the name into a 'green' folder, files with 'red' in the name into a 'red' folder, and files which don't match either into an 'unmatched folder'.
<h2>Taking Things Further</h2>
Once you have this understood this simple NiFi dataflow, there are a few things you could do to extend it:
<ul>
<li>Add some more sophisticated regex to limit which files are picked up by getFile</li>
<li>Try out some other aspects of the <a href="https://nifi.apache.org/docs/nifi-docs/html/expression-language-guide.html#searching">NiFi string matching</a> to pick up different file names</li>
<li>Try out using NiFi <a href="https://nifi.apache.org/docs/nifi-docs/html/expression-language-guide.html">expression language</a> in PutFile to change output directory depending on file name</li>
</ul>
