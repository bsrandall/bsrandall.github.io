---
layout: post
title: Administrative Distance
category: General Routing
tag: knowledge
---
Administrative Distance is used to determine which route should be installed into the IP routing table when there is a tie between different sources for the route (static vs EIGRP vs OSPF, etc). Administrative Distance is sometimes called the trustworthiness of the source. When a decision has to be made, the table containing Administrative Distance is consulted to choose the best route, with lower being better. Administrative Distance is only local and can be different for each router.

The `distance` command is used with the different routing protocols to change its Administrative Distance. Here is a list 

| **Routing Protocol**      | **AD** |
| Directly connected  | 0    |
| Static route| 1 |
| EIGRP Summary | 5 |
| External BGP | 20 |
| EIGRP | 90 |
| IGRP | 100 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| ODR | 160 |
| External EIGRP | 170 |
| Internal BGP | 200 |  
| Unknown | 255 |

