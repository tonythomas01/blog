---
author: tttwrites
comments: true
date: 2014-09-12 13:15:52+00:00
layout: post
slug: creating-self-hosted-puppetmaster
title: Creating Self Hosted puppetmaster in Wikitech labs
wordpress_id: 635
categories:
- FOSS
- Public
- Technical
- Unix shell
- Wikimedia
tags:
- puppet
- puppet configuration
- self puppet master
- wikitech-labs
---

While trying to test an exim-puppet patch ( gerrit.wikimedia.org/r/#/c/155753/ ) which adds a new router in one of my labs instance, I came across the need to create a self hosted puppetmaster. For starters ( like I was few days before ), puppet is a provisioning language, as they call it and applies pre-written configuration files to various daemons and tools coming under its realm. For example, I can set it to generate a standardized `exim4.conf` file when its run, this standardizing file need not be on the local machine you are working on. A self hosted puppetmaster will have all the configuration files packed inside a local directory - which is inside ` /var/lib/git/operations/puppet/ `
Where it come useful :
* It come into use when you want to play around with the default configuration files of your instance.
* When you dont want your changes **not** to be overwritten by the default puppet configured files.
Steps to make your Wikitech labs instance as a self hosted puppetmaster:
* make sure that all previously enabled roles were applied and puppet is running completely. 
[code language="bash"]
$ sudo puppet agent -tv
[/code]
* go to ` Special:NovaInstance ` and select ` configure ` on your preferred instance.
* now, add tick the role `**role::puppet::self** `. This is our required self puppetmaster role
* go to your instance shell and give the command: 
[code language="bash"]
$ sudo service puppetmaster restart
$ sudo puppet agent -tv 
[/code]
* now make sure you have the pupept repo in your local instance. 
[code language="bash"]
$ cd /var/lib/git/operations/puppet/ 
[/code] if the folder exists - Yay! 
Now, you can apply your operations/puppet patches to this folder.
