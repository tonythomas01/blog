---
author: tttwrites
comments: true
date: 2014-11-08 06:28:06+00:00
layout: post
slug: mediawiki-php-unit-tests-reading-contents-from-a-file-dataprovider
title: 'MediaWiki PHP unit tests : Reading contents from a file ( @dataProvider )'
wordpress_id: 698
categories:
- FOSS
- PHP
- Wikimedia
tags:
- dataProvider functions
- mediawiki php unit tests
- reading from a file
---

While writing php unit tests for the BounceHandler extension, I came across a scenario in which I had to read contents from a text file and feed that to the test function as a variable. With the dataProvider functions it was solved simple.

Problem:
* function testProcessTextfile( $foo ) function requires $foo to be read from a file from **bar/foo.txt **

Solution:
In the class extending ApiTestCase give :

[code language="php"]
public static function provideFoo() {
	$foo = file_get_contents( __DIR__ .'/bar/foo.txt' );
	return array (
		array ( $foo )
	);
}

/**
* @dataProvider provideFoo
* @param $foo
*/
function testProcessTextfile( $foo ) {
	//code to process $foo
}
[/code]

That would do ! Happy hacking!
PS: Please note that the following wont work without the correct function comments and headers :)
