---
author: tttwrites
comments: true
date: 2014-12-01 13:20:48+00:00
layout: post
slug: conect-php-to-postgresql-database
title: Connect PHP to PostgreSQL database
wordpress_id: 728
categories:
- PHP
- Snippets
- Technical
- Web
tags:
- connect to database
- insert php
- php
- postgresql
---

Connecting to PostgreSQL is quite simple, but bit different from what we have with MYSQL.

Here we go: 
[code language="php"]
$pgconnection = pg_connect( "host=http://yourhost.com port=5432 dbname=yourdbname user=yourusername password=yourpassword" );
if ( !$pgconnection ) {
	echo "Cannot connect to datbase";
}
[/code]

to insert into an existing table named **FOO( bar1 varchar, bar2 numeric )**
[code langauge="php"]
$bar1 = "MyFoo";
$bar2 = "69";

$query=<<<EOF
INSERT INTO FOO( bar1, bar2 ) VALUES ( '$bar1', '$bar2' );
EOF;

$ret = pg_query($pgconnection, $query);

if ( !$ret ) {
	echo "Cannot write to database";
}
[/code]

References: 
1) http://www.tutorialspoint.com/postgresql/postgresql_php.htm
2) http://php.net/manual/en/ref.pdo-pgsql.connection.php
