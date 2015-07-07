---
author: tttwrites
comments: true
date: 2014-06-06 04:54:44+00:00
layout: post
slug: exim4-generating-a-simple-exim-conf-file
title: 'Exim4: Generating a single exim.conf file'
wordpress_id: 511
categories:
- Exim
- Technical
- Wikimedia
tags:
- exim
- exim.conf
---

Debian split file configuration of exim4 brings in new opportunities, but if your cluster is small, and you are bored to open various folders to configure your router, transport or acl, you can always go for the earlier single `exim.conf`. How much it simplifies things, is a mystery. Problem: * Installed exim4 in the Debian split configuration method, configs files split up all over in conf.d/ neatly * You need to generate the earlier singe `exim.conf` in `/etc/exim4/` Solution: * The solution is pretty straight forward -- found it somewhere in deep in the docs.
[code language="bash"]
sudo cd /etc/exim4/ 
sudo update-exim4.conf --keepcomments --output /etc/exim4/exim4.conf 
[/code]
That will do the trick :) Enjoy. PS: You can even go without ` --keepcomments ` if the comments seem to clutter up.
