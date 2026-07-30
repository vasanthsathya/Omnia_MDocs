---
hide:
- toc
---
# Terminology

## Verity Managed Objects
| Term | Description |
| ------- | --------------------------------------------- |
| **vNETC** | Verity Virtual Network Orchestration platform.|
| **SDLC** | Verity application that hosts containers associated to switches and other system functions.|
| **Device Controller** | A container within the SDLC application used to manage a switch.|

## General Networking Terms
| Term | Description |
| - | - |
| **Spine-Leaf** | A data center network topology that consists of two switching layers— a spine and leaf. The   leaf layer consists of access switches that aggregate traffic from servers and connect directly into the spine or network core. Spine switches interconnect all leaf switches in a full-mesh topology.|
| **Pod** | A set of connected spines and leafs.|
| **Superspine** | A third switch layer that is used to connect Pods to each other.|
| **Underlay** | The layer 3 VxLAN based connections between the spines and leafs in the data center.|
| **Tenant** | A logical separation of services within the datacenter architecture. The tenants’ connections constitute the **overlay** of the datacenter architecture.|
| **Management Switch** | A switching device used to provide connectivity between the Verity applications and the out of band management connections of the spines and leafs.|

## Verity Functionality Terms
| Term | Description |
| - | - |
| **Service** | A layer 2 Ethernet model of VLAN identification, QoS, multicast and other layer 2 related options. |
| **Endpoints** | (Managed Endpoints, Service Endpoints) – The “edge” of the network where services connect to client devices. Examples of service endpoints are a room number, street address, office desk location or pole location. Service Endpoints specifically are not a physical network device, but have an “Edge Device”, such as an ONT or Ethernet switch, associated with them. |
| **Edge Device** | a physical unit, such as an ONT or an Ethernet switch, that is fully managed by the Verity system. The ports of the Edge Device deliver the services to the client equipment. |
| **Top of Rack Switch (TOR)** | The layer 2 device that is at the top of the access network topology. It connects to services and routers above, and to the Aggregation Switches and Edge Devices below. In redundant systems there are two TORs, referred to as TOR A and TOR B.
| **Aggregation Switch (Agg)** | The layer 2 devices that connect the TOR to the Edge Devices. There can be multiple layers of Agg switches. Ports on Agg switches may be used as Service Endpoints as well. |
| **Switch Endpoint** | the database object associated with switch fabric devices (TOR and Agg). |
| **Service Port** | entry point of a layer 2 service into the access network normally through the TOR switch. |
| **Service Drop** | Ethernet port at the edge of the access network that connects to client devices. |
| **Direct Endpoint** | a Service drop directly egressing the network from the fabric switch complex (TOR or AGG) without using an Edge Device. Usually for craft PCs, back-office connections, trunks to unmanaged devices outside the scope of Verity. |
| **White Box Switch** | commercial, off the shelf switch fabric hardware installed with Verity Network Operating System (NOS). The NOS uses standard ONIE installer methods. |
| B**lack Box Switch** | any “non-open” switching gear managed by the Verity system. In other words, a TOR, Agg or Edge Device that cannot use Verity NOS. They are usually managed internally by the Verity system using SNMP, CLI or NETCONF. |
| **ONT** | Optical Network Terminal (aka Optical Edge Device) – an Edge Device providing connectivity at the Endpoint that has an optical WAN interface and multiple service drops. |
| **SDLC** | The controller virtual application that hosts containers associated to BlackBox switches. |
| **Device Controller** | A container within the SDLC application used to manage a “black box” switch as a TOR, Agg or Edge Device. |


-   Templating Terms – (the flow of these items is shown on the configuration map)
    -   MAC Filters – set of parameters related to MAC Addresses and Hexadecimal MASKs
    -   Ethernet Port Settings – set of parameters related to the physical layer of an ethernet interface (e.g. Speed, full/half duplex, LLDP, PoE etc.)
    -   Ethernet Port Profiles – combination of Ethernet Port Settings and one or more Services and MAC Filters defining the Layer 1 and layer 2 connection for the service drop. (e.g. High-Speed Internet, Video)
    -   Authenticated Ethernet Port – list of possible Ethernet Port Profiles to be applied to the service drop based on connect client authentication (e.g. 802.1x, MAC authentication)
    -   Service Port Profile – collection of services applied to a Service Port
    -   Voice Port Settings – parameters related to VoIP protocols, interfaces, and related features.
    -   Device Settings – set of parameters associated to a physical device such as Power-over-Ethernet (PoE) and LED behavior.
    -   Device Voice Settings – parameters related to the VoIP client installed on an Edge Device.
    -   Endpoint Bundle – collection of Device Settings, Ethernet Port Profiles, Resident Applications, and Voice Port Settings to be applied to a Managed Edge Device
    -   Domain – group of sites in multi-site Verity system
    -   Site – physical site at a location. A site may contain multiple separated layer 2 switch topologies.
    -   Top of LAN – The switch at the top of a LAN instance within a site with multiple LANs.
