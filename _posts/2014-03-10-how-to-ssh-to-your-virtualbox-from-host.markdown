---
author: tttwrites
comments: true
date: 2014-03-10 12:21:52+00:00
layout: post
slug: how-to-ssh-to-your-virtualbox-from-host
title: How to ssh your VirtualBox from host (Ubuntu Linux)
wordpress_id: 444
categories:
- Technical
- Unix shell
tags:
- ssh
- virtualbox
---

Last day, I went into a scenario when I had to ssh a Virtual Box (running Ubuntu 12.04) from my host machine. My MediaWiki mentor (Jeff Green) came up with the solution.
Scenario: VM Machine (name - box1, having a user bob, on port 127.0.0.3 after forwarding, and box1 is accessible with an IP 10.0.2.250 from Host)
1) Add the following entry to your box1, Network settings -> Adapter1 -> Port Forwarding 
` 
Name: ssh 
Protocal: TCP 
Host IP: 127.0.03 
Host Port: 2222 
Guest IP:  10.0.2.250 
Guess Port: 22
`
2) Edit your ~/.ssh/config and add the following entries 
`Host box1
Hostname 127.0.0.3
Port 2222
User bob
`
Done :) Now open up the Host terminal and type in 
`ssh box2 ` 
What's done :- When you give ssh box2, the request is forwarded by the ssh sevice as 
` ssh bob@127.0.0.3 -p 2222 `
 and this gets forwarded by the VBox configuration as
[caption id="attachment_446" align="aligncenter" width="415"][![ssh ](http://tttwrites.files.wordpress.com/2014/03/ssh-tunnel14.jpg)](http://tttwrites.files.wordpress.com/2014/03/ssh-tunnel14.jpg) ssh [/caption]`ssh bob@10.0.2.250 -p 22 `
*Similarly, you can forward HTTPS port by
`http|TCP|  | 8080 | 10.0.2.250 | 80`
`https|TCP|  | 8443 | 10.0.2.250 | 443 `
