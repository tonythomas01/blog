---
author: tttwrites
comments: true
date: 2014-07-19 11:11:47+00:00
layout: post
slug: using-pearmimedecode-to-strip-email-bounce-out-of-its-headers
title: Using PEAR::mimeDecode to strip email bounce out of its headers
wordpress_id: 602
categories:
- composer
- FOSS
- PHP
- Snippets
- Technical
- Wikimedia
tags:
- bounce email
- BounceHandler
- email headers
- mimeDecode
- PEAR mimeDecode
---

Writing indigenous email header stripping functions involve tedious work and a lot of regex, as the bounce headers email can be encoded. up/down cased, and saving it, we planned to include the mailMimeDecode class - a pretty straightforward approach. Header stripping is quite easy, and it can be installed via composer too. 
* Prepare your ** composer.json **
[code language="php"]
{
    "require":
    {
        "pear/mail_mime-decode": "1.5.5",
        "pear/pear_exception": "1.0.x-dev"
    }
}
[/code]
* Now, in the mail decode class, add the following to initialize the mimeDecode object
[code language="php"]
<?php
	// mimeDecode configurations
	$params['include_bodies'] = true;
	$params['decode_bodies'] = true;
	$params['decode_headers'] = true;

	$decoder = new Mail_mimeDecode( $email );
	$structure = $decoder->decode( $params );

	$emailHeaders = $structure->headers;
	
	$to = $emailHeaders[ 'to' ];
	$subject = $emailHeaders[ 'subject' ];
	$emailDate = $emailHeaders[ 'date' ];
	$permanentFailure = $emailHeaders[ 'x-failed-recipients' ];
?>
[/code]
Now, you have the To, Subject, Date and X-Failed Recipients headers ready. Please note that, you need to just put the lower-cased default email header-name as 'key' in the $emailHeaders array, to fetch it. 
Yay! Happy Hacking 
