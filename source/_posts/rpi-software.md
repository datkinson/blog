---
title: Raspberry Pi Cluster - Part 2
date: 2016/3/28 12:47:00
categories:
- Software
tags:
- cluster
- rpi
- raspberry pi
---
### Introduction

In the [previous post](/2016/03/25/rpi-cluster/) I talked about setting up the physical hardware for a home made cluster using Raspberry Pis with the goal of creating a hardware and software stack for learning how to use clustering technologies.

The hardware for the [Raspberry Pi Cluster](/2016/03/25/rpi-cluster/) is in a usable state so the next step is to install software on it.

### Software

I'm aiming for a basic setup that I can keep building upon to get the desired result; A load balanced set of applications that can be scaled.

First step is to install an application into the cluster that will show the user some information.  In this case it will be a simple PHP application, but it can be anything such as NodeJS, Python, Ruby etc...
PHP is just being used as an example.

![PHP Logo](/images/rpi/php.svg "PHP Logo")

One of the Raspberry Pis will need to have a web server installed to server the PHP.  First of all install [raspbian from the official website](https://www.raspberrypi.org/downloads/raspbian/), I used the lite version as the cluster does not need a full desktop environment only a lightweight server.  Instructions on how to do this can be found [here](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).

Once that has been installed installing PHP and a web server is next, again this does not have to be httpd it could be nginx, webrick or anything else.

{% vimhl vim %}
  sudo apt-get install php5-common php5-cgi php5 lighttpd
  sudo lighty-enable-mod fastcgi-php
  sudo service lighttpd force-reload
{% endvimhl %}

### Application

For simplicity I added an index.php to /var/www/html/ which just displays the Raspberry Pis hostname.

{% vimhl vim %}
  <?php print_r(gethostname()); ?>
{% endvimhl %}

![PHP Script Output](/images/rpi/rpi-c.png "PHP Script Output")

I did the same again on another of the Raspberry Pis so that I had 2 different outputs.

![Second PHP Script](/images/rpi/rpi-b-c.png "Second PHP Script")

Now we have 2 nodes in the cluster both running the same application but outputting different content so we can identify which one we have connected to via our web browser.

### Load Balancer

![Load Balancer](/images/rpi/load-balance.svg "Load Balancer")

The load balancer is what is going to distribute the traffic among the different applications but the end user will just go to a single address and all the magic will happen behind that.

For this I am going to use something called [haproxy](http://www.haproxy.org/#desc).  It will take http requests from a web browser over port 80 and redirect them internally to the different raspberry pis.

{% vimhl vim %}
  sudo apt-get install haproxy
{% endvimhl %}

The configuration for the proxy is stored in "/etc/haproxy/haproxy.cfg" and is very simple.  You have to define a front-end and bind it to a port, we will use port 80.  The following can be put at the bottom of the configuration file.

{% vimhl vim %}
  frontend http
    bind *:80
    mode http
    default_backend web-backend
{% endvimhl %}

Now we need to create the web-backend that is referenced in the front-end.

I have custom DNS in my setup so my Raspberry Pis have domain names, you can replace the domain names with the IP address of each of your Pis.
the parts to replace are "rpi-b" and "rpi-c".

The back-end configuration can be added underneath the front-end one as follows:

{% vimhl vim %}
  backend web-backend
    balance roundrobin
    mode http
    server web1 rpi-b:80 check
    server web2 rpi-c:80 check
{% endvimhl %}

Same example again but using IP addresses:

{% vimhl vim %}
  backend web-backend
    balance roundrobin
    mode http
    server web1 192.168.1.100:80 check
    server web2 192.168.1.101:80 check
{% endvimhl %}

The type of load balancing we are using here is "roundrobin" which will cycle through each server with each incoming request.  There are other modes such as "leastload" but I will cover those in a later post.

Once this is done and you have to reload the haproxy:

```sudo service haproxy reload```

Go to your web browser to the address of your Raspberry Pi you just configured with haproxy and keep loading it.  You should see the response cycle between each of your applications in order due to the roundrobin configuration, as you keep refreshing the page.

![Load Balancing](/images/rpi/rpi.gif "Load Balancing")

In summary we configured 3 devices, 2 of those are serving content and the 3rd to balance load between each application.  In my next post I will talk about data storage and how we can balance load across data nodes and how to keep the data in sync.
