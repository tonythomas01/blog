---
author: tttwrites
comments: true
date: 2014-12-01 13:38:09+00:00
layout: post
slug: solved-fedora-boots-into-tty-after-replacing-gdm-with-kdm
title: '[SOLVED] Fedora boots into tty after replacing GDM with KDM'
wordpress_id: 730
categories:
- Operating Systems
- Technical
- Unix shell
tags:
- boots into tty
- Fedora
- install kdm fedora
- remove gdm
---

This one gave me enough worries - but somehow got the right link to sort this one out. First things first:
GDM = Gnome Desktop Manager
KDM = KDE Desktop Manager 
tty = Teletype Terminals ( You get it usually with Ctrl+Alt+F1 )
Scenario: 
You removed gdm - and installed kdm - but Fedora boots only to a tty shell. You login there and give kdm - the KDE boots up. 
You want to skip the tty steps :)

[code language="php"]
$ sudo systemctl disable gdm
$ sudo systemctl enable kdm
[/code]

on the next boot, fedora boots up directly to KDE! Yay! 
That would do :)
