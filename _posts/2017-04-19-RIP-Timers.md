---
layout: post
title: RIP Timers
category: RIP
tag: knowledge
date: 2017-04-19 08:06:45
---
There are several timers related to RIP. The **update timer** on Cisco routers varies between 25.5 and 30 seconds (to prevent synchronization). This is the interval a router waits before sending new periodic Response messages.

Cisco calls the expiration timer (or timeout) the **invalid timer**. This is the amount of time a route can stay in the route table without being updated. The default Cisco invalid timer for RIP is 180 seconds (6 Update periods). If an updated route is not heard within the invalid timer, the hop count for the route is changed to 16, the equivalent of making the route unreachable. In IOS, the route in the routing table will say “possibly down” when viewed via `show ip route`.

The **garbage timer** (or flush timer) is the amount of time the route that was made unreachable by the invalid timer will continue to be advertised.. Once the garbage timer expires, the route will be completely removed from the routing table. With Cisco IOS it is set to 240 seconds by default, 60 seconds longer than the invalid timer.

RFC 1058 for RIP does not call for the use of **holddown timers**, but Cisco’s implementation implements it. We saw this earlier - the timer starts when a route is received that is already in the route table, but the new route has a higher hop count than the stored route. It is 180 seconds by default.

The four timers can be manipulated with the command:
**timers basic** *update invalid holddown flush*