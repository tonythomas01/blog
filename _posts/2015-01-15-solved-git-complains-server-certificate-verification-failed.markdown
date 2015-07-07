---
author: tttwrites
comments: true
date: 2015-01-15 15:32:22+00:00
layout: post
slug: solved-git-complains-server-certificate-verification-failed
title: '[SOLVED] Git complains ''server certificate verification failed''!'
wordpress_id: 811
categories:
- FOSS
- Git/gerrit
- Technical
tags:
- certificate git CA
- git server verification failed
- git ssl
- server verification failed
---

Just met with this error, and here is the hack ! 
**Problem: **
* You are in a public wifi, and usually connect SSL via a Certificate issued by the authority.
* The certificate file is **Downloads/CA_Certificate.cer**
**Solution: **
* Global git fix 
[code language="bash"]
git config --global http.sslcainfo Downloads/CA_Certificate.cer
[/code]

That would do ! do git pull now. 
Happy _hacking!_

