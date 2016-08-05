---
title: GSoC Report - Week 1
date: 2014-05-29 17:16:18
foreword: In the first week I made progress with the Bug 975542 to add image capturing support to set user icon and it is in its final stage. I have mentioned the details about the bug in the last post.
---
In the first week I made progress with the [Bug 975542](https://bugzilla.mozilla.org/show_bug.cgi?id=975542) to add image capturing support to set user icon and it is in its final stage. I have mentioned the details about the bug in the [last post](../community-bonding-report/). Some of the major changes that were made include:

* The UI is closer to the Australis menu of Ff and has a better space management.
* The video is overlayed and image is clipped so that consistency of the icon is maintained throughout the panel.
* mozGetUserMediaDevices is dependent on getUserMedia, so we have a temporary fix to detect the webcam device attached.
* The panel is to be tested for accessibility with the screen reader for the blind and vision impaired people.

Took another enhancement [Bug 1004930](https://bugzilla.mozilla.org/show_bug.cgi?id=1004930) to develop a generic method to add conversation toolbar buttons as we would be needing this for different new features we are going to develop this summers.

* Instead of writing separate `toolbarbutton` for each item in `"conv-info-large"` and `"conv-info-small"` binding we now have a `children` element which automatically inherits the generated content and merge the XML element to the XBL content which makes it easier for us to add buttons.
* The toolbarbutton should be discoverable. So we decided to have one like the new Firefox Toolbar buttons. New buttons can now easily be added and modified. Since adding panel was out of scope for this bug I’ll do it in the coming days.

In the next week I plan to work on adding video call for XMPP protocol with support to recieve and end calls. I’ll file a bug for it soon.