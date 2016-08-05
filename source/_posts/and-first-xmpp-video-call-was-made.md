---
title: and...First XMPP Video Call Was Made
date: 2014-06-16 17:16:18
foreword: Until last week there used to be a harcoded offer and we converted this offer to XML Stanza and then retrieve it back. Moving forward we added the WebRTC methods in the conversation.xml binding which would generate the SDP offer in the DOMWindow.
---
Until last week there used to be a harcoded offer and we converted this offer to XML Stanza and then retrieve it back. Moving forward we added the WebRTC methods in the conversation.xml binding which would generate the SDP offer in the DOMWindow. But the problem was, “How will the generated offer reach the prpl?”. The solution was simple but not straight forward, I had to create a method in the interface `prplIConvIM` so that the method becomes available at the `xmpp.jsm` too. I followed the standard approach as directed i.e. added a method startCall() in the <conde>prplIConv</conde> interface, set default at `jsProtoHelper.jsm` and then defined also at `prplIConvIM` since it was the interface the startCall method in converation binding was going to use. I was able to generate the offer and the client was able to receive and convert the same.

The startCall method in the conversation binding looked like this

`
    <body>
    <![CDATA[
      let conv = this._conv;
      let fail = function(err) {
        conv.systemMessage(err);
      };
      let pc = this.initPeerConnection();
      this.getVideo(function() {
        pc.createOffer(function(offer) {
          pc.setLocalDescription(offer, function() {
            conv.startCall(offer.sdp);
          }, fail);
        }, fail);
      }, fail);
    ]]>
    </body>
`

The initPeerConnection method adds the UI for “localVideo” and “remoteVideo”, creates a `mozRTCPeerconenction` object and adds stream. getVideo method is used for adding playback stream to localVideo and the `createOffer` is used to generate the SDP offer. We send the SDP part of the generated offer to prpl using startCall() for conversion to XML Stanza.

Using `notifyObservers()` the offer received and converted at the callee’s end is sent to the converastion binding and this offer is then used to generate answer.

Now I had to repeat the same procedure i.e. use the received SDP offer to create an answer and then again send it to the caller to establish the call. I followed and added createAnswer() which sends the SDP part of the answer to the prpl which then converts it to XML Stanza and send it to caller…and so on.

When all the above steps is completed and the caller accepts the answer (auto accepting presently), webrtcAnswerCall method is called and the call session is established between the two users. i.e. the video is transmitted! :) You can follow up the whole procedure at the [Bug 1018060: Voice and video call support in XMPP using WebRTC](https://bugzilla.mozilla.org/show_bug.cgi?id=1018060)

Next in the priority series is to add call disconnect feature, improve the UI as per the [prototype](http://i.imgur.com/UcxFIju.png) and add the ability to start a new conversation when making a video call.