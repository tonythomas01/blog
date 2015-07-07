---
author: tttwrites
comments: true
date: 2014-03-24 15:34:11+00:00
layout: post
slug: greying-out-submit-button-untill-user-give-input-jquery-snippets-1
title: 'Greying out submit button untill user give input  :  jQuery snippets #1'
wordpress_id: 458
categories:
- jQuery
- Snippets
- Wikimedia
tags:
- grey out
- Jquery
- JS
- subimt button
---

Scenario
/*
The submit button needs to wait till the user enter something into the input box. This is useful in most cases, where null injection can cause trouble
*/

Challenge
/*
* The button should initially become disabled
* It should become alright after the user enters some stuff
* It should go back to disabled state once the user have cleared everything out
*/

Code
` `

$( '#buttonClick' ).prop( 'disabled', true );
$('.input').on('input', function() {
$(this).next().prop('disabled', $(this).val().length < 1);
});

Hope it helps someone.

Related links:-
[1] http://jsfiddle.net/4gxuU/
[2] https://gerrit.wikimedia.org/r/#/c/120487/
