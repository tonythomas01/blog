---
author: tttwrites
comments: true
date: 2015-03-10 16:30:34+00:00
layout: post
slug: reflecting-changes-in-your-python-web-app-without-restarting-apache
title: Reflecting changes in your python web-app without restarting apache
wordpress_id: 834
categories:
- FOSS
- Snippets
- Technical
- Unix shell
- Web
tags:
- apache wsgi update web app
- django update website
- reflect changes python
- wsgi file update
---

This would be a pretty simple hack, and concern the devs using python web frameworks - hosted with apache-wsgi. The Django help to deploy a web-app on the apache server can be found over here[1].
In either way, you will have your apache configuration pointing to the path of the wsgi file of your web-app. You will have something similar to the following in your apache conf. 
[code language="bash"]
WSGIScriptAlias /mysite  /path/to/your/application.wsgi
[/code]

Now - problem come when you have made some local changes to your repo, and do not have sudo privilege to restart your webserver to make the changes take effect. You can fix the same with this simple hack. 
[code language="bash"]
$ touch /path/to/your/application.wsgi
[/code]

touch command[2] in GNU/Linux can do wonders! It can create a new file ( if not exist ), and can refresh the timestamp if one exists.

[1] https://docs.djangoproject.com/en/1.7/howto/deployment/wsgi/modwsgi/
[2] https://en.wikipedia.org/wiki/Touch_(Unix)
