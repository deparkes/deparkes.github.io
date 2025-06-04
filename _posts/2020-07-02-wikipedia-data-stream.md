---
layout: post
title: Wikipedia Data Stream
date: 2020-07-02 19:38:02.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- api
- data
- python
- rest
- streaming
- wiki
- wikimedia
author: deparkes
permalink: "/2020/07/02/wikipedia-data-stream/"
---
<a href="https://aws.amazon.com/streaming-data/">Streaming data</a> is an important part of modern data processing. If you are just starting out, and perhaps don't yet work somewhere with access to a big data <a href="https://www.pcmag.com/news/inside-the-tech-that-powers-your-favorite-video-streaming-services">streaming infrastructure</a>, it can be hard to know where to start. This post talks you through a simple wikipedia data stream example from the wikimedia documentation.
<h2>Wikipedia Data Stream</h2>
A little known feature about wikipedia is that it publishes a stream of recent changes. The wikipedia data stream is actually just one part of a larger stream of real-time edits to sites in the <a href="https://wikitech.wikimedia.org/wiki/Event_Platform/EventStreams">wikimedia group.</a>
We can use this example to gain access to a simple data stream example, but it's also been used for very cool projects like <a href="https://listen.hatnote.com/">Listen To Wikipedia</a> which lets listen to edits as they happen!
<h2>Streaming Data Basics</h2>
Having access to a data stream immediately brings home some of the <a href="https://www.talend.com/resources/data-streaming-challenges/">challenges</a> it brings that static data just doesn't have. The <a href="https://wikitech.wikimedia.org/wiki/Event_Platform/EventStreams">Wikipedia data stream</a> is a nice example stream for playing around with some of the basics of working with stream data.
For this example to work you will need to install the <a href="https://github.com/btubbs/sseclient">sseclient</a> library for handling server-side events - it lets you iterate over messages sent by the server.

```python
from sseclient import SSEClient as EventSource
stream_url = 'https://stream.wikimedia.org/v2/stream/recentchange'
for event in EventSource(url):
    print("Do something with the event")
```

<h3>Capture a stream</h3>
Using the python example on the <a href="https://wikitech.wikimedia.org/wiki/Event_Platform/EventStreams">wikimedia page</a>, it is quite easy to start capturing the stream.
At time of writing (check <a href="https://wikitech.wikimedia.org/wiki/Event_Platform/EventStreams">the documentation</a> in case it has changed) the returned message format is this

```
event: message
id: [{"topic":"eqiad.mediawiki.recentchange","partition":0,"timestamp":1532031066001},{"topic":"codfw.mediawiki.recentchange","partition":0,"offset":-1}]
data: {"event": "data", "is": "here"}
```

We can access the five most recent messages like this:

```python
from sseclient import SSEClient as EventSource
url = 'https://stream.wikimedia.org/v2/stream/recentchange'
event_count = 1
for event in EventSource(url):
    print("Stream message: " + str(event_count))
    print(event.event)
    print(event.data)
    event_count += 1
    if event_count &gt; 5:
        break
```

If you run this (once you've installed sseclient), you should get back five recent messages.
<h3>Parsing streamed data</h3>
We can now extend to the <a href="https://wikitech.wikimedia.org/wiki/Event_Platform/EventStreams">full example</a> in the wikimedia documentation. I've modified it below to only return five recent messages.
This full example parses the json message as it arrives and prints some of the message out.

```python
import json
from sseclient import SSEClient as EventSource
url = 'https://stream.wikimedia.org/v2/stream/recentchange'
wiki = 'commonswiki'
event_count = 1
for event in EventSource(url):
    if event.event == 'message':
        try:
            change = json.loads(event.data)
        except ValueError:
            continue
        if change['wiki'] == wiki:
            print('{user} edited {title}'.format(**change))
            event_count += 1
            if event_count &gt; 5:
                break
```

