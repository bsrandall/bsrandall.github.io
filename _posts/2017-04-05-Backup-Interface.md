---
layout: post
title: Backup Interface
category: General Routing
tag: knowledge
---
Backup Interface is a Cisco feature that can be used in place of floating static routes on point-to-point interfaces. 

```
interface Serial0/0/0
  backup interface Serial0/0/1
  backup delay 10 30
```
In the example above interface Serial0/0/1 is the backup for interface Serial0/0/0. If Serial0/0/0 is down for 10 seconds, then Serial0/0/1 will take over as the primary interface. After Serial 0/0/0 has been up for 30 seconds, it will resume its role as the primary interface.