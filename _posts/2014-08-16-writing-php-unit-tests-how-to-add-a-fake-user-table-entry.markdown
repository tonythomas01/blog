---
author: tttwrites
comments: true
date: 2014-08-16 15:35:32+00:00
layout: post
slug: writing-php-unit-tests-how-to-add-a-fake-user-table-entry
title: 'Writing PHP unit-tests : How to add a fake user table entry'
wordpress_id: 616
categories:
- FOSS
- PHP
- Wikimedia
tags:
- extension-test
- php
- phpunittest
- user-table. mediaiwki
---

Flexibility of the Mediawiki PHP unit-tests wrapper extends to the fact that fake database entries can be made and tested upon without causing any harm to the actual one. 
As I scribbled in the earlier post, the class-comments play a vital role, and dont forget to give them like this:
[code language="php"]
<?php
/**
 * Class to test table lookups
 *
 * @group Database
 */
class ModifyUserTableTest extends MediaWikiTestCase {
	function testModifyUserTable() {
        // Lets add a fake user named TestUser, and check that his email is confirmed and then get his User Id  
		$user = User::newFromName( 'TestUser' );
		$user->setEmail( 'bob@example.ext' );
		$user->addToDatabase();

		$user->confirmEmail();
		$user->saveSettings();

		$this->assertTrue( $user->isEmailConfirmed() );

		$uid = $user->getId();
        }
}
[/code]

This would create a fake user TestUser in a fake table - mediawiki_unittest. Later this user can be used for any other testing purpose within the class ! Yay!
