---
layout: post
title: EtherChannel
category: EtherChannel
tag: knowledge
date: 2017-02-23 14:40:45
---
LAG goal is to trick our Spanning Tree Protocol into forwarding active/active across multiple links. The risk we take is an infinite loop in the data plane, as there is no TTL with Ethernet. The LAG negotiation protocols help to mitigate this risk. Static LAG is supported but not recommended, as a failure to LAG can cause an STP Loop. If you do deploy Static LAG, it is recommended to deploy EtherChannel Guard to help mitigate the chances of a loop.

PAgP and LACP accomplish the exact same thing, just in different ways.

Since both PAgP and LACP both require the member ports to have the same characteristics, a good command to start with is `show interfaces status`.