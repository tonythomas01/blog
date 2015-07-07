---
author: tttwrites
comments: true
date: 2013-06-18 03:44:56+00:00
layout: post
slug: getting-into-the-linux-root-grub_editing
title: Getting into the linux root - grub editing
wordpress_id: 165
categories:
- Technical
---

As this page [says](www.linfo.org/root.html) _root_ is the user name or account that by default has access to all commands and files on a Linux or other Unix-like operating system. It is also referred to as the _root account_, _root user_ and the _superuser. _Getting into the linux root is a necessity when talking about privileges and _ let me _show you how to get the easy access.

You shall need :-



	
  1. An Linux operating system -(Ubuntu ,Fedora or anything .. )

	
  2. Direct access to the system, ie you need to restart it alright.

	
  3. The Recovery mode enabled in the GRUB is not a necessity.


The steps :-

	
  1. So, the vector is the GRUB boot loader, we see just after booting on our system :-

	
  2. Here, select the first option , and press 'e' as it says to edit.(Ubuntu,with LINUX ) <!-- more -->[![2](http://tttwrites.files.wordpress.com/2013/03/2.png?w=300)](http://tttwrites.files.wordpress.com/2013/03/2.png).

	
  3. Here edit the line : set root = '(hd0,msdos1x)[![4](http://tttwrites.files.wordpress.com/2013/03/4.png?w=300)](http://tttwrites.files.wordpress.com/2013/03/4.png)' to ' '

	
  4. press F10 to boot and you will get into the root@none shell :D

	
  5. now enter : mount -rw -o remount /
Actually you are remounting the base file-system '/' in rw (read-write) mode so that you can actually change the / contents .

	
  6. now enter the password changing command : passwd

	
  7. enter new passwords :)

	
  8. enter the command : sync      To make the changes permanent (can skip of course.)

	
  9. reboot -f      and you are ready to go :).

	
  10. Now to access root terminal from a local account :- Open the terminal, and type su ; enter the root password and :)


Thank You !

Disclaimer :- Working in the root terminal can cause irrecoverable errors to the system. Please be careful.I shall never be held responsible though. :D
