---
layout: post
title: Spanning Tree BPDU Filter
category: Spanning Tree
tag: knowledge
date: 2017-03-28 14:40:45
---
BPDU Filter is another optional feature of STP. It is similar to BPDU Guard, in that it is used to terminate the STP domain. Like BPDU Guard, it can be enabled globally or per interface, but unlike BPDU Guard, BGPU filter behaves differently depending on how it is enabled.

If BPDU Filter is enabled at the interface level, it silently drops all received inbound BPDUs and does not send outbound BPDUs. Unlike BPDU Guard, there is no err-disabled option for BPDU Filter. Here is an example of BPDU Filter enabled at the interface level:
```
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
SW1(config-if)# spanning-tree bpdufilter enable
```

When BPDU Filter is enabled globally, it will only affect PortFast enabled ports. The switch will send out exactly 11 BPDUs, and inbound BPDUs are not filtered. The reason 11 BPDUs are sent is the default Hello timer is 2 seconds and the default Max Age timer is 20 seconds. If the switch receives inbound BPDUs, the port loses its PortFast status and STP is negotiated normally on that port. For this reason, you can say that BPDU Filter enabled globally is a safer option than BPDU enabled at the interface level, as STP loops cannot form.