---
layout: post
title: IPv6 Addressing
category: IPv6 General
tag: knowledge
date: 2017-04-16 17:54:45
---
IPv6 is a 128-bit address compared to IPv4 32-bit address. It is represented as 8 16-bit fields separated by colons. Since these 16-bit fields are written in hex, it is 8 four-digit hex values. A couple of rules exist to shorten the address:
- *leading* 0’s of any 16-bit field can be eliminated :00FF can become :FF
- any single contiguous string of one or more 16-bit segments consisting of all 0’s can be shortened with a double colon - FE80:0000:0000:0000:0000:0000:0000:0001 becomes FE80::1
	- however only one double colon is allowed to exist in any address.

Within an IPv6 address, each hexadecimal number represents 4 bits. For example F represents 1111 and 8 represents 1000. IPv6 address format makes it very clear that an address is not something numerical, it is a bit string versus a numerical number. IPv4 often fools people into thinking the address is something that can be quantified when it cannot.

IPv6 prefixes are always identified with a bitcount. 3ffe:1944:100:a::bc:2500:d0b/64 for example. When you are writing just the prefix, you set the host bits to all 0’s just as you would with an IPv4 address - 3ffe:1944:100:a::/64 would be the prefix of the address above.

On Cisco routers, IPv6 routing has to be specifically enabled using the global configuration command **ipv6 unicast routing**. If a router is configured with IPv6 addresses, but IPv6 is not enabled using the **ipv6 unicast routing** command, then the router is essentially acting as an IPv6 host.
