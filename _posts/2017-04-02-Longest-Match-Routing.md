---
layout: post
title: Longest Match Routing
category: General Routing
tag: knowledge
date: 2017-04-02 14:40:45
---
Longest Match Routing is the idea that a packet will follow the most specific route entry that it matches. So if there was a host route (/32) that existed for the destination, the host route would have precedence over any shorter prefix such as a /24.