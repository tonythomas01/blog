---
layout: post
title: "Things I wish was there in the Mailgun code"
description: "Few code issues I noticed while writing an extension to integrate Mailgun with Mediawiki"
category: [Wikimedia]
tags: [mailgun, integrating with Mediawiki ]
---
{% include JB/setup %}

Alright, recently I wrote an extension for Mediawiki ( The code is still getting reviewed in [Gerrit](https://gerrit.wikimedia.org/r/#/c/224984/) ) to make it use Mailgun API to send emails. Mailgun API allows fast and powerful transactional emails in bulk, and its not fair that Mediawiki doesnt have support to it. Phabricator and other services have their own plugins for Mailgun, and the attractive thing about mailgun is - its FREE until 10K emails/month. 

While writing the extension, I came across the following difficulties in the code: 

* The creation of new Mailgun::Connection object doesnt take the **domain** as a variable. 

{% highlight php %}
    $mailgunTransport = new \Mailgun\Mailgun( 'MailgunAPIKey' );
{% endhighlight %}
This should accept the ***domain*** then and there, so that it needen't later be sent at the sending stage. 

* The **BatchMessage** and **MessageBuilder** class should share same function to send an email. 
Currently, ***BatchMessage*** class send an email by: 
{% highlight php %}
	$message->finalize();
{% endhighlight %}
and ***MessageBuilder** class send an email by: 
{% highlight php %}
	$mailgunTransport->sendMessage( 'MailgunDomain', $message->getMessage() );
{% endhighlight %}

This is something I found really weird, and it made me write a condition check in the end, and send the email accordingly using <br>
{% highlight php %}
if ( $message instanceof Mailgun\Messages\BatchMessage ) {
    $message->finalize();
} else  if ( $message instanceof Mailgun\Messages\MessageBuilder ) {
	$mailgunTransport->sendMessage( 'MailgunDomain', $message->getMessage() );
}
 {% endhighlight %}

* Something more to add up, finding the **Exceptions** used in the extension was again a trouble. I had to finally satisfy with 
{% highlight php %}
try { 
	//Code
} catch ( Exception $e ) {
	$e->getMessage();
}
{% endhighlight %}

* Apart from that, everything went cool - and yeah - I plan to write pull requests to [Github:Mailgun-php](https://github.com/mailgun/mailgun-php)

