---
author: tttwrites
comments: true
date: 2014-07-13 15:09:46+00:00
layout: post
slug: writing-a-job-queue-to-deal-with-load-when-post-ing-from-exim-to-mediawiki-api
title: Writing a Job queue to deal with load when POST-ing from exim to MediaWiki
  API
wordpress_id: 588
categories:
- Exim
- PHP
- Wikimedia
tags:
- bounce emails
- BounceHandler
- email headers
- Job runner
- mediawiki API
- mediawiki Job Queue
- POST to script
---

Last day, Tim Landscheidt from Wikimedia [scribbled](http://tttwrites.wordpress.com/2014/07/11/post-ing-bounce-email-to-a-mediawiki-api-directly-from-exim/#comment-54) on my earlier post that I should use a job queue to handle load of the bounce handling API. I talked with Legoktm on this, and he said it was a great idea, as there can be a chance of multiple email bounces reaching the API simultaneously. I will jot down how we made that happen.
*Firstly, register and load the Job handler class 
[code language="php"]
//Register and Load Jobs
$wgAutoloadClasses['BounceHandlerJob'] = $dir. '/includes/job/BounceHandlerJob.php';
$wgJobClasses['BounceHandlerJob'] = 'BounceHandlerJob';
[/code]
* Now, create the file BounceHandlerJob.php extending class BounceHandlerJob from Job. 
I wanted to get the $email, which will be passed from ApiBounceHandler::exectue();
[code language="php"]
class BounceHandlerJob extends Job {
	public function __construct( Title $title, array $params ) {
		parent::__construct( 'BounceHandlerJob', $title, $params );
	}

	/**
	 * Queue Some more jobs
	 * @return bool
	 */
	public function run() {
		$email = $this->params[ 'email' ];

		if ( $email ) {
			// The function in the API where the header 
			// stripping and other stuff happen
			ApiBounceHandler::processEmail( $email );
		}

		return true;
	}
}
[/code]
* Now, we need to make the APIBounceHandler class to receive the POST request, and create a Job queue object so that our objective is accomplished.
[code language="php"]
$email = $this->getMain()->getVal( 'email' );
$params = array ( 'email' => $email );
$title = Title::newFromText( 'BounceHandler Job' );
$job = new BounceHandlerJob( $title, $params );
JobQueueGroup::singleton()->push( $job );
[/code]
Yay ! done. now the public static processEMAIL function needs to be defined with the necessary actions and you are good to go. 
PS: Please add the following to ` LocalSettings.php` to see the results.
[code language="php"]
$wgRunJobRate = 0;
[/code]
To ensure things are working well, run the script 
[code language="bash"]
php runJobs.php
[/code]. Correct errors if any, and the perfect run will output something like.
[code language="bash"]
2014-07-13 15:02:38 BounceHandlerJob BounceHandler_Job email=string(1862) STARTING
2014-07-13 15:02:38 BounceHandlerJob BounceHandler_Job email=string(1862) t=100 good
[/code]. Thanks
