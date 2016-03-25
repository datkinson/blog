---
title: Docker
date: 2016/3/24 18:00:00
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

With docker you can set up networks between your containers as if each individual container is a physical machine.  With this in mind I set up a bunch of containers each to do one specific job (microservices).

- Load Balancer
- PHP Application
- MySQL Database

In this configuration the load balancer acted in a similar fashion to nginx as a simple proxy, the PHP application interacted with the MySQL server to serve content.

This all worked as you would expect if they were 3 physical machines on a network all communicating with each other.

The next step was to make it actually balance load between multiple applications.

To run this all I did was start another PHP container and another MySQL container.


![Load Balance Diagram](/images/docker/load-diagram.svg "Load Balance Diagram")

The load balancer was set in a very basic configuration of ```Round Robin``` which will just send every incoming request to the next application in the list, in this case it would just switch between the 2 PHP applications in turn.  This is not great as by chance one could be under very little load and the other overloaded when though they are sharing exactly half the traffic each.  This could be because the actions the users accessing the application are performing tasks that require more power than other users.

The next step was to set up health checks and tell the load balancer to always route traffic to the application with the least load.
This was fairly easy for PHP and seemed to work well.  But this was hard to tell with only 2 nodes.


The problem I came into with my testing was that MySQL was locking up due to either too many connections or slowing down trying to process too many writes into the database.

Time to load balance my databases.

You might think they are already split 50/50 but again the load balancer does not know what the users are doing to the database only the strain on the PHP applications.

Enter Galera Cluster

This is a clustering tool you can use for MySQL/MariaDB databases.  This can queue syncing of writes to the database and pick the best available node in the cluster to perform the operation you request.

Again I used docker to set all of this up quite simply linking lots of containers together as if they were hardware.

![Database Cluster](/images/docker/database-cluster.svg "Database Cluster")

This clustering of databases seems to work well so far.  I'm not waiting for previous operations to finish before running the next operation from a different application instance.

I have not yet hit an issue where I'm writing data then reading it back out again and it not being there, which I thought would happen.
The cluster does seem to handle that and not choke.

I will have to run harder stress tests on it and find out.
