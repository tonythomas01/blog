---
author: tttwrites
comments: true
date: 2014-11-13 17:04:32+00:00
layout: post
slug: mwwgextensionfunctions-run-a-function-when-an-extension-is-evoked
title: '[MW]$wgExtensionFunctions : Run a function when an extension is evoked'
wordpress_id: 719
categories:
- FOSS
- PHP
- Snippets
- Technical
- Wikimedia
tags:
- $wgExtensionFunction
- extension development
- mediawiki
- set mediawiki global
---

Working further with making the BounceHandler extension more production friendly - we came up with a scenario in which I wanted some of the extension global variables to take values from a MediaWiki global variable. It would've looked like $myExtensionGlobal = $mwGlobal - which looks weird.
Thanks to Hoo( WMDE ), I got introduced to **[$wgExtensionFunctions[]](https://www.mediawiki.org/wiki/Manual:$wgExtensionFunctions) **[1]

Scenario:
You need to run a function once your extension gets loaded. In my case, I want to check if $wgFoo ( which defaults to null ) was set in the original myExtension.php and if not - set it to the MW global - $wgBar
Solution:
in your myExtension.php

[code language="php"]
$wgFoo = null;
$wgExtensionFunctions[] = function() {
	global $wgBar;
	$wgFoo = $wgFoo ? : $wgBar;
}
[/code]

This would introduce a nameless function which would do our required manipulations.
You can even make it a named function as in :

[code language="php"]
$wgExtensionFunctions[] = &amp;quot;myFunction&amp;quot;;
function myFunction() {
         // Code your task
}
[/code]

Hope it help someone ! Happy Hacking :)
[1] https://www.mediawiki.org/wiki/Manual:$wgExtensionFunctions
