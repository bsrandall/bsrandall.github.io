---
layout: post
title: Private VLANs
category: Layer 2
tag: knowledge
---
Protect Ports (discussed earlier) are a nice security feature of Cisco switches. When two ports are protected, they are not allowed to have direct communication with each other. But one limitation of protected ports is that they are only locally significant, so there is no way for protected ports to exist on different switches and follow the protection rules.

The Private VLAN feature was created to solve this limitation. Private VLANs are more complex and can span multiple physical switches. Private VLANs split what would normally be a single broadcast domain defined by a single VLAN into multiple isolated broadcast subdomains, that are defined by a primary VLAN and its secondary VLANs. In essence it allows us to create VLANs inside VLANs, and is not un-similar to the concept of Confederations in BGP.

Private VLANs are used to increase security. We most often see them in a shared color facility. This allows the color provider to have the customers exist on the same VLAN (and thus the same subnet), without allowing the different customers to communicate directly with each other.

One pitfall you have to remember with Private VLANs is that it requires VTP to either be in Transparent mode or to be off.

There is some terminology to remember when dealing with Private VLANs:
- *Promiscuous ports* are allowed to talk to all other ports within the primary VLAN
- *Isolated ports* are only allowed to talk with promiscuous ports
- *Community ports* are allowed to talk with other ports in their own community as well as any promiscuous ports,  but they are not allowed to talk to ports in other communities

The configuration steps are a little unnatural as well. The port roles are defined by the interface’s association to a primary VLAN and one or more secondary VLANs. First the secondary VLANs are created and defined as either community or isolated. Then the primary VLAN is defined, and the secondary VLANs are associated with the primary VLAN.

Here is an example configuration with VLAN 500 as the primary VLAN, 501 a secondary community VLAN, and VLAN 502 a secondary isolated VLAN. Ports FastEthernet0/1 and FastEthernet0/2 are associated to VLAN 501, while FastEthernet03 and FastEthernet0/4 are associated with the secondary isolated VLAN 502.

```
SW1(config)# vtp mode transparent
SW1(config)# vlan 501
SW1(config-vlan)# private-vlan community
SW1(config-vlan)# vlan 500
SW1(config-vlan)# private-vlan primary
SW1(config-vlan)# private-vlan association add 501
```

Next, let’s go ahead and associate FastEthernet0/1 and FastEthernet0/2 to the 501 Secondary Community we just created:
```
SW1(config)# interface range fa0/1-2
SW1(config-if-range)# switchport mode private-vlan host
SW1(config-if-range)# switchport private-vlan host-association 500 501
```

Now, we can go ahead and configure FastEthernet0/24 as a promiscuous port.
```
SW1(config)# interface fa0/24
SW1(config-if)# switchport mode private-vlan promiscuous
SW1(config-if)# switchport private-vlan mapping 500 501
```

Now we turn our attention to the creation of the isolated VLAN, VLAN 502.
```
SW1(config)# vlan 502
SW1(config-vlan)# private-vlan isolated
SW1(config-vlan)# vlan 500
SW1(config-vlan)# private-vlan primary
SW1(config-vlan)# private-vlan association add 502
```

Now we must associate our interfaces:
```
SW1(config)# interface range fa0/3-4
SW1(config-if-range)# switchport mode private-vlan host
SW1(config-if-range)# switchport private-vlan host-association 500 502
```

And finally, we must add another association for our promiscuous port:
```
SW1(config)# interface fa0/24
SW1(config-if)# switchport mode private-vlan promiscuous
SW1(config-if)# switchport private-vlan mapping 500 502
```

One great way to test your Private VLAN setup is to send a single ping to the broadcast address with `ping 255.255.255.255 repeat 1`.  The replies will only be from the hosts in your broadcast domain.