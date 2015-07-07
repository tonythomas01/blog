---
author: tttwrites
comments: true
date: 2014-06-22 12:12:47+00:00
layout: post
slug: altering-e-mail-return-path-with-exim4-and-php-mailer-in-wikitech-labs
title: Altering e-mail 'Return-Path' with exim4 and PHP mailer in Wikitech Labs
wordpress_id: 545
categories:
- Exim
- FOSS
- Wikimedia
tags:
- headers
- return-path
- verp
- wikitech
---

While implementing VERP, I always found that the 'Return-Path' address of any send email -- was getting rewritten to `root@wikimedia.org`. This was frustrating as I had already changed the ` $header['Return-Path']` many times in the ` UserMailer.php ` and the result was just this one. 
**Problem:- **
* Rewrite custom generated Return-Path to email-headers while sending 
* Implement VERP addressing to handle bounces 
**Solution:- **
*The PHP part:
 + Make sure the UserMailer.php ( or anyother file that sends the mail ) have custom header configurations such as: 
[code 1="=" 2=""php" language="language"]
$headers[ 'Return-Path' ] = 'return-to-here@domain' ;
 mail( $to, $sub, $body, $headers );[/code]
*Now, the exim4 part: 
 + Open your ` sudo nano /etc/exim4/exim4.conf ` and add the following line to the main configuration area: 
( optional )
[code language="bash"]
# Return Path
return_path_remove = false [/code] 
+ Remove the line errors_to from the desired router (( here wiki_mail router  )
[code language="bash"]
wiki_mail:
driver = manualroute
condition = ${if eqi{$header_X-Mailer:}{MediaWiki mailer}}
errors_to = ${if def:h_return-path: {${address:$h_return-path:}} fail}
headers_remove = return-path
transport = remote_smtp
route_list = *     
[/code]
Yay! all done. Now, ` $ sudo /etc/init.d/exim4 restart `
Now test it by sending a mail to some remote id, using ` Special:EmailUser ` 
PS: There is a shorter version, with just removing the ` errors_to` from the **wiki_mail** router. 
