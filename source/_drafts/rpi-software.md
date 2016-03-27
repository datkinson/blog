---
title: Raspberry Pi Cluster - Part 2
date: 2016/3/27 17:44:00
categories:
- Software
tags:
- cluster
- rpi
- raspberry pi
---

The hardware for the [Raspberry Pi Cluster](/2016/03/25/rpi-cluster/) is in a usable state so the next step is to install software on it.

I'm aiming for a basic setup that I can keep building upon to get the desired result.

First step is to install an application into the cluster that will show the user some information.  In this case it will be a simple PHP application.

![PHP Logo](/images/rpi/php.svg "PHP Logo")

One of the Raspberry Pis will need to have a web server installed to server the PHP.  First of all install [raspbian from the official website](https://www.raspberrypi.org/downloads/raspbian/), I used the lite version as the cluster does not need a full desktop environment only a lightweight server.  Instructions on how to do this can be found [here](https://www.raspberrypi.org/documentation/installation/installing-images/README.md).

Once that has been installed installing PHP and a web server is next.

{% vimhl vim %}
  sudo apt-get install php5-common php5-cgi php5 lighttpd
  sudo lighty-enable-mod fastcgi-php
  sudo service lighttpd force-reload
{% endvimhl %}

For simplicity I added an index.php to ```/var/www/html/``` which just diplays the Raspberry Pis hostname.

{% vimhl vim %}
  <?php print_r(gethostname()); ?>
{% endvimhl %}

![PHP Script Output](/images/rpi/rpi-c.png "PHP Script Output")
