---
author: tttwrites
comments: true
date: 2014-11-22 08:59:40+00:00
layout: post
slug: installing-a-deb-file-in-debianubuntu-variants
title: Installing a .deb file in Debian/Ubuntu variants
wordpress_id: 724
categories:
- Public
- Technical
- Unix shell
tags:
- apt-get
- deb
- debian packages
- installing deb file
---

As the title says - this would be the most simple one step command. Quoting it here as I had a lot of trouble installing these things myself in the start. 

Scenario: 
* install software package **bar/foo.deb**

Solution:
[code language="bash"]
$ cd bar/
$ sudo dpkg -i foo.deb
[/code]

Simple as that :) If you hit with some dependency clashes, you would probably want to give this later: 
[code language="bash"]
$ sudo apt-get install -f 
$ sudo apt-get autoremove
[/code]
to remove any clutter !!

