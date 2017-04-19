---
layout: post
title: Policy Based Routing
category: General Routing
tag: knowledge
---
Policy-based routing can be used to change the next-hop IP address for traffic matching certain criteria. This can be useful to overrule the routing table for certain types of traffic. For example you may want to force all traffic from a certain host to use an alternate link. The key to making this work is an access-list and a route map.

For example, let’s assume that we want all ICMP traffic from host 192.168.1.100 to traverse a link whose next hop is 192.168.13.3 if the destination IP address is 4.4.4.4. We can use an extended access list to classify the traffic.
```
`R1(config)# ip access-list extended ICMP-H1
R1(config-ext-nacl)# permit imp host 192.168.1.100 host 4.4.4.4
R1(config)# end
```
`Now the next step would be to use a route map to set the next hop IP when we have a match.
```
`R1(config)# route-map PBR-H1 permit 10
R1(config-route-map)# match ip address ICMP-H1
R1(config-route-map)# set ip next-hop 192.168.13.3
R1(config)# end
```
`Now, we must make sure we activate it on the ingress interface.
```
`R1(config)# interface GigabitEthernet0/1
R1(config-if)# ip policy route-map PBR-H1
R1(config)# end
```
`
`debug ip policy` will turn debugging on for policy routing.

This configuration is for traffic passing *through* the router. To apply policy based routing for traffic that is 8originated8 by the router, see the next post “Local Policy Routing”.

One thing to remember is that there can only be one ip policy on the interface, so if you need to perform multiple actions, you may have to use a route map with multiple sections like this.
```
`R1(config)# route-map RM-R4-R6 permit 20
R1(config-route-map)# match ip address FROM-R4
R1(config-route-map)# set ip next-hop 155.146.13.1
R1(config-route-map)# route-map RM-R4-R6 permit 20
R1(config-route-map)# match ip address FROM-R6
R1(config-route-map)# set ip next-hop 155.1.0.5
R1(config-route-map)# exit
```
`
Some important show commands are listed below:
```
`R1#sh ip policy
Interface      Route map
Gi0/1.146      RM-R4-R6
R1\#
```
````
`R1#show route-map
route-map RM-R4-R6, permit, sequence 10
  Match clauses:
ip address (access-lists): FROM_R4
  Set clauses:
ip next-hop 155.1.13.3
  Policy routing matches: 18 packets, 1116 bytes
route-map RM-R4-R6, permit, sequence 20
  Match clauses:
ip address (access-lists): FROM_R6
  Set clauses:
ip next-hop 155.1.0.5
  Policy routing matches: 9 packets, 564 bytes
```
`