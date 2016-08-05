---
title: Implementing Entitiy Discovery - Part 2
date: 2014-07-15 17:16:18
foreword: Finally entity capability implementation for XMPP is complete and is ready for review cycles. We have added the video discovery capability.
---
Finally entity capability implementation for XMPP is complete and is ready for review cycles. We have added the video discovery capability. As discussed in [Part 1](http://mayanktg.github.io/implementing-entitiy-discovery-part-1/) after adding the receive capability and decoding it now we move forward for the sending part.

We need to send a `c` node along with the `presence` stanza to the user. We create a presence stanza like:
{% codeblock Presence stanza lang:xml %}
<presence xmlns="jabber:client" id="6" xml:lang="en" from="xyz@abc.com/Instantbird">
 <show xmlns="jabber:client">
  away
 </show>
 <status xmlns="jabber:client">
  I am currently away from the computer.
 </status>
 <c xmlns="http://jabber.org/protocol/caps" ver="5guaTqssTb94FuNI4uMKvCOspHE=" hash="sha-1" node="http://instantbird.com"/>
</presence>
{% endcodeblock %}
On receiving this stanza the machine performs the check as previously discussed in last post and if needed sends a service discovery request stanza.
{% codeblock service discovery request stanza lang:xml %}
<iq type="get" id="id-ig57r" to="xyz@abc.com/Instantbird">
  <query xmlns="http://jabber.org/protocol/disco#info" node="http://instantbird.com#5guaTqssTb94FuNI4uMKvCOspHE="/>
</iq>
{% endcodeblock %}
Now when a client receives this stanza it has to generate its own service capability stanza and send this to the user as a IQ result. Currently we use a `generateServiceDiscovery()` :
{% codeblock Service capability function lang:javascript %}
generateServiceDiscovery: function() {
  let queryStanza = Stanza.node("query", null, {xmlns: "http://jabber.org/protocol/disco#info",
                                                node: "http://instantbird.com"});
  queryStanza.addChild(Stanza.node("identity", null, {type: "pc",
                                                      name: "Instantbird",
                                                      category: "client"}));
  queryStanza.addChild(Stanza.node("feature", null, {var: "urn:xmpp:jingle:apps:rtp:video"}));
  queryStanza.addChild(Stanza.node("feature", null, {var: "urn:xmpp:jingle:apps:rtp:audio"}));

  // Added to maintain interportability with other clients.
  queryStanza.addChild(Stanza.node("feature", null, {var: "http://www.google.com/xmpp/protocol/voice/v1"}));
  queryStanza.addChild(Stanza.node("feature", null, {var: "http://www.google.com/xmpp/protocol/video/v1"}));
  queryStanza.addChild(Stanza.node("feature", null, {var: "http://www.google.com/xmpp/protocol/camera/v1"}));

  return queryStanza;
}
{% endcodeblock %}
Now one of the prime task is to be able to actually detect our own video/audio devices and perform the video call only if the device is capable. For this we have used a callback method detectVideocapability() which detects the audio and video devices using `mozGetUserMediaDevices` and proceeds for the call only if the media devices are present.
{% codeblock Media device discovery lang:xml %}
<method name="detectVideoCapability">
  <parameter name="aSuccessCallback"/>
  <parameter name="aErrorCallback"/>
  <body>
  <![CDATA[
      navigator.mozGetUserMedia({audio: false, video: false},
                                function() {}, function() {});

      navigator.mozGetUserMediaDevices({video: true, audio: true},
                                       aSuccessCallback,
                                       aErrorCallback);
  ]]>
  </body>
</method>
{% endcodeblock %}
The WIP for the entity capability implementation can be tracked at [Bug 1025150](https://bugzilla.mozilla.org/show_bug.cgi?id=1025150).