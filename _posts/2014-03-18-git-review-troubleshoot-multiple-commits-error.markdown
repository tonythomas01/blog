---
author: tttwrites
comments: true
date: 2014-03-18 13:53:42+00:00
layout: post
slug: git-review-troubleshoot-multiple-commits-error
title: Git-Review troubleshoot:- Multiple commits error
wordpress_id: 454
categories:
- Git/gerrit
- Technical
- Wikimedia
tags:
- bug
- git
- git-review
- mediawiki
- multiple commits
- multiple commits error git
---

Playing with code review tools like gerrit and git-review, one of the common error a user can hit with is the Multiple Commits problem. 
Background: 
* You have checked out a new branch, made your edits, added the files and did git commit with necessary commit message. 
* You give the command 
` git review ` 
and git complains that you are going to submit a number of commits. 
[![A sample error screen after giving git review](http://tttwrites.files.wordpress.com/2014/03/review.png?w=646)](http://tttwrites.files.wordpress.com/2014/03/review.png)
* You can see your commit on the top of the list with `HEAD` along with commit id. 
Fix: 
* give the following in order 
` $ git diff HEAD^ ` This will list down your latest commit. Make sure thats the one you need to commit. 
* ` $ git rebase -i origin/master ` 
This would bring up an interactive git-rebase in your default text editor. 
* Delete all the lines, except the line showing your commit message. 
* Close the editor. Do ` $ git review ` 
and it works :) Thanks!  
