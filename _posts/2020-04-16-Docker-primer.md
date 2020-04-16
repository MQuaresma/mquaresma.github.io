---
layout: post
title:  "Docker Primer"
date:   2020-04-16 21:58:42 +0000
categories: devops containers docker
---

# Docker Primer
##  Backstory 
Docker, along with containers, are technologies that I've been trying to understand for quite sometime now,
as I've had to use them more than once. However, I always managed to just Copy-Paste commands without really
understanding how Docker worked under the hood. This meant that, whenever a problem would arise, I'd have to
Google for the solution and be totally lost on whether the solution was actually the right one for the
problem I was facing.  This summer I finally decided to spend sometime reading through some of it's
documentation and, with the help of [Jake Wright's video](https://www.youtube.com/watch?v=YFl2mCHdv24) I
took some notes that I thought could be useful for anyone in the same situation I was in.


##  Terminology 
Here's some terminology to take into account when dealing with Docker:
* Image: 
  * template describing the desired environment
  * steps to build the image are specified in a Dockerfile
  * DockerHub includes a collection of community images that can be customized to suit your needs
* Container
  * running instance of a Docker Image

For those familiar with Object Oriented Programming, you can look at Images as classes and Containers as
objects.  So, with those concepts out of the way, let's now focus on what Docker really is and how to use
it.


##  Brief overview of Docker 
Containers are frequently confused with Virtual Machines however, while macOS does require a Virtual Machine
instance to be running alongside Docker due to the lack of native support (for containers), containers
running in Linux use the host's machine kernel instead of creating an additional one, unlike VMs.  The main
purpose of Docker containers is to provide a reliable environment with which to develop and deploy
applications. Additionally, containers also provide an isolated environment in which to run applications,
even though this isolation is not as strong as in VMs.


##  Usage 
As I've explained previously, the base of Docker are images as they are used to describe a specific
environment.  When you want to spin up a container, you must tell Docker where the image for that container
is.  To obtain images you can either create a Dockerfile and build the image from it:

```
$ docker build -t <image_tag> <Dockerfile_file>
```


or grab one from [Docker Hub](https://hub.docker.com/search?q=&type=image) using docker pull:

```
$ docker pull <image_name>
```


After building an image you can spin as many containers as you want from that image

```
$ docker run <image_id>
```


**Tip:** to launch a container and get an interactive shell use the `-t` flag:

```
$ docker run -it <image_id>
```

Another usefull feature that Docker provides is container orchestration, which facilitates the deployment of
multi-container setups.  The usefullness of this feature lies in the fact that most applications nowadays
are multi-layered systems, where each layer runs in a separate environment but must interact with the other
layers. [Docker compose](https://docs.docker.com/compose/) is a tool provided by Docker that has commands
for managing the lifecycle of multi-layered applications. The initial configuration is achieved via a YAML
file, docker-compose.yml, which indicates the images (or Dockerfiles) used for the containers, called
services, as well as the volumes, ports and dependencies of each service.
