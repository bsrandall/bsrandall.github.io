---
layout: post
title: VTP Messages
category: VTP
tag: knowledge
---
All VTP packets contain these fields in the header:
- VTP version (1, 2, or 3)
- VTP Message Type
	- Summary advertisements
	- Subset advertisement
	- Advertisement requests
	- VTP Join Messages
- Management domain length
- Management domain name

Most VTP packets contain the *configuration revision number* of the sender. This is used to determine if the received information is more recent than the current version.

By default, *summary advertisements* are sent every 5 minutes. The summary advertisement contains the VTP domain name and the current configuration revision number. If the VTP domain matches the switch's configured VTP domain, and the configuration revision number is higher than its own revision, the switch will send an *advertisement request*. Otherwise, it ignores the packet.

#### Summary Advertisement Packet Format
![][image-1]

A *subset advertisement* will follow a summary advertisement - it is the message that actually contains a list (or a subset of a list) of the VLANs being advertised.

A switch will send an *advertisement request* in these situations:
- the switch has been reset
- the VTP domain name has been changed on the switch
- the switch has received a VTP summary advertisement with a higher configuration than its own

[image-1]:	http://www.cisco.com/c/dam/en/us/support/docs/lan-switching/vtp/10558-21c.gif