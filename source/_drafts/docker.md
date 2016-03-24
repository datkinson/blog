---
title: Docker
categories:
- Software
tags:
- docker
---

Within my role as a systems administrator I have to set up a number of software services on a regular basis.  An extension of that is also researching and trying out new pieces of technology that could assist the systems and developer I am responsible for supporting.

The way I used to do this was have several servers spare to do testing on or fire up a virtual machine every time I wanted to try something new.

This is fairly resource heavy and time consuming to do, especially when I only have a small amount of downtime to do something useful with.

![Docker](/images/docker/Logo-Docker.svg "Docker")


### Enter Docker

First off, I love this tool.

It helps me quickly evaluate something without having to dive into all of the configuration files and system dependencies a product might require.

What is Docker I hear you ask?
It is a tool that allows you to wrap up an application and system setup into a ```container``` which is portable and should have the same behavior on any system that can run it.
If you want more information than my very brief summary then head over to the [Docker Website](https://www.docker.com/what-docker) and check it out.

This for me is especially useful when having to run the same software stack with the same configuration on 2 different systems such as Centos and Ubuntu.  They are both Linux systems but have differences, mostly subtle from the applications point of view but still it can make a difference.  Docker removes this problem for me.

It also allows me to get everything set up on one system, export it then import it on another in seconds.

### Example

Recently I have been looking into load balancing for web applications, typically PHP and MySQL based ones as that is what the company I work for mainly produces.
