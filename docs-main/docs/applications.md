---
title: "Applications"
description: "Assign IP Address to VLAN"
tags: [VLAN, Service]
search:
  boost: 1
parent: Advanced Configuration

hide:
- toc
---

# Applications

**Applications** enable users to select VLAN interfaces and configure IP address assignments for those interfaces on the switch.
This feature enables network segmentation and service configuration by allowing users to associate IP addresses with defined Services. 

![](media/applications_6_6.png)

Each Service represents a logical grouping of VLAN configuration parameters, providing a streamlined approach to network resource allocation and traffic management. 

![](media/applications_values.png)

## Create IP-to-VLAN Mapping
1. To perform the IP-to-VLAN mapping you need to edit-enable (![](media/buttons/6.2/btn_edit.png){: class="btn"}) in the Applications tile. ![](media/applications_edit.png){: class="pop"}
1. Select the desired Service from the **Service** drop-down menu. ![](media/application_service.png){: class="pop"}
1. Under the field titled **Source IP/MASK**, type the desired IP/MASK. ![](media/applications_ip_mask.png){: class="pop"}
1. Enable the change ![](media/buttons/6.2/enable_check.png){: class="pop"} and save the edit (![](media/buttons/6.2/save.png){: class="btn"}).