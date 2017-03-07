---
layout: post
title: CDP Configuration
category: Layer 2
tag: configuration
---

To enable CDP globally we use `cdp run`. To enable CDP on a per-interface basis, use `cdp enable`.

`R1#(config) cdp timer seconds`  specifies the frequency of CDP update transmissions.

`R1#(config) cdp holdtime seconds` specifies the amount of time a receiving device should hold the information sent by your device before discarding it.

`R1#(config) no cdp adertise-v2` disables the advertisement of CDPv2 advertisements if for some crazy reason you need to.

`R1#(config) clear cdp counters` resets the traffic counters to zero.

`R1#(config) clear cdp table` deletes the CDP table of information about neighbors

`R1#(config) show cdp` displays the interval between CDP transmissions, the number of seconds a CDP advertisement is valid for a given port, and the version of the advertisement

`R1#(config) show cdp interface [type number]` displays information about interfaces on which CDP is enabled

`R1#(config) show cdp entry device-name` displays information about a specific neighbor

