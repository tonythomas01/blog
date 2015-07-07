---
author: tttwrites
comments: true
date: 2014-07-11 08:54:45+00:00
layout: post
slug: post-ing-bounce-email-to-a-mediawiki-api-directly-from-exim
title: POST-ing bounce email to a Mediawiki API directly from exim
wordpress_id: 576
categories:
- Exim
- Technical
- Wikimedia
tags:
- API mediawiki
- bouncehandle
- email to php
- exim
- POST to script
---

While moving forward with the BounceHandler extension, I was advised by my mentors to make sure that the bounce emails are directly fed to an API inside the extension, so that no manual queries are required, and its more safe. 
An API, with the name ` foo ` can be accessed in the URL by ` http://localhost/mw-core/api.php?action=foo`. A POST request with the name ` bar ` can be sent by URL ` http://localhost/mw-core/api.php?action=foo&bar=value`
* How to add the new API
In your extension.php, register the new API, named `bouncehandler` firstly by:

[code language="php"]
$wgAutoloadClasses['ApiBounceHandler'] = $dir. '/ApiBounceHandler.php';
$wgAPIModules['bouncehandler'] = 'ApiBounceHandler';
[/code]

* Make exim forward the emails directly to the API. Put this under the appropriate pipe transport.

[code language="cpp"]
command = /usr/bin/curl http://localhost/core/core/api.php -d "action=bouncehandler" --data-urlencode "email@-" -o /dev/null
[/code]
 or this can be done in a shell script too. You can direct the command to the shell script. 

[code language="cpp"]
command = /path/to/script.sh
[/code]
 and in the script.sh

[code language="bash"]
#!/bin/bash
curl -d &amp;quot;action=bouncehandler&amp;quot; --data-urlencode &amp;quot;email@-&amp;quot; http://localhost/core/mw-core/api.php
[/code]

* Now, on reception of a mail, it gets automatically transferred to the API, with the email as a POST param. The generated POST url will be of the form ` http://localhost/core/mw-core/api.php?action=bouncehandler&email=the_email`
* You can recieve the email POST param in the API by

[code language="php"]
class ApiBounceHandler extends ApiBase {
	public function execute() {
             $email = $this-&gt;getMain()-&gt;getVal( 'email' );
        }
}
[/code]

Yay! further handling of the emails coming up in next post! :) Happy Hacking!
