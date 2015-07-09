---
layout: post
title: "Phabricator in OpenShift   Preparing your Catridge [1/7]"
description: ""
category: FOSS
tags: [ 'OpenShift', 'Phabricator in OpenShift', 'PHP Catridge Openshift']
promotion : "Setting up your OpenShift catridge to host Phabricator - the most simple steps"
---
{% include JB/setup %}

This should be the most simple steps in the Phabricator hosting steps. You have online manuals for everything, but I am quoting it here to make things look from 0 to 1. 

## Getting things ready

* Create an account in [www.openshift.redhat.com](http://openshift.redhat.com)
* Create a new app, you can find instructions [here](https://developers.openshift.com/en/php-getting-started.html) and install a PHP latest catridge - which might be **PHP 5.4**.
* Install *MySql** catridge, and a **PHPMyAdmin** too so that we can get the requirements ready.
* Import your **SSH keys** to Openshift so that you can SSH to your phabricator machine.
* Good to go, now login via SSH to your machine. You can find more details [here](https://blog.openshift.com/dive-into-openshift-with-ssh/) 

Something you need to understand now !
		
    The  Apache Document root is pointing to /app-root/repo/index.php

* You need to have your Phabricator setup somewhere in **/app-root/repo/** 


We will be completing that in the next post. Stay Tuned ;) 

