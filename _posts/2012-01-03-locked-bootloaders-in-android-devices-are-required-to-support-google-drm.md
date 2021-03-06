---
layout: post
title: Locked bootloaders in Android devices are required to support Google DRM
date: 2012-01-03 10:53
---

From ASUS on their "Facebook page":http://www.facebook.com/ASUS/posts/300815559961849 regarding the locked bootloader on the EEE Pad Transformer Prime:

> Regarding the bootloader, the reason we chose to lock it is due to content providers' requirement for DRM client devices to be as secure as possible. ASUS supports Google DRM in order to provide users with a high quality video rental experience. Also, based on our experience, users who choose to root their devices risk breaking the system completely.

It never occured to me that a locked bootloader was because of DRM requirements from Google Video.  I just figured it was an anti-root measure to prevent warranty claims for bricked devices.

From HTC via their "Unlocking Your Bootloader page":http://htcdev.com/bootloader:

> Some content on your device may also be invalidated and cannot be accessed any more because of invalid DRM security keys. This includes content that you may have purchased through a 3rd party vendor and through HTC.

From Motorola Mobility's Twitter account when addressing the "locked bootloader on the Motorola RAZR":https://twitter.com/#!/Motorola/status/126351629791412225:

> The bootloader was locked per the carrier, in addition to meeting security, safety and regulatory guidelines.

While it may be possible to ship a tablet without a locked bootloader, it seems to me that it may not even be _possible_ to ship a cell phone device _without_ a locked bootloader because of regulatory guidelines.

Ars Technica also "mentions":http://arstechnica.com/gadgets/news/2011/05/google-blocks-android-movie-rentals-from-rooted-devices.ars YouTube-powered movie rentals as being a point of incompatibility with rooted devices:

> Google is restricting access to its YouTube-powered movie rental service to non-rooted devices. Users with rooted devices attempting to watch Android rentals will get an "Error 49" message, noting that their device was unable to "fetch license for movie."

It seems to me that manufacturer provided bootloader unlocking tools are a good way of catering to the unlocker community as well as being a convenient way for manufacturers to display a warning message that unlocking the bootloader also voids the warranty.  The "HTC unlock process":http://htcdev.com/bootloader/preview_unlock_process involves submitting a device ID token to a HTC web site which then sends you back an unlock key.  This sounds like a great way to track devices who have voluntarily unlocked their device and therefore voided the warranty.

