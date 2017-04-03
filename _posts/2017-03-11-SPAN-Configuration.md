---
layout: post
title: SPAN Configuration
category: Layer 2
tag: configuration
---
Basic SPAN Configuration:

```
SW1(config)# monitor session 1 source interface fa0/12
SW1(config)# monitor session 1 destination interface fa0/24
```

Here is an example where we will only monitor respective traffic from fa0/18 and only monitor sent traffic from interface fa0/19. Additionally we will filter (remove) VLANs 1 through 3. Finally, we will preserve the encapsulation from the sources:

```
SW1(config)# monitor session 1 source interface fa0/18 rx
SW1(config)# monitor session 1 source interface fa0/19 tx
SW1(config)# monitor session 1 filter vlan 1-3
SW1(config)# monitor session 1 destination interface fa0/24 encapsulation replicate
```

Next we have a RSPAN sample configuration. We will monitor all traffic on VLANs 66-68 on SW1 and send it to VLAN 199, which will then be delivered to port fa0/24 on SW2:

```
SW1(config)# vlan 199
SW1(config-vlan)# remote span
SW1(config-vlan)# exit
SW1(config)# monitor session 1 source vlan 66-68
SW1(config)# monitor session 1 destination remote van 199
```
```
SW2(config)# vlan 199
SW2(config-vlan)# remote span
SW2(config-vlan)# exit
SW2(config)# monitor session 2 source remote vlan 199
SW2(config)# monitor session 2 destination interface fa0/24
```

Notice above that the monitor session numbers do not have to match on each switch.

Finally, we have a ERSPAN example. We will configure R1 to capture received traffic and send it to SW1 gig2/1.

```
R1(config)# monitor session 1 type erspan-source
R1(config-mon-erspan-src)# source interface gig1/1 rx
R1(config-mon-erspan-src)# no shutdown
R1(config-mon-erspan-src)# destination
R1(config-mon-erspan-src-dst)# erspan-id 101
R1(config-mon-erspan-src-dst)# ip address 10.1.1.1
R1(config-mon-erspan-src-dst)# origin ip address 172.16.1.1
```
```
SW1(config)# monitor session 2 type erspan-destination
SW1(config-mon-erspan-dst)# destination interface gig2/1
SW1(config-mon-erspan-dst)# no shutdown
SW1(config-mon-erspan-dst)# source
SW1(config-mon-erspan-dst-src)# erspan-id 101
SW1(config-mon-erspan-dst)# ip address 10.1.1.1
```

A couple of configuration notes. First, you must make sure the destination port is not in a shutdown state or else the SPAN session will not come up.

If you want to leave the original encapsulation of the frames intact, use the `encapsulation replicate` option on the monitor session destination command. 

One confusing option is the `ingress dot1q vlan 10` option on the destination interface. This is actually telling the switch to accept incoming frames on the *destination* monitor switch and place the frames in VLAN 10. This would let you use the destination port like a normal access port. Seems kind of silly to me as to why you would want to do that, but I am sure there is a reason.

```
`monitor session 1 destination interface gig0/24 ingress dot1q vlan 146
```
`The above accepts inbound packets with 802.1Q encapsulation with the given VLAN as the default VLAN. Compare that to the example below, which accepts incoming packets with untagged encapsulation type with the specified VLAN as the default VLAN.
```
`monitor session 1 destination interface gig0/24 ingress vlan 146
```
`
To view the session, simply use `show monitor session 1`.

