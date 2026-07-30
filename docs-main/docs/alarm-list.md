---

title: "Alarm List"
description: "Alarm API"
tags: [Monitoring]
search:
  boost: 0.01
parent: Monitoring


---

[SNMP MIBs available here.](downloads.md)

| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0013 | ERROR | alarm | System Provisioning Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Gateway | {{element_id}} has the same {{fields}} as {{gateway_id}} while provisioned on the same switch | Correct the provisioning conflict |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0014 | WARNING | alarm | System Provisioning Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Gateway | {{element_id}} is provisioned multiple times on {{switch_id}} | Correct the provisioning conflict |
| Gateway Profile | {{element_id}}'s Virtual Port VLAN conflicts with {{conflict_id}}'s VLAN | Correct the provisioning conflict |
| Gateway Profile | {{element_id}} has more than one BGP Gateway with an empty Egress VLAN | Only one BGP session can configured on a L3 configured port |
| LAG | {{element_port}} - {{vlan}} has conflicting external VLAN | Correct the invalid Ethernet Port Profile |
| LAG | {{element_port}} - is Peer-LAG/IDS and provisioned across multiple sites | Switch pairs must exist on the same site. Either correct the site assignment or correctly identify the switches intended to be in a pair. |
| Endpoint Bundle | {{element_id}} has one or more eth port profiles with conflicting RADIUS names. | Update the Profile to remove the conflict |
| Device Controller | {{element_id}} LLDP chassis identifier does not match managed device | Update the chassis or serial number identified correct in the Device Controller |
| Device Controller | {{element_id}} sharing Management VLAN with ONTs, cannot be Managed on native VLAN | The service in the Active SFP Device Controller must be changed to use a different management VLAN than the one used by the ONTs connected on the OLT. |
| Site | {{element_id}} has multiple services using VLAN {{vlan}} with conflicting settings | It is not recommended to use the same VLAN ID on the same site. Change the VLAN IDs to be unique for the site. |
| Site | {{element_id}} missing management service | Ensure that site settings are referencing a valid management service |
| Site | {{element_id}}: {{service_id}} is Externally Routed but has no Service Ports | Services may switch only locally inside the LAN, or can connect to the uplinks of the LAN to egress the network. The option in the service indicates whether to expect this service as local only or leaving the fabric. In this case, the service is marked to egress the fabric, but the service is not provisioned on any uplink Service Port Profiles. Correct the provisioning in either case. |
| Switch | {{element_id}} connected to SD-WAN is not provisioned as TOR | Remove {{element_id}}'s connection to SD-WAN or provision as TOR |
| Site | Base Management VLAN not defined | Define in Admin - Settings tab |
| Device Controller | {{element_id}} is provisioned on {{prov_device_port}} but it's managed Device is appearing on {{real_device_port}} | Check the network fabric connections to make sure that the provisioning of the switch controller matches the desired network physical connectivity. Correction required either in provisioning or cabling. |
| Device Controller | {{element_id}} is provisioned as Static Port, but the location is incomplete | Finish provisioning the location |
| Device Controller | Discovery non-operational because no Site is defined | Contact support and provide system snapshot |
| Device Controller | LLDP Search String does not match the device currently connected to {{device_port}} | Check the network fabric connections to make sure that the provisioning of the switch controller matches the desired network physical connectivity. Correction required either in provisioning or cabling. |
| Endpoint Bundle | {{element_id}} has mismatched voice protocol with Voice Device Profile {{voice_device_profile_id}} | Fix protocol mismatch |
| Endpoint Bundle | {{element_id}} has mismatched voice protocol with Voice Port Profile {{voice_port_profile_id}} on POTS ${row} | Fix protocol mismatch |
| Endpoint Bundle | {{element_id}} - the RG feature will not be operational | Fix provisioning |
| Endpoint Bundle | {{element_id}} - IPTV cannot be processed two ways. IPTV application (IGMP Proxy) and IPTV Filtering (IGMP Snooping) both provisioned on single ONT, IGMP Proxy will take precedence | Remove the IPTV application or the IPTV Filtering |
| Endpoint Bundle | {{element_id}} - Port advertised by LLDPmed is not provisioned in the Eth-Port Settings and is not present in the Eth Port Profile | Provision the advertised port or correct the assigned Ethernet Port profile. |
| ONT | {{element_id}} - LLDP MED service {{service_id}} is being used on a translated 802.1x port | Remove the service. These features are mutually exclusive. |
| Eth-Port Profile | {{element_id}} has VLAN collision on VLAN {{vlan}} and {{acl_id}}. Rows cannot have the same MAC filter and exit VLAN | Remove one of the conflicting VLANs |
| Eth-Port Profile,ONT,Switch | {{element_id}} has a VLAN collision on VLAN {{vlan}}. | Remove one of the conflicting VLANs |
| Switch,Eth-Port Profile | {{element_id}} has multiple services with the same VLAN {{vlan}}. | Remove one of the conflicting services |
| Eth-Port Profile,Service Port Profile | {{element_id}} - TLS trunk with a non-TLS service | Remove the non-TLS service or change this to not be a TLS trunk |
| Interface | MAC Security provisioned but will not be applied to {{element_port}} | Fix MAC collision |
| LAG | {{element_id}} is a IDL/IDS LAG whose provisioned ports do not match it's physical connections. | Fix the provisioning/physical mismatch |
| LAG | {{element_id}} is IDL/IDS and provisioned across multiple Sites. | Multichassis Switch pairs cannot cross site boundaries. Limit provisioning to a single site |
| LAG | {{element_id}} is missing physical connections on provisioned fabric LAG ports | Provisioning indicates an expected connection from downstream device. Connect the new device or unprovision the port |
| LAG | {{element_id}} has mismatched interfaces, Upstream : {{up_size}}, Downstream : {{dn_size}} | Correct the Port Settings of either the upstream or downstream interfaces |
| Switch | {{element_id}} - OLAG detected but not supported | Remove the OLAG |
| Switch | {{element_id}} has more than the supported number of LAGs. Supported: {{supported_count}}, Current: {{current_count}} | Remove extra LAGs |
| Switch | {{element_id}} Mistmached provisioning on TOR uplinks | Make sure the provisioning is the same on all uplinks |
| Interface | {{element_port}} PoE allocated is greater than PoE available on {{element_id}} | Reduce allocated PoE |
| Interface | {{element_id}} - {{prov_error}} | Fix the provisioning or connections |
| Static IP | {{element_id}} - {{service_id}} not provisioned on targeted {{located_by}} | Provision the service on the correct location |
| Service | {{element_id}} is provisioned on too many leaf swithes | The service is provisioned on more leaf swithes than its Tenant's DHCP relay subnet supports. Increase the subnet size of the DHCP relay subnet so that more addresses can be allocated for the Tenant. |
| Service | {{element_id}} has invalid DHCP server provisioned. | Service has DHCP server IP without a DHCP Relay source subnet defined for the Tenant. |
| Switch Pair | {{element_pair}} no interconnect provisioned | Provision an interconnect |
| Interface | {{element_port}} has {{eth_id}} provisioned but, {{radius_id}} has no enabled rows | Add an enabled Radius entry |
| Endpoint Bundle | {{element_id}} - mixed (trusted and untrusted) port levels are not supported on ONTs. All Eth Port Profiles must be of one kind. By default, all ports will now be untrusted. | Change to use only trusted or untrusted port levels |
| Endpoint Bundle | {{element_id}}, Authenticated Eth-Port provisioned but RADIUS is disabled or missing a service | Enable RADIUS and add a service |
| Switch | ACS {{element_id}} doesn't have IP Source type set | Complete provisioning of the ACS device. |
| Switch | Gaia object was not found, skip provisioning | Ensure installation process successfully compeleted and that an SDLC with ACS and Gaia has been created. |
| Switch | Managed device {{element_id}} does not have an associated Device Controller | Correct provisioning of the Device Controller if this physical device is expected to be on the network. |
| Switch | Maximum number of Device Controllers reached for device {{element_id}} | More SDLC VMs should be added to the system to handle the excess capacity. |
| Switch | ACS object was not found | Ensure installation process successfully compeleted and that an SDLC with ACS and Gaia has been created. |
| Switch | Site {{site_id}} IDL {{idl_id}} doesn't have both the switchpoints listed | Ensure that the switch pairs are properly provisioned with a LAG created and provisioned between them. |
| ONT | System has no RADIUS server set up but has Authenticated Eth Port profiles provisioned on device {{element_id}} | Add the provisioning for the RADIUS server in the Admin section or remove the Authenticated Eth Port profile from the bundle. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0015 | NOTICE | alarm | System Provisioning Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Interface | {{element_port}} is provisioned and being used as a port mirror destination | Remove from port mirror destination or remove the provisioning |
| Interface | {{gateway_profile_id}}'s Source IP/Mask is /30 or greater | Make sure the Source IP/Mask is /29 or less to allow for 3 valid ip addresses |
| Interface | Source IPs, Neighbor IP address, and Helper Hop IP Address are not unique for {{gateway_id}} in {{gateway_profile_id}} and {{other_gateway_profile_id}} | Make sure all IP's are unique |
| Interface | {{gateway_id}}'s Helper Hop IP Address is not within the Source IP/Mask subnet defined in {{gateway_profile_id}} | Make sure the Helper Hop IP Address is within the Source IP/Mask subnet |
| Interface | {{gateway_id}}'s Neighbor IP address is not within the Source IP/Mask subnet defined in {{gateway_profile_id}} | Make sure the Neighbor IP address is within the Source IP/Mask subnet |
| Interface | {{gateway_id}} Source IP/Mask's have different subnets in Switch Pair | Make sure the Source IP/Mask on each profile have the same subnet |
| Interface | {{gateway_id}} has the same Peer GW value on boths side of Switch Pair | Change one of them so that they are different |
| Interface | {{lagg_id}} has {{gateway_id}} provisioned on only one side of Switch Pair | Either remove {{gateway_id}} or add it to the other side |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0022 | CRITICAL | alarm | Ethernet Port is Down |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Interface | {{element_port}} Critical port is link down | Determine cause and correct faulty cables or SFPs. May be transitory alarm as the connected switch reboots. Disable and re-enable the port |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0023 | ERROR | alarm | Ethernet Port is Down |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Interface | {{element_port}} Storm : Shutdown | Disconnect the device connected to the port and disable and re-enable the port. If problem persists replace the connected device or adjust the storm control settings if that traffic is expected. |
| Interface |  | Disconnect the device connected to the port and disable and re-enable the port. If problem persists replace the connected device or adjust the storm control settings if that traffic is expected. |
| Interface | {{element_port}} MAC {{violation}} | Disconnect the device connected to the port and disable and re-enable the port. If problem persists replace the connected device or adjust settings if that MAC is expected. |
| Interface | {{element_port}} Unidirectional Connection Detected | Caused by multimode fiber incorrectly connected. Ensure that the fiber connection TX and RX for the same ports are properly connected. Disable and re-enable the port |
| Interface | {{element_port}} is disabled by CRC error detection | Caused by excessive connection layer errors. Determine cause and correct faulty cables or SFPs. Also, the CRC error threshold can be adjusted to relax the port removal. Disable and re-enable the port |
| Interface | {{element_port}} Fabric port is link down | Determine cause and correct faulty cables or SFPs. May be transitory alarm as the connected switch reboots. Disable and re-enable the port |
| Interface | {{element_port}} Monitored port is link down | Determine cause and correct faulty cables or SFPs. May be transitory alarm as the connected switch reboots. Disable and re-enable the port |
| Interface | {{element_port}} Loop Detected | Determine cause and correct looped cables. May be directly connected cables or may be caused by unmanaged devices connected off of the Ethernet port. Once the loop is removed, disable and re-enable the port |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0063 | ERROR | alarm | Device Provisioning Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | {{element_id}} - Device controller failure - {{status_error}} | Can be the result of communication errors to the device, or a provisioning failure between Verity and the device or and error from the device's operating system. Show the error output dialogue at the top of the switch in the GUI to determine if its a direct error from the OS. If not, try to revert the last config changes of the system to determine if that is the cause. Enable or disable provisioning objects related to last change. If issue persists, capture a system snapshot in the support menu, and a snapshot for the affected switch. |
| Switch | {{element_id}}: Device Controller is out of communication, unable to provision | May be a transitory error. If it persists, make sure the connections/routes are intact between the SDLC VM and the Vnetc and that the firewall settings on the vnetc are correct in the Admin Settings page. |
| ONT,Switch | {{element_id}} has failed to provision - {{error}} | Can be the result of communication errors to the device, or a provisioning failure between Verity and the device or and error from the device's operating system. Show the error output dialogue at the top of the switch in the GUI to determine if its a direct error from the OS. If not, try to revert the last config changes of the system to determine if that is the cause. Enable or disable provisioning objects related to last change. If issue persists, capture a system snapshot in the support menu, and a snapshot for the affected switch and send to technical support. |
| ONT | {{element_port}} - {{fault8021x}} | Fix the 802.1x error |
| Interface | {{element_port}} - {{config_error}} | Fix the configuration |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0073 | ERROR | alarm | Fabric Device(s) Communications Down |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | {{element_id}}: Device Controller is powered off | Power on the device controller when ready to resume normal operations |
| Switch,ONT | {{element_id}} is out of communication | Can be caused by a device failure,  physical link failures between the device and the Verity platform or a system process going through recovery. When dependent conditions are cleared, the communications will automatically recover. If all other recovery methods have failed, reboot the device. |
| Switch | ACS event polling failed | This is normally caused by a transient condition due to SDLC or ACS restart. Wait for the SDLC/ACS to return to service. |
| Switch | Unknown Device Controller connectivity for device {{element_id}}: {{controller_connectivity}} | Internal System Processing Error. Create system snapshot and contact support. |
| Switch | Cannot configure Device Controller without controller_connectivity on {{element_id}}! | Internal System Processing Error. Create system snapshot and contact support. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0092 | CRITICAL | alarm | ACS Down |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| ACS | ACS connection lost | Check that the SDLC and ACS are running.  Contact support if the condition persists |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0162 | CRITICAL | alarm | Loss of LAG Redundancy |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| LAG | {{element_id}}: {{status}} | Make sure all ports are fully operational |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0163 | ERROR | alarm | Loss of LAG Redundancy |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Olag Channel | {{element_olag_chan}}: {{status}} | Make sure all Ethernet ports are fully operational. Review traffic graphs for any packet layer errors. Run ping test between Router ID IP Addresses. Disable/Re-Enable ports. Reboot each switch individually |
| LAG | {{element_id}}: {{status}} | Make sure all ports are fully operational |
| LAG | {{element_fabric_lagg_type}}: {{status}} | Make sure all ports are fully operational |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0164 | WARNING | alarm | Loss of LAG Redundancy |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| LAG | {{element_id}} is experiencing loss of redundancy | Make sure all ports are fully operational |
| LAG | {{element_id}} is IDL/IDS and is out-of-service | Make sure all ports are fully operational |
| Switch Pair | {{element_pair}}: {{state}} | Make sure each Switch is fully operational |
| Switch | {{element_id}}: {{state}} | Make sure parents are fully operational |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0173 | ERROR | alarm | LAG Setting Mismatch |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| LAG | {{element_id}} - Mismatched SFP speeds in a single LAG. Failure to correct will impact LAG operation | Make sure all SFP speeds are the same |
|  | {{device_controller_id}} is located by LAG, but {{element_id}} is missing provisioned LAG on port {{element_port}} | Add Fabric LAG provisioning to the parent switch connecting to the target device. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0183 | ERROR | alarm | Topology Detection Conflict |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Device Controller | {{element_id}} is a statically located switch controller but has {{device_id}} plugged in. | Check the network fabric connections to make sure that the provisioning of the switch controller matches the desired network physical connectivity. Correction required either in provisioning or cabling. |
| Interface | {{element_port}} has a connection but is provisioned as {{eth_id}} | Remove the provisioning or move the connection |
| Switch | {{element_id}} is connected to itself | Remove self connection |
| Interface | Unequal crosslink provisioning for connected ports: {{element_port}} {{conn_port}} | Make sure the provisioning matches |
| Switch | {{element_id}} is treated as Edge-Device but, has a downstream connection | Remove the connection or un mark as Edge-Device |
| Switch | Failed to create Channel groups on {{element_id}} | Internal System Processing Error. Create system snapshot and contact support. |
| Switch,ONT | Loop detected in topology on {{element_id}} {{element_port}} | Remove one of the connections causing the loop and determine what the intended connections should be and re-connect. |
| Switch,ONT | {{element_id}} {{element_port}} - connection conflict - {{reject_reason}} | Remove the connection causing the issue or re-adjust the roles of the switches in the fabric. |
| Switch,ONT | Topo_connections - {{topo_connections}} and VNETC - {{vnetc}} versions do not match | This is an expected transient condition during system upgrades. If the problem persists, create a system snapshot and notify support. |
| Switch,ONT | {{element_id}} {{element_port}} - rejected connection reason - {{reject_reason}} | Remove the connection causing the issue or re-adjust the roles of the switches in the fabric. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0193 | ERROR | alarm | Device Upgrade Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| ONT | {{element_id}} - {{download_error}} | The system automatically retries the upgrade after a wait period. |
| ONT | {{element_id}} - {{sw_error}} | Ensure that the system has the correct core, image or firmware packages installed |
| Switch | Switch connection for {{dev_id}} failed | This is normally caused by a transient condition due to switch restarting during an upgrade. Wait for the switch to return to service. |
| Switch | Protocol failed for dev_id {{dev_id}}, treating as lost connection -- {{detailed_error}} | This is normally caused by a transient condition due to switch restarting during an upgrade. Wait for the switch to return to service. |
| Switch | Dev_id {{dev_id}} dl_id {{dl_id}} upgrade failed -- {{error_code}} {{error_text}} | System will retry upgrade periodically after failures. If the device still fails to download make sure that the proper package is selected for the device. |
| Switch | Download failed with code -- {exit_code} | System will retry upgrade periodically after failures. If the device still fails to download make sure that the proper package is selected for the device. |
| Switch,ONT | vNetC upgrade failure: {{detailed_error_text}} | Internal System Processing Error. Create system snapshot and contact support. |
| Switch | Switch upgrade for {{dev_id}} failed -- {{detailed_error}} |  |
| Switch | ONIE failure for switch {{switch_sn}} from {{ip_address}}: {{detailed_error}} | Ensure switch model is supported and the necessary firmware package is loaded |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0203 | ERROR | alarm | Device Hardware Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | Stats reporting is disabled | Statistics reporting has been disabled in a prior release.  Contact support to have it restored |
| Switch,ONT | Database connection failed | Internal System Processing Error. Create system snapshot and contact support. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0204 | WARNING | alarm | Device Hardware Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | {{element_id}} PSU failures: {{psu_status}} | Replace or repair the PSU |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0213 | ERROR | alarm | Device Internal Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | Processing overran monitoring period by {{time}} | This is normally caused by a transient condition due to system load.  Contact support if the condition persists. |
| Switch,ONT | Processing almost overran monitoring period by {{time}} | This is normally caused by a transient condition due to system load.  Contact support if the condition persists. |
| Switch,ONT | Load has fallen below {{thresh}} to {{load}} | This indicates system load has recovered from a prior high-load condition.  No action is required. |
| Switch,ONT | Load has risen above {{thresh}} to {{load}} | This indicates system load has entered a high-load condition.  Contact support if the condition persists. |
| Switch,ONT | {{prev_value}} is now {{current_value}} | This message is for information only. No action is required. |
| Switch,ONT | {{block_count}} postgres transaction{{transaction_id}} blocked by {{blocker}} blocker{{blocker_id}} for at least {{time}} | Consider restarting the vNetC if the condition persists.  If it recurs, contact support. |
| Switch,ONT | Postgres notification queue utilization {{usage}} exceeds limit {{limit}} | This indicates system load has entered a high-load condition.  Contact support if the condition persists. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0235 | NOTICE | alarm | Device Manually Placed Out of Service |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | {{element_id}} is marked manually out of service | Mark in service when ready to resume normal operations |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0243 | ERROR | alarm | System Licensing Error |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | License not found, no provisioning attempted | Contact support to obtain a valid license for this site. |
| Switch,ONT | License file missing or has no licenses defined | Contact support to obtain a valid license for this site. |
| Switch,ONT | License file has a license entry with no tenant_id | Contact support to obtain a valid license for this site. |
| Switch,ONT | Site license could not be loaded even without checks -- {{detailed_error}} | Contact support to obtain a valid license for this site. |
| Switch,ONT | Site license has expired | Contact support to obtain a valid license for this site. |
| Switch | Called with model {{element_id}}, expecting ipho.ivas, assuming licensed | Internal System Processing Error. Create system snapshot and contact support. |
| Switch | License check already run, skipping additional check for device {{element_id}} | Contact support to obtain a valid license for this site. |
| Switch | Using FAKE license data | Contact support to obtain a valid license for this site. |
| Switch | License has duplicate model {model} | Contact support to obtain a valid license for this site. |
| Switch | Setting missing license tier {{tier}} to blocked for device {{element_id}} | Contact support to obtain a valid license for this site. |
| Switch | POST for {{element_id}} does not include an 'hw_model', assuming unlicensed | Contact support to obtain a valid license for this site. |
| Switch | Controller {{obj_id}} has dev_id {{dev_id}} but is unlicensed -- checking licensing | Contact support to obtain a valid license for this site. |
| Switch | Could not determine license tier for model {{model}}, controller {{ctrl}} for dev_id {{dev_id}} | Contact support to obtain a valid license for this site. |
| Switch | Controller {{ctrl}}, dev_id {{dev_id}} has unknown license tier {{tier}}, marking unlicensed | Contact support to obtain a valid license for this site. |
| Switch | Controller {{ctrl}}, dev_id {{dev_id}} licensing for tier {{tier}} is blocked, marking unlicensed | Contact support to obtain a valid license for this site. |
| Switch | Controller {{ctrl}}, dev_id {{dev_id}} licensing for tier {{tier}} would exceed limit of {{limit}} | Contact support to obtain a valid license for this site. |
| Switch | Model {{element_id}} matched {{n_model}} models though OUI {{oui}} matched none, using model_id {{model_id}} | Contact support to obtain a valid license for this site. |
| Switch | Model {{element_id}} matched {{n_model}} models, using model_id {{model_id}} with no OUI available | Contact support to obtain a valid license for this site. |
|  | {{license_type}} license limit {{limit}} - exceeded by {{exceeded}} | Contact support to obtain a valid license |
|  | License will expire on {{expiration_day}} | Contact support to obtain a new valid license |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0273 | ERROR | alarm | Pair Degraded |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch Pair | {{element_pair}} is out of sync | Check status of the LAG between the pair of switches and review traffic graphs for any packet layer errors. Run ping test between Router ID IP Addresses. Disable/Re-Enable ports. Reboot each switch individually |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0305 | NOTICE | incident | User Account Updated |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | {{obj_name}} updated | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0315 | NOTICE | incident | Device Created |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | {{purpose}}Created {{model_name}}{{obj_name}} {{obj_id}} | This message is for informational purposes. |
| Switch,ONT | {{purpose}}{{user_id}} created {{model_name}}{{obj_name}} | This message is for informational purposes. |
|  | Bizd will run on site {{site_id}} impacted devices {{device_list}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0325 | NOTICE | incident | Device Deleted |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | {{purpose}}Destroyed {{model_name}}{{obj_name}} {{obj_id}} | This message is for informational purposes. |
| Switch,ONT | {{purpose}}{{user_id}} destroying {{element_id}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0345 | NOTICE | incident | Object Created |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | {{purpose}}{{user_id}} created {{element_id}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0355 | NOTICE | incident | Object Deleted |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | {{purpose}}{{user_id}} deleting {{element_id}} | This message is for informational purposes. |
| Provisioning Object | {{user_id}} failed to delete {{element_id}} | Internal System Processing Error. Create system snapshot and contact support. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0365 | NOTICE | incident | Object Modified |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | {{purpose}}{{user_id}} updated {{element_id}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0395 | NOTICE | incident | System incident |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch Pair | {{user_id}} completed installation, updating feature flags |  |
|  | Forget connection on {{element_port}} --> {{target_port}} triggered by {{user_id}} | User manually removed automatically discovered fabric connection. No action required. |
|  | {{event}} | Information only. No action required. |
|  | {{alarm_key}} mask {{element_pair}}{{element_fabric_lagg_type}}{{element_port}} expired | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0403 | ERROR | alarm | Failed login attempt |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | Failed login attempt by IP: {{ip_address}}, username: {{username}} | This message is for informational purposes. |
|  | Failed connection attempt by IP: {{ip_address}}, common name: {{cn}}, message: {{message}} | Check correct CRLs and Certificate Chains are loaded |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0413 | ERROR | alarm | Monitoring Down |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | Monitoring VM not reachable, monitoring feature not available. | Ensure that the Monitoring VM is properly installed and can communicate with the vNetC. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0425 | NOTICE | incident | Name Changed |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switchpoint | From {{old_name}} to {{new_name}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0433 | ERROR | alarm | System Component Provisioning Failure |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | {{element_id}} - {{detailed_error}} | Remove user provisioning or add redundancy |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0443 | ERROR | alarm | Failed login attempt in last 24 hours |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | Failed login attempt (check history for details) | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0453 | ERROR | alarm | Failed login attempt by blocked IP address |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | Failed login attempt by blocked IP address: {{ip_address}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0463 | ERROR | alarm | BGP Issue |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | {{element_id}} <--> {{sub_id}} : {{status}} | Ensure physical connections are in service with no errors. Ensure that the path and the devices associated with the BGP neighbor are all in service. Re-check the BGP parameters in the Gateway object and Gateway Port Profile, and that they match the external neighbor |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0464 | WARNING | alarm | BGP Issue |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | {{element_id}} <--> {{sub_id}}: {{status}} | Ensure physical connections are in service with no errors. Ensure that the path and the devices associated with the BGP neighbor are all in service. Re-check the BGP parameters in the Gateway object and Gateway Port Profile, and that they match the external neighbor |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0475 | NOTICE | alarm | Read Only Pending |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch | {{element_id}} is read only with pending changes | Review reasons for pending changes. This can be caused by direct provisioning on the device that conflicts with the Verity intended configurations, or changes as a result of a software upgrade. Also can be caused by changes made to the system provisioning while the device was in read only mode. When ready to resume normal operations, take out of read only mode to apply changes, or revert provisioning changes manually on the device.  |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0485 | NOTICE | incident | Global read only modified |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | {{user_id}} set global read only to {{global_read_only}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0494 | WARNING | alarm | Onboarding enabled |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | {{user_id}} enabled onboarding with stop time {{stop_time}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0505 | NOTICE | incident | Onboarding stopped |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | stopped by {{user_id}} | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0515 | NOTICE | alarm | Unsupported Feature |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | Unsupported Capabilities present on the system, see report for more details | Certain provisioned features are not supported by Verity and/or the physical device. Feature capabilities are display at the top of the switch in the GUI. A warning triangle on the switch indicated which specific feature is causing the alarm. This error is a warning to the user and can be ignored, or the provisioning objects can be modified to eliminate the unsupported feature. |
| Interface | {{element_port}} - The chosen breakout override is not supported | Update the Port Breakout selection |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0525 | NOTICE | alarm | Unregistered Device Present |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | Unregistered device present on the system, see report for more details | Usually a transitory state on the system as new devices are discovered. Allow the system initialization of the device to complete. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0535 | NOTICE | incident | Global firmware upgrades modified |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| System | {{user_id}} {{state}} global firmware upgrades | This message is for informational purposes. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0555 | NOTICE | incident | Import incident |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | Completed {{user_id}}'s import, adds: {{adds}}, deletes: {{deletes}}, changes: {{changes}} | This provides a short summary of what changed during a user import. |
| Provisioning Object | {{user_id}} started import | This indicates that a user started an import, either through the GUI or the NBI |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0564 | WARNING | alarm | External backup failed |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
|  | Backup to external server {{server}} failed: {{message}} | Ensure external server is accessible and necessary authentication keys are installed on it |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0575 | NOTICE | incident | User action |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Switch,ONT | {{user_id}} rebooted {{element_id}} | Indicates that a user started a reboot of a device. |

---
| Dict key | Severity | Type | Description |
| -------- | -------- | ---- | ----------- |
| AMP0585 | NOTICE | incident | NBI incident |

| Element type | Error text | Corrective action |
| ------------ | ---------- | ----------------- |
| Provisioning Object | Completed NBI request by {{user_id}}, adds: {{adds}}, deletes: {{deletes}}, changes: {{changes}} | This provides a short summary of what changed during a NBI user request. |