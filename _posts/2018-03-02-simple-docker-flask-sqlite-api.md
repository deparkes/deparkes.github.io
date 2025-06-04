---
layout: post
title: Simple Docker Flask SQLite API
date: 2018-03-02 15:30:56.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- api
- docker
- flask
- python
- restful
- sql
- sqlite
- web
author: deparkes
permalink: "/2018/03/02/simple-docker-flask-sqlite-api/"
---
Flask is a lightweight python web framework which can used for creating <a href="https://restfulapi.net/">RESTful APIs</a>. This post shows you how to make a simple Docker Flask SQLite API. This post builds on the excellent <a href="https://programminghistorian.github.io/ph-submissions/lessons/creating-apis-with-python-and-flask">Flask API Lesson</a> on <a href="https://programminghistorian.org/">The Programming Historian</a>.
If you just want to dive straight into a Docker Flask SQLite API example you can clone this <a href="https://github.com/deparkes/docker_flask_example">git repository</a>.
<h1>The building blocks</h1>

<table class="tg">
<tbody>
<tr>
<td class="tg-yw4l"><em><a href="https://www.docker.com/"><img class="alignleft" src="{{site.baseurl}}/assets/2018/03/docker-mark-blue.png" alt="Docker logo horizontal spacing" width="80" height="68"></a></em></td>
<td class="tg-yw4l">
<a href="https://www.docker.com/"><em>Docker</em></a> -  a lightweight container platform. In this case I was interested in using it to simplify the development process and have a self contained development webserver in a docker container.</td>
</tr>
<tr>
<td class="tg-yw4l"><a href="https://flask.palletsprojects.com/en/stable/"><em><img class="shrinkToFit transparent alignleft" src="https://palletsprojects.com/static/content/projects/flask-logo.png" alt="Flask logo" width="300" height="75"></em></a></td>
<td class="tg-yw4l">
<a href="https://flask.pocoo.org/"><em>Flask</em> </a>- a lightweight web framework for python. It comes with a <a href="https://stackoverflow.com/questions/12269537/is-the-server-bundled-with-flask-safe-to-use-in-production">development server</a>, which can be combined with <a href="https://ironboundsoftware.com/blog/2016/06/27/faster-flask-need-gunicorn/">other tools</a> to make it <a href="https://flask.pocoo.org/docs/0.12/deploying/#deployment">production ready.</a>
</td>
</tr>
<tr>
<td class="tg-yw4l"><a href="https://www.sqlite.org/"><em><img class="logo alignleft" src="{{site.baseurl}}/assets/2018/03/sqlite370_banner.gif" alt="SQLite" border="0"></em></a></td>
<td class="tg-yw4l">
<a href="https://www.sqlite.org/"><em>SQLite</em> </a>- a database provides some persistent storage for a web application. Other SQL databases such as <a href="https://www.mysql.com/">MySQL</a> and <a href="https://www.postgresql.org/">PostgreSQL</a> are perhaps more common associated with web development, but SQLite is <a href="https://www.sqlite.org/whentouse.html">capable</a> of running a web site. The simplicity of SQLite also means that it is a good candidate for testing and prototyping.</td>
</tr>
</tbody>
</table>
<h1>Assembling the Blocks</h1>
As I have already noted, I am essentially using the flask api developed in the programming historian guide. The difference here is that things are encapsulated in a docker container.
What we want to happen is:
<ul>
<li>We want to largely replicate the functionality of <a href="https://programminghistorian.github.io/ph-submissions/lessons/creating-apis-with-python-and-flask">The Programming Historian example</a>, but in a docker container.</li>
<li>We write and develop our python code in our local machine, and save the files to a particular folder.</li>
<li>We configure docker to know which folder we are working in and which packages it should install inside that container.</li>
<li>Docker should start our app when we start the container</li>
<li>We will need to direct a port on our server - <a href="https://en.wikipedia.org/wiki/Localhost">localhost</a> in this example - to the appropriate port on the docker container.</li>
<li>A database will provide persistent storage outside of the container (all data inside the container is lost when it is brought down).</li>
</ul>

| ![Docker flask sqlite api]({{site.baseurl}}/assets/2018/03/DockerFlaskSQLite_schematic-300x289.png) |
|:--:|
| *Docker flask sqlite api* |

<h2>Docker</h2>
Docker is going to take the place of our usual physical system, so we will start there. I'm using a base docker image based on alpine - a lightweight docker image.
We then just need to do some other set up work:
<ul>
<li>copy the directory containing the docker image into '/web' inside the container so the container has access to the project.</li>
<li>Set the working directory to be the correct directory within web.</li>
<li>Run pip install with the requirements.txt file inside this working directory.</li>
</ul>
<h3>Dockerfile</h3>

```dockerfile
FROM python:3.4-alpine
COPY . /web
WORKDIR /web/api
RUN pip install -r ./requirements.txt
ENTRYPOINT ["python"]
CMD ["app.py"]
```

Since we want the docker container to interact with the filesystem, we will need to mount the right directory to do docker when we spin up the container. We could <a href="{{site.baseurl}}/2017/10/20/run-docker-container/">run this dockerfile directly</a>, but instead we will use docker compose.
<h3>Docker-compose</h3>
<a href="https://docs.docker.com/compose/overview/">Docker compose</a> is primarily a way for controlling multi-container builds, but we can use it here to encapsulate some of our configuration.
For this case the docker-compose.yaml file controls: how the container is built, the port mapping, and which volumes to mount.

```yaml
version: '2'
services:
    web:
        build: .
        ports:
            - "5000:5000"
        volumes:
            - .:/web
```

Docker should now be configured to pick up the contents of the development directory and try to run 'app.py' in that directory using python. app.py will be our flask app which we now need to create.
The docker file also expects to find a file '<a href="https://stackoverflow.com/questions/7225900/how-to-pip-install-packages-according-to-requirements-txt-from-a-local-directory">requirements.txt</a>' which will define which packages need to be installed to the docker container with pip.
<h2>SQLite</h2>
For the purposes of this example I am using the <a href="https://github.com/deparkes/docker_flask_example/tree/master/data">sample database</a> used in the programming historian guide. The flask application will read from this. I put it in a directory 'data', but it is largely up to you where you put it.
The data directory is in the same directory as the docker file, so will be included in the mounted volume specified by the docker-compose.yaml file.
<h2>Flask<strong>
</strong>
</h2>
With these things in place we can write our flask code in app.py. As noted elsewhere my example here is based on the programming historian example. My code is available here.
I won't go too much into the detail of the flask app - you can download it <a href="https://github.com/deparkes/docker_flask_example">here</a> - but will point out a couple of things to watch out for when developing:
<ul>
<li>While developing this flask app we should run flask in debug mode so it shows us the debugging info in the command line.</li>
<li>Flask should be set to run on host '0.0.0.0' - This makes the flask server <a href="https://flask.pocoo.org/docs/0.12/quickstart/">externally visible</a>. Since flask is inside a docker container, externally visible just means visible from outside that container.</li>
</ul>
<h1>Running the API</h1>
To test run the API we run <em>docker-compose up --build</em>. Which runs docker with the docker-compose configuration we defined earlier and builds a docker container using the dockerfile.
If all is successful the api should be accessible on localhost:5000.
There are more examples on the programming historian site, but a couple you can try to test out your api are:
<ul>
<li><a href="https://localhost:5000/api/v1/resources/books?author=Jo+Walton">https://localhost:5000/api/v1/resources/books?author=Jo+Walton</a></li>
<li><a href="https://localhost:5000/api/v1/resources/books/all">https://localhost:5000/api/v1/resources/books/all</a></li>
</ul>
