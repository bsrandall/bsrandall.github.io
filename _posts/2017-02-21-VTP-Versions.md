---
layout: post
title: VTP Versions
category: VTP
tag: knowledge
---
VTP is a Cisco proprietary protocol that allows VLAN administration to be shared across switches. It gives an administrator the capability to centrally administer VLAN creation across one or two switches, and have those VLANs propagate across a VTP domain made up of any number of switches.


There are 3 versions of VTP, versions 1, 2, and 3.  There are not many significant changes between versions 1 and 2, except version 2 introduced support for Token Ring VLANs.

Version 3 introduced the following enhancements:
- hidden authentication (does not appear in plain text in the configuration file)
- Extended VLAN support. Versions 1 and 2 only support VLANs 1 - 1000 only.
- Support for private VLANs
- Support for MST
- primary and secondary servers

With version 3, there are two types of VTP servers - primary and secondary. There is only one primary server, and the rest of the secondary servers act as backups to the primary. To declare a server as primary, use the following:
```
`SW1# vtp primary vlan
```
Notice the command is done in privileged mode, not configure mode!