---
title: GSoC Progress Report
date: 2014-07-22 17:16:18
foreword: The last week was dedicated mostly for making changes and landing the earlier bugs so that I can proceed with other patches already waiting to be fixed.
---
The last week was dedicated mostly for making changes and landing the earlier bugs so that I can proceed with other patches already waiting to be fixed. Here is a list of the things I did in the past week:

*   Made some necessary changes for the [Bug: 975542 - Set user icon using webcam](https://bugzilla.mozilla.org/show_bug.cgi?id=975542) and it was added to the nightlies.
*   Fixed the [Bug: 1004930 - Generic way to add toolbarbuttons](https://bugzilla.mozilla.org/show_bug.cgi?id=1004930). The toolbarbuttons are now aligned with the displayName which fixed the bottom border issue and it now has a better CSS too.
*   Since [Bug:1018060 - Add video call support for XMPP](https://bugzilla.mozilla.org/show_bug.cgi?id=1018060) is probably the next patch which is going to land so it should be ready. I changed how the xml2sdp() generated the Jingle XML stanza from the SDP offer. The method looks clearer and is easy to understand now.
*   Currently I’m working on the [Bug:1027779 - Inability to send call notification if no conversation has taken place before](https://bugzilla.mozilla.org/show_bug.cgi?id=1027779). This happens because the target resource has not been set and the user doesn’t know which is the most suitable resource to whom the notification should be sent. For this I need to find the most preferred resource available (i.e. the one for which voice call is supported) and then send the notification to only that resource.

In the upcoming week I’ll fix the Bug 1027779 and also try to land the video call patch.