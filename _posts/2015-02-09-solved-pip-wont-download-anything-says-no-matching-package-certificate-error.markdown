---
author: tttwrites
comments: true
date: 2015-02-09 17:00:37+00:00
layout: post
slug: solved-pip-wont-download-anything-says-no-matching-package-certificate-error
title: '[SOLVED] pip wont download anything, says no matching package - Certificate
  error'
wordpress_id: 828
categories:
- Snippets
- Technical
- Unix shell
tags:
- pip
- pip certificate add
- pip download nothing
- pip download ssl error
---

Recently met with this error, but failed to understand it was a network certificate issue. Pip tries to download source from the internet, and probably HTTPS will be handled by your CA Certificate, and - how would the download succeed?. This would be your scenario :
[code language="bash"]
$ (env) pip install Django==1.6.0
Collecting Django==1.6.0
  Could not find any downloads that satisfy the requirement Django==1.6.0
  No distributions at all found for Django==1.6.0
(env)➜ 
[/code]

Fix : Explicitly pass the certificate to pip. Considring you have certificate under ` /home/foo/CA_cert.cer`
[code language="bash"]
$ (env) pip --cert /home/foo/CA_cert.cerr install Django==1.6.0
Collecting Django==1.6.0
  Downloading Django-1.6-py2.py3-none-any.whl (6.7MB)
[/code]

Here you go :). If you have your requirements in a file requirements.txt
[code language="bash"]
$ (env) pip --cert /home/foo/CA_cert.cerr install -r requirements.txt
[/code]

fun!
