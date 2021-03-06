---
layout: post
title: Disabling third party cookies in Firefox. How it should be according to RFC 2109
date: 2012-02-25 01:52
---

In the wake of the recent controversy of "Google bypassing the Safari browser setting for disabling third party cookies":http://julianyap.com/2012/02/16/google-tracked-iphones.html, I decided to review my settings in Firefox which is my desktop browser of choice and implement the same setting.  I have been running this mode for over a week now without any noticeable issues with general web browsing.

John Gruber on Daring Fireball has a "great response":http://daringfireball.net/2012/02/cookies_and_privacy to John Battelle who argues that accepting third party cookies is how things are "done on the open web".

In further research I was interested to learn that in the first formal specification for cookies, "RFC 2109":http://tools.ietf.org/html/rfc2109, identified the privacy threat of third party cookies and explicitly states that third party cookies should be disabled by default.

In section: 8.3  Unexpected Cookie Sharing:

> A user agent should make every attempt to prevent the sharing of session information between hosts that are in different domains. Embedded or inlined objects may cause particularly severe privacy problems if they can be used to share cookies between disparate hosts.  For example, a malicious server could embed cookie information for host a.com in a URI for a CGI on host b.com.  User agent implementors are strongly encouraged to prevent this sort of exchange whenever possible. 

RFC 2109 was superseded by "RFC 2965":http://tools.ietf.org/html/rfc2965 in October 2000 but contains the exact same section and wording.

Below is how you implement disabling of third party cookies in Firefox for Windows and Mac.

*Windows*

Open Options → Privacy → Select Firefox will: Use custom settings for history → Uncheck Accept third-party cookies

*Mac*

Open Preferences → Privacy → Select Firefox will: Use custom settings for history → Uncheck Accept third-party cookies

