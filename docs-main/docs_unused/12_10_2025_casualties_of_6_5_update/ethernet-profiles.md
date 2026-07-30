---

title: "Ethernet Port Profiles (Eth-Port Profiles)"
description: "How to create Services and VLANS"
tags: [Service, VLAN]
search:
  boost: 2           # ← Lower than main overview
parent: Advanced Configuration
hide:
- toc
---
# Ethernet Port Profiles (Eth-Port Profiles)
An **Eth-Port Profile** is a package of **Services** provided by this port.  This object simplifies the provisioning of ports by allowing the operator to group related services (Layer-2 VLANs) that are required by servers.

## Creating an Eth-Port Profile
1. Navigate to the Eth-Port Profiles section by clicking **Templates (![](media/buttons/6.3/button_templates.png){: class="btn"}) / Templates / Eth-Port Profiles**. ![](media/199151ed05ad043796bab1e39a8d52ec.png){: class="pop"}
1. Create a new Eth-Port Profile object by clicking the **Add** button (![](media/buttons/6.2/button_add_item.png){: class="btn"}). 
1. In the prompt that appears, name the Eth-Port Profile and assign it a group.
1. Check the **Enable** box.

### Assigning Services to an Eth-Port Profile
1. Open the Eth-Port Profile tile and set the **Service** and **External VLAN** from the drop down menu. ![](media/eth_port_settings_service.png){: class="pop"}
1. Enable your selection(s) by selecting the **Enable** checkbox.