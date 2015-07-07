---
author: tttwrites
comments: true
date: 2013-09-10 16:15:44+00:00
layout: post
slug: the-evalbase64_decode-virus-attack-in-wordpress
title: The eval(base64_decode) virus attack in wordpress
wordpress_id: 289
categories:
- Public
- Technical
tags:
- eval
- malicious sites
- plugin virus
- redirects
- theme
- wordpress vulnerability
---

Last day, it came into my notice that our FOSS website, foss.amrita.ac.in gets redirected to some .uk malicious websites, when external links were clicked from websites like Facebook, Google. I was going through the wp-admin->Edit Theme files and it came to my notice that the entire files were infected by a virus which encoded some php code in base_64 encryption.

[![snapshot3](http://tttwrites.files.wordpress.com/2013/09/snapshot31.png?w=604)](http://tttwrites.files.wordpress.com/2013/09/snapshot31.png)
<!-- more -->On decoding, I found that it was responsible for all those malicious redirects.
[![snapshot2](http://tttwrites.files.wordpress.com/2013/09/snapshot2.png?w=604)](http://tttwrites.files.wordpress.com/2013/09/snapshot2.png)
How to remove it:-



	
  1. Disable all plugins and delete all the unwanted plugin files from wp-content/plugins

	
  2. Inorder to find which all files got infected, run a ' grep -r base64 *' under the wp-content folder via ssh or ftp access

	
  3. Delete all plugin folder's which will have the malicious code, for me it was inside a particular plugin, which I removed later to clear all issues.

	
  4. Reinstall the theme files again.

	
  5. Share the website link on facebook, try clicking on it again.


What to be taken care of :-

	
  1. Never leave any file permission above 755. Feel free to give 755 or 754 to folders in wp-content/plugins or wp-content/themes.

	
  2. Make sure that the file permission of wp-config.php is 600.

	
  3. Never install unpopular plugins or themes.


