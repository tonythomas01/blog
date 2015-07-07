---
author: tttwrites
comments: true
date: 2015-01-01 15:41:27+00:00
layout: post
slug: shift-from-local-dns-to-google-dns
title: Shift from local DNS to Google DNS
wordpress_id: 737
categories:
- FOSS
- Public
- Technical
- Unix shell
- Web
tags:
- acess blocked
- check dns
- github
- google dns
- linux dns
---

Shifting to Google DNS than local ISP has become essential one of these days, and here we go: DNS stands for Domain Name Resolution service and essentially converts our requests to web address to its raw IP form. Its like : You request for : www.google.com ---->[ ISP DNS Server ]----->( resolves to IP )-----> Your System connects to IP. 1 ) Using terminal:

[code language="bash"]
sudo nano /etc/resov.conf
[/code]

and add the following to the end of the file

[code language="bash"]
nameserver 8.8.8.8
nameserver 8.8.4.4
[/code]

restart networking using :

[code language="bash"]
sudo /etc/init.d/networking restart
[/code]

2 ) Graphical Way:![Selection_020](https://tttwrites.files.wordpress.com/2015/01/selection_020.png) And restart the network. **Detect your current DNS** To test settings are correct - give this:

[code language="bash"]
dig github.com
[/code]

and check for the ** SERVER ** para matches

[code language="bash"]
;; SERVER: 8.8.8.8#53(8.8.8.8)
[/code]

Edit : You can use multiple alternatives like Open DNS ( https://www.opendns.com ) etc. to get the same effect. Enjoy !
