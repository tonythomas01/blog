---
author: tttwrites
comments: true
date: 2014-07-11 09:18:52+00:00
layout: post
slug: parsing-email-for-relevant-headers
title: Parsing email for relevant headers
wordpress_id: 581
categories:
- PHP
- Wikimedia
tags:
- date and subject
- email headers
- extracting headers
- parse incoming mail
- return-path
- to address
---

Often people love to show off their regex skills, but makes a lot of confusion to people like me trying to understand whats being grepped out. 
Problem :
* Extract the To, Subject and Date from an email, received by POST or whatever. 
Solution :
[code language="php"]
/**
  * Extract the required headers from the received email
  *
  * @param $email
  * @return string
  */
protected function getHeaders( $email ) {
	$emailLines = explode( "\n", $email );
	foreach ( $emailLines as $emailLine ) {
		if ( preg_match( "/^To: (.*)/", $emailLine, $toMatch ) ) {
			$headers[ 'to' ] = $toMatch[1];
		}
		if ( preg_match( "/^Subject: (.*)/", $emailLine, $subjectMatch ) ) {
			$headers[ 'subject' ] = $subjectMatch[1];
		}
		if ( preg_match( "/^Date: (.*)/", $emailLine, $dateMatch ) ) {
			$headers[ 'date' ] = $dateMatch[1];
		}
		if ( trim( $emailLine ) == "" ) {
			// Empty line denotes that the header part is finished
			break;
		}
	}
	return $headers;
}
[/code]. 
Now the headers can be used in the calling function by 
[code language="php"]
$to = $emailHeaders[ 'to' ];
$subject = $emailHeaders[ 'subject' ];
$emailDate = $emailHeaders[ 'date' ];
[/code]
Used here (https://github.com/wikimedia/mediawiki-extensions-BounceHandler).
PS: Please note that Date timestamp will be of the type RFC 2822. (Tue, 17 Jun 2014 05:53:13 GMT ). Happy Hacking again!
