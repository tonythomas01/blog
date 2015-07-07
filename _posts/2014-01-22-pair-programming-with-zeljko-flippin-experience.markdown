---
author: tttwrites
comments: true
date: 2014-01-22 18:23:02+00:00
layout: post
slug: pair-programming-with-zeljko-flippin-experience
title: Pair programming with Zeljko Flippin Experience
wordpress_id: 333
categories:
- FOSS
- Wikimedia
---

 I just had the opportunity to pair up online with one of the Mediawiki Quality assurance developer Zeljko Flippin, from Croatia. I came across this bug ( [Mediawiki: 46887 ](https://bugzilla.wikimedia.org/show_bug.cgi?id=46887)) on removing some variable "sleep" from browser tests and alter the tests in the Mediawiki browser tests. I told I was interested in the same on the bugzilla, and Zeljko came with [2]. We had one of the meeting last wednesday, but that day I was in level 0, and I couldn't even complete configuring my linux to run browser tests. Inorder to run the tests, it required ruby version 2.1 isntalled, but I couldn't configure my rvm to specifically use that version.




[![347px-MediaWiki_Vagrant.svg](http://tttwrites.files.wordpress.com/2014/01/347px-mediawiki_vagrant-svg.png)](http://tttwrites.files.wordpress.com/2014/01/347px-mediawiki_vagrant-svg.png)I found out in the following days that, I can use rvm to select a particular version of ruby gems and got some idea of how a gem was used. The whole browser tests came in a 'Selenium gem' and had to be executed using "cucumber" application. When executed, cucumber executes up a Firefox browser with the latest mediwiki clone and runs a predefined test - say downloading the whole page as a pdf and checks for any errors in the process and reports. Zeljko that day told we can have a session the following week, and I worked on getting my system ready.




<!-- more -->




               Today, 3 of us (Tina, Anu and me) went to the TBI labs, where Arvind ettan and Shankar ettan helped us getting everything setup for the video conference. One another developer (Nick: mayankmadan) too joined us, and we could start the session by about 7:15 pm. For the first half an hour, he showed swiftly how to run the test, detect the failure, and he successfully removed one of the sleep variable and altered the code to work. I never got any clue what he was doing, but nodded my head to everything he told. For the next half hour, he asked me to share my screen, and he tutored me in getting another variable fixed in my own repo. Once, while executing an unknown command, he asked me to wait and asked me whether I had any idea exactly what I was doing. That was a surprise, but I told him what I knew. He added to it, and helped me getting it done, along with explaining what I was doing. And by 8:30 I could push my on patch [3].




               As the program is titled - (Pair programming for Fun and Profit) , it was really fun and one of my first ever experience with a developer in vedio conf. Setting up the environment was one of the most difficult task for me, but somehow I could crack it. I recommend each of the one doing contribution to mediawiki do a bug in Component = Quality Assurance and pair with Zeljko or other and get a browser test bug.







[1] [https://bugzilla.wikimedia.org/show_bug.cgi?id=46887](https://bugzilla.wikimedia.org/show_bug.cgi?id=46887)




[2] [https://www.mediawiki.org/wiki/Pair_programming_Friday_for_fun_and_profit](https://www.mediawiki.org/wiki/Pair_programming_Friday_for_fun_and_profit)




[3] [https://gerrit.wikimedia.org/r/#/c/108918/](https://gerrit.wikimedia.org/r/#/c/108918/)
