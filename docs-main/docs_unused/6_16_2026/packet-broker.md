---
hide:
- toc
---

# Packet Broker
A **Packet Broker** is a network device placed between network traffic sources and monitoring tools (or other destinations). It forwards network traffic according to filtering and transformation rules to designated destinations. In Verity, the Packet Broker aggregates network traffic for delivery to multiple destinations. It operates on a dedicated network infrastructure that is physically separated from both the production and management networks. This infrastructure includes packet broker switches, optimized for packet processing rather than general-purpose switching.

## Components
| Term | Description |
| - | - |
| **Packet Broker Switch (PBS)** | A SONiC-based network switch dedicated to aggregating traffic for delivery to multiple analyzers. These switches don't perform typical functions like VLAN switching.| 
| **Packet Broker Network (PBN)** |  A network of interconnected PBS switches, used to forward packets based on Access Control Lists (ACLs).| 
| **Packet Broker Ingress Switch (PBIS)** | The PBS that connects to the network and receives incoming traffic.| 
| **Packet Broker Egress Profile (PBP)** | A user-created profile that specifies forwarding rules for traffic, including IP filters for traffic management.| 
| **Tap** | A hardware device used to passively monitor and copy network traffic without interrupting it.| 

## Functionality
The **Verity Integrated Packet Broker** uses **Packet Broker Switches (PBS)**, which aggregate network traffic for delivery to various **Analyzers**. These PBS switches form a **Packet Broker Network (PBN)**. The PBS switches in this network don’t perform traditional switching functions, such as VLAN switching. Users create **Packet Broker Egress Profiles (PBP)** to define which traffic should be forwarded, applying these profiles to any port in the PBN.

Verity automatically detects the PBS connections and configures the interconnected ports, designating all other ports as input ports. Once **PBPs** are assigned, Verity sets up the packet forwarding rules from ingress to egress.

Verity manages Packet Broker Switches utilizing out-of-band ports. The **PBN** is displayed in the **Topology** section of the Verity interface, where PBS switches are shown in left-to-right order, representing the traffic flow. The **PB Ingress Switch (PBIS)** is where traffic begins. The PBN can have multiple PBISs depending on the traffic inputs and load, though PBISs cannot connect to each other.

Each port in the PBN can have a **PBP** assigned, but traffic can only flow from ingress to egress, as shown in the GUI from left to right. When PBS switches are connected, **Link Aggregation Groups (LAGs)** are created automatically for the connected ports. It is the user's responsibility to ensure that the fabric (the ports connecting PBS switches) has the capacity to handle the required traffic.

## Architecture
This high-level example diagram shows how traffic flows through the PBN. While there's flexibility of where to place inputs, connections and egress ports, it is recommended to connect input ports to designated PBISs and place egress ports on the lowest tier switches (shown on the right of the diagram and Verity GUI). The network should follow a non-blocking architecture so all input traffic can reach egress switches without congestion.

![](media/pbn_diagram.png)


### Packet Broker Calculator
This spreadsheet provides estimates for how many switches are needed based on traffic capturing capacity requirements.

[Packet Broker Calculator available here.](downloads.md)


## Profiles and Filters

The **PBPs** include IP filters that specify which traffic is allowed or denied based on criteria such as protocol, IP address subnet, and port. These filters can be tailored to allow or block specific IP addresses, protocols, and ports, including finer control with **IPv4** or **IPv6** addresses.

## UI Overview
In the Verity interface, these sections are used for managing the Packet Broker:

- **Fabric** &rarr; **Packet Broker**
- **Templates**  &rarr; **Filters** &rarr; **IPV4 Filters** / **IPV6 Filters**
- **Templates** &rarr; **Diagnostics** &rarr; **PB Egress Profiles**

### Fabric View
- **Fabric** &rarr; **Packet Broker**

**Packet Broker** switches are organized as Egress or Ingress.Packet Broker switches are organized as **Egress** or **Ingress**. To add one, select the switch type and click **Add Packet Broker Switch** in the upper right of the window.


![](media/packet_broker_icon_.png)

<!-- Devices are arranged left to right, representing the direction of *data flow* ![](media/packet_broker_data_flow.png){: class="pop"}. -->

### Packet Broker Templates

The Template navigation menu contains these options used to configure Packet Broker.

- **Templates**  &rarr; **Filters** &rarr; **IPV4 Filters** / **IPV6 Filters** / **IPv4 List Filters** / **IPv6 List Filters** 
- **Templates** &rarr; **Diagnostics** &rarr; **PB Egress Profiles**

These tools let users create filter rules and group them into collections called **PB Egress Profiles**, which are then assigned to specific ports in the PBN.

![](media/template_tools_for_packet_broker_6_5.png)

