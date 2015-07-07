---
author: tttwrites
comments: true
date: 2014-05-11 05:07:36+00:00
layout: post
slug: x-server-error-gtk-terminal
title: X server error when GTK+ apps as sudo from terminal [SOLVED]
wordpress_id: 489
categories:
- FOSS
- Unix shell
tags:
- gtk+
- sudo
- x-server
---

Often I hit with this error message on running apps like gpartd, partitionmanager as sudo from the root/user shell.
**Case**
` $sudo gpartd
No protocol specified
(gpartedbin:8630): Gtk-WARNING **: cannot open display: :0
`
**Fix**
Open up a new terminal, and give
`$ export XAUTHORITY=/home/<username>/.Xauthority`
That would fix it :). Thanks!
PS. Now to make it permanent,
` sudo nano .zshrc ` ( can be .bashrc, if you use bash )
add the following line to the end of the file
`$ export XAUTHORITY=/home/<username>/.Xauthority`
save & exit
` sudo source .zshrc `
