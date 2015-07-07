---
author: tttwrites
comments: true
date: 2014-06-06 19:58:18+00:00
layout: post
slug: forwarding-mails-to-a-php-script-with-exim4
title: Forwarding mails to a PHP script with exim4
wordpress_id: 526
categories:
- Exim
- Technical
- Unix shell
- Wikimedia
tags:
- exim
- forwarding mails
- php forward
- pipe transoprt
---

Forwarding mails to a script enables the Mail admin to work around with the incoming email a bit, before it gets delivered. A VERP address check, destination or sender address extraction, SPAM checks, and a lot more can be done by these e-mail parsing. 
**Problem:**
* You have a mail addressed to `root@localmac` and you need to get it directed to a script, located at ` /var/mail/script.php`
* You have exim4 running on port25
* You have got ` root : root ` in /etc/aliases - meaning emails to root get delivered to root. 
* You have got ` domainlist local_domains = +system_domains ` in your ` exim4.conf `
Solution: 
Just to start from the basics: 
* add the following to the `/etc/exim4.conf`

under begin_routers: [code language="cpp"]
# Use the system aliasfile /etc/aliases for system domains
system_aliases:
	driver = accept
	domains = +local_domains
	transport = use_pipe
[/code]
under begin_transport: [code language="cpp"]
use_pipe:
	debug_print = " Using the pipe transport"
	driver = pipe
	command = /etc/exim4/script.php
	return_path_add
  	delivery_date_add
	envelope_to_add
	return_output
[/code]
Now, exim is good to go. Thinking of what you will put up in the script.php ?
You can always find it here https://github.com/tonythomas01/exim4box1verp/blob/piped/script.php
Now, test the entire settings by :
` 
# exim -bt root@localmac
>root@localmac
>router = system_aliases, transport = use_pipe
# mail -s "Subject" root@localmac
Type the body here. Click ctrl+D to quit
` now check in the **exim logs**
`# nano /var/log/exim4/mainlog ` It will have something like 
`
2014-06-06 18:49:06 1WszCM-000360-D6  root  R=system_aliases T=use_pipe
2014-06-06 18:49:06 1WszCM-000360-D6 Completed
`
The message_id, date and time will vary though :P
PS:- This looks like my B'day post. I am 20 :)
