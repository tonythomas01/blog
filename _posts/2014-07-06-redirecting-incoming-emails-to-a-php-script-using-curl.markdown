---
author: tttwrites
comments: true
date: 2014-07-06 17:15:18+00:00
layout: post
slug: redirecting-incoming-emails-to-a-php-script-using-curl
title: Redirecting incoming emails to a PHP script using curl
wordpress_id: 556
categories:
- Exim
- Technical
- Wikimedia
tags:
- bash exim4
- exim4. email to script
- pipe transport
---

While working with the bounce handling project for Mediawiki, we met with a challenge to get the bounce-emails redirected directly to a PHP script, which would accept the email as a ` $_REQUEST['email'] ` variable so that processing is easy and direct. The other version includes storing the emails using an IMAP client such as dovecot, and later retrieving the mails one by one using the PHP script. 
* courtesy [ http://serverfault.com/questions/414148/redirect-all-incoming-mail-into-a-script ].

Assumptions: 
* MTA running exim4 on the receiving end.
* We are redirecting mails to a router ` system_aliases ` and the transport is ` use_pipe ` 
* PHP script located at ` http://localhost/mail.php `
* The PHP script accepts accepts a ` $_REQUEST['email'] ` variable, 
* The working of the script can be verified by writing the contents of ` $_REQUEST[['email'] ` to a ` sample.txt` withing the PHP script.

Problem: 
Redirect the bounce emails to a PHP script using curl

Solution: 
* Edit the ` system_aliases` router: 
` $ sudo nano /etc/exim4/exim4.conf ` 
[code language="cpp"]
system_aliases:
debug_print = "R: system_aliases for $local_part@$domain"
driver = accept
transport = use_pipe
[/code] and edit the use_pipe transport to have: 
[code language="cpp"]
use_pipe:
debug_print = " Using the pipe transport"
driver = pipe
command = /usr/bin/curl http://localhost/mail.php --data-urlencode "mail@-"
user = nobody
group = nogroup 
return_path_add
delivery_date_add
envelope_to_add
[/code]
This will make sure that the receiving email reach the required ` $_REQUEST['POST'] ` in `mail.php` 
Yay. Done. 
PS:- If you want to test whether the email reached the PHP script completely, consider giving in something like this :- 
[code language="php"]
$email = $_REQUEST['email'];
$fh = fopen("sample.txt","a+");
fputs($fh,$text);
[/code]
Now that would put the contents of the email to a file `sample.txt` in the same folder. Happy Hacking! 


