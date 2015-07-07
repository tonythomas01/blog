---
author: tttwrites
comments: true
date: 2015-01-05 18:39:27+00:00
layout: post
slug: mediawiki-unit-tests-truncating-table-after-each-test
title: 'MediaWiki Unit Tests : Truncating table after each test'
wordpress_id: 736
categories:
- FOSS
- Wikimedia
tags:
- mediawiki tests
- tablesUsed
- truncate table
- user-table. mediaiwki
---

Writing PHP unit tests for the BounceHandler extension to prune old Bounce Records, I got into a situation where I had to truncate the 'bounce_records' and 'user' table after each single test. You would want the same when the test manipulates part of your table - and you dont want those changes to show up in your next test. Initially, I did this by manually truncating rows in both the table, but later I came across the use of

**$this->tablesUsed = array( 'table_name1', 'table_name2' );**

Implemented by :

[code language="php"]
class DoSomethingTest extends MediaWikiTestCase {
	protected function setUp() {
		// Your test initialization code here
		$this->tablesUsed = array( 'tableName' );
	}
}
[/code]

This would truncate 'tableName' table after each test ! Yay.
protected $tablesUsed = array(); is declared in MediaWikiTestCase.php[1] and its contents truncated after each test run !

[1] https://doc.wikimedia.org/mediawiki-core/master/php/html/MediaWikiTestCase_8php_source.html#l00038
[Ref : https://gerrit.wikimedia.org/r/#/c/176366/20/tests/PruneOldBounceRecordsTest.php ]
