---
author: tttwrites
comments: true
date: 2014-07-11 09:04:01+00:00
layout: post
slug: mediawiki-restricting-post-requests-to-api-using-ip-whitelisting
title: 'Mediawiki : Restricting POST request''s to API using IP Whitelisting'
wordpress_id: 579
categories:
- Technical
- Wikimedia
tags:
- IP whitelisting
- IP::isInRange
- mediawiki API
- securtiy
---

A simple hack that can make sure that your API doesn't fall into the wrong hands. 
* Firstly, make an array of allowed IPs. This can be in the CIDR format ( 127.0.0.1/32 ) or ususal IP ( 127.0.0.1 ). You can define them in your YourExtension.php as:- 
[code language="php"]
/*Allow only internal IP range to do the POST request */
$wgAllowedInternalIPs = array( '127.0.0.1', '::1' );
[/code]
* Now, on the top of your API definition, add 
[code language="php"]
class ApiBounceHandler extends ApiBase {
	public function execute() {
		global $wgAllowedInternalIPs;
		$requestIP = $this->getRequest()->getIP();
		$inRangeIP = false;
		foreach( $wgAllowedInternalIPs as $BounceHandlerInternalIPs ) {
			if ( IP::isInRange( $requestIP, $BounceHandlerInternalIPs ) ) {
				$inRangeIP = true;
				break;
			}
		}
		if ( !$inRangeIP ) {
			wfDebugLog( 'Extension_name', "POST received from restricted IP $requestIP" );
			return false;
		}
	}
}
[/code]
Please note, IP::isInRange() can take up strings in the format ( 127.0.0.1 or 127.0.0.1/32 - the subnet ).
This will make sure that your API ran for the right IP. Happy Hacking!

