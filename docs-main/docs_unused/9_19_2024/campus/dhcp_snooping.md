#  DHCP Snooping


**Enable DHCP Snooping** is now available from site settings. This feature is intended to improve system security.

![](../media/enable_dhcp_snooping.png)

The Enable DHCP Snooping feature is used to stop any malicious DHCP packets from affecting your network. DHCP Snooping protects your network by listening to DHCP traffic and blocking DHCP OFFER messages on untrusted ports. Only devices designated as *trusted* can forward DHCP OFFER messages.

## Trusted Port

To set a port as Trusted, you go to Eth-Port Profiles, open your selected tile and check the box titled **Trusted Port**.

![](../media/trusted_port.png)

## Static IPs

The **Static IPs** feature is applied to switch ports and intended for devices that are assigned static IP addresses and that do *not* request IP data from a DHCP server.

Static IP settings can be set by zooming in on a selected port and double-clicking the Static IPs window.

![]../(media/static_ip.png)

Static IP settings are also available at the bottom of the **Navigation Network**.

![](../media/navigation_network_static_ip.png)

To add a new device, go to the Static IPs tile and click the **Add a new static** IP button.

![](../media/add_static_ip_window.png)

Edit the tile information and enable the IP by clicking the edit button and checking the enable checkbox.

![](../media/enabled_static_ip_window.png)

## Static IPs Reports

Static IPs are available in Reports.

![](../media/static_ip_in_reports.png)

## DHCP Assigned IPs Reports

DHCP Assigned IPs are available in Reports.

![](../media/DHCP_assigned_IP_reports.png)

## Static IPs Import/Export

Static IPs feature information can be exported and imported via the Import/Export Workbench.

![](../media/static_ip_import_export_workbench.png)
