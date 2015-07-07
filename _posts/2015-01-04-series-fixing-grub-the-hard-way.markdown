---
author: tttwrites
comments: true
date: 2015-01-04 08:14:45+00:00
layout: post
slug: series-fixing-grub-the-hard-way
title: '[Grub] Fixing GRUB the hard way'
wordpress_id: 746
categories:
- GRUB
- Unix shell
tags:
- boot-repair
- debian
- grub
- grub rescue
- live
- not booting
- uefi
---

It's been almost an year since I touched the Linux Grub and for the past two days, I have been paying very well for that. 
Situation: 
* Created Debian Wheezy (7) live USB disk wont boot in UEFI mode ( It just wont show up in BIOS )
* Windows 8.1 is installed in UEFI mode. 
* Debian Wheezy installed in Legacy mode. 
* Grub wont show up - shows grub rescue :\ 
* Tried Boot-Repair : it wont fix as I can only boot the Debian Live in Legacy mode. Boot repair needs Linux to be booted in EFI mode to fix this. Deadlock situation in which the boot repair needs a UEFI booted OS to fix the GRUB and your USB wont boot in UEFI mode.

The following series will be fixing these one by one :) Stay tuned. Happy hacking!
