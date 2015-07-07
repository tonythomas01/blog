---
author: tttwrites
comments: true
date: 2014-09-15 16:53:13+00:00
layout: post
slug: reset-a-muddled-up-git-local-repo
title: Reset a muddled up git local repo
wordpress_id: 654
categories:
- FOSS
- Git/gerrit
- Public
- Technical
tags:
- git commands
- git repo reset
- rebase issue
- reset HEAD git
- reset to master
- screwed up git repo
---

This looks childs play, but often I have heard people wondering how to reset their git local repo once they find they have screwed it enough. This can happen usually due to branches diverging or a badly executed command, or even altering some wanted files.

* To reset the entire repo to the remote branch master:
[code language="bash"]
git stash
git checkout master .
git checkout master
git fetch --all
git pull origin master
git reset --hard origin/master
git rebase origin/master
[/code]
even the same would work without these entire commands, but given all of these, you will have your git repo back to normal and the HEAD pointer pointing to the topmost master commit.

* To reset a single file ` foo/bar.php ` with the remote master:
[code language="bash"]
git checkout master foo/bar.php
[/code]

* If you were in between some rebase, and you need to cancel the same, and get back
[code language="bash"]
rm -fr .git/rebase-apply
[/code]
Yay! Hope it helps someone.
