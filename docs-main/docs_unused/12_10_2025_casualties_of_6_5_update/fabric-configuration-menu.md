---
hide:
- toc
---

# Fabric Configuration Menu

## General Fabric
Manages fundamental network infrastructure settings, including a shared Anycast MAC address for redundancy and load balancing. It controls how network devices handle address aging and connection restoration, ensuring stable and efficient baseline network communication.

## Leaf Config
These settings control how leaf devices establish and maintain BGP connections, including timing for connection checks, routing updates, and connection establishment, ensuring stable and responsive network edge communications.

## Multihoming Config
Provides advanced timing controls that optimize connection stability and performance. These settings allow network administrators to fine-tune how devices handle interface state changes, link detection, and MAC address management. By adjusting Link State Timeout, Startup Delay, and MAC Holdtime, users can customize network resilience and reduce unnecessary connection disruptions.

## Spine Config
Defines how spine devices maintain and establish BGP (Border Gateway Protocol) connections. These settings manage network behaviors such as connection keepalive intervals, connection timeout periods, and routing information exchange.

## Reserved Ranges
The **Reserved Ranges** section displays a set of editable value ranges for networking identifiers used in the provisioning process. On a new system, it populates with working default values, so the user doesn't need to perform any custom configuration to have a working system.


## SFP Breakouts
SFP stands for Small Form-factor Pluggable. These are compact, hot-pluggable network transceivers used for both telecommunications and data communications applications.