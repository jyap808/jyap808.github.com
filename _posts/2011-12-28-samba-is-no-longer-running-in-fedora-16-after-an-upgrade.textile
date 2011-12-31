---
layout: post
title: Samba service is no longer running in Fedora 16 after an upgrade
date: 2011-12-28 10:46
---

I found that the Samba service was no longer running after an upgrade to Fedora 16 and it didn't show up as an actual service.

Services are now controlled by systemd instead of system V. Look for samba with something like:

{% highlight bash %}
systemctl list-units --all |grep smb
{% endhighlight %}

This should show you something like this unless the service is missing:

{% highlight bash %}
smb.service               loaded active   running       Samba SMB Daemon
{% endhighlight %}

If it is not started you can start it with your old service command but under systemd you can use something like:

{% highlight bash %}
systemctl enable smb.service
systemctl start smb.service
{% endhighlight %}

The enable command moves the smb service file into the correct spot (previously like "chkconfig <service> on") and start then starts it up. To see the status you can run:

{% highlight bash %}
systemctl status smb.service
{% endhighlight %}

Which should look like this:

{% highlight bash %}
smb.service - Samba SMB Daemon
	  Loaded: loaded (/lib/systemd/system/smb.service; enabled)
	  Active: active (running) since Wed, 28 Dec 2011 10:41:13 -1000; 13s ago
	 Process: 2828 ExecStart=/usr/sbin/smbd $SMBDOPTIONS (code=exited, status=0/SUCCESS)
	Main PID: 2829 (smbd)
	  CGroup: name=systemd:/system/smb.service
		  ├ 2829 /usr/sbin/smbd
		  └ 2831 /usr/sbin/smbd
{% endhighlight %}

Based off of "this.":http://www.fedoraforum.org/forum/showthread.php?t=273554

