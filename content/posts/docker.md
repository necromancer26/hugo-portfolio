+++
title = "Docker"
description = ""
date = "2023-07-29T13:36:19+01:00"
tags = ["", ""]
categories = ["", ""]
draft = true
+++
# Docker 🐳
Why docker and why now?
+ Isolation: containers give us similar isolation to vms, containers have their own ip address, filesystem, process space, without the need of full operating system.
+ Environment: containers remove the need to worry about required dependencies and environment required to run the app as it offers a standardized way to run an application no matter the plateform
+ Speed: moving from host to container we can isolate the workloads inside them and safely run the together on the same kernel.
# Image vs. Container
+ An image is the application we want to run
+ A container is an instance of that image running as a process
+ You can have many containers running off the same image
+ Docker default image registry is called "Docker Hub"
# Docker basics
1. docker looks for an image locally in cache, doesnt find anything
2. then looks in remote repositoriy (default to docker hub)
3. downloads the latest version
4. creates a new container 🏺 based on that image
5. gives it virtual ip on a private network inside docker engine
6. opens up port 80 on host and forwards to port 80 in container
7. starts container by using CMD in the image DockerFile
**Running a container**
`docker container run --publish 80:80 nginx`
this command fetches an nginx image from the registry and keeps it running on the background.
to fix the problem we add the `--detach` flag before nginx to keep the container running in the background as a process.
`docker container run --publish 80:80 --detach nginx`
*output*:
`3ed66a4947739...`
**Listing container**
`docker container ls`
this command only shows by default running containers
to list all container use :
`docker container ls -a`
**Stopping container**:
`docker container stop <container-uid/name>`
**Naming a container**:
`docker container run --publish 80:80 --detach --name webhost nginx`
**Removing a container**:
`docker container rm <container-name>`
## Containers vs. VMs
**Containers arent Mini-VM's** even though they are often compared together.
+ Containers are just processes
+ Limited to what ressource they can access
+ Exit when process stops