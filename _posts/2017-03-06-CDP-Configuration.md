---
layout: post
title: CDP Configuration
category: CDP
tag: configuration
---

To enable CDP globally we use `cdp run`. To enable CDP on a per-interface basis, use `cdp enable`.

`cdp timer *seconds*`  specifies the frequency of CDP update transmissions.
`cdp holdtime *seconds*` specifies the amount of time a receiving device should hold the information sent by your device before discarding it.