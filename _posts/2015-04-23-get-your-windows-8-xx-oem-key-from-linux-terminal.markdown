---
author: tttwrites
comments: true
date: 2015-04-23 11:41:17+00:00
layout: post
slug: get-your-windows-8-xx-oem-key-from-linux-terminal
title: Get your Windows 8.xx OEM key from linux terminal
wordpress_id: 851
categories:
- Operating Systems
- Public
tags:
- oem key from linux
- retrieve key
- windows 8 key
---

Situation: 
Laptop came with original windows, you did something tricky to install linux - and resulted in removing your entire windows. 

Fix: 
Boot into your Linux OS. If you dont have one, try making a linux bootable USB stick. In terminal,
[code language="bash"] 
sudo hd /sys/firmware/acpi/tables/MSDM
[/code]

This would give your key on the right side of the hex-dump! Enjoy :) 
Courtesy : http://malwaretips.com/threads/how-to-retrieve-your-windows-8-oem-key-with-linux.28560/
