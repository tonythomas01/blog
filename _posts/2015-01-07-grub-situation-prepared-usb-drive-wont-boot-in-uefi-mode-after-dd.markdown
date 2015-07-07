---
author: tttwrites
comments: true
date: 2015-01-07 09:04:58+00:00
layout: post
slug: grub-situation-prepared-usb-drive-wont-boot-in-uefi-mode-after-dd
title: '[Grub] Situation : prepared USB drive wont boot in UEFI mode after dd.'
wordpress_id: 791
categories:
- FOSS
- GRUB
- Technical
tags:
- boot issue
- grub resuce
- linux
- linux debian
- no uefi
- no uefi usb
- wheezy
---

Bah ! If you are in that situation when you created the Linux live USB disk using dd as per my previous post[1] and reboot to find out that the UEFI entry for the USB drive is not listed in the bios boot menu - I bet - You would be frustrated. 

This situation happened almost a dozen times to me - specifically while using debian-7.2-kde-live.iso. Believe me, this can be tackled as far as you are getting the **grub_rescue>** terminal on reboot. 

You can move forward with the installation - that would be a legacy mode installation and of course - you will have to see a grub_resuce terminal once you finish installation.

Situation: 
* Prepared USB drive wont show up as a UEFI entry in the boot-menu ( F10 while booting ) 
* Linux installed in legacy ( no UEFI == Legacy ) - reboot greets you with ** grub_rescue: **
* Reboot shows "Invalid media : blahblah" or something and a **grub_resuce** terminal is seen.

Fix : 
* You can boot directly from the **grub_rescue** terminal !! Find out in my next blog post.

[1]http://tttwrites.wordpress.com/2015/01/04/grub-creating-a-uefi-bootable-linux-usb-drive-using-dd/
