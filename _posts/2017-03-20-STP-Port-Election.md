---
layout: post
title: STP Root Bridge Election
category: Spanning Tree
tag: knowledge
---
After the election of the STP Root Bridge, all ports in the Layer 2 Switch topology will need to be assigned a state. The steps can be listed as follows:
- All ports on the Root Bridge become Designated Ports
- On each non-root switch, exactly ONE port is elected as the *Root Port* which is the port having the lowest path-cost to the Root Bridge.
- Each segment between switches will have one Designated Port which is the port on the segment that has the lowest path-cost to reach the root bridge.
- The Root and Designated Ports are placed into a Forwarding State.
- The ports that are not Root ports or Designated Ports will be placed in the Blocking State. These are displayed in show commands with an A for Alternate.

It is helpful to remember that Designated Ports lead away from the Root Bridge, while Root Ports lead toward the Root Bridge.

What are the tiebreakers for Root Ports and Designated Ports?

The tiebreaker for Spanning Tree decisions is as follows:
- Lowest root bridge ID (used for root bridge election)
- Lowest path cost to root bridge
- Lowest sender bridge ID (used when a switch is connected to two switches through which it has equal cost to reach the root bridge)
- Lowest sender port ID (when the switch has two interfaces connecting to the same switch and the cost to reach the root bridge is the same through either interface, it will use the interface with the lowest number as the root port (or designated port).

It is helpful to keep in mind for elections that there is only one bridge that originates BPDUs - the root bridge. Other bridges update some fields (such as Sending Bridge ID, Message Age, etc) when retransmitting out their designated ports.

The access ports will be designated ports typically and will send BPDUs toward the host, unless BPDU Filter is set.