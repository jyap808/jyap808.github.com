---
layout: post
title: Digital Ocean - First impressions
date: 2013-10-08 23:12
post-link: https://www.digitalocean.com/?refcode=571ac31ec1b5
---

I signed up for [Digital Ocean](https://www.digitalocean.com/?refcode=571ac31ec1b5) the other day since I was planning on using it for some online services. I also felt the service had reached a point of growth and maturity where it felt like they were "sticking around".

Here are some first impressions.

You can choose to create a virtual machine (a "droplet") in 1 of 4 data centers (a "region").  Only the "New York 2" data center supports Private Networking so for example if you create a VM in "San Francisco 1", the VM will only have a public IP interface.  If you are thinking of deploying a permanent system which will use N+1 servers then deploying to the "New York 2" data center is your only option so you don't need to expose services on a public IP just to talk to another one of your servers.  When creating a VM, "New York 2" is the default data center selected.

Ubuntu 12.04 x32 is the default distribution selected when creating a VM.  You should change this to a 64-bit distribution so that you have less hassles in case you want to resize your VM.  I had initially installed an Ubuntu 13.04 x64 VM but I had issues starting up the IPTables firewall and noticed that all of the documentation refers to 12.04 which would then be considered their best supported and maintained Ubuntu distribution version.

You should add a SSH key first in the web console so that you can select this during the install.  The installer only installs with a 'root' user and emails you the created password.  Having your SSH key pre-installed means you can automate additional install process items such creating another user account and disabling remote 'root' access.  Digital Ocean also has a nice REST API which spits back JSON.

On the default Ubuntu 12.04 x64 install there was no firewall installed by default.  You should definitely [install UFW](https://www.digitalocean.com/community/articles/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server) and implement a security policy for SSH access at a bare minimum.

I ran some quick tests and benchmarks and Digital Ocean lives up to the hype.  Performance is fast and consistent.

The main issue I have with VM online providers is inconsistent performance, be it disk, CPU or network IO.  Inconsistent performance means you need implement less than ideal workarounds such overprovisioning your servers or perform workarounds like [implementing software RAID 10](http://blog.9minutesnooze.com/raid-10-ebs-data/).

Imagine: The flexibility of virtual machines with the predictability of bare metal

Another thing I see myself doing is spinning up a VM just for quick testing.  Creating a VM literally takes a minute.

Here is a quick ApacheBench test of a [Go application](https://github.com/jyap808/g0bin) serving up a static template.

{% highlight console %}
# sysctl -w net.netfilter.nf_conntrack_max=131072
# ab -n 20000 -c 20 http://myserver/new/
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
…

Document Path:          /new/
Document Length:        4022 bytes

Concurrency Level:      20
Time taken for tests:   29.186 seconds
Complete requests:      20000
Failed requests:        0
Write errors:           0
Total transferred:      82740000 bytes
HTML transferred:       80440000 bytes
Requests per second:    685.27 [#/sec] (mean)
Time per request:       29.186 [ms] (mean)
Time per request:       1.459 [ms] (mean, across all concurrent requests)
Transfer rate:          2768.51 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       5
Processing:     2   29   3.0     29      53
Waiting:        0   29   3.0     29      53
Total:          2   29   3.0     29      53

Percentage of the requests served within a certain time (ms)
  50%     29 
  66%     30 
  75%     31 
  80%     31 
  90%     32 
  95%     33 
  98%     34 
  99%     35 
 100%     53 (longest request)
{% endhighlight %}

Here is a test of downloading a 100MB file from various locations from a VM created at the "San Francisco 1" data center.

{% highlight console %}
# curl -O http://speedtest.fremont.linode.com/100MB-fremont.bin
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  100M  100  100M    0     0  44.7M      0  0:00:02  0:00:02 --:--:-- 51.2M
# curl -O http://speedtest.tokyo.linode.com/100MB-tokyo.bin
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  100M  100  100M    0     0  12.5M      0  0:00:07  0:00:07 --:--:-- 16.4M
# curl -O http://speedtest.london.linode.com/100MB-london.bin
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  100M  100  100M    0     0  8459k      0  0:00:12  0:00:12 --:--:-- 10.0M
# curl -O http://speedtest.dallas.linode.com/100MB-dallas.bin
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  100M  100  100M    0     0  21.9M      0  0:00:04  0:00:04 --:--:-- 22.8M
{% endhighlight %}


