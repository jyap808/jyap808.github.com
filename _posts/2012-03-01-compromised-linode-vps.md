---
layout: post
title: The story of the compromised Linode VPS and further analysis
date: 2012-03-01 17:40
post-link: http://bitcoinmedia.com/compromised-linode-coins-stolen-from-slush-faucet-and-others/
---

An interesting story found on Hacker News where a VPS running on Linode was compromised.  Most interesting was Marek's "support ticket log":http://pastebin.com/UW7iT5fj since it sounds like he is well versed technically.  Here is some of my analysis and thoughts.

From the article, the root passwords were changed through the "Linode Manager" which would initially suggest a compromised Linode Manager account.

The support person rules out the possibility of a brute force login attempt and Marek then asks for the records of Linode Manager logins and notices no false login records.  This would indicate to me a security compromise across Linode Manager itself through an alternative access method.  Linode has also just released a "status update":http://status.linode.com/2012/03/manager-security-incident.html to this security incident which indicates that 8 customers had their Linode Manager account compromised which would indicate what I said is true.  The Linode Manager compromise then meant the attacker was able to target customers who ran Bitcoin servers.

The support ticket then concludes with Linode admitting that yes, the Linode Manager was accessed through compromised credentials through Linode's customer support interface.  Yes, this does mean that any Linode customer was vulnerable.

Through further research, the Linode wiki "mentions":http://www.linode.com/wiki/index.php/FAQ#How_do_I_recover_or_reset_the_root_password.3F the functionality of the root password reset:

> Log into the Linode Manager and select the Linode that you wish to reset the password on. Shut down the Linode and navigate to the "Rescue" tab. From this tab, you can use the "Reset Root Password" utility to enter your desired password and apply the change. After the task has completed, you may boot your Linode and log in. 

This sounds like the Linode VPS root password is reset through single user mode.

Linode should immediately disable root password resets through the Linode Manager.  Root passwords should only be reset by a customer service representative and only after the identidy of the authorized user for that Linode VPS has been confirmed.

Linode also states that they are further reviewing their policies which is the correct course of action.

