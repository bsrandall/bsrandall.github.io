---
layout: post
title: CDP Configuration
category: CDP
tag: configuration
---

To enable CDP globally we use `cdp run`. To enable CDP on a per-interface basis, use `cdp enable`.

`R1#(config) cdp timer seconds`  specifies the frequency of CDP update transmissions.

`R1#(config) cdp holdtime seconds` specifies the amount of time a receiving device should hold the information sent by your device before discarding it.