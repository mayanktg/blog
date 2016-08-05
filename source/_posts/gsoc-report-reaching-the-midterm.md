---
title: GSoC Report - Reaching the Midterm
date: 2014-06-25 17:16:18
foreword: Proceeding further the next priority task was to first add a “call disconnect” support to the video call and then it was to remove the auto connecting calls and instead send the notification to the callee whether to Accept/Reject the call.
---
Proceeding further the next priority task was to first add a “call disconnect” support to the video call and then it was to remove the auto connecting calls and instead send the notification to the callee whether to Accept/Reject the call.

*   For adding the call disconnect support I created a “endCall” menthod in the conversation binding which restores the UI to the normal chat convresation state, stops the ongoing peerconnection and then calls the “endcall()” of the prpl to send the “session-terminate” IQ stanza to the callee. When the callee receives a session-terminate stanza it also does the same excluding the sending the stanza part.
*   Now to send call notification I used `notificationbox` which popups a notification bar to the callee with an “accept” and “reject” button.
*   I spent a day improving the UI of the call and using CSS’s `calc()` to dynamically vary the size instead of using the resizeVideo method I defined earlier, added a close call button and an ongoing call state to the video call button.
*   In the meantime :aleth suggested to add a countdown call timer which would disconnect the call automatically on both ends if unanswered for 30 sec. I implemented that too using `setTimeout` and `clearTimeout` functions.

The next milestone is to get the patch ready and also land the generic buttons patch. We are also suppose to add Entity discovery which would enable Video/Voice call iff the compatible device is detected.

Keeping XMPP Call project aside I worked on the bug to build a generic way to add icons to the toolbar. Plus the best part of this week was that I met Saurabh and Nihanth who are also the other GSoCers @ Instantbird.