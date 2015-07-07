---
author: tttwrites
comments: true
date: 2015-01-07 09:39:31+00:00
layout: post
slug: grub-booting-linux-from-a-faulty-grub-rescuing-grub_resuce
title: '[Grub] Booting Linux from a faulty grub - rescuing grub_resuce'
wordpress_id: 794
categories:
- FOSS
- Git/gerrit
- GRUB
- Technical
tags:
- boot from grub
- grub boot
- grub issue
- grub params
- grub rescue
- non-booting grub
---

This would be the most interesting post in the grub series - if you have read the previous ones and you are in the above situation. 

Situation: 
* Grub wont show up - shows an error and grub_resuce> 
* Cannot do boot repair - as the live disc is booting only in Legacy mode - and UEFI entry for the USB drive is missing from the boot menu [1]
* Linux was successfully installed somewhere on your drive - and you forgot where - and you want to boot that one.

Fix: 
I am personally attaching a few screenshots to add beauty to the steps. These are taken from my Virtualbox - where linux was installed as legacy.
* You would have a grub rescue terminal similar to this one: 
[![Grub rescue](https://tttwrites.files.wordpress.com/2015/01/selection_001.png?w=620)](https://tttwrites.files.wordpress.com/2015/01/selection_001.png)
* Find the partition where you installed Linux
[code language="bash"]
grub > ls
(hd0) (hd0,msdos5) (hd0,msdos4)
[/code]
If your partition is a GPT one. ie OS was installed as UEFI : you would find something like :
[code language="bash"]
grub > ls
(hd0) (hd0,gpt5) (hd0,gpt4)
[/code]
* Bruteforce 'ls' to find your Linux partition:
[![ls](https://tttwrites.files.wordpress.com/2015/01/selection_002.png?w=620)](https://tttwrites.files.wordpress.com/2015/01/selection_002.png)
You should be going like ( in GPT ):
[code language="bash"]
grub > ls (hd0) 
grub > ls (hd0,gpt5)
[/code]
until you find out something like 
[![initrd](https://tttwrites.files.wordpress.com/2015/01/selection_006.png)](https://tttwrites.files.wordpress.com/2015/01/selection_006.png)
[code language="bash"]
grub > ls (hd0,msdos1)
Filesystem type ext2 - Last modiifcation date : blahblah
[/code]
The ext2 type of partition shows that you have probably hit the right one. To ensure that:
[code language="bash"]
grub > ls (hd0,msdos1)/
[/code]
[![ls into partition](https://tttwrites.files.wordpress.com/2015/01/selection_003.png?w=620)](https://tttwrites.files.wordpress.com/2015/01/selection_003.png)
Yay ! That looks similar to a standard Linux '/' partition. So you would get that your linux resides in (hd0,msdos1).
* Start the boot procedures.
Before we start - let me copy paste a standard grub: 
[![standard grub](https://tttwrites.files.wordpress.com/2015/01/selection_004.png?w=620)](https://tttwrites.files.wordpress.com/2015/01/selection_004.png)
We will have to give roughly similar params to make sure that our grub boots right.
[code language="bash"]
grub> set root=(hd0,msdos1)
grub> linux /boot/vmlinux-3.2.x.x  root=/dev/sda1
grub> initrd /boot/initrd.img-3.2.x.x 
grub> boot
[/code]
[![boot params](https://tttwrites.files.wordpress.com/2015/01/selection_005.png?w=620)](https://tttwrites.files.wordpress.com/2015/01/selection_005.png)
Hint: You can find out the proper ** root=/dev/sda1 ** with a trick. 
(hd0,msdos1) means /dev/sda1.
(hd0,msdos2) means /dev/sda2.
(hd1,msdos1) means /dev/sdb1.
(hd0,gpt1) means /dev/sda1.
Thats it ! Hit enter - and you will see your installed linux booting !! Yay!
You will find out how to re-install grub in the next post !
