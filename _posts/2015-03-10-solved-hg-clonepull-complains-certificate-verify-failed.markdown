---
author: tttwrites
comments: true
date: 2015-03-10 10:36:27+00:00
layout: post
slug: solved-hg-clonepull-complains-certificate-verify-failed
title: '[SOLVED] hg clone/pull complains certificate verify failed'
wordpress_id: 832
categories:
- FOSS
- Technical
tags:
- hg certificate error
- hg clone
- hg ssl
- insecure hg clone
---

If you are behind a firewall, you would probably see something like this happen very often: 
[code language="bash"]
$  hg clone https://user@somewhere.com/myrepo 
abort: error: _ssl.c:504: error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify failed
[/code]
This is a dirty fix for the same [ mind it, we are going to switch off the HTTPS host certificate  authentication check, before cloning] 
[code language="bash"]
$  hg clone --insecure https://user@somewhere.com/myrepo 
[/code]

The insecure way of ** hg pull ** would be 
[code language="bash"]
$ hg pull --insecure
[/code]

Now. If you have your CA certificate alright, you should do something like this one : http://mercurial.selenic.com/wiki/CACertificates
[code language="bash"]
$ nano ~/.hgrc 
[web]
cacerts = /path/to/cacerts.crt
[/code]

Enjoy!
