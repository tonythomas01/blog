---
author: tttwrites
comments: true
date: 2014-06-04 19:34:36+00:00
layout: post
slug: git-renaming-a-release-tag
title: 'Git: Renaming a release tag'
wordpress_id: 499
categories:
- Git/gerrit
- Technical
- Wikimedia
tags:
- github
- renaming tag
---

Often you meet with the problem with a release tag, prepared in haste. It can be renamed in a few simple steps. The damage caused due to this may vary. Application can range from - correcting typos to making tag compatible with tools like composer.
**Problem:-**
* Erroneous release tag
**Assumptions**
+ tag_old = old tag 
+ tag_new = new tag (required)
**Solution**
* The approach is pretty simple.
`$ git tag tag_new tag_old
$ git tag -d tag_old ` 
That would create a new tag out of the existing one and kill the old one
` git push origin :refs/tags/tag_old` This will delete the tag in your remote location 
` git push --tags ` This will update the new tag in your remote :)
Bingo! You are done.  
PS: There are alternate ways too. 
