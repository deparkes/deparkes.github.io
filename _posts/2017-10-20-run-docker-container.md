---
layout: post
title: How to Run a Docker Container
date: 2017-10-20 15:00:22.000000000 +01:00
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
permalink: "/2017/10/20/run-docker-container/"
---
<a href="https://wp.me/p4DE9r-TQ">Docker containers</a> are used for lightweight system virtualisation. It's quite simple to run a docker container, but there is also a bewildering range of options for things you can do. In this post I've pulled together a few of the more common and useful ways to run a docker container.
I'm assuming you have downloaded and <a href="https://docs.docker.com/engine/installation/">installed docker</a> on your system, and are able to run docker commands.
<h1><b>Start With A Docker Image
</b></h1>
It is possible<a href="https://www.howtoforge.com/tutorial/how-to-create-docker-images-with-dockerfile/"> build your own docker image</a>s, but for now we can pull an existing image from the docker registry. Whether you download an image or build one yourself, the run steps here should be the same.
The <a href="https://docs.docker.com/registry/">docker registry</a> contains pre-built docker images which you can use without having to define your own.
We could have picked pretty much any image on the <a href="https://hub.docker.com/">registry</a>, but I've picked an example of a <a href="https://hub.docker.com/_/alpine/">lightweight base image</a> called <a href="https://github.com/gliderlabs/docker-alpine">Alpine</a> that's useful for building small containers. <a href="https://gofore.com/en/lean-docker-alpine-linux">Alpine </a>is also available as a fully-functioning Linux distribution.
We can get the latest alpine images from the registry by running

```
docker pull alpine
```

If we now run

```
docker images
```

We will see that the 'alpine' image (called a repository here) is now available to us.

```
REPOSITORY  TAG     IMAGE ID    CREATED    SIZE
alpine    latest 76da55c8019d   2 weeks   3.97MB
```

<h1>Run The Docker Image</h1>
Now that we have a docker image available on our system, we need to <a href="https://stackoverflow.com/questions/18497688/run-a-docker-image-as-a-container">run it to start up a docker container</a>.
In the previous step we  found out information about the docker images we pulled down from the registry. This gives us two ways we can run  this alpine image on our system: either use the 'repository' name (alpine in this case), or using the image id (76da55c8019d in this case).
We can use either of these two identifiers to run a container:

```
docker run -it --rm alpine /bin/ash
```


```
docker run -it --rm 76da55c8019d /bin/ash
```

If you run either of these commands you should find that your command line changes to show a '#' symbol, indicating that you are now inside the docker container.
Have a play around inside the container, where the <a href="https://www-uxsup.csx.cam.ac.uk/pub/doc/suse/suse9.0/userguide-9.0/ch24s04.html">usual Linux commands</a> should work.
<h2>Some Optional Flags</h2>
Even in this simple run command we have included some optional flags to suit our needs.
<em>--rm</em> specifies that the container should be removed when we exit (useful to include this when experimenting),
<em>-it </em> is a shorthand for -i (for interactive) -t (for running like a terminal).
The final component of <em>/bin/ash</em> specifies an initial command that should be run when the container is loaded - in this case the '<a href="https://en.wikipedia.org/wiki/Almquist_shell">ash</a>' shell.

<h2>Exiting the Container</h2>
When you are ready to exit, type and run 'exit' and you should return to your host system. Remember that because we used the '--rm' flag when we started the container, the container will also be removed when we exit.
We can verify this by running

```
docker ps -a
```

Which shows all docker containers on our host system. In this case there should not be any as the test container was removed after exiting.
<h2><b>Named containers</b></h2>
An easy modification we can make to the run command is to give the container a name.  If we don't choose a name for the container, <a href="https://frightanic.com/computers/docker-default-container-names/">docker will randomly assign a name</a> to it.
We can choose a name for the container with the '--name' flag. For example:

```
docker run --name my_alpine_container alpine
```

Check that the container does indeed have the name you chose with:

```
docker ps -a
```

You can remove the container with e.g.

```
docker rm -f my_alpine_container
```

(The '-f' flag forces the container to be removed)
<h1><b>Other ways to run a docker container</b></h1>
So far we've covered some basic ways to run a container, but there are some other useful variations on the docker run command.
<h2><b>Get into a running container</b></h2>
It is also useful to know how to <a href="https://stackoverflow.com/questions/30172605/how-to-get-into-a-docker-container">get into a running container</a>. You can do this with the <a href="https://docs.docker.com/engine/reference/commandline/exec/">exec </a>command.
For example:
Run the container:

```
docker run --name my_alpine_container alpine
```

Then enter into it

```
docker exec -it my_alpine_container /bin/ash
```

You should fine your terminal changes to #, indicating you are in the container.
<h2><b>Port Mapping</b></h2>
For this example we are going extend our alpine image by also pulling down an <a href="https://www.nginx.com/resources/wiki/">nginx </a>server <a href="https://hub.docker.com/_/nginx/">image</a>.
First we pull the nginx:alpine image (by default, <a href="https://blog.docker.com/2015/04/tips-for-deploying-nginx-official-image-with-docker/">nginx uses an ubuntu base</a> which takes the image size from around 20 MB for Alpine to 100MB for Ubuntu).

```
docker pull nginx:alpine
```

We have had to specify the 'tag' of the image. The tag is often used for different versions, or in this case to denote a different base image.
We can run this as before with

```
docker run -it --name mynginx1 nginx:alpine /bin/ash
```

Which allows us to run shell commands from with the container. That's all well and good, but for a web server like nginx (or many other apps and services) we would like access via a <a href="https://en.wikipedia.org/wiki/Port_(computer_networking)">port</a>. The nginx image is configured to open up port 80 for access to the nginx server. This will be the same in every nginx container we start up. There is only one port '80' on our machine, so we need to map other ports on our machine to the port 80 in the image.
There are two ways we can do this:
A) Manually assign the ports. With '-p' we need to specify which port we want to use on our machine. We don't want to create a conflict on our machine, so this could get difficult. E.g.

```docker run --name mynginx2 -p 8888:80 nginx:alpine```

where port '8888' is on our (host) machine.
B) Randomly assign the ports. With '-P' this will randomly map a port on our (host) machine to port 80 in the docker container. E.g.

```docker run --name mynginx2 -P nginx:alpine```

If we randomly select a port from our host machine we need to check which port was selected once the container is up and running. We do this by running

```docker ps```

We can check that our nginx server is working by navigating to 'localhost:&lt;my_port&gt;' where &lt;my_port&gt; is the port we either specified with -p, or were assigned with -P.
<h2>Detached Mode</h2>
Another common way to run a docker container is 'detached' using the '-d' flag. Until now, all of our docker container processes have been attached to our terminal window, running in the foreground. It is often desirable to have docker containers run in the background. We can do this by running in <a href="https://stackoverflow.com/questions/34029680/docker-detached-mode">detached mode</a>.

```
docker run --name mynginx1 -P -d nginx:alpine
```


```
docker run -it --name mynginx1 -P -d nginx:alpine
```

The docker container is started, but you are not immediately presented with the '#' of the container command line, and can continue using the command line on your host machine. To get into the container you would need to get into the running container with 'exec', as described above.
