---
layout: post
title: PPP Multilink
category: Layer 2 WAN
tag: knowledge
---
Multilink PPP is a method used to aggregate multiple single PPP links and utilize them as one. It is not that dissimilar from EtherChannel used with Ethernet. PPP frames can be fragmented, sent down different links, and then reassembled in order on the far side of the link. Multilink PPP uses a 2 or 4 byte sequencing header in each packet, and the remote MLPPP recover is tasked with reconstructing the frames in the correct order. The configuration is pretty straightforward.

```
interface Serial0/1
  description Link to R1
  no ip address
  encapsulation ppp
  ppp multilink
  ppp multilink group 1
  serial restart-delay 0
end

interface Serial1/1
  description Link to R1
  no ip address
  encapsulation ppp
  ppp multilink
  ppp multilink group 1
  serial restart-delay 0
end

interface Multilink 1
  ip address 192.168.12.2 255.255.255.0
  ppp multilink
  ppp multilink group 1
end
```

Some optional parameters include `ppp multilink interleave`. Interleaving allows large packets to be multilink encapsulated and fragmented into a small enough size to satisfy the delay requirements of real-time traffic. The interleaving feature also provides a special transmit queue for the smaller, delay-sensitive packets, enabling them to be sent earlier than other flows. `ppp multilink fragement delay 10` is the command that determines the maximum delay - MLPPP will then chose a fragment size based on the configured delay.