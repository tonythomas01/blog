---
author: tttwrites
comments: true
date: 2014-08-16 14:12:09+00:00
layout: post
slug: writing-php-unit-tests-to-verify-extension-api-post
title: Writing PHP Unit tests to verify extension API POST
wordpress_id: 613
categories:
- FOSS
- PHP
- Wikimedia
tags:
- API
- extension
- php
- phpunittest
---

PHP unit tests are crucial before deployment to make sure that the degree of damage your extension can cause is minimal. How to start was always my worry, and here we go.
Considering I have an API called 'myapi' that POST's string $myvar :
[code language="php"] 
<?php
/**
 * Tests for API module
 * @group API
 * @group medium
 */
class ExtensionTest extends ApiTestCase {
	/**
	 * @var string
	 */
	static $myvar = "This is a test var";

	/**
         * This needs to be called on every ApiTestCase childs
         */  
        function setUp() {
		parent::setUp();
		$this->doLogin( 'sysop' );
	}
	/**
	 * Tests API
	 * assuming you have the myapi as per the guidelines below
	 */
	function testAPI() {
		$this->setMwGlobals( 'wgMyGlobalArray', array( '1231' ) );
		list( $apiResult ) = $this->doApiRequest( array(
			'action' => 'myapi',
			'email' => self::$myvar
		) );

		$this->assertEquals( 'job', $apiResult['myapi']['submitted'] );
	}
}
[/code]
The ` job = submitted ` makes sure that the job is completed, and can be implemented by adding this to the API end:
[code language="php"]
$this->getResult()->addValue(
			null,
			$this->getModuleName(),
			array ( 'submitted' => 'job' )
		);
[/code]
PS: you can run the PHP unit test by running this from MediaWiki-core/
[code language="bash"]
tests/phpunit/phpunit.php extensions/<ExtensionName>/tests/ExtensionTest.php
[/code]
Funny thing about PHP unit tests in MediaWiki is that, even the comment headers too matter :) 
Happy Hacking :)
