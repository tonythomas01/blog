---
layout: post
title: "[Fix] A start job is running for dev disk"
description: "Fixing the disk check issue slowing boot time in Linux"
category: FOSS, Linux
tags: [slow start debian, ubuntu start job, fstab edit, swap off]
---

I have been stuck with this error for few days thinking it was something wrong with the kernel, but it looks like it came from a wrong entry in `/etc/fstab`. Lets try dissecting the same here.

**Problem**

Your installed Debian/Ubuntu Linux takes a long time to boot up, and you can see something similar to this one showing up during the boot time in the black background 

	A start job is running for dev-disk-by\x2uuid-f782f311\<more numbers>.device [1min 30s]

and it will take roughly 1 min 30 sec to finish the same, before you get booted up. Sad, isnt it ?

**Causes** 

What went wrong with me was, I tried running a `Kali Linux` in USB persistence mode Live in my system, and forgot to turn it off properly. This would've added some additional entires of swap area to `/etc/fstab`. The boot manager looks in `/etc/fstab` for devices to mount and finds that this device is missing. The 150 seconds check confirms the same, and shows up an error report. How rude :\

**Solution** 

Thanks to various neat resources available in the internet - I could find what was wrong easy
{% highlight bash %}
# nano /etc/fstab
{% endhighlight %}
You will find partitions over there which will be ( usually ) `/` , `/home`, `/boot/efi` and `swap`. In my case, I had an additional `swap` partition which was pointing to `/media/cdrom0` or something like that.

	# swap was on /dev/sda3 during installation
	UUID=81fdd36c-95af-4482-b32e-1904d62e6583 none            swap    sw              0       0
	/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0


You can find which device is causing the issue by carefully examining the boot time messages. You will get the `UUID` of the device causing the issue. Now, you need to disable that check for the device, and you can just **comment it out**

	# swap was on /dev/sda3 during installation
	#UUID=81fdd36c-95af-4482-b3fe-1904d62e6583 none            swap    sw              0       0
	#/dev/sr0        /media/cdrom0   udf,iso9660 user,noauto     0       0

**Adding back your original swap**

If you do not find a swap mounted in there:

* Open some partition manager like `gparted` and check for your swap partition. 
* Right click -> properties, and get the UUID number 
* Add an entry to the bottom of `/etc/fstab` which looks similar to:

{% highlight bash %}

UUID=ae3e609f-4a01-4b9e-a097-4bdaee99778 none swap defaults 0 0
{% endhighlight %}



