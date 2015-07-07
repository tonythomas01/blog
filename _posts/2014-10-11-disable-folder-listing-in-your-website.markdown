---
author: tttwrites
comments: true
date: 2014-10-11 06:02:45+00:00
layout: post
slug: disable-folder-listing-in-your-website
title: Disable folder listing in your website
wordpress_id: 667
categories:
- Unix shell
- Web
tags:
- access denied
- disable folder listing
- folder view
- forbid file
- htaccess
- permission file
- sensitive information
- web hosting
---

Folder listing is an avoidable danger, which you do not want to have in your website. Malicious guys can get access to sensitive information - and you're dead, Jim!

Solution:
Simple addition of a **.htaccess** can be the easy fix.
to block folder view of say folder http://bar.com/foo/

[code language="bash"]
$ cd foo/
$ nano .htaccess
Options -Indexes
[/code]
Save and close, and thats it ! Yay.
Check http://bar.com/foo/ again. 

PS: You can forbid access to foo/file.ext by :
[code language="bash"]
$ chmod 400 file.ext
[/code]
That would make it completely un-available for public eyes!
