---
author: tttwrites
comments: true
date: 2014-10-31 06:41:37+00:00
layout: post
slug: js-removing-trailing-dots-from-a-string
title: 'JS: Removing trailing dots from a string'
wordpress_id: 673
categories:
- FOSS
- jQuery
- Public
- Snippets
tags:
- jquery remove trailing dots
- regex jquery to remove last character
- remove last character from jquery string
- trim jquery
- trim trailing dots in srting js
---

Met with this bug https://bugzilla.wikimedia.org/71704 in the UploadWizard extension last day, which was to make sure that the file name string do not contain dots or whitespace as that can cause trouble later. Thanks to Mark Traucer ( Wikimedia ), we got a wonderful solution for the same.

Problem:
Remove trailing dots from a string foo.
Solution:

[code language="js"]
cleanedFoo = $.trim( foo.replace( /\.+$/g, '' ) );
[/code]

That would remove 'n' number of dots trailing in string foo
My personal solution to this was a bit more easy, but would work with only one trailing dot:

[code language="js"]
if ( foo.slice( -1 ) === '.' ) {
        cleanedFoo = foo.slice( 0, -1 );
}
[/code]

The change is in gerrit : https://gerrit.wikimedia.org/r/#/c/169326/. :)
Happy Hacking !!
