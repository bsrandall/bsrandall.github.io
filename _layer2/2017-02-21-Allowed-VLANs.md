---
layout: post
title: VLANs
category: VLAN
tag: knowledge
date: 2017-02-21 15:40:45
---
By default, all VLANs are allowed to traverse an 802.1Q trunk once it is active. To restrict which VLANs are allowed to cross a trunk, you must go into IOS and explicitly define the VLANs that are allowed.

`SW1# switchport trunk allow VLAN 15-20,22,25`

`SW1# switchport trunk allowed vlan add 27`

`SW1# switchport trunk allowed vlan remove 18`

You must remember that if an allowed VLAN list is already configured on a trunk, issuing the `SW1# switchport trunk allowed vlan 16-20,2,25` command will overwrite the previously defined VLANs. You must use the *add* and *remove* commands if there is already an allowed clan configuration in the running config.