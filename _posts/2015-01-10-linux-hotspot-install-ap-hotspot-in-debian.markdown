---
author: tttwrites
comments: true
date: 2015-01-10 15:30:24+00:00
layout: post
slug: linux-hotspot-install-ap-hotspot-in-debian
title: '[Linux Hotspot] Install ap-hotspot in Debian'
wordpress_id: 808
categories:
- FOSS
- Technical
- Unix shell
tags:
- ap-hotspot
- create hotspot
- debian wifi android
- infrastructure wifi
---

Sharing Linux wired network with mobile devices is difficult when you consider the simplicity offered by Connectify in the Windows environment. You have a hotspot option by default in the Debian Network Manager - but that creates an **Ad-hoc** type network - and Android phones cannot connect to it by default.
You need to create an **Infrastructure** mode network - and welcome ap-hotspot

Steps:
[code language="bash"]
$ sudo apt-get update && sudo apt-get install hostapd dnsmasq 
$ wget http://ppa.launchpad.net/nilarimogard/webupd8/ubuntu/pool/main/a/ap-hotspot/ap-hotspot_0.2.1-1~webupd8~1_all.deb
$ sudo dpkg -i sudo dpkg -i ap-hotspot_0.2.1-1\~webupd8\~1_all.deb
[/code]

Done ! You can find the updated version of ap-hotspot from http://pkgs.org/ubuntu-12.04/webupd8-i386/ap-hotspot_0.2.1-1~webupd8~1_all.deb.html

You can later configure it by giving
[code language="bash"]
$ sudo ap-hotspot configure
[/code]

Detailed tutorials on configuring ap-hotspot on the same can be found on the web. Thanks ! 
