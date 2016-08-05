---
title: GSoC Wrap-up
date: 2014-07-22 17:16:18
foreword: Its been long since I have blogged about my GSoC progress. I had been performing changes and nits for my patches so that they could land soon. I’m summarizing about some of my patches. You can check my code by visiting the Bug links.
---
Its been long since I have blogged about my GSoC progress. I had been performing changes and nits for my patches so that they could land soon. I’m summarizing about some of my patches. You can check my code by visiting the Bug links.

* [Bug:1004930 - Generic way to add toolbarbutton:](https://bugzilla.mozilla.org/show_bug.cgi?id=1004930)After fixing the issues about the display of the buttons when viewed at smaller window size the patch is ready to land. It has greatly reduced the steps taken to add buttons in the conversation for different purposes/features.
* [Bug:1018060 - Add video call support for XMPP:](https://bugzilla.mozilla.org/show_bug.cgi?id=1018060)Earlier I was using HTML Document to create the video call window, but Florian had a better idea that we should be using XBL binding for creating the UI. Thus, the UI now uses a simpler code to add the video call elements needed. I made further changes to the sdp2Xml and xml2Sdp and the backend XMPP code.
* [Bug:1025150 - Implement Entity Capabilities in XMPP:](https://bugzilla.mozilla.org/show_bug.cgi?id=1025150)This patch now also stores capabilities info received from each resource and changes the availabilityDetails based on the current preferred resource. I made other changes to it as per the review comments.
* [Bug:1027771 - Add fullscreen support for video calls:](https://bugzilla.mozilla.org/show_bug.cgi?id=1027771)This is a WIP using which we can now switch to fullscreen mode during a video call.

Next I need to add better interface for the videoc calls when the user is using a wider window, implement Audio call support and to add suppport for hold/mute during video/audio calls.