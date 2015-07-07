---
author: tttwrites
comments: true
date: 2014-02-23 17:12:13+00:00
layout: post
slug: setting-up-smtp-mail-server-for-locally-hosted-mediawiki
title: Setting up SMTP mail server for locally hosted Mediawiki
wordpress_id: 401
categories:
- Exim
- Technical
- Wikimedia
tags:
- email service
- mediawik
- smtp
---

Email service is a MediaWiki Component, which do not come pre-configured and requires some edits to the LocalSettings.php to set up. Basically, you are sending mails from your mediawiki running on your localhost/ or vagrant using the gmail smtp server.



	
  1. You need to install the following packages :

sudo apt-get install php-pear
sudo pear install mail
sudo pear upgrade MAIL Net_SMTP
	
  2. Now edit your LocalSettings.php to include :

$wgEmergencyContact = "apache@localhost";
$wgPasswordSender = "apache@localhost";
$wgNoReplyAddress = "user@gmail.com";

$wgSMTP = array(
'host' => "ssl://smtp.gmail.com",
'IDhost' => "gmail.com",
'port' => 465,
'auth' => true,
'username' => "user@gmail.com",
'password' => "yourPassword"
);


If your firewall doesn't check port 465 && smtp service is unblocked, you are ready to send your mail.  In order to test, go to
localhost/mediawiki/Special:ConfirmEmail
and click on send Confirmation Code. Check your inbox ! :)
Instructions to check whether your port is open will be included in the next post.
Courtesy:https://help.ubuntu.com/community/MediaWiki#Email_Support
