---
author: tttwrites
comments: true
date: 2014-11-01 18:48:47+00:00
layout: post
slug: contributing-to-mediawiki-for-dummies-from-scratch
title: Contributing to MediaWiki for Dummies  ( from scratch )
wordpress_id: 679
categories:
- FOSS
- Public
tags:
- bug fix
- bugzilla mediawiki
- Contributing to mediaiwki
- gerrit
- start with mediawiki
---

I have written this quick tutorial in super-haste keeping in mind a potential beginner who know little of PHP and a bit of linux operating system. Please mind that I have assumed some typical conditions - and that can vary in between. Sorry for the raw links and bad indentations :)
Here we go:

###Preparing your computer

1. [Install apache, mysql](https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Ubuntu) and make sure [http://localhost/](http://localhost/)[1] shows something up.

2. Follow the Gerrit tutorial from [https://www.mediawiki.org/wiki/Gerrit/Tutorial#Setting_up_Git](https://www.mediawiki.org/wiki/Gerrit/Tutorial#Setting_up_Git)

3. Create accounts both in [http://gerrit.wikimedia.org](http://gerrit.wikimedia.org/) and [http://wikitech.wikimedia.org](http://wikitech.wikimedia.org/)

4. Generate a fresh SSH key and import both to gerrit and wikitech accounts ( check under preferences )

5. Make sure the below command works !
	
			ssh <USERNAME>@gerrit.wikimedia.org -p 29418

6. You would find that that [http://loclahost/](http://loclahost/) points to your folder /var/www/html/ - now to test that, make a file in there called new.php and write
{% highlight php %}
<?php 
	echo "Hello World";
?>
{% endhighlight %}

You would want to change the permission to make the file, and even to make it accessible from the browser. You can change the permission of the folder /var/www/html/ by :
{% highlight bash %}
cd /var/www/
sudo chmod 777 html/*    #This would make all the files and folders inside html folder accessible from everywhere 
sudo chown `whoami` html/  #This would make you the owner of html/. 
sudo touch new.php #Now you can create a file \o
{% endhighlight %}

Now try to access the file new.php from the browser by http://localhost/new.php. If it shows 'hello', then you are good to go! 

###Clone Mediawiki and install skins 
Now clone via SSH only the mediawiki-core to /var/www/html/ using something similar to

{% highlight bash %}
	git clone ssh://USERNAME@gerrit.wikimedia.org:29418/mediawiki/core.git
{% endhighlight %}

* You will have to install a new skin too. Please see that skins are installed in mediawiki-core/skins/. So you would follow [this tutorial](https://www.mediawiki.org/wiki/Download_from_Git#Using_Git_to_download_MediaWiki_skins)  ( You need to start the process by going inside mediaiwki-core/ directory )

	
* Open [http://localhost/mediawiki-core/](http://localhost/mediawiki-core/)  ( sometimes it can be core/ - you need to check what is the location of your MW installation by cd /var/www/html/ - if you see the foldername as core, then you can just do localhost/core/ ). A folder foo under /var/www/html/foo will be accessed from browser via localhost/foo.

### Install Mediawiki	

* Install the Mediawiki, following the steps that would show up in the browser, and in the last step it would download the LocalSettings.php - you copy paste that to the place it would show in the browser ( probably /var/www/core/ ) and you are done - refresh the page.

	
* You can next try installing an extension, say AbuseFilter [2]. You can follow the steps in [2] strictly, clone the extension to core/extensions/. You can check whether the extension install was successful by going to [http://localhost/core/index.php/Special:Version](http://localhost/core/index.php/Special:Version) ( The actual link can change ). If you see the extension listed in the table over there, you are well and good.



###Start your contribution

Now you have MediaWiki running in your system, its time for you to hack things out. You need to visit the bugzilla bug tracker ( [bugzilla.wikimedia.org](http://bugzilla.wikimedia.org/) ). Follow:

* Make an account in [phabricator.wikimedia.org](http://phabricator.wikimedia.org) - The Wikimedia bug tracker 
	
* You can see a lot of bugs listed over there, but the easy-good bugs would be a good way to start. Visit [3] and tick saved searches like 'easy non-assigned bugs' or 'easy-bugs' and things like that. Save it and you will see that these searches will show up in your bugzilla left sidebar. Click on the 'easy non-assigned bugs' and you will get a lot of them. Now, patch can be prepared either to the things in MediaWiki core ( that would be shown as Product: Mediawiki ) or to an extension ( shown as Product: Mediawiki Extension ). Pick one that you think would be easy, clone the extension ( if product == extension ) on which you have to fix the bug ( can be found under Component ). If you see something like Echo over there - clone echo. You might comment something like ' I would like to work on this bug, someone assign this to me ', even though its not required to start working on a bug.

	
* Choose bugs that have minimum number of discussions already for starters, and later you can join in the warfare.

* Before you touch the code, make sure you are following Gerrit tutorial strictly from here [https://www.mediawiki.org/wiki/Gerrit/Tutorial#Update_master](https://www.mediawiki.org/wiki/Gerrit/Tutorial#Update_master) - You need to create a new branch in your git repo and when you do git review - you are actually pushing that branch to Gerrit ( you should know that )

	
* grep is an important shell command that can help you the exact location of a keyword. Like you want to know where the word 'eeb_event_priority' come in the Extension echo - you can cd extensions/Echo/  and on the terminal give a
{% highlight bash %}
	$ grep -R "eeb_event_priority" *
{% endhighlight %}

* Another faster and improved way of grepping would be

{% highlight bash %}
	$ git grep "eeb_event_priority" *
{% endhighlight %}

	
* This would get you the required line that has got the issue, and its upto you to find a way to get the issue fixed.


* If you are adding a localization message, or editing one - please make sure you are editing only the languages/en.json. The other languages get automatically corrected by the translation bot. More info, here[4]


* You can get an idea on fixing front-end or design issues to a minimum level by taking out Inspector in your browser ( pressing Ctrl+shift+I ) and make some hackse there and try to apply it to the code later.


* If you are stuck trying to find a particular line of code that prints something in the browser - grep for what is printed in the browser or you can grep for things that are near to what is being printed in the corresponding repo and you will find the code somewhere around.



* Now you push that one to Gerrit[6] and add reviewers to your patch - This can be mainly people in the CC list of the bug, and so on. You can find strict instructions over here[7], follow that.

	
* Hit with any trouble ? join #wikimedia-dev and #mediawiki on freenode irc - and ask the devs over there. You can find instructions here ( [https://www.mediawiki.org/wiki/MediaWiki_on_IRC/en](https://www.mediawiki.org/wiki/MediaWiki_on_IRC/en)). I personally suggest some cool IRC web-clients like [http://irccloud.com](http://irccloud.com/) or [https://try.waartaa.com/](https://try.waartaa.com/) which have better login and logging facilites.

###Few things to note

* All extensions should be cloned to core/extensions/


* Always use SSH clone from Gerrit  ( git clone ssh :// ... )


* LocalSettings.php - This is the overall configuration file of your MW installation. You can add or remove extensions from here, after you would've cloned the extension.


 Gerrit is the code-review tool used by Wikimedia and is a broker between your code and the original Wikimedia code hosted in Github[5]. You need to get your patch approved from here, and it would become installed in the main repo in few minutes/hours.


[1] [https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Ubuntu](https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Ubuntu)
[2] [https://www.mediawiki.org/wiki/Extension:AbuseFilter](https://www.mediawiki.org/wiki/Extension:AbuseFilter)
[3] [https://bugzilla.wikimedia.org/userprefs.cgi?tab=saved-searches](https://bugzilla.wikimedia.org/userprefs.cgi?tab=saved-searches)
[4] [https://www.mediawiki.org/wiki/Localisation](https://www.mediawiki.org/wiki/Localisation)
[5] [https://github.com/wikimedia](https://github.com/wikimedia)
[6] [https://www.mediawiki.org/wiki/Gerrit/Tutorial#Push_your_change_set_to_Gerrit](https://www.mediawiki.org/wiki/Gerrit/Tutorial#Push_your_change_set_to_Gerrit)
[7] [https://www.mediawiki.org/wiki/Gerrit/Tutorial#Review_before_merge](https://www.mediawiki.org/wiki/Gerrit/Tutorial#Review_before_merge)



