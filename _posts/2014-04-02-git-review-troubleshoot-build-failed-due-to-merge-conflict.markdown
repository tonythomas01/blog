---
author: tttwrites
comments: true
date: 2014-04-02 14:09:33+00:00
layout: post
slug: git-review-troubleshoot-build-failed-due-to-merge-conflict
title: Git-Review troubleshoot :- Build failed due to merge conflict
wordpress_id: 461
categories:
- Git/gerrit
- Technical
- Wikimedia
tags:
- gerrit
- git
- git-review
- rebase
---

This error is caused due to merge conflicts between your working branch and master.
Background: 
* The master branch have changed while you were busy working on your branch. 
* You made some \unacceptable\ changes. 
How to: 
[caption id="attachment_462" align="aligncenter" width="480"][![git-rebase](http://tttwrites.files.wordpress.com/2014/04/git-rebase.png)](http://tttwrites.files.wordpress.com/2014/04/git-rebase.png) git-rebase[/caption]
* Checkout to the master branch. 
` $ git checkout master ` 
* Hard reset to your original master branch 
` $ git fetch --all ` 
` $ git reset --hard origin/master ` 
[optional]
` $ git pull origin master ` 
* Checkout to the working branch 
` $ git review -d ` 
* Rebase the patch with master 
` $ git rebase master ` 
# The conflicts will be listed. The easiest way to fix a conflict is to checkout that file with the master. Eg: for a file bar.foo causing problems - do : 
` $ git checkout master bar.foo ` 
REMEMBER:- you need to `add` the files after you have made the changes  via
` $ git add bar.foo `
# Once you have fixed all the errors, continue with the rebase process. 
` $ git rebase --continue ` 
* Amend git commit- This would make sure the new PS would not be sent as a new Change, but as a new Patch set.
` $ git commit --amend  ` 
* Push the code 
` $ git review -R `  

PS:- If you hit with an error while rebasing, always delete the rebase files 
` $ rm .git/rebase-apply ` 

