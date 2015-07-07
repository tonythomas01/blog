---
author: tttwrites
comments: true
date: 2015-07-06 12:03:23+00:00
layout: post
slug: hosting-a-phabricator-install-in-openshift-07
title: Hosting a phabricator install in OpenShift [0/7]
wordpress_id: 875
categories:
- FOSS
- Public
- Technical
- Unix shell
tags:
- host phabricator freely
- openshift
- phabricator in openshift
- phabricator install
---

Few days ago, I could finish with a fully functional Phabricator install in OpenShift hosting by Red-Hat. OpenShift[openshift.redhat.com] is a free hosting provider nurtured by Redhat. The hosting service allows you to: 



	
  1. Host atmost 3 small-scale apps for free 

	
  2. Use your own custom domain for the app, like http://phab.amritafoss.in 



I will be writing on how to get your Phabrcator installation up and running in the coming blog posts, and the outline of the whole process would be: 

	
  1. Creating your openshift account, and a new web-app with 'PHP' catridge

	
  2. Installing Phabricator in there following https://secure.phabricator.com/book/phabricator/article/installation_guide/

	
  3. Configuring Phabricator to use the openshift configurations 

	
  4. Writing the `.htaccess` file to finish things 

	
  5. Setting up Mailgun API to handle mails 

	
  6. Adjusting CNAME records in your domain name provider to redirect correctly

        
  7. Wrapping up :) 



Stay Tuned! 
