---
title: Community Bonding Report
date: 2014-05-21 17:16:18
foreword: After being selected I had one fundamental task for the community bonding period, to become familiar with the Instantbird codebase as much as possible.
---
After being selected I had one fundamental task for the community bonding period, to become familiar with the [Instantbird codebase](http://hg.mozilla.org/comm-central/file/) as much as possible. The discussion about the project with my mentor [Benedikt P.[:Mic]](https://mozillians.org/en-US/u/benediktp/) and the Instantbird team lies in the [Etherpad](https://etherpad.mozilla.org/ib-webrtc) and a track of my progress and mockups I created for the project resides in the [Trello](https://trello.com/b/knpAD9if/ib-webrtc-2014) page.

I started working on the enhancement [Bug 975542](https://bugzilla.mozilla.org/show_bug.cgi?id=975542) I filed. It taught me some of the most basic things about writing good code, XUL, CSS, getUserMedia, mozGetUserMedia (freaked us out for a day), File.write. Eventually it took more time than we thought as new features kept brainstorming but still I’m happy as its almost ready and would be added in the nightlies soon.

*   Wrote XUL code for creating a panel for the enhancement.
*   Create video frame in canvas –> capture a single frame –> clip it to suit as square icon.
*   Write the image to a tmp image file and copy it to profile directory –> remove tmp file (we are generous ;) ) –> set the image as user icon (already had code for that).
*   Media devices detection using mozGetUserMediaDevices to disable the button if no video capturing device found. I’ll blog about it someday.

Florian has already written a patch a year ago for video call using WebRTC in Thunderbird Chat. I looked at it and had an understanding about how the RTCPeerConnection API would work. Also the enhancement [Bug 1004930](https://bugzilla.mozilla.org/show_bug.cgi?id=1004930) to develop a generic way to add action buttons to a conversation has been added with my project.

Do not use vague language, say “No I don’t understand” if you don’t understand it, take pleasure in saying thanks :) , pastebin it, Firefox pref settings are life saver… are few other lessons I learnt during CB which I’m sure is going to help me in future.

May the force `to write more code + more tests + more comments` be with you.