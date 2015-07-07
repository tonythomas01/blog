---
author: tttwrites
comments: true
date: 2014-09-20 03:39:17+00:00
layout: post
slug: testing-a-custom-exim4-conf-file-for-syntactical-errors
title: Testing a custom exim4.conf file for syntactical errors
wordpress_id: 657
categories:
- Exim
- Technical
- Wikimedia
tags:
- exim configuraion
- exim4.conf
- syntactical error exim configuration
- testing exim
---

Often you will come to a scenario when you want to hack the ` exim` configurations and you end up generating a new ` exim4.conf` file. The beauty of exim is that, you can even copy this file from another instance and make it run perfectly in your instance. 
* To make sure that your exim4.conf file contains no syntactical and various other errors :
[code language="bash"]
root@box:~# sudo exim -C </path/to/new/exim4.conf> 
[/code]

For a syntactically perfect exim4.conf, you will receive a welcome message like:
[code language="bash"]
root@box:~# exim -C /etc/exim4/exim4.conf
Exim is a Mail Transfer Agent. It is normally called by Mail User Agents,
not directly from a shell command line. Options and/or arguments control
what it does when called. For a list of options, see the Exim documentation.
[/code]
and in the else case 
[code]
root@box:/etc/exim4# exim -C exim4.conf
2014-09-20 03:36:10 Exim configuration error in line 6 of exim4.conf:
#error message here
[/code]
Happy exim-hacking :)  
Ref: http://www.exim.org/exim-html-current/doc/html/spec_html/ch-the_exim_run_time_configuration_file.htmle
