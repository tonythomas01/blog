---
author: tttwrites
comments: true
date: 2014-06-05 19:23:21+00:00
layout: post
slug: composer-loading-specific-tags-instead-of-branches
title: 'Composer : Loading specific ''tags'' instead of ''branches'''
wordpress_id: 506
categories:
- composer
- Git/gerrit
- Technical
- Wikimedia
tags:
- composer
- github
- tags
---

The beauty of composer comes to play when we want to have a custom fork of a software, say hosted in Github to be autoloaded. Again, introducing composer to people who are new:-
Quoting from https://getcomposer.org/doc/00-intro.md


<blockquote>Composer is a tool for dependency management in PHP. It allows you to declare the dependent libraries your project needs and it will install them in your project for you.</blockquote>


The docs tells exactly how to load a developement branch, using the ` dev-` prefix (https://getcomposer.org/doc/05-repositories.md#vcs)
Problem:
* You want to load a custom release tag version from Github
+ You want to load release tag - `5.0-patch` from Github repo of monolg
Solution:
* Edit the composer.json`
{
"repositories": [
{
"type": "vcs",
"url": "https://github.com/igorw/monolog"
}
],
"require": {
"monolog/monolog": "5.0-patch"
}
}
`
* save it, run `$ composer update `
There you go ! :) Thanks
