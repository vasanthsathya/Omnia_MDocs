---
title: "Changelog"
description: "Version Change"
tags: [Changelog, Version Updates]
search:
  boost: 0.1
hide:
  - toc
---

# Changelog

## Verity 6.6

_Release notes will be published here when Verity 6.6 ships. See the [BE Networks site](https://be-net.com/) or contact your sales representative for current release status._

## Verity 6.5

### New Features

| Feature | Description |
|-|-|
| PLM-247	Threshold Based Alarms for Time Series Data | Adds the ability to generate threshold alarms on any time series metrics and feed into system wide alarm mechansim |
| PLM-250	Support AS4625-54/30 with BE NOS | Support for Campus Environment only |
| PLM-251	sFlow Management and Display| Provision SONiC switches with sFlow capability and support Satori or external data collection|
| PLM-263	Tunable ROCEv2 Port Parameters| Allows for Adjustmennt of RoCE specific QOS varables 
| PLM-265	Support Collecting and Display of TCAM ASIC resource statistics| TCAM usage information displayed in Satori dashboard|
| PLM-273	React Framework| Migrate Tenant and Template Provisioning screens from Map style to React framework classic management methods|
| PLM-289	NBI Interface - Device On boarding and Changeset Enhancements| Allows for complete management of Verity from standard Northbound Interface|
| PLM-291	Full Support IPV6 for the Datacenter Overlay| IPV6 and Dual stack management of SONiC switches |
| PLM-297	Port Level - IP ACL Management| Apply INGRESS and EGRESS ACLs to SONiC switch ports |
| PLM-300	Hyperscale Architecture (Spine Plane)| Visual Display and Wiring validation of hyperscaler CLOS architectures |
| PLM-310	BFD Status Reporting and Alarming| Create alarms and status disaplys of BFD feature in Verity and Satori |
| PLM-322	Policy Based Routing| Manages Next Hop control of traffic INGRESSing switchports on SONiC switches| 
| PLM-326	Satori Dashboard images map| Add Switch images to Switch Dashboards within Satori| 

### Resolved Issues and Minor Feature Additions

| Issue | Description |
|-|-|
|IVN-20763	|Cannot change SNMP community string in Device Controller without hitting tab first
|IVN-20188	|System should be automatuically update on any feature flag changes
|IVN-19444	|Provide more detaul on "Oh No!" page for fatal web interface connection
|IVN-19158	|Need to block packet capture on (source or destination) mirror sessions
|IVN-18259	|Pie Graphs: Pie graphs in firmware sets in Upgrade page are reporting incorrect numbers
|IVN-18228	|SONiC Switch Marked Out of service does not gracefully remove traffic
|IVN-18187	|SFP Breakout DB updates are too slow. Improved update time for changes
|IVN-17480	|Partner Image Update package select should include package name
|IVN-17423	|Auto detect single SFPs in order to set speeds
|IVN-15783	|Changed management VLAN from Admin page, but management service did not change
