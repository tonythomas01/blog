---
author: tttwrites
comments: true
date: 2014-06-13 06:40:17+00:00
layout: post
slug: using-imap-with-dovecot-in-wikitech-labs-instance
title: Using IMAP with dovecot in Wikitech labs instance
wordpress_id: 538
categories:
- Exim
- Public
- Unix shell
- Wikimedia
tags:
- dovecot
- imap
- wikitech-labs
---

While working with the VERP project, we thought of installing a `dovecot` IMAP environment and alter the `local_delivery` to a `Maildir` in ` $home/Maildir` according to https://nsrc.org/workshops/2005/pre-SANOG-VI/bc/mail/maildir.htm
Problem: 
* Set up and open IMAP in labs instance 
Solution: 
* First install dovecot using the commands 
` sudo apt-get install dovecot-imapd dovecot-pop3d`
and edit `etc/dovecot/dovecot.conf:` to add 
` protocols = imap imaps`
Configure Mailboxes 
`mail_location = maildir:~/Maildir`
and now, if you are using ` exim4 ` as your mailer 
go to ` /etc/exim4/exim4.conf `
and edit the `local_delvier` part to [2]:
`
local_delivery:
  driver = appendfile
  directory = $home/Maildir
  maildir_format
  maildir_use_size_file
  delivery_date_add
  envelope_to_add
  return_path_add
`
Now you have done with dovecot, and exim -- time to open up the `IMAP` port ` 143 ` 
in terminal, give: 
` # sudo iptables -A INPUT -p tcp --dport 143 -j ACCEPT ` 
and give ` reboot` to reboot the system
now, to test things are working, give 
` # telnet localhost imap ` 
if you see a connection refused, you will have to add the IMAP port (143) to the ` Wikitech-I labs [Manage Security Groups](https://wikitech.wikimedia.org/wiki/Special:NovaSecurityGroup).
now, again reboot, if necessary -- and do ` # telnet localhost imap ` 
and you will recieve the telnet shell :) Horray 
* References:  
[1] https://help.ubuntu.com/community/Dovecot
[2] https://nsrc.org/workshops/2005/pre-SANOG-VI/bc/mail/maildir.htm