## TAPs
A **TAP** (Test Access Point) is a hardware device inserted into the network cabling to passively copy network traffic. The TAP icon in the user interface represents the point where network traffic is accessed and copied for the Packet Broker network.
<!-- ![](media/tap_flow.png) -->

![](media/tap_example_for_6_5.png)

## Creating & Applying Filters

Filtering determines whether selected network data is forwarded to a destination device or blocked.

1. **Determine the Traffic to be Screened**: Identify IP type (IPv4 or IPv6), protocol by name (ip/tcp/udp/icmp only) or IANI number, bidirectional or unidirectional, source and/or destination IP or IP range, source and/or destination ethernet port(s) or range of ethernet ports with appropriate port operators (if applicable). Determine if filter is to Deny and/or Permit traffic types.
1. **Create Filters**: Go to **Templates &rarr; Filters** and create filters based on the type of traffic identified in step 1.![](media/template_filters_for_packet_broker_6_5.png){: class="pop"}
1. **Assign Filters to PB Egress Profiles**: Once filters are created, group them into **PB Egress Profiles**.
1. **Apply the PB Egress Profile to Ports**: Assign the created PB Egress Profiles to device ports.

### Apply Filter Rules to a Range of IP Addresses
1. Select either IPv4 Filters or IPv6 Filters, depending on the address type. ![](media/pb_filter_selection_6_5.png){: class="pop"}
1. Click the **Add** button, name the filter and click the **Create Filter** button ![](media/add_filter_with_name_6_5.png){: class="pop"}
1. In the filter settings, edit the rules and apply the changes. ![](media/ipv4_filter_form.png){: class="pop"}

**Filter Rules**

|Filter|Function|
|-|-|
|**Protocol**|IP protocol by name (ip, tcp, udp, or icmp, only) or IP Protocol by IANI number (0-255).|
|**Bidirectional**|Bidirectional packets if selected, else unidirectional.|
|**Source IP**|IPv4 or IPv6 packet source address.  Use IP mask for range of IPs.|
|**Source Port Operator**|This field determines which match operation will be applied to TCP/UDP port(s). The choices are equal, greater-than, less-than or range.|
|**Source Port 1**|This field is used for equal, greater-than or less-than TCP/UDP port value in match operation. This field is also used for the lower value in the range port match operation.|
|**Source Port 2**|This field will only be used in the range TCP/UDP port value operation to define the top value in the range
|**Destination IP**|IPv4 or IPv6 packet source address. Use IP mask for range of IPs.|
|**Destination Port Operator**|This field determines which match operation will be applied to TCP/UDP ports. The choices are equal, greater-than, less-than or range.|
|**Destination Port 1**|This field is used for equal, greater-than or less-than TCP/UDP port value in match operation. This field is also used for the lower value in the range port match operation.|
|**Destination Port 2**|his field will only be used in the range TCP/UDP port value match operation to define the top value in the range.|

### Filtering Individual Addresses as Lists
To filter individual IP addresses or lists of individual IP addresses, use an **IPv4 List Filter** or **IPv6 List Filter** and enter the addresses in the provided field. A comma must be used between each IP address.  There are no spaces used in the lists. ![](media/ipv4_filter_list_6_5.png){: class="pop"}

1. Navigate to **Packet Broker Templates**.
1. Create an **PB Egress Profile** and enable it. ![](media/packet_broker_egress_profile_enabled_6_5.png){: class="pop"}
1. Edit the **PB Egress Profile** by assigning filters to any of the the four available options:
    - IPv4 Deny 
    - IPv6 Deny 
    - IPv4 Permit 
    - IPv6 Permit
1. Check the Enabled box to activate the filter(s). ![](media/enabled_pb_egress_filter_6_5.png){: class="pop"}
1. Use the plus button at the bottom-right of the list to create additional rows for assigning multiple filters. ![](media/egress_profile_add_row_6_5.png){: class="pop"}
1. When in Edit Mode save changes by clicking the Save button ![](media/edit_mode_save_6_5.png){: class="pop"} .
### Applying PB Egress Profile to Device Port

1. Once the filters are configured and saved, apply the PB Egress Profile to a device port.
1. Double-click on the device port in the Packet Broker Topology view.
1. Select the appropriate PB Egress Profile from the dropdown menu. ![](media/egress_profile_on_port.png){: class="pop"}

## Packet Queuing

This feature lets you set the priority for packets depending on bandwidth and is
available at **Templates** &rarr; **Layer-2** &rarr; **Packet Queues** ![](media/packet_ques_menu_item_6_5.png){: class="pop"}.

The window that appears lets you make your changes. Here you set the priority for p-bits and set the bandwidth (**BW**) for each queue as a percentage. The percentage is the maximum average percentage of the port output bandwidth that packets in that queue will be allowed to consume. The value cannot exceed 100 and a value of 0 means no limit is set.

![](media/packet_queue_6_5.png)