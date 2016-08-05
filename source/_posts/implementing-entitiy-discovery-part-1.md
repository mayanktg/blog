---
title: Implementing Entitiy Discovery - Part 1
date: 2014-07-8 17:16:18
foreword: Entity Discovery helps you figure out the device supported at both the ends of the conversation even before the service has been called for action so that the user knows about the capability of the service.
---
I would be coding the rest of my summers from college.

The implementation of <a href="">XEP-1115: Entity Discovery</a> is going to be a major milestone for two of the Instantbird GSoC projects (<a>File Transfer using XMPP</a> and <a>Video/Voice Call using XMPP</a>).

In layman terms Entity Discovery helps you figure out the device supported at both the ends of the conversation even before the service has been called for action so that the user knows about the capability of the service. To understand further let us take an example of the most popular Hangouts. Sign in to Google Hangouts with a webcam enabled machine and then you’ll see a video call button during the conversation. Now disable your webcam and you’ll figure out that the button has now disappeared. How does the computer at the other end knows that the service is no longer supported? Simple, the user sends the new entity information to other users and they now know about its supported service list.

Now my task is to implement this feature for XMPP protocol which uses XML Stanzas for the conversation. As you must have seen in the example above it can be divided into two parts

1. Send an Entity Discovery stanza
2. Receive and decode an Entity Discovery stanza

Simple as it sounds, what we did was we broke it bottom-up and started from the second step. When we connected a buddy using a chat client Jitsi which already has video call support for XMPP we received a `c` node containg the SHA-1 encrypted, Base 64 encoded `ver` attribute. This attribute is unique for a list of entities. Thus we needed to recreate such a stanza for implementing voice call entity discovery. The steps to create a “ver” attribute has been defined here [](http://xmpp.org/extensions/xep-0115.html#ver-proc)[http://xmpp.org/extensions/xep-0115.html#ver-proc](http://xmpp.org/extensions/xep-0115.html#ver-proc). A little complex as I got confused with the steps mentioned. ;)

#### READ ALERT: Why we are not using XEP-0030: Service Discovery?

The [XEP-0030](http://xmpp.org/extensions/xep-0030.html) is now obsolute since it floods the conversation with service discovery stanzas for each user. There might be a condition that two users are sharing same service discovery information. Instead of sending and receving things repeatedly we save the entity information with the ver attribute received and use it for later comparisions. This saves bandwidth and is less time consuming.

We request a service discovery info only if we don’t have a similar ver attribute received before for an Instantbird session. On receive of the Query Stanza of type result containing the `identity` and `feature` child nodes we try to reconstruct the ver attribute as mentioned above. Upon successful regeneration we now know the entities mapped with the hashed string.

Send this entity information to the conversation binding by using an integer as a register and then creating an JS object from the same containing the entity list. The user will map his own capabilities to that of client’s and enable the support of only those services for whom intersection of flags is true for both the ends.

My next task is to implement the Entity Discovery Creation part which would be easy as most of the parts has been already covered.