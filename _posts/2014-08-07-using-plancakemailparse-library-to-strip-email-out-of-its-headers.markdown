---
author: tttwrites
comments: true
date: 2014-08-07 14:34:11+00:00
layout: post
slug: using-plancakemailparse-library-to-strip-email-out-of-its-headers
title: Using Plancake::MailParse library to strip email out of its headers
wordpress_id: 606
categories:
- composer
- FOSS
- PHP
- Snippets
- Technical
- Wikimedia
tags:
- BounceHandler
- composer
- parse email
- plancake
- regex
---

Due to some issues with composer loading we had to shift our mail parse library from pear::mimeDecode to a more good looking email parse library by Plancake. Just quoting down how we will employ the library to extract headers from an email:
Add the dependancy to your `composer.json`
[code language="php"]
    "require":
    {
        "floriansemm/official-library-php-email-parser": "dev-master"
    }
[/code]
Now in the mail decode class, add this to perform the extraction:
[code language="php"]
/**
  * Extract headers from the received bounce email using Plancake mail parser
  *
  * @param string $email
  * @return array $emailHeaders.
  */
public function extractHeaders( $email ) {
	$emailHeaders = array();
	$decoder = new PlancakeEmailParser( $email );

	$emailHeaders[ 'to' ] = $decoder->getHeader( 'To' );
	$emailHeaders[ 'subject' ] = $decoder->getSubject();
	$emailHeaders[ 'date' ] = $decoder->getHeader( 'Date' );
	$emailHeaders[ 'x-failed-recipients' ] = $decoder->getHeader( 'X-Failed-Recipients' );

	return $emailHeaders;
}
[/code]
Now you can have the headers ready in $emailHeaders :) yay! 
* The library has no other dependencies and looks neat as a whole. The code can be found here :https://github.com/plancake/official-library-php-email-parser ! Enjoy ! Happy Hacking!
