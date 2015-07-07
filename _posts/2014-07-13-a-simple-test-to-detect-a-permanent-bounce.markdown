---
author: tttwrites
comments: true
date: 2014-07-13 18:48:07+00:00
layout: post
slug: a-simple-test-to-detect-a-permanent-bounce
title: A simple test to detect a permanent bounce
wordpress_id: 598
categories:
- Exim
- PHP
- Technical
- Wikimedia
tags:
- bounce handlin
- failed recipient email
- filter soft and hard bounce
- permanent bounce
- php code to parse email
---

There are _n_ chances for an email to get bounced back after being rejected and discussing it all here is out of scope of this post, and are broadly categorized into permanent (hard) and temporary (soft) bounces. Jotting down some reasons for a temporary bounces:



	
  * A server is unavailable or down -Network failure

	
  * The server is overloaded

	
  * Recipient mailbox is over-quota 

	
  * Too long e-mail message 

        
  * Vacation response is on 


The reasons for permanent failures are still many, and those who are desirous, can check [here](http://www.activecampaign.com/help/bounces-soft-bounce-vs-hard-bounce/). 
Only the permanent bounces needs to get parsed, and actions taken upon, while temporary needs to be neglected. Since there are another _n_ number of cases for a bounce to occur, there are _n_ varieties of bounce emails too. We were searching for how to filter only the permanent bounces out.
We hit with this exim4-doc [here](http://www.exim.org/exim-html-current/doc/html/spec_html/ch-how_exim_receives_and_delivers_mail.html) and found that, exim4 adds an **_X-Failed-Recipients:_** header to permanent bounces. Sticking to that, filtering out the permanent bounces is a little regex code. 
[code language="php"]
/**
  * Filter a given boucne for hard or soft
  *
  * @param string $email
  * @return array $headers
  */
protected static function checkForPermanentBounce( $email ) {
	$emailLines = explode( "\n", $email );
	foreach ( $emailLines as $emailLine ) {
		if ( preg_match( "/^X-Failed-Recipients: (.*)/", $emailLine, $failureMatch ) ) {
			$headers[ 'permanentFailure' ] = $failureMatch;
		}
		if ( trim( $emailLine ) == "" ) {
			// Empty line denotes that the header part is finished
			break;
		}
	}

	return $headers;
}
[/code]
Now, on the calling function, you can just check:
[code language="php"]
$permanentFailure = $emailHeaders[ 'permanentFailure'];
if ( $permanentFailure !== null ) {
       //code to do processing!
}
[/code]
Yay! Thats it. 
PS: We sticked to exim, as mchnery uses exim. There are still chances of a bounce from an internal server, and we are working on how to fix that too. Thanks
