---
author: tttwrites
comments: true
date: 2015-06-29 10:47:14+00:00
layout: post
slug: sharing-your-linux-folders-with-android-over-ftp-samba-es-explorer-12
title: Sharing your Linux folders with Android over FTP [ Samba + ES Explorer ] [1/2]
wordpress_id: 854
categories:
- FOSS
- Public
- Technical
- Unix shell
tags:
- file share
- ftp secure linux
- linux android
- samba
- sharing file
- sharing file samba
---

As a kid, I remember setting up file sharing in my local WiFi with my windows machine, and yesterday, I thought of doing the same with my Linux machine and Android phone.
Problem:
You need to share your files in `/media/sam/mypics` with your Android phone.
Requirements:



	
  1. GNU/Linux machine with internet connections

	
  2. Android phone with ES-Explorer installed


Approach:
**Install FTP server and samba file share in your linux machine with login. Access it via your ES Explorer. **
Steps:



	
  * **Install SAMBA**



You need to setup and install samba in your linux machine. You can get it by


[code languages="bash"]
$ sudo apt-get update
$ sudo apt-get install samba
[/code]


	
  * **Create a samba username and password**


You can use your own login name as your FTP username to access the file system, but you need to create a separate samba password to access the same. This is recommended as you need not give your original password to someone who you wish to share your files with. Considering we are making for username sam.

[code languages="bash"]
$ sudo smbpasswd -a sam
[/code]


	
  * **Configure samba so that you can share `/media/sam/mypics` with the public**


The tricky steps are up.

[code languages="bash"]
$ sudo nano /etc/samba/smb.conf
[/code]

Add the following to the end of the file

[code languages="bash"]
[mypics]
path = /media/sam/mypics
available = yes
valid users = sam
read only = no
browseable = yes
public = yes
writable = yes
[/code]



	
    1. **Restart `samba-server` so that the changes take place**

[code languages="bash"]
$ sudo /etc/init.d/samba restart
$ sudo /etc/init.d/smbd restart
[/code]





Bravo! Your FTP server is up. I will talk about accessing the same via an android phone in the next post. Stay tuned!
