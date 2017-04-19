---
layout: post
title: IP SLA Overview
category: General Routing
tag: knowledge
date: 2017-02-20 17:40:45
---
Cisco IP SLA uses active traffic monitoring for measuring traffic performance. It performs this by generating traffic in a continuous, reliable, and predictable manner and then analyzing the results. The information collected includes response time, one-way latency, jitter, packet loss, voice quality scoring, network resource availability, application performance, and server response time.

If configuring simple IP SLA Operations such as ICMP echo, the operation only has to be configured on the local router. But for the more advanced Operations, you must set up the remote router or device to *respond* to your IP SLA traffic. The IP SLA Responder is a component embedded in the destination Cisco device that allows the system to anticipate and respond to IP SLA request packets. Only a Cisco device can be a source for a destination IP SLA Responder.

To see the IP SLA Operation types, enter IP SLA configuration mode as follows:
```
R1(config)#ip sla 1
R1(config-ip-sla)#?
IP SLAs entry configuration commands:
  dhcp         DHCP Operation
  dns          DNS Query Operation
  ethernet     Ethernet Operations
  exit         Exit Operation Configuration
  ftp          FTP Operation
  http         HTTP Operation
  icmp-echo    ICMP Echo Operation
  icmp-jitter  ICMP Jitter Operation
  mpls         MPLS Operation
  path-echo    Path Discovered ICMP Echo Operation
  path-jitter  Path Discovered ICMP Jitter Operation
  tcp-connect  TCP Connect Operation
  udp-echo     UDP Echo Operation
  udp-jitter   UDP Jitter Operation
  voip         Voice Over IP Operation
```

To set up a Cisco routing device as an SLA responder, you would use the following:
```
R1(config)# ip sla responder
```

After an IP SLA Operation has been configured, you must schedule the operation to run:
```
R1(config)# ip sla schedule 1 start-time now life forever
```

To then see the results of the IP SLA configuration, use the following:
```
R1# show ip sla statistics
```

So starting from the top, a real quick example of an IP SLA configuration to ping an IP address every 30 seconds for 3 hours would look like this:
```
R1(config)# ip sla 1
R1(config-ip-sla)# icmp-echo 150.1.3.3
R1(config-ip-sla-echo)# frequency 30
R1(config-ip-sla-echo)# exit
R1(config)# ip spa schedule 1 start-time now life 10800
R1(config)# exit
```