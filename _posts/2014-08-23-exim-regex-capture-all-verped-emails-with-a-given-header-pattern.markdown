---
author: tttwrites
comments: true
date: 2014-08-23 07:04:57+00:00
layout: post
slug: exim-regex-capture-all-verped-emails-with-a-given-header-pattern
title: 'Exim regex: Capture all VERPed emails with a given header pattern'
wordpress_id: 619
categories:
- Exim
- FOSS
- Public
- Wikimedia
tags:
- API post
- bounce handler
- exim
- exim regex
- verp
---

Consider your VERP generater produces a Return-Path header of the form: 
` **bounces-testwiki-2a-nanrfx-Tn14EQZWaotS2XNn@mytesthost.com **` 
and you want a router to capture all bounce emails having this/similar as the `To` header. This router can serve multiple purpose like - feeding to a bounce processor, silently killing all bounces ( not intended ) or POSTing the email to an API. 
Suppose you have a router named ` **bounceprocessor** ` that HTTP POST to an API named ` bouncehandler `at ` localhost/api.php`, we will design the Regex as:
[code language="bash"]
begin routers

bounceprocessor:
	driver = pipe
	domains = +local_domains
	condition = ${if match{$local_part}{^bounces-\w+-\w+-\w+-\w+$}{true}{false}}
	command = /usr/bin/curl "action=bouncehandler" --data-urlencode "email@-" http://localhost/api.php
	user = nobody
	group = nogroup
[/code]

Please note that
[code language="bash"]
\w = words 
\d = digits 
[/code]

Thanks to Mark Bergsma and Jeff Green for helping me with the regex.
