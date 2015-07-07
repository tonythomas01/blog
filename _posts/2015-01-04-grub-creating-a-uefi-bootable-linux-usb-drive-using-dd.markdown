---
author: tttwrites
comments: true
date: 2015-01-04 16:43:26+00:00
layout: post
slug: grub-creating-a-uefi-bootable-linux-usb-drive-using-dd
title: '[Grub] Creating a UEFI bootable Linux USB drive using dd'
wordpress_id: 749
categories:
- GRUB
- Unix shell
tags:
- boot debian
- dd
- dd command
- ubuntu live
- uefi
- uefi boot
- usb
---

First things first, you need to make your USB drive bootable in UEFI. You should :



	
  1. Plug in your pendirve ( minimum 4 Gig ) 

	
  2. Give [code language="bash"] $ sudo fdisk -l [/code]
Find out your USB drive mount name from the output. Hint : You can always check for the drive size and spot that one out. The above command would give something similar to :
[code language="bash"]
# sudo fdisk -l
Disk /dev/sdc: 15.9 GB, 15854469120 bytes
255 heads, 63 sectors/track, 1927 cylinders, total 30965760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x094a46d6
[/code]
You will figure out that /dev/sdc corresponds to your pendrive. For the ease, I would continue with the assumption that /dev/sdc is your USB drive. 


	
  3. Open terminal, move to the place where you have your iso file ready

	
  4. Use dd command to clone the iso to the pendrive
[code language="bash"]
$ sudo if=ubuntu14.iso of=/dev/sdc
[/code]


	
  5. The cloning will take few minutes depending on the speed of your pendrive. Once finished, give the final step : 
[code language="bash"]
$ sync
[/code]


That's it ! You are ready with your UEFI bootable pendrive ! Now restart the system - press F9 or something similar to change the boot order and select :
[code language="bash"]
 SANDISK UEFI BOOT Ubuntu
[/code]
or something similar from the boot menu and boot!

