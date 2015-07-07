---
author: tttwrites
comments: true
date: 2015-06-30 14:59:49+00:00
layout: post
slug: sharing-your-linux-folders-with-android-over-ftp-samba-es-explorer-22
title: Sharing your Linux folders with Android over FTP [ Samba + ES Explorer ] [2/2]
wordpress_id: 862
categories:
- FOSS
- Public
- Technical
- Unix shell
- Web
tags:
- access file from android
- es explorer ftp
- ftp linux
- linux file share
- linux FTP access android
---

You would've got how to start files sharing `samba` service running in your linux machine in the previous post ( If you haven't yet [[part1](https://tttwrites.wordpress.com/2015/06/29/sharing-your-linux-folders-with-android-over-ftp-samba-es-explorer-12/)] ). Now lets go to the fun part - accessing the file system from your Android phone.

**Problem: **
You need to access the samba shared files in `/media/sam/mypics` from your Android phone.
**Requirements:**



	
  1. Android phone with ES-Explorer or similar app installed

	
  2. Your linux machine having samba service running


**Approach: **
The approach is still the same:
Install FTP server and samba file share in your linux machine with login. Access it via your ES Explorer in Android phone
**Steps**



	
  1. Setup a WiFi hotspot in your Android phone, and connect your laptop with it[![makingHotspot](https://tttwrites.files.wordpress.com/2015/06/makinghotspot.png)](https://tttwrites.files.wordpress.com/2015/06/makinghotspot.png)

	
  2. Obtain the IP address of your Linux machine by `sudo ifconfig`

	
  3. Open ES-Explorer in your Android phone, and go to LAN -> Add new as per the figure[![unnamed](https://tttwrites.files.wordpress.com/2015/06/unnamed.png)](https://tttwrites.files.wordpress.com/2015/06/unnamed.png)

	
  4. Give the IP address of the Linux machine you got, and the username and password as what you gave while setting up Samba ( ref: [[part1]](https://tttwrites.wordpress.com/2015/06/29/sharing-your-linux-folders-with-android-over-ftp-samba-es-explorer-12/) ).[![addingFTP](https://tttwrites.files.wordpress.com/2015/06/addingftp.png)](https://tttwrites.files.wordpress.com/2015/06/addingftp.png)

	
  5. Next time, you can see that your FTP server automatically shows up !
[![listingConnected](https://tttwrites.files.wordpress.com/2015/06/listingconnected1.png)](https://tttwrites.files.wordpress.com/2015/06/listingconnected1.png)

	
  6. Enjoy :)


