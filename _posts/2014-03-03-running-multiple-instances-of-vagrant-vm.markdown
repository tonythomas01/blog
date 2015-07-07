---
author: tttwrites
comments: true
date: 2014-03-03 16:14:11+00:00
layout: post
slug: running-multiple-instances-of-vagrant-vm
title: Running multiple instances of Vagrant VM
wordpress_id: 421
categories:
- Technical
- Unix shell
- Wikimedia
tags:
- multiple instance
- vagrant
---

Today, I hit with a scenario where I wanted to setup a Mediawiki -Mail server model, so that I can test the working of the main email system. My goal was to implement the handling of mail bounces using VERP as part of my [GSoC proposal](https://www.mediawiki.org/wiki/User:01tonythomas/mediawiki_VERP). My mentors suggested that I should be able to mange two VM's in vagrant - one running the MediaWiki web- server, which will send the mail with the help of the inbuilt php functions and the other box, which would run a plain installation of Ubuntu with a mail-server installed -Exim4. Exim4 is used by the MediaWiki servers.
Setting up two vagrant instances was the difficult part. I am explaining, how I went through.You can get the Mediawiki Vagrant from [here](https://github.com/wikimedia/mediawiki-vagrant)) .
Now, the usual steps for a single instance vagrant-for-MWiki, as [given](http://www.mediawiki.org/wiki/MediaWiki-Vagrant)  is to clone the repo, get inside, and give vagrant up. So, inorder to run multiple instances, we need to understand clearly what happens on vagrant up.

[![Vagrant](http://tttwrites.files.wordpress.com/2014/03/vagrant.png?w=474)](http://tttwrites.files.wordpress.com/2014/03/vagrant.png)
Now, every vagrant has a VagrantFile, which basically controls what all goes inside the box, or what all needs to come up, when 'vagrant up' is given.Going through the [vagrantfile ](https://github.com/wikimedia/mediawiki-vagrant/blob/master/Vagrantfile)) , you can see that
`Vagrant.configure('2') do |config|`
is the main function under which the default configurations for the linux is written. Now, going through (http://docs.vagrantup.com/v2/multi-machine/) will show exactly how to add the two servers.<!-- more -->

/* The boxes I need to add are named "webserver" and "mail"
*I need to have both the VM's under the same private network, so that they will communicate.
*Therefore, I need to assign Box#1 with 10.11.12.10 amd Box#2 with 10.11.12.13.
*Make sure you change all required `vm.box` to `webserver.vm.box`
*Make sure you give different `forwarded_port` to both of your installations.
*Consider giving 1024 to first and 1025 to second better delete the declaration
*`FORWARDED_PORT = 8080` line, and just substitute it with the corresponding port numbers.
*/

Now, inorder to append the existing Vagrant file :
[code language="php"]
Vagrant.configure('2') do |config|
config.vm.define "webserver" do |webserver|
config.vm.hostname = 'mediawiki-vagrant.dev'
webserver.vm.box = 'precise-cloud'
webserver.vm.network :private_network,
ip: '10.11.12.10'[/code]
and continue it till
[code language="php"]
puppet.facter = $FACTER = {
'fqdn' =&gt; config.vm.hostname,
'forwarded_port' =&gt; 1240,
'shared_apt_cache' =&gt; '/vagrant/apt-cache/',
}
end[/code]
after which, add the configurations for your second "mail" box:-
[code language="php"]
config.vm.define "mail" do |mail|
mail.vm.box = 'precise-cloud'
config.vm.hostname = 'eximmail'
mail.vm.network :private_network,
ip: '10.11.12.13'
mail.vm.network :forwarded_port,
guest: 80, host:1250, id: 'http'[/code]
and copy all the code from above from
[code language="php"] # www-data needs .. to
'shared_apt_cache' =&gt; '/vagrant/apt-cache/',
}
end[/code] so that it will have all the properties of the other VM.
And at the last, make sure you `end` the box configs.
Now, fire up the separate boxes with the commands:
[code language="bash"]
vagrant up webserver
vagrant up mail[/code]
Now, follow instructions in (http://askubuntu.com/questions/22743/how-do-i-install-guest-additions-in-virtualbox) to install the LinuxGuestAdditions.Any queries, please comment.
