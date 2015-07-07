---
author: tttwrites
comments: true
date: 2014-05-06 07:02:57+00:00
layout: post
slug: mosh-ing-into-the-wikitech-bastion-host
title: $ mosh - ing into the Wikitech bastion host
wordpress_id: 481
categories:
- FOSS
- Unix shell
- Wikimedia
tags:
- mosh
- wikitech
- wikitech-labs
---

Those who got no idea what bastion server is :- 
*** bastion host** :- _A Bastion host is a special purpose computer on a network specifically designed and configured to withstand attacks. The computer generally hosts a single application, for example a proxy server, and all other services are removed or limited to reduce the threat to the computer. _  ( from wikipedia ;) 

Being far away from the Wikitech hosts, I had my own difficulties connecting to my Wikitech labs instance. The response time between key stroke and output almost crossed 1 sec in certain cases. Desperate, I was searching for alternatives for SSH, and came across this amazing software, **mosh** (http://mosh.mit.edu/).
You can install mosh by :-  ` $ sudo apt-get install mosh ` 
You can connect via mosh using the folowing command : 
` $ mosh user@server.com ` 
instead of ` $ ssh user@server.com `

**Troubleshooting connection to Wikitech-Labs:- **
* If you get an error message like : 
`
$ mosh user@bastion.wmflabs.org
mosh-server: invalid option -- 'l'
Usage: mosh-server new [-s] [-i LOCALADDR] [-p PORT] [-c COLORS] [-- COMMAND...]
mosh-server: invalid option -- 'l'
Usage: mosh-server new [-s] [-i LOCALADDR] [-p PORT] [-c COLORS] [-- COMMAND...]
mosh-server: invalid option -- 'l'
Usage: mosh-server new [-s] [-i LOCALADDR] [-p PORT] [-c COLORS] [-- COMMAND...]
setlocale: No such file or directory
Connection to bastion.wmflabs.org closed.
/usr/bin/mosh: Did not find mosh server startup message.
`
if you are using 
* the default bash shell :
`** $ nano .bashrc** `
* the zsh shell :
` **$ nano .zshrc **` 

and add the following lines to the end of the file :- 
` 
 export LANG="en_US.UTF-8 locale"
 export LC_ALL="en_US.UTF-8"
` 
to update the shell, run 
`** $ source .zshrc** `
or 
` **$ source .bashrc** `
