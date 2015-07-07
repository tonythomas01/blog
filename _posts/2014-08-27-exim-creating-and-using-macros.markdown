---
author: tttwrites
comments: true
date: 2014-08-27 06:47:55+00:00
layout: post
slug: exim-creating-and-using-macros
title: 'Exim: Creating and using Macros'
wordpress_id: 625
categories:
- Exim
- FOSS
- Public
- Technical
- Wikimedia
tags:
- exim
- exim regex
- macros
- regex
---

The topic looks easy, but implementing them was a great learning experience, as I found it. Macros helps to make reuse a lot of code, and make the exim configuration look tidy. In the earlier post, I scribbled how to define an Exim regex to capture all VERPed emails as :

[code language="bash"]
begin routers

mw_verp_api:
	driver = accept
	domains = +local_domains
	condition = ${if match{$local_part}{^bounces-\w+-\w+-\w+-\w+$}{true}{false}}
	transport = mwverpbounceprocessor
[/code]

and under transports:

[code language="bash"]
mwverpbounceprocessor:
	driver = pipe
	command = /usr/bin/curl -H 'Host: <%= @verp_post_connect_server %>' <%=@verp_bounce_post_url
	%> -d "action=bouncehandler" --data-urlencode"email@-"
	user = nobody
	group = nogroup

[/code]

Tidying this up a bit, we can make something like:



[code language="bash"]

#Under main configurations 
VERP_BOUNCE_LOCALPART_REGEXP = ^bounces-\w+-\w+-\w+-\w+$
VERP_BOUNCE_POST_URL = http://localhost/api.php

mw_verp_api:
	driver = accept
	domains = +local_domains
	condition = ${if match{$local_part}{VERP_BOUNCE_LOCALPART_REGEXP}{true}{false}}
        transport = mwverpbounceprocessor
[/code]
and under transports
[code language="bash"]
mwverpbounceprocessor:
	driver = pipe
	command = /usr/bin/curl action=bouncehandler --data-urlencode email@- VERP_BOUNCE_POST_URL
	user = nobody
	group = nogroup
[/code]

Hope it helps someone tidy-code :D
