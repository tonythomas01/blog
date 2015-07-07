---
author: tttwrites
comments: true
date: 2014-11-09 15:37:17+00:00
layout: post
slug: resolved-bluetooth-loading-patch-failed-in-debian-wheezy
title: '[Resolved] Bluetooth : Loading patch failed in Debian Wheezy !'
wordpress_id: 704
categories:
- FOSS
- Public
- Technical
- Unix shell
tags:
- atheros
- Bluettoth
- failed bluetooth
- loading patch file
- wheezy
---

Before we start - special thanks to my friend [Tina](http://tinaj1234.wordpress.com/) for finding out the necessary fix for this error ( I dont do much kernel stuff ). Almost one year pass since I moved to Debian Wheezy stable - and I had this funny little ( humongous ) problem with my laptop - Bluetooth adapter was not getting detected, and I couldn't sent/receive a single file from any single devices :\
I searched a bit ( wrong ) in Google but never cracked a hint, but today I am happy - we got it fixed.
Problem:
During boot time you get this error

[code language="bash"]
Bluetooth: Loading patch file failed
[/code]

and once the Debian boots up - you are left with no Bluetooth. Keep in mind, this works for only ** Atheros ** adapter - and you can find yours by

[code language="bash"]
$ dmesg | grep Blue
[    2.262111] usb 3-1.1: Product: Bluetooth USB Host Controller
[   11.837440] Bluetooth: Core ver 2.16
[   11.837459] Bluetooth: HCI device and connection manager initialized
[   11.837462] Bluetooth: HCI socket layer initialized
[   11.837464] Bluetooth: L2CAP socket layer initialized
[   11.837471] Bluetooth: SCO socket layer initialized
[   11.884260] Bluetooth: Generic Bluetooth USB driver ver 0.6
[/code]

* Solution :
Simple command !

[code language="bash"]
sudo apt-get install firmware-atheros
[/code]

Re-boot and once you are up - you will find your bluetooth working ! yay ! I still dont understand - why this never came bundled with the OS - and I'm no Kernel Janitor, so exit();
