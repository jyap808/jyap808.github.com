---
layout: post
title: CentOS 6 minimal install CD - You may not want to bother with it
date: 2011-08-10 22:40
post-link: http://lists.centos.org/pipermail/centos-announce/2011-July/017660.html
---

I tried out the CentOS 6 minimal install CD yesterday when installing CentOS 6 for the first time on a virtual server.  Just a precaution: It is really minimal.  There are no package selection options during the install process and lots of things which I thought would be on a minimal install (you know based on past releases, that kind of thing) were missing which was frustrating.

I think I'll use the Netinstall or "LightWeightServer (LWS) CD" (or will the LWS bite me in the ass too?) in future (Why does CentOS 6 span over 2 DVD's? A lot of my servers don't have DVD drives).  Now previously, I only needed the first CentOS CD out of the multiple CD set to get my previous 'minimal' install working.

For example, CentOS 6 minimal install doesn't ship with Perl, Cron or a MTA.

So here are some other things I needed:

{% highlight bash %}
yum install perl
yum install crontabs
yum install postfix
yum install sudo
yum install wget
yum install vim-enhanced
yum install git
yum install bind-utils
{% endhighlight %}

If you install a service (such as crond), you will most likely need to then enable that service:

{% highlight bash %}
chkconfig crond on
{% endhighlight %}

And then start up the service:

{% highlight bash %}
/etc/init.d/crond start
{% endhighlight %}

Why didn't I just start again?  You know the scenario.  It's a busy work day so you take a gamble and go with the minimal install CD...  Then you start setting up your server and it's all like "OK, where the hell is Perl?"  Then 30 minutes later, "OK, why is there no /etc/crontab?"  And sooner or later you've reached the point in time where you've spent so much time with the server, you can't go back and perform a reinstall.  You may as well keep going.

Just today after work I thought to myself "You know, I don't recall receiving a Logwatch email over night".

*UPDATE:* September 7 @ 1:59pm. You can install the Base group of packages by running "yum groupinstall base".  You will probably be surprised to see what is missing.  I was surprised that I was missing some more essentials such as: at, lsof, man-pages, tcpdump, time.  IMHO any 'minimal install CD' should have the base group installed at a minimum. It is what we have come to expect and know when we have selected a 'minimal install' in the past.  It may increase the CD download size slightly but it makes sense.

