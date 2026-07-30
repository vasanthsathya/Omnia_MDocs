---
title: "Parameters"
description: "Verity Parameters List"
tags: [Parameters, API]
search:
  boost: 0.01
parent: Miscellaneous
hide:
  - toc
---

| Parameter Group | UI View | Name | Default | Description |
|-|-|-|-|-|
| Site | Frames at the bottom of the Network Section | Aggressive Reporting | "true" | Fast Reporting of Switch Communications, Link Up/Down, and BGP Status |
||| Anycast MAC Address| "(auto)" | Site Level MAC Address for Anycast |
||| CRC Failure Threshold | "5"| Threshold in Errors per second that when met will disable the links as part of LAGs|
||| Enable DHCP Snooping| "false"| Enables the switches to monitor DHCP traffic and collect assigned IP addresses which are then placed in the DHCP assigned IPs report. |
||| BGP Advertisement Interval| "30"| Leaf BGP Advertisement Interval |
||| BGP Connect Timer| "120" | BGP Connect Timer|
||| BGP Hold Down Timer| "180" | Leaf BGP Hold Down Timer|
||| BGP Keep Alive Timer| "60"| Leaf BGP Keep Alive Timer |
||| MAC Address Aging Time| "600" | MAC Address Aging Time |
||| MCLAG Delay Restore Timer| "300" | MCLAG Delay Restore Timer |
||| BGP Advertisement Interval| "30"| Spine BGP Advertisement Interval|
||| BGP Connect Timer| "120" | BGP Connect Timer|
||| BGP Hold Down Timer| "180" | Spine BGP Hold Down Timer |
||| BGP Keep Alive Timer| "60"| Spine BGP Keep Alive Timer|
||||||
| AS Path| Global Section - Route Map Definitions| Notes|""| User notes describing this provisioning object |
||| Enable | "false"| Enable flag of this provisioning object|
||| Enable | "false"| Enable of this AS Path Access List |
||| Regular Expression |""| Regular Expression to match against BGP Community Strings|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Permit/Deny| "permit" | Action to take on a match of the Community Strings, either Permit or Deny |
||||||
| User Authentication| Admin Tab - Users and Permissions| Overridden Object| "0"| Denotes provisioning object that has been overridden.|
||| isPredefined | "false"| Denotes this is a predefined provisioning object|
||| Enable | "true"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Server \# Enable| "false"| Enable flag of this Authentication server|
||| Server \# IP |""| IP of this Authentication server|
||| Server \# Port| "1812"| Port of this Authentication server |
||| Server \# Role| "Auth"| Role of this Authentication server |
||| Server \# Shared Secret|""| Shared Secret of this Authentication server |
||||||
| Badges | Global Section - Badges| Notes|""| User notes describing this provisioning object |
||| Color| "blue"| Color of Badge|
||| Enable | "true"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Number | "0"| Number of Badge|
||||||
| Device Controller| VNFs Device Controllers| CLI Access Mode | "SSH" | CLI Access Mode|
||| SNMP Community String | "private"| Comm Credentials |
||| Comm Type | "snmpv2" | Comm Type|
||| Co-located VNFs | "routed" | vNetC and SD LAN Controller are both located in the managed compute server|
||| Gateway|""| Gateway |
||| IP and Mask|""| IP and Mask|
||| IP Source | "dhcp"| IP Source|
||| Uses Tagged Packets| "false"| Indicates if the direct interface expects tagged or untagged packets|
||| Enable Password |""| Enable Password - to enable privileged CLI operations|
||| Enable | "false"| Enable flag of this provisioning object|
||| Switch |""| Switchpoint locating the Switch to be controlled|
||| Upstream is LAG | "false"| If checked, then ZTP will provision the TOR switch with the first 32 ports as a lag to facilitate plug-n-play |
||| LAG |""| LAG|
||| LLDP Search String |""| Optional unless Located By is 'LLDP' or Device managed as 'Active SFP'. Must be either the chassis-id or the hostname of the LLDP from the managed device. Used to detect connections between managed devices. If blank, the chassis-id detected by the Device Controller via SNMP/CLI is used |
||| Located By| "LLDP"| Controls how the system locates this Device within its LAN |
||| Switchpoint|""| Switchpoint reference|
||| Managed on native VLAN| "true"| Managed on native VLAN |
||| Device managed as| "switch" | Mode |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Password|""| Password|
||| Port|""| Port locating the Switch to be controlled|
||| Power State| "on"| Power state of Switch Controller|
||| SDLC|""| SDLC that Device Controller belongs to|
||| Connection Service | "service.79"| Connect a Service|
||| Passphrase|""| Passphrase |
||| Authentication Protocol| "MD5" | Protocol|
||| Private Password|""| Password|
||| Private Protocol| "DES" | Protocol|
||| Security Type| "noAuthNoPriv" | Security level|
||| SNMPv3 Username |""| Username|
||| SSH Key or Password|""| SSH Key or Password |
||| Switch Gateway|""| Gateway of Managed Device |
||| IP and Mask|""| IP and Mask|
||| Target Model | "generic_advanced_snmp" | Target Model|
||| SFP MAC Address or SN |""| SFP MAC Address or SN|
||| Uplink Port|""| Uplink Port of Managed Device|
||| Username|""| Username|
||||||
| SFP Breakouts| Global - SFP Breakouts | isPredefined | "false"| Denotes this is a predefined provisioning object|
||| Enable | "false"| Enable|
||| Breakout| "1x100G" | Breakout definition; defines number of ports of what speed this port is brokenout to. |
||| Vendor |""| Vendor|
||| Part Number|""| Part Number|
||| Enable | "false"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||||||
| Switch Provisioning| Network View - on each switch| CLI Commands |""| CLI Commands|
|| Tenants - \<Tenant\> - Tenant Slice| Enable | "false"| Enable flag of this provisioning object|
||| Device Settings | "eth_device_profile.76" | Device Settings for this device |
||| Eth Port \# Eth Port Profile|""| Eth Port Profile for this Eth Port |
||| Eth Port \# Eth-Port Settings|""| Choose an Eth Port Settings|
||| Eth Port \# Gateway Profile |""| Gateway Profile for this Eth Port|
||| Device Voice Settings |""| Device Voice Settings for this device |
||||||
| Community List| Global Section - Route Map Definitions| Notes|""| User notes describing this provisioning object |
||| Any/All| "any" | BGP does not advertise any or all routes that do not match the Community String |
||| Enable | "false"| Enable flag of this provisioning object|
||| Standard/Expanded| "standard"| Used Community String or Expanded Expression|
||| Community String/Expanded Expression |""| Community String in standard mode and Expanded Expression in Expanded mode|
||| Enable | "false"| Enable of this Community List|
||| Mode| "community" | Mode |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Permit/Deny| "permit" | Action to take on a match of the Community Strings, either Permit or Deny |
||||||
| DHCP Server| VNFs - System Applications - DHCP Server | Row \# Service|""| Connect a Service|
| DHCP Server|| Enable | "false"| Enable flag of this provisioning object|
| DHCP Server|| Excluded Addresses - High|""| Count of excluded addresses that DHCP server will not hand out below the maximum subnet address|
| DHCP Server|| Excluded Addresses - Low |""| Count of excluded addresses that DHCP server will not hand out starting at the base subnet address|
| DHCP Server|| Lease Duration (minutes) |""| Lease duration in minutes |
| DHCP Server|| Name|""| Name of this provisioning object. Must be unique in its type|
| DHCP Server|| Add acs|""| ACS is a required system component that communicates with ONTs. You choose the SDLC to place it on|
||||||
| Switch Provisioning| Network View - on each switch| Eth \# Label |""| Label of this Eth Port |
||| BGP AS-Number| "(auto)" | BGP Autonomous System Number for the site underlay|
||| Device Serial Number|""| Device Serial Number|
||| Disabled Ports|""| Disabled Ports|
||| Enable | "true"| Enable flag of this provisioning object|
||| Breakout|""| Breakout|
||| Switch Router-ID(IP/Mask)| "(auto)" | Switch BGP Router Identifier |
||| Switch VTEP-ID(IP/Mask)| "(auto)" | Switch VETP Identifier |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Out of Band Management| "false"| For Switch Endpoints. Denotes a Switch is managed out of band via the management port |
||| Pod |""| Pod â€“ subgrouping of spine and leaf switches |
||| Rack|""| Physical Rack location of the Switch|
||| Read Only Mode| "false"| When Read Only Mode is checked, vNetC will perform all functions except writing database updates to the target hardware|
||| Type| "leaf"| Type of Switchpoint |
||||||
| Device Template | Provisioning - Device Settings| Enable | "false"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| External Battery Power Available| "40"| External Battery Power Available|
||| External Power Available | "75"| External Power Available|
||| Mode| "IEEE 802.3af" | Mode |
||| Usage Threshold | "0.99"| Usage Threshold|
||| Security Audit Interval| "60"| Frequency in minutes of rereading this Switch running configuration and comparing it to expected values.\<br\>if the value is blank, audit will use default switch settings.\<br\>if the value is 0, audit will be turned off. |
||| Commit to Flash Interval | "60"| Frequency in minutes to write the Switch configuration to flash.\<br\>if the value is blank, commit will use default switch settings.\<br\>if the value is 0, commit will be turned off.|
||||||
| Physical Layer Port Template| Provisioning - Eth-Port Settings| CLI Commands |""| CLI Commands|
||| Duplex Mode| "Auto"| Duplex Mode|
||| BPDU Filter| "false"| Drop all Rx and Tx BPDUs|
||| BPDU Guard| "false"| Block port on BPDU Receive|
||| Fast Learning Mode | "true"| Enable Immediate Transition to Forwarding|
||| Guard Loop| "false"| Enable Cisco Guard Loop|
||| Detect Bridging Loops | "false"| Enable Detection of Bridging Loops |
||| STP Enable| "false"| Enable Spanning Tree on the port. Note: the Spanning Tree Type (VLAN, Port, MST) is controlled in the Site Settings |
||| Enable | "false"| Enable flag of this provisioning object|
||| FEC | "unaltered" | FEC is Forward Error Correction which is error correction on the fiber link.None: Disables FEC on an interface. FC: Enables FEC on supported interfaces. FC stands for fire code. RS: Enables FEC on supported interfaces. RS stands for Reed-Solomon code.|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Allocated Power | "0.0" | Power the PoE system will attempt to allocate on this port |
||| Enable | "false"| PoE enable |
||| Priority| "High"| Priority given when assigning power in a limited power situation |
||||||
| Ethernet Port Profile Template | Provisioning - Eth-Port Profiles| Port Monitoring |""| Defines importance of Link Down on this port|
||| Enable | "false"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Row \# Enable| "false"| Enable flag for this row|
||| Row \# Service|""| Choose a Service to connect|
||| Row \# External VLAN|""| Choose an external vlan|
||| Trusted Port | "false"| Trusted Ports do not participate in IP Source Guard, Dynamic ARP Inspection, nor DHCP Snooping, meaning all packets are forwarded without any checks.|
||||||
| Extended Community List| Global Section - Route Map Definitions| Notes|""| User notes describing this provisioning object |
||| Any/All| "any" | BGP does not advertise any or all routes that do not match the Community String |
||| Enable | "false"| Enable flag of this provisioning object|
||| Standard/Expanded| "standard"| Used Community String or Expanded Expression|
||| Enable | "false"| Enable of this Extended Community List|
||| Mode| "route"| Mode |
||| Route Target/Expanded Expression|""| Match against a BGP extended community of type Route Target|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Permit/Deny| "permit" | Action to take on a match of the Community Strings, either Permit or Deny |
||||||
| Gateway Port Profile| Provisioning - Gateway Profiles | Group|""| Group|
||| Enable | "false"| Enable flag of this provisioning object|
||| Enable | "false"| Enable flag for this row|
||| Source IP/Mask|""| Source address on the port if untagged or on the VLAN if tagged used for the outgoing BGP session |
||| Gateway|""| BGP Gateway referenced for this port profile|
||||||
| External Gateway Profile | Tenants - Gateways| Name|""| Name of this provisioning object. Must be unique in its type|
|| Network view - Site Gateway| Group|""| Group|
||| Advertisement Interval| "30"| The minimum time in seconds between sending route updates to BGP neighbor |
||| Anycast IP/Mask |""| The Anycast Address will be used to enable an IP routing redundancy mechanism designed to allow for transparent failover across a leaf pair at the first-hop IP router.|
||| Connect Timer| "120" | Time in seconds between sucessive attempts to Establish BGP session |
||| Default Originate| "false"| When set, switch sends a default route to BGP neighbor|
||| Ebgp-Multihop| "255" | Allows external BGP neighbors to establish peering session multiple network hops away.|
||| Enable | "false"| Enable flag of this provisioning object|
||| Export Route Map|""| A route-map applied to routes exported into the current tenant from the targeted BGP router with the purpose of filtering or modifying the routes |
||| Fabric Interconnect| "false"||
||| Gateway Mode | "BGP" | Gateway Mode. Can be BGP, Static, or Default|
||| Helper Hop IP Address |""| Helper Hop IP Address|
||| Hold Timer| "180" | Time, in seconds, used to determine failure of session Keepalive messages received from remote BGP peer |
||| Import Route Map|""| A route-map applied to routes imported into the current tenant from the targeted BGP router with the purpose of filtering or modifying the routes |
||| Keepalive Timer | "60"| Interval in seconds between Keepalive messages sent to remote BGP peer |
||| Local AS Number |""| Local AS Number|
||| MD5 password |""| MD5 password|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Neighbor AS-Number |""| Autonomous System Number of remote BGP peer |
||| Neighbor IP address|""| IP address of remote BGP peer|
||| Enable | "false"| Enable of this static route|
||| IPv4 Route Prefix|""| IPv4 unicast IP address followed by a subnet mask length|
||| Next Hop IP Address|""| Next Hop IP Address. Must be a unicast IP address |
||| Tenant |""| Tenant|
||| Source IP address|""| Source IP address used to override the default source address calculation for BGP TCP session|
||| Egress VLAN|""| VLAN used to carry BGP TCP session |
||||||
| LAG | Network View - External LAGs | Color| "anakiwa"| Choose the color to display the connectors on the network view|
|| Network View - on each switch| Enable | "false"| Enable flag of this provisioning object|
||| Eth Port Profile|""| Choose an Eth Port Profile|
||| Is Fabric | "false"| Indicates this LAG is used for peer-to-peer Peer-LAG/IDS link |
||| Is Peer Link | "false"| Indicates this LAG is used for peer-to-peer Peer-LAG/IDS link |
||| LACP| "true"| LACP |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||||||
| Prefix List| Global Section - Route Map Definitions| Notes|""| User notes describing this provisioning object |
||| Enable | "false"| Enable flag of this provisioning object|
||| Enable | "false"| Enable of this IP Prefix List|
||| Greater than Equal Value |""| Match IP routes with a subnet mask greater than or equal to the value indicated |
||| IPv4 Prefix|""| IP address and subnet to match against|
||| Less than Equal Value |""| Match IP routes with a subnet mask less than or equal to the value indicated |
||| Permit/Deny| "permit" | Action to take on a match of the Community Strings, either Permit or Deny |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||||||
| Reserved Ranges | Admin Tab - Provisioning Reserved Ranges | Base Anycast MAC Address | "00:00:00:00:01:01"| Starting MAC address to use with static Anycast gateway IP addresses|
||| Base BGP AS Number | "61000"| Base BGP Autonomous System Number used for switches in the fabric|
||| Base L3 VLAN ID | "2000"| Starting L3 VLAN ID |
||| Enable | "false"| Enable flag of this provisioning object|
||| Max Sites | "500" | Maximum number of Sites|
||| Max Switches | "2000"| Max number Switches to support in this site |
||| Max Tenants| "500" | Maximum number of VxLAN/EVPN Tenants in the site|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Paired IP Subnet| "192.168.254.0/24"| IP address range reserved for communication between paired switches |
||| Paired Leaf VLAN| "1999"| VLAN used to establish connection between paired leaf switches|
||| Paired Link VLAN| "4089"| VLAN used to establish connection between paired switches|
||| Router ID Base Prefix | "172.16.0.0"| Router ID starting IP address|
||| Vtep ID Base Prefix| "172.16.10.0"| Vtep ID starting IP address|
||||||
| Route Maps| Global Section - Route Map Definitions| Notes|""| User notes describing this provisioning object |
||| Match fields shown |""| Match fields shown|
||| Enable | "false"| Enable flag of this provisioning object|
||| Match AS Path Access List|""| Match AS Path Access List |
||| Match Community List|""| Match Community List|
||| Match EVPN Route Type |""| Match based on the indicated EVPN Route Type|
||| Match EVPN Route Type Default|""| Match based on the type of EVPN Route Type being Default'|
||| Match Extended Community List|""| Match Extended Community List|
||| Match Interface Number|""| Match Interface Number |
||| Match Interface VLAN|""| Match Interface VLAN|
||| Match IPv4 Address IP Prefix List |""| Match IPv4 Address IP Prefix List|
||| Match IPv4 Next Hop IP Prefix List|""| Match IPv4 Next Hop IP Prefix List |
||| Match Local Preference|""| Match BGP Local Preference value on the route|
||| Match Metric |""| Match Metric of the IP route entry |
||| Match Origin |""| Match routes based on the value of the BGP Origin attribute|
||| Match Peer Interface|""| Match BGP Peer port the route was learned from |
||| Match Peer IP Address |""| Match BGP Peer IP Address the route was learned from |
||| Match Peer VLAN |""| Match BGP Peer VLAN over which the route was learned |
||| Match Source Protocol |""| Match Routing Protocol the route originated from|
||| Match Tag |""| Match routes that have this value for a Tag attribute|
||| Match VNI |""| Match based on the VNI value |
||| Match VRF |""| Match VRF the route is associated with|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Permit/Deny| "permit" | Action to take on a match of the Community Strings, either Permit or Deny |
||| Notes|""| User notes describing this provisioning object |
||| Enable | "false"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Enable | "false"| Enable|
||| Route Map Clause|""| Route Map Clause is a collection match and set rules |
||||||
| Service| Tenants-Services | Anycast IP/Mask |""| Static anycast gateway address for this service|
||| DHCP Server IP|""| IP address(s) of the DHCP server for this service. May have up to four separated by commas. |
||| Enable | "false"| Enable flag of this provisioning object|
||| MTU | "1500"| MTU (Maximum Transmission Unit) The size used by a switch to determine when large packets must be broken up into smaller packets for delivery. If mismatched within a single vlan network, can cause dropped packets.|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Tenant |""| Tenant|
||| VLAN|""| A Value between 1 and 4096|
||| VNI | "(auto)" | Indication of the outgoing VLAN layer 2 service|
||||||
| Static Fabric Connections| Network View - on each switch| isPredefined | "false"| Denotes this is a predefined provisioning object|
||| Endpoint1 for a Static Connection |""| 1st Switchpoint for a Static Connection|
||| Endpoint2 for a Static Connection |""| 2nd Switchpoint for a Static Connection|
||| Endpoint1 for a Static Connection |""| 1st Switchpoint for a Static Connection|
||| Port2 for a Static Connection|""| 2nd Port for a Static Connection|
||| Enable | "true"| Enable flag of this provisioning object|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||||||
| Tenant | Tenant| DHCP Relay: Source IPs Subnet|""| Range of IP addresses (represented in IP subnet format) used to configure the source IP of each DHCP Relay on each switch that this Tenant is provisioned on. |
||| Enable | "true"| Enable flag of this provisioning object|
||| Export Route Map|""| A route-map applied to routes exported into the current tenant from other tenants with the purpose of filtering or modifying the routes|
||| Import Route Map|""| A route-map applied to routes imported into the current tenant from other tenants with the purpose of filtering or modifying the routes|
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Route Distinguisher|""| Route Distinguishers are used to maintain uniqueness among identical routes from different routers. If set, then routes from this Tenant will be identified with this Route Distinguisher (BGP Community). It should be two numbers separated by a colon.|
||| Route Target Export|""| A route-target (BGP Community) to attach while exporting routes from the current tenant. It should be a comma-separated list of BGP Communities: each Community being two numbers separated by a colon. |
||| Route Target Import|""| A route-target (BGP Community) to attach while importing routes into the current tenant. It should be a comma-separated list of BGP Communities: each Community being two numbers separated by a colon. |
||| Enable | "false"| Enable|
||| Tenant |""| Tenant|
||| Layer-3 VLAN | "(auto)" | VLAN value used to transport traffic between services of a Tenant|
||| Layer-3 VNI| "(auto)" | VNI value used to transport traffic between services of a Tenant |
||| VRF Name| "(auto)" | Virtual Routing and Forwarding instance name associated to tenants|
||||||
| User Accounts| Admin Tab - Users and Permissions| isPredefined | "false"| Denotes this is a predefined provisioning object|
||| Base Provisioning| "true"| Capability to edit objects in the provisioning section and non-fabric lags|
||| Device Endpoint | "true"| Capability to edit unlocked ONT endpoints|
||| Device Management| "true"| Capability to manage Devices |
||| Enable | "false"| Enable flag of this provisioning object|
||| Globals| "true"| Capability to edit Badges and Radius Servers|
||| Idle Time Logout (min)| 240"| Idle Time Logout in minutes|
||| Import | "true"| Capability to import|
||| Locked Switch Endpoint| "true"| Capability to edit locked switch endpoints|
||| Mod |""| Role Modifier |
||| Name|""| Name of this provisioning object. Must be unique in its type|
||| Network| "true"| Capability to edit Sites, Domains, Switch ordering, LANs, Switch Pairing, and System/Site wide management buttons|
||| User Permitted Sites|""| User Permitted Sites|
||| Role| "rw"| Role |
||| SD-Admin Access | "true"| Capability to access SD-Admin|
||| Services| "true"| Capability to edit services|
||| Sets| "true"| Capability to edit endpoint sets|
||| Site Permissions| "false"| Capability to edit Sites|
||| Switch Endpoint | "true"| Capability to edit unlocked switch endpoints|
||| Views| "true"| Capability to edit endpoint views |