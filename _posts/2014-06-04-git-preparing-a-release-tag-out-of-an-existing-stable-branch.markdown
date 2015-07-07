---
author: tttwrites
comments: true
date: 2014-06-04 19:21:38+00:00
layout: post
slug: git-preparing-a-release-tag-out-of-an-existing-stable-branch
title: 'Git: Preparing a release-tag out of an existing stable branch'
wordpress_id: 495
categories:
- composer
- Git/gerrit
- Wikimedia
tags:
- branch
- composer
- github
- release-tag
---

Just to mention what branches and tag are, A tag represents a version of a particular branch at a moment in time. A branch represents a separate thread of development that may run concurrently with other development efforts on the same code base[1].
Now, last day I hit into a situation of creating a release tag for the WMF cluster out-of the swiftmailer v5.2.0 stable release.
we will use
`
foo - our repo
v1.2 - the latest stable release tag in a newly created branch foo/1.2
`
**Problem**:- 
* The source master-branch is buggy, and you want to impress by taking up their latest stable branch (v1.2).
* You want to push some patches into the checked-out (v1.2) branch, and make it a new release-tagged as v1.2-bar.
**WorkFlow**:- 
* clone the local fork of the repo. (If you have write access, the main one itself)
* create a branch starting from the v1.2 tag. 
` $ git checkout v1.2 ` 
you will reach a detached head state
` $ git checkout -b foo/1.2 `
now you are in a new branch foo/1.2 ` git status ` to verify that
* now work around the code, fix up the first patch. After committing
` $ git push origin HEAD ` 
This will push all the latest branch and commit into the repo. Continue this for all the patches.
**Creating a new release tag:**
* Now once all the patches are done and pushed into the repo, do
` git tag v1.2 `
` git push origin HEAD ` 
bingo! You will have your new tag ready for release :). Thank You
[1]http://stackoverflow.com/questions/1457103/what-is-the-difference-between-a-tag-and-a-branch-in-git
