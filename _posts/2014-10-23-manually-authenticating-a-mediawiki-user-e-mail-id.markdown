---
author: tttwrites
comments: true
date: 2014-10-23 17:09:07+00:00
layout: post
slug: manually-authenticating-a-mediawiki-user-e-mail-id
title: Manually authenticating a MediaWiki user e-mail id
wordpress_id: 670
categories:
- PHP
- Public
- Wikimedia
tags:
- eval.php
- manual confirmation email wiki
- manually authenticate email mediaiwki
- manually confirm user
---

While testing with emails and user accounts, you will probably hit with a scenario when you have to create a fake account and make the Wiki send e-mails to it - so that you can analyse the results. Something similar turned up to me today, and thanks to Legoktm & Hoo, here we go:
* Scenario:
You have to manually confirm e-mail id of user 'FooBar'
* Solution: 
[code language="bash"]
$ cd mediawiki/maintenance/
$ php eval.php 
> $user = User::newFromName('FooBar');
> $user->confirmEmail();
> $user->saveSettings();
[/code]
You're done! Navigate to Specail:Preferences to make sure the email id is authenticated ! 
What you did ? You created a User object corresponding to the User Name = 'FooBar'. You can even user ** User::newFromId(123); ** if you know the user id ( You can get it from the 'user' table of your wiki )
Happy Hacking!
