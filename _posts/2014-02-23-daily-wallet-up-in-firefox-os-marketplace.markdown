---
author: tttwrites
comments: true
date: 2014-02-23 16:40:53+00:00
layout: post
slug: daily-wallet-up-in-firefox-os-marketplace
title: Daily Wallet up in Firefox OS Marketplace !
wordpress_id: 381
categories:
- FOSS
- Public
tags:
- daily wallet
- Firefox OS
- HTML5
- webapp
---

Some four months after its start, our app Daily wallet is up in the market place.  Basically, the app is an effective wallet management tool for school and college students. The user can enter all his income and how its gone through the interface, and details of all the transactions including date and time will be stored and retrieved at ease.  Tina and  I was working on the same for the Firefox OS App Days at Kochi, but couldn't complete the same.

Marketplace link:  [https://marketplace.firefox.com/app/dailywallet/](https://marketplace.firefox.com/app/dailywallet/)

Some of the issues we faced and how it got fixed :




	
    1. Storing the history of transactions even after the phone is rebooted - had been a major issue as local file storage would require additional permissions and reading the data is again and issue - Used HTML5 browser localStorage.  Now data can be added and retrieved simply by using `localStorage.history`. Read about localStorage [here](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#localStorage).



[gallery type="rectangular" ids="392,391,396,395,394,393"]

	
  1. Getting the clicked id, so that it can be stored for further use - For eg, when the user spends 40 Rs for Breakfast, we wanted the app to store it like : (--Rs 40 - breakfast) in localStorage.history. After going through various JS concepts, we got into the idea of a button that throws its id on click.
_button_ _id="foo" onclick="reply_click(this.id)">button_name</button>_
Now it can be handled anywhere in the JS file to respond correctly to the clicks.

	
  2. Initializing the localStorage.balance variable - The localStorage.balance holds the Wallet balance and  it is altered throughout the app arithmetically. But, initially there should be a code that resets it to 0, in order for further +/- to result in values. The worry was where  to define this statement. Atlast, we made a separate button called 'Reset' that would reset the localStorage.balance, and needs to be given at the initial use of the app. Its a one time work, so no worry !

	
  3. Optimizing the code for the Firefox OS Marketplace- The  menus were redesigned to use JQuery accordion, and inputs are recieved via JS prompts. Pushing into the marketplace requires packing of the app and styling coding conventions. Was not a big issue at all.


Specifications :
O/S - Firefox OS
Language used : HTML, JS, JQuery, CSS, HTML5
Storage : HTML5 LocalStorage
Github link :[ https://github.com/tonythomas01/DailyWallet](https://github.com/tonythomas01/DailyWallet)
