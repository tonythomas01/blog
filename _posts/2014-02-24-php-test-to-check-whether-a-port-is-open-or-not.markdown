---
author: tttwrites
comments: true
date: 2014-02-24 13:50:05+00:00
layout: post
slug: php-test-to-check-whether-a-port-is-open-or-not
title: PHP test to check whether a port is open or not
wordpress_id: 410
categories:
- Public
- Technical
tags:
- php
- port-test
- smtp
---

You need to replace the
$address ="the_test_address.com";
$port = 'port_number';

/*Code starts*/
/*port test*/

<?php
$address="smtp.gmail.com";
$port = '456';
if (isset($port) and
($socket=socket_create(AF_INET, SOCK_STREAM, SOL_TCP)) and
(socket_connect($socket, $address, $port)))  {
$text="Connection successful on IP $address, port $port";
socket_close($socket);
}
else  {
$text="Unable  connect<pre>".socket_strerror(socket_last_error())."</pre>";
}
echo "<html><head></head><body>".
$text.
"</body></html>";
?>

/*code ends*/
code courtesy: http://php.net/socket_connect

How to test :- Copy this code to a file say, porttest.php, change the $address , $port to the required and put it somewhere accessible by your server , like /var/www/ in linux. And run the same by opening localhost/porttest.php
