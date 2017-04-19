---
layout: post
title: Neighbor Discovery Protocol
category: IPv6 General
tag: knowledge
date: 2017-04-17 16:54:45
---
Neighbor Discovery Protocol (NDP) is used by IPv6 hosts and routers for the following purposes:
- Stateless Address Autoconfiguration (SLAAC)
- Duplicate Address Detection
- for Layer-2 Data-Link address resolution (similar to IPv4 ARP)
- to determine if neighbors are reachable (Neighbor Unreachability Detection)
- when a router fails, a host actively searches for functioning alternates.

Neighbor Discovery uses 5 ICMPv6 messages:
1. Router Solicitation message
2. Router Advertisement message
3. Neighbor Solicitation message
4. Neighbor Advertisement message
5. Redirect message

Router Solicitation messages are used by hosts when it needs prefix, prefix length, default gateway, and other information for Stateless Address Autoconfiguration (SLAAC). Router Advertisement messages are the messages used by Routers to convey that information to hosts.

Neighbor Solicitation and Neighbor Advertisement messages are two more protocols that use ICMPv6 Neighbor Discovery. These messages are used by a device to request Layer 2 link layer address information from another device on the same network or to provide this information to the requesting device. Neighbor Solicitation and Neighbor Advertisement messages are part of three important processes:
1. Address resolution
2. Duplicate Address Detection (DAD)
3. Neighbor Unreachability Detection (DUD)

An IPv6 host will maintain two tables for each interface:
- Neighbor cache
- Destination Cache

The Neighbor cache is equivalent to an ARP table in IPv4. The neighbor cache contains mappings of hosts on the same network, while the destination cache contains layer-2 to layer-3 resolutions for devices on other links or networks.  To see the Neighbor table, issue `show ipv6 neighbors` command.

