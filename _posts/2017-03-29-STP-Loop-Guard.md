---
layout: post
title: Spanning Tree Loop Guard
category: Spanning Tree
tag: knowledge
---
Loop Guard is a Spanning Tree feature that was added to prevent loops from forming due to hardware issues or STP software problems. A Spanning Tree loop occurs when a port that was previously in the blocking state is erroneously  transitioned to the Forwarding state.

When a non-designated port stops receiving BPDUs, it will eventually transition itself to a designated port and begin forwarding BPDUs. Loop Guard works by preventing that non-designated port from transitioning to a forwarding state. Instead, it transitions the port to STP loop-inconsistent blocking state. So Loop Guard prevents a non-designated port from becoming a designated port, while Root Guard prevents a designated port from transitioning to a Root Port.

Loop Guard is very similar to UDLD, but Loop Guard uses STP BPDUs to determine if there is a loop.

Loop Guard is enabled on a per-port basis with the interface subcommand `spanning-tree guard loop`. To be completely effective, Loop Guard should be enabled on *all* non-designated ports, including root ports and alternate ports. Loop Guard can also be enabled globally with the `spanning-tree loopguard default` global configuration command. You can then disable Loop Guard on a per-port basis with `no spanning-tree guard loop`.


