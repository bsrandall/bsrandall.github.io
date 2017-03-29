---
layout: post
title: Debugging Spanning Tree Events
category: Spanning Tree
tag: knowledge
---
Here is a configuration for debugging Spanning Tree events:

```
SW1# debug spanning-tree events
SW1# debug condition vlan 2
SW1# config t
SW1(config)# service timestamps debug datetime msec
```