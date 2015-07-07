---
author: tttwrites
comments: true
date: 2015-01-21 16:45:43+00:00
layout: post
slug: solved-mosh-complains-did-not-find-mosh-server-startup-message
title: '[SOLVED] Mosh complains ''Did not find mosh server startup message.'''
wordpress_id: 817
categories:
- FOSS
- Technical
- Unix shell
tags:
- Did not find mosh server
- mosh
- no file directory
- setlocale
---

Just met this error few minutes before, and here goes the shortest fix : )

**Situation** 
mosh exits with an error message like: 
[code language="bash"]
$ mosh user@somewhere.org
mosh-server: invalid option -- 'l'
Usage: mosh-server new [-s] [-i LOCALADDR] [-p PORT] [-c COLORS] [-- COMMAND...]
setlocale: No such file or directory
Connection to somewhere.org closed.
/usr/bin/mosh: Did not find mosh server startup message.
[/code]
**Solution** 
[code language="bash"]
$ nano /etc/ssh/ssh_config
[/code]
and comment the line 
[code language="bash"]
#SendEnv LANG LC_*
[/code]

Done ! Enjoy mosh ! 
