---
layout: post
title: "A visual introduction to Docker"
date: 2019-09-22
comments: true
tags:
  - Docker
---

# A visual guide to how Docker works

The goal of this article is to gain a visual mental model of how docker works
to be able to use it properly. This article doesn't teach how to use docker.

Warnings: This article focus on Linux, and may include inexact assumptions

## TOC

* Docker Engine
* OS and docker
* Docker objects
  * images
    * Dockerfile and image layer
  * containers
  * volumes (to do)
  * services (to do)
  * stack (to do)


# Docker Engine

The docker engine is a client-server app written in Go. It is made of 3 parts:

* the server, the docker deamon (dockerd) that runs on the host and builds, runs,
distributes containers
* a REST API that other programs can use to talk to the docker deamon
* the CLI client, the `docker` command. (But It can really be any program that
use the REST API to communicate with the docker deamon)

![Image Node js, dockerfile layers](/img/docker/docker_engine.png)

# OS and docker

The goal of docker is to run applications in an isolated environment. Each
application can behave like it's running on its own finely tuned machine. Docker
containers give the same advantages as virtual machines without requiring to
install a full operating system (OS) with a kernel. Instead, Docker containers
share the same OS kernel, the one installed on the host machine (unless the host
is windows?).

## the Kernel

The kernel is a software that provide an abstraction layer of the hardware. The
kernel defines how processes, threads, memory, files, networking... work.
Every time a program on a computer needs to interact with the hardware, it will
make a system call to request a service from the kernel.

## Host OS

The Host OS, also called container host, is the OS on which docker clients and
docker deamons run. The host OS shares its kernel with running docker containers.

## Contained or Base OS

The contained or base OS refers to an image that contains an "OS" (ex: Ubuntu,
CentOS, alpine, windowsservercore...). 

Windows containers require a Base OS while Linux containers do not.

![docker host images and containers](/img/docker/docker_host_image_container.png)

# Docker objects

When using Docker, we create Docker objects:

* images
* containers
* networks
* volumes
* plugins
* ...

## images

An image is a read-only template with instructions for creating a Docker container.
Images are usually based on another image. You can create your own image using
a Dockerfile or by downloading other images in a image registry like
[Docker hub](https://hub.docker.com/).

### Dockerfile and image layer

Images are made by executing instructions of a **Dockerfile**. A Dockerfile is just
a regular text file that tells the steps to take to create an image. Each
instruction in a Dockerfile creates a **layer**. Layers are also called
**intermediate images**.

Consider this simple Dockerfile to run a NodeJS server:

    FROM node:10
    COPY package*.json ./
    RUN npm install
    COPY server.js ./
    EXPOSE 8080
    CMD ["node", "server.js"]

It will create the following layers:

![Image Node js, dockerfile layers](/img/docker/nodejs_image_layers.png)

A layer is like a "commit" of the filesystem. A file (or directory) can be added,
deleted, or changed in a layer. If a file is created in a layer and modified in
another, the entire file will be copied into this layer. So if a file is deleted
in a layer, it will still exist in all the previous layers where it existed.

![Delete file1 in a layer](/img/docker/delete_file1_in_layers.png)

Layers are read-only and uniquely identifiable, which allows to share them
across images. An image contains reference to layers, so several images can
share the same layers.

The reason why you should care about layer is because the order in which they
are created can increase or decrease the build time. If we go back to our
nodeJS example, if we had written:

    FROM node:10
    COPY . ./
    RUN npm install
    EXPOSE 8080
    CMD ["node", "server.js"]

Then everytime we modify a source file, docker will have to re-run `npm install`,
and re-build a layer containing the massive node_moludes directory.

## Containers

A container is a runnable instance of an image. We can create, start, stop, move,
delete a container.

When a container is created, the container stacks its own read-write layer on
top of the image layers.

![container layer](/img/docker/container_layer.png)

Every read of a file goes down through the layers until it finds the file, or
finds a layer that marked the file as deleted, or does not find the file. Every
write will copy the file up to the writable layer before making changes to it.

![container writable layer](/img/docker/container_writable_layer.png)

That's why changes made in a docker container are not persistent. 
You can save the changes made in the container layer with the command
`docker commit`. This will create a new image and save the writable layer as a
"read-only image layer".

## Volumes

TODO

## services

Services allow us to scale containers across multiple Docker deamons, which all
work together as a **swarm** with multiple *managers* and *worders*.
TODO

## stack

TO DO

# Go deeper

* cgroups
* namespace

## the sauce

* [What is the difference between a process, a container, and a VM?](https://medium.com/@jessgreb01/what-is-the-difference-between-a-process-a-container-and-a-vm-f36ba0f8a8f7)
* [Digging into Docker layers - Jessica  G](https://medium.com/@jessgreb01/digging-into-docker-layers-c22f948ed612)
* [Dockerizing a Node.js web app](https://nodejs.org/de/docs/guides/nodejs-docker-webapp/)
* <https://stackoverflow.com/a/51660942>
* [Explaining Docker image IDs - Nigel Brown](https://windsock.io/explaining-docker-image-ids/)

