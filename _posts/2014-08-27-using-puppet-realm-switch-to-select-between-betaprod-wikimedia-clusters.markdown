---
author: tttwrites
comments: true
date: 2014-08-27 07:12:24+00:00
layout: post
slug: using-puppet-realm-switch-to-select-between-betaprod-wikimedia-clusters
title: Using puppet realm switch to select between beta/prod ( Wikimedia clusters
  )
wordpress_id: 630
categories:
- FOSS
- Public
- Technical
- Unix shell
- Wikimedia
tags:
- bash exim4
- beta-prod
- BounceHandler
- puppet
- realm-switch
---

Since the BounceHandler extension is currently installed only in the beta clusters ( Official testing servers of Wikimedia- deployment.wikimedia.beta.wmflabs.org ), writing a custom router in the exim configs of operations/puppet ( configuration repo managed by puppet ) to collect in all the bounce emails and HTTP POST to the extension API seemed risky. This was due to the fact that operations/puppet is meant for production and something beta specific in it, that too continuous API requests dont look sane ( we cant estimate the traffic yet ). 
Marius Hoch ( WMF ) came with the idea of an exim-realm switch, which seemed to solve the issue. You can switch variables between beta and production by:
We edited
[code language="bash"]
$ sudo <editor> templates/exim/manifests/mail.pp
[/code]
and added this before the inclusion of exim4.conf.SMTP_IMAP_MM.erb.

[code language="bash"]
# config - labs vs. production 
case $::realm {
    'labs' : {
	$verp_post_connect_server = 'deployment.wikimedia.beta.wmflabs.org'
	$verp_bounce_post_url = 'http://deployment.wikimedia.beta.wmflabs.org/w/api.php'
    }
    'production': {
	$verp_post_connect_server = 'appservers.svc."${::mw_primary}".wmnet'
	$verp_bounce_post_url = 'http://meta.wikimedia.org/w/api.php'
    }
    default: {
	fail('unknown realm, should be labs or production')
    }
}
[/code]

The internal networks selection was done to make sure the bounce gets POSTed to the right wiki. Now, this configuration can be used in ` exim4.conf.SMTP_IMAP_MM.erb ` by editing the ` bouncehandler ` router by:

[code language="bash"]
command = /usr/bin/curl -H 'Host: <%= @verp_post_connect_server %>' <%= @verp_bounce_post_url %> -d "action=bouncehandler" --data-urlencode "email@-"
[/code]
Hope it helps someone in beta :)
