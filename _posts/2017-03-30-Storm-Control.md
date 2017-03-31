---
layout: post
title: Storm Control
category: Layer 2
tag: knowledge
---
Broadcast storms can create havoc on a Layer 2 network, quickly bringing the network to an unusable state. Software solutions to storm control are inefficient, because by the time the software has identified the storm, the hardware resources are at max utilization and there is no resources available to abate the storm.

Cisco has a storm control feature built into its switches. It is a hardware based solution that allows us to set a threshold on interfaces to limit the amount of broadcast, multicast, or unknown unicast traffic an interface receives. It also allows us to select a couple of actions to take when that threshold is met.

Let’s jump right into a configuration example.
```
SW1(config)# interface GigabitEthernet0/1
SW1(config-if)# storm-control broadcast level 30
```

The ’30’ in the example above designates the rising threshold. When broadcast traffic exceeds 30% of the interface bandwidth, storm control will kick in and take action. The default action is to drop exceeding traffic.

You can also specify bps as below. Adding k, m, or g identifies the value as Kbps, Mbps, or Gbps respectively. The example below would limit broadcast traffic to 30 Mbps on the Gigabit interface.
```
SW1(config)# interface GigabitEthernet0/1
SW1(config-if)# storm-control broadcast level bps 30m
```

You can also designate a falling threshold. The falling threshold sets a value to which the traffic has to fall before that type of traffic is allowed again.
```
SW1(config)# interface GigabitEthernet0/1
SW1(config-if)# storm-control broadcast level bps 30m 20m
```
In the example above the broadcast traffic would have to drop below 20 Mbps before any broadcast traffic would be allowed into the port.

We can also control the action. `storm-control action shutdown` shuts the interface down in case the level is exceeded. `storm-control action trap` sends an SNMP trap if the level is exceeded.

`show storm-control [unicast | multicast | broadcast]` is used to see the configuration as well as the current amount of traffic passing through the port. 