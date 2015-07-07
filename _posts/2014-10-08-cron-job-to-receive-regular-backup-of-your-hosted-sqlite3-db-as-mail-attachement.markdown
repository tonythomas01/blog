---
author: tttwrites
comments: true
date: 2014-10-08 13:29:38+00:00
layout: post
slug: cron-job-to-receive-regular-backup-of-your-hosted-sqlite3-db-as-mail-attachement
title: Cron job to receive regular backup of your hosted sqlite3 db as mail attachement
wordpress_id: 663
categories:
- FOSS
- Technical
- Unix shell
tags:
- attachment via command line
- backup db
- cronjob
- mutt
- send emails from command line
- sqlite3
---

While hosting **debutsav.in**, I came to a scenario to get regular backups of the registration db. This would be a regular requirement for anyone working with web, and cares about data security. I went through various blogs available - and let me share the one that helped me great :) 

The key is to add a cronjob to the linux system - to automate the mailing part. To write the cron job.
[code language="bash"]
# crontab -e 
[/code]
That would sometimes bring about a confirmation message, otherwise proceed to next step.
You will need a file `emailbody.txt` that would contain the email body. 
** IMP: This would mail you the db backup every day at 12:00 am ( sometimes pm :D ).**
[code langauage="bash"]
0 0 * * * mutt -s "Database Backup" -a /path/to/sqlitedb.db -- yourname@yourdomain.ext < /path/to/emailbody.txt
[/code]
Save and close the file, and you are good to go :) 

Checklist:
* What if your web hosting provider do not allow emails ?
> You can check that one by running this command:
[code language="bash"]
$ mail yourusername@yourserver.ext
[/code] enter a test subject and body - and click '.' to finish of the email body and send the mail :)
