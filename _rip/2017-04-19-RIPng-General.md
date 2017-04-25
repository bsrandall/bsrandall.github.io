---
layout: post
title: RIPng General
category: RIPng
tag: knowledge
date: 2017-04-19 20:36:45
---
RIPng is based on RIPv2, but is not an extension and rather an entirely new protocol. RIPng has no support for IPv4, so in order to run dual stack you must run both RIP and RIPng.

But RIPng uses the same timers, procedures, and message types as RIPv2. One exception is authentication, which with RIPng is performed via the built-in authentication methods of IPv6.

Unlike RIPv1 and RIPv2 which run on UDP port 520, RIPng operates on UDP port 521.

The message format is slightly different. Unlike with RIPv2, each route does not list a next-hop address. Instead, RIPng specifies the next-hop address in a special route entry and then groups all route entries that use the next-hop address after it.