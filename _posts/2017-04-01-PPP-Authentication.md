---
layout: post
title: PPP Authentication
category: Layer 2 WAN
tag: knowledge
---
There are two forms of authentication available for PPP, PAP and CHAP. It is important to remember that these technologies are one way in nature, and therefore do not need to be configured bidirectionally. You really should think of this as a Client / Server model.

With PAP authentication, a two-way handshake is used to establish identity. After the PPP link establishment is complete, a username and password pair is repeatedly sent by the remote node (in clear text) until authentication is acknowledged, or the connection is terminated. PPP is not secure as passwords are sent across the link in clear text.

PAP supports either unidirectional or bidirectional authentication. This is the configuration for unidirectional, where R1 is the called device and R2 is the calling device:
```
R1(config)# username ROUTER2 password cisco
R1(config)# interface serial0/0
R1(config-if)# encapsulation ppp
R1(config-if)# ppp authentication pap
R1(config-if)# end
```
And here is the configuration for R2, the client:
```
R2(config)# interface serial0/0
R2(config-if)# encapsulation ppp
R2(config-if)# ppp pap sent-username ROUTER2 password cisco
R2(config-if)# end
```

CHAP identifies peers by use of a three-way handshake. The general steps are:
- After the LCP phase is complete, and CHAP is established as the authentication protocol between devices, the authenticator sends a challenge message to the peer
- The peer responds with a value calculated through a one-way hash function (MD5)
- The authenticator checks the response against its own calculation of the expected hash value. If the values match, the authentication is successful, otherwise the connection is terminated.

Like PAP, authentication is one-way but can be configured bidirectionally. In this example, R1 is the CHAP server and R2 is the CHAP client.
```
R1(config)# username ROUTER2 password cisco
R1(config)# interface serial0/0
R1(config-if)# encapsulation ppp
R1(config-if)# ppp authenticate chap
R1(config-if)# end
```
And now,  R2 (the client) configuration:
```
R2(config)# username ROUTER1 password cisco
R2(config)# interface serial0/0
R2(config-if)# encapsulation ppp
R2(config-if)# end
```