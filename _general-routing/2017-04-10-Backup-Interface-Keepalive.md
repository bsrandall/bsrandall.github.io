---
layout: post
title: Backup Interface and Keepalives
category: General Routing
tag: knowledge
date: 2017-04-10 13:40:45
---
By default, the state of a point-to-point GRE interface is determined by routing availability for the tunnel destination, thus as long as the router has a route for the tunnel destination, the tunnel interface state will be UP. However, this does not account for possible transit issues. To fix the problem, GRE keepalives can be enabled on the point-to-point GRE tunnels. The format of the command is `keepalive <interval> <number_of_retries>`. The interval defines the frequency in seconds for sending keepalives and the number of retries defines the maximum number of keepalives being sent after the first failed keepalive, before the router changes the tunnel state to DOWN.
