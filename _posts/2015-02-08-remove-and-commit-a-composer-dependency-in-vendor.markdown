---
author: tttwrites
comments: true
date: 2015-02-08 06:33:25+00:00
layout: post
slug: remove-and-commit-a-composer-dependency-in-vendor
title: Remove and commit a composer dependency in vendor/
wordpress_id: 822
categories:
- composer
- Git/gerrit
- Wikimedia
tags:
- composer clash
- composer revert
- mediawiki composer
- remove composer dependency
---

Reverting a composer dependency addition directly via 'Revert Change' from gerrit would break composer, as we experienced after merging https://gerrit.wikimedia.org/r/#/c/188547/.  The patch was to revert Plancake dependency due to compatibility issues in HHVM. I was un-aware of the fact that removing a dependency from `composer.json` would actually remove the dependency references from the vendor/ directory. Summing up - the correct way of producing a removal of a composer dependency would be:



	
  1. Remove the dependency from composer.json

	
  2. run `composer update`

	
  3. git add - -all

	
  4. git commit



A backport to an earlier branch can be produced with the following steps:
[code language="bash"]
git pull --rebase
git checkout -b 'backportTo15' orgin/wmf/1.25wmf15
vi composer.json //remove dependecny
composer update
git add --all
git commt
[/code]

If you screw up your backport in between - this would be an easy fix :
[code language="bash"]
cd vendor
git pull --rebase
git review -d <change_id>
git checkout origin/wmf/1.25wmf15 . // would reset all files to wmf/1.25wmf15
vi composer.json // and remove the un-wanted dependency
composer update
git add --all 
git commit --amend
git review -R
[/code]

Some moments from  wikimedia-dev :)
[17:09:38] tonythomas: You're meant to get composer to update itself. Otherwise it makes a huge mess.
[17:11:28] tonythomas: Yeah, composer and git aren't friends. :-(

