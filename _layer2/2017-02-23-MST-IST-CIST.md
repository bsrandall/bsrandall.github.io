---
layout: post
title: MST IST-CIST
category: MST
tag: knowledge
date: 2017-02-23 12:40:45
---

IST is the Internal Spanning Tree, also known as instance 0. This instance is designated to carry all STP information, including information from other instances. MSTP does not send BPDUs for ever instance separately - these are all contained within the IST BPDU.

To accommodate, the other instances information is carried within the IST BPDU using special M-Record fields - one for every active MSTI. These fields carry carry MSTP information such as bridge priority, root path cost, and port priority.

IST also plays a huge role in multiple MSTP region configurations. When a switch receives a BPDU from another region, it marks the corresponding port as MSTP *boundary*. The interconnected, different region switches then form a CIST spanning across the regions.

![][image-1]

Remember, an IST is internal to a region while a CIST is the IST spanning across multiple regions.

Here is a sample MST BPDU:

![][image-2]

The CIST Root is elected among all regions while the CIST Regional Root is elected in every region. The IST Root = CIST Regional Root in cases where multiple MST regions interoperate. The CIST Root is the bridge that has the lowest Bridge Id among all regions - the CIST Root could be a bridge inside a region or a boundary switch in a region. The CIST Regional Root is a *boundary switch* elected for every region based on the shortest external path cost to reach the CIST Root. As mentioned above, it is important to remember that the CIST Regional Root becomes the root of the IST for the given region as well - the region changes its IST election process to make the CIST Regional Root the IST root.

When an MST switch boots up, it declares itself the CIST Root and CIST Regional Root and announce that it its outgoing BPDUs on all internal ports. On boundary ports (those that have received BPDUs from another region), the switch will only advertise its CIST Root Bridge ID and CIST External Root Path Cost, hiding the details of the region’s inner topology.

The region that contains the CIST Root automatically places all of its boundary ports in an unblocked state.

The *CIST External Root Path Cost* is the cost to reach the CIST Root across the links connecting the boundary ports. When a BPDU is received on an internal link, this cost is not changed.

Only a boundary switch can be elected as the CIST Regional Root, and this is the switch with the lowest cost to reach the CIST Root. If a boundary switch receives a BPDU with a lower CIST External Root Path cost on one of its internal ports, it will stop announcing itself as the CIST Regional Root and start announcing the new metric out of its boundary ports.

If a switch is a CIST Regional Root, it elects one of its boundary ports as the CIST Root port and blocks all other boundary ports. If a boundary switch is not the CIST Regional Root, it will mark its boundary ports as Designated or Alternate, Designate only if it has a better External Root Path cost or in case of a tie, lower CIST Regional Root Bridge ID.

The regional MSTIs are constructed independently at every region, but they have to be mapped to the CIST at the boundary ports. This equates to the inability to load-balance VLAN traffic on the boundary links by mapping VLANs to different instances.

A topology change in the CST could change all paths in the topology thus requiring massive MAC address relearning.


[image-1]:	http://blog.ine.com/wp-content/uploads/2010/02/mstp-3-multi-region-physical-topology.png
[image-2]:	http://blog.ine.com/wp-content/uploads/2010/02/mstp-3-multi-region-cst-mstp-packet-format.png