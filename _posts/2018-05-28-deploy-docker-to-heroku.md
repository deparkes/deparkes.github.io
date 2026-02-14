---
layout: post
title: Deploy Docker To Heroku
date: 2018-05-28 15:30:21.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- DevOps
tags:
- app
- development
- docker
- flask
- heroku
- hosting
- paas
- web
- webapp
author: deparkes
permalink: "/2018/05/28/deploy-docker-to-heroku/"
---
<a href="https://www.heroku.com/">Heroku</a> is a 'platform as a service' (<a href="https://en.wikipedia.org/wiki/Platform_as_a_service">PaaS</a>) cloud provider. Heroku makes it easy to deploy apps by pushing to git repositories or using docker containers. This post shows you how you can deploy docker to Heroku.

The Heroku website already has <a href="https://devcenter.heroku.com/articles/container-registry-and-runtime">some good guide</a>s to help you deploy docker to Heroku, but I found there were some things that didn't quite make sense to me.

In this post I build on my previous post which showed <a href="{{site.url}}/2018/03/02/simple-docker-flask-sqlite-api/">how to make a simple flask app</a> in a docker container. In that post we made a simple app which we could access in a locally hosted docker container. If we want others to be able to access it it we need to deploy it or host it elsewhere.
<h1>Get Set Up With Heroku</h1>
<h2>Heroku Basics</h2>
To follow along with the rest of this post you'll need to create <a href="https://signup.heroku.com/">a heroku account</a> and install the <a href="https://devcenter.heroku.com/articles/heroku-cli">heroku cli app</a>.
<h2>Install the Heroku Docker Plugin</h2>
<a href="https://devcenter.heroku.com/articles/container-registry-and-runtime">Docker is supported in Heroku</a>, but you need to install a plugin first. You can do this by running this command:
```
heroku plugins:install @heroku-cli/plugin-container-registry
```
Then start up docker on your local machine, and run (make sure you have already logged into heroku CLI):
``` heroku container:login ```
<h2>Create a Heroku App</h2>
Our container will need to run from within a heroku app. If you don't already have one, <a href="https://devcenter.heroku.com/articles/creating-apps">create a new app</a> with this command:
``` heroku create ```
<h1>Prepare Your Docker Container</h1>
You will need to make some alterations to your docker container and your app to prepare it to be hosted on Heroku. To illustrate the kind of things you need to consider I will modify my existing <a href="{{site.url}}/2018/03/02/simple-docker-flask-sqlite-api/">simple flask app</a>.
<a href="https://github.com/deparkes/docker_flask_example/tree/heroku_app">Checkout the example heroku docker app on github.</a>
<h2>Change Docker User</h2>
Heroku runs docker apps a a non-root user. To help when it comes to testing locally, it is recommended to add the follow lines to your dockerfile, before the 'CMD' command that runs the app script:
```
RUN adduser -D myuser
USER myuser
```
<h2>Port Forwarding</h2>
Heroku is all about <a href="https://www.heroku.com/about">running web apps</a>. It takes requests from the internet and passes them to a particular port on the Heroku app. The way Heroku is configured, the port the our app should listen to is set by the ```$PORT``` environment variable in the Heroku app.

As far as Heroku is concerned, the docker container is the web service, and needs to be listening on the port set by the ```$PORT``` environment variable.
Running locally you can expose which ever port you want, and you would typically expose the port needed by the process or service running within the container (e.g. port 5000 is the default port for a Flask app).

But Heroku requires that the web process (i.e. the docker container) listens on a particular port specified by the ```$PORT``` environment variable. This is the only port open for use, and Heroku will throw an error if the running service does not connect to that port within 60 seconds.

| ![Opening ports]({{site.url}}/assets/2018/05/PORT_variable-300x266.png) |
|:--:|
| *Opening ports* |

Behond the scenes, heroku must be running something like
```docker run -p 80:$PORT -e PORT=$PORT``` where '80' is the port heroku exposes to the internet, and ```$PORT``` is the environment variable Heroku sets when an app is created. Running this would the correct port in the docker container when it is run. So far so good.

This is fine, but our web app will not work unless it knows that it should not be listening on it's default port, but instead on this new port that docker is expecting to open up. The final peice of the puzzle, then, is to configure the service or process running on the docker container to also use the ```$PORT``` environment variable.

For my simple Flask app inside a docker container I needed to add the port argument to 'app.run' in the flask script, and use the ```os.environ.get()``` to capture the envioronment variable:
``` app.run(debug=True, host='0.0.0.0', port=os.environ.get('PORT')) ```
<h2>Test Your Container Locally</h2>
Changing the docker container to be suitable for Heroku also changes how we run it locally. In particular, our app now expects a ```$PORT``` environment variable, and we need to make sure the docker container exposes that port.

First we can set the PORT environment variable.
When we run docker we need to tell it to create an environment variable 'PORT' which will be picked up by the
```docker run -p 5000:5000 -e PORT=5000 <image-name>```
Or configure a docker-compose script to forward the appropriate ports, and create an environment variable within the docker container:

```yaml
version: '2'
services:
    web:
        build: .
        ports:
            - "5000:5000"
        volumes:
            - .:/web
        environment:
- PORT:5000
```

You can then run your local, development version with this command:

```docker-compose run --service-ports web```

<a href="https://devcenter.heroku.com/articles/local-development-with-docker-compose">Read more about heroku and docker compose</a>.
<h2>Push Your Container to Heroku</h2>
Pushing your docker container to heroku is quite simple.
```heroku container:push web --app HEROKU_APP_NAME```
<h1>Try Out Your App</h1>
Run your new app with this command:
```heroku open --app ${YOUR_APP_NAME}```
This will open up your app url in a browser window.
https://medium.com/travis-on-docker/how-to-run-dockerized-apps-on-heroku-and-its-pretty-great-76e07e610e22
