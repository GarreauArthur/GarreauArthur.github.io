
# A visual guide to how Docker works

The goal of this article is to gain a visual mental model of how docker works
to be able to use it properly. This article doesn't teach how to use docker.

Warnings: This article focus on Linux, and may include inexact assumptions

## TOC

* OS vs Kernel
* Isolation

## the Kernel

The kernel is a software that provide an abstraction layer of the hardware. The
kernel defines how processes, threads, memory, files, networking... work.
Every time a program on a computer needs to interact with the hardware, it will
make a system call to request a service from the kernel.

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
Images are usually based on another image.

### Dockerfile and image layer

Images are made by executing instructions of a **Dockerfile**. A Dockerfile is just
a regular text file that tells the steps to take to create an image. Each
instruction in a Dockerfile creates a **layer**. Layer are also called
**intermediate image**.

Consider this simple Dockerfile to run a NodeJS server:

    FROM node:10
    COPY package*.json ./
    RUN npm install
    COPY server.js ./
    EXPOSE 8080
    CMD ["node", "server.js"]

It will create the following layers:

![Image Node js, dockerfile layers](nodejs_image_layers.png)

A layer is like a "commit" of the filesystem. A file (or directory) can be added,
deleted, or changed in layer. If a file is created in a layer and modified in
another, the entire file will be copied into this layer. So if a file is deleted
in a layer, it will still exist in all the previous layers where it existed.

![Delete file1 in a layer](delete_file1_in_layers.png)

Layers are read-only and uniquely identifiable, which allows to share them
across images. An images contains reference to layers, so several images can
share the same layers.


talk about the order of 
if you copy all your files, everytime you modify a source file, docker will
  rebuild the layers and rerun npm install
but why ? is it true ?

## Containers

TO DO: edit below
Inside a container, you see the image filesystem, but that filesystem is not copied. On top of those image layers, the container mounts it's own read-write filesystem layer. Every read of a file goes down through the layers until it hits a layer that has marked the file for deletion, has a copy of the file in that layer, or the read runs out of layers to search through. Every write makes a modification in the container specific read-write layer.

![container layer](container_layer)

A container is a runnable instance of an image.
We can create, start, stop, move, delete a container.

A container is a group of processes

If a container needs to change a file from the read-only image that provides its
filesystem, it copies the file up to its own private read-write layer before
making the change.

## services

## 






# Go deeper

* cgroups
* namespace

## the sauce

* [What is the difference between a process, a container, and a VM?](https://medium.com/@jessgreb01/what-is-the-difference-between-a-process-a-container-and-a-vm-f36ba0f8a8f7)
* [Digging into Docker layers - Jessica  G](https://medium.com/@jessgreb01/digging-into-docker-layers-c22f948ed612)
* [Dockerizing a Node.js web app](https://nodejs.org/de/docs/guides/nodejs-docker-webapp/)
* <https://stackoverflow.com/a/51660942>
* [Explaining Docker image IDs - Nigel Brown](https://windsock.io/explaining-docker-image-ids/)
