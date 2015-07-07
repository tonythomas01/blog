---
author: tttwrites
comments: true
date: 2014-04-29 17:03:01+00:00
layout: post
slug: getting-exim4-running-on-port-25-overriding-default-configs
title: Getting exim4 running on PORT 25, overriding default configs
wordpress_id: 468
categories:
- Exim
- Technical
- Wikimedia
tags:
- exim4
- port 25
- start exim 25
- telnet port 25 fail
---

Last day, while working on one of the wikimedia labs instance, I had to make a box with exim4 running and actively listening on port 25. The labs instance was heavily puppetized, and when I gave 
` $: /etc/init.d/exim4 restart ` 
it showed similar stuff like 
` Stopping MTA for restart           OK
Restarting MTA                       OK ` 
But, when I gave the command 
` $: telnet localhost 25 ` 
I found that the connection timed out. strange! 
How to solve : 
` $: sudo nano /etc/default/exim4 ` 
find the line 
` QUEUERUNNER='queueonly' ` 
change it to 
` QUEUERUNNER='combined' ` 
done ! now 
` $: sudo /etc/init.d/exim4 restart ` 
to test  
` $: telnet localhost 25 `
