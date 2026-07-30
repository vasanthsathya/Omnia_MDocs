# Port Level IP ACL Management

An **ACL (Access Control List)** is a collection of IP address filters. Verity lets administrators configure ACLs at the Service and Port level. Applying an ACL to a Service and/or Port is composed of these steps:

- Create and enable a Port ACL.
- Create and configure IPv4 and/or IPv6 filters.
- Apply filters to the Port ACL.
- From within a chosen Eth-Port profile, assign the ACL to a Port and/or Service(s).

## Create Port ACLs
Navigate to **Templates** and select Port ACLs. To create a new Port ACL, click the + button, give the Port ACL a name, and click the checkmark (save button) to save. The window that appears is composed of four quadrants titled IPv4 Deny, IPv4 Permit, IPv6 Deny, and IPv6 Permit. These quadrants contain filters that determine whether selected network data is forwarded to a destination device or blocked.

![](media/port-acls.png)

## Create and Configure Filters

Before applying filters to an ACL you must first create and configure the filters. To do so, go to **Templates** and select **IPv4 Filters** or **IPv6 Filters**. This is where you create and configure filters.

![](media/ipv4_ipv6_filters_menu_6_5.png)


1.  Select either IPv4 Filters or IPv6 Filters, depending on the address type
2.  Click the **Create New Filter** button
3.  Name the filter and click Save
4.  In the filter settings, edit the rules and apply the changes.


![](media/Ipv6_filter_example.png)

**Filter Rules**

-   **Protocol**: IP protocol by name (ip, tcp, udp, or icmp, only) or IP Protocol by IANA number (0-255).
-   **Bidirectional**: Bidirectional packets if selected, else unidirectional.
-   **Source IP**: IPv4 or IPv6 packet source address. Use IP mask for range of IPs.
-   **Source Port Operator**: This field determines which match operation will be applied to TCP/UDP port(s). The choices are equal, greater-than, less-than or range.
-   **Source Port 1**: This field is used for equal, greater-than or less-than TCP/UDP port value in match operation. This field is also used for the lower value in the range port match operation.
-   **Source Port 2**: This field will only be used in the range TCP/UDP port value operation to define the top value in the range
-   **Destination IP**: IPv4 or IPv6 packet source address. Use IP mask for range of IPs.
-   **Destination Port Operator**: This field determines which match operation will be applied to TCP/UDP ports. The choices are equal, greater-than, less-than or range.
-   **Destination Port 1**: This field is used for equal, greater-than or less-than TCP/UDP port value in match operation. This field is also used for the lower value in the range port match operation.
-   **Destination Port 2**: This field will only be used in the range TCP/UDP port value match operation to define the top value in the range.

## Apply filters to the Port ACL

In the Port ACL you apply the filters by setting them under the field named **Filter**. You activate the Filter by checking the **Enable** box.

![](media/apply_acl_filter_example.png)

## How to Assign a Port ACL to a Port or Service

After assigning filters to Port ACL(s), apply the Port ACL to the Service and/or Port within a selected Eth-Port Profile. To do this, navigate to **Templates \> Eth-Port Profiles**.

**Assigning ACL to a Port**

Assigning ACL to the Port is performed in the topmost Ingress ACL and Egress ACL settings.

![](media/ingress_acl_highlight.png)

**Assigning ACL to a Service**

Each service in the Eth-Port Profile has Ingress and Egress ACL fields. These fields are where you set the ACL Port.

![](media/port_acl_services.png)

**Common processing order**

1.  **Port ACL** is applied first (affects all VLANs on the port)
2.  **Service ACL** is applied second (affects only the specific VLAN)
3.  Traffic must satisfy both ACLs to be permitted
