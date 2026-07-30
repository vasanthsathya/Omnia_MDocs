---

title: "Device Management"
description: "How to configure devices for verity"
tags: [Leaf, Spine]
search:
  boost: 3           # ← Lower than main overview
parent: Advanced Configuration

hide:
- toc
---

# Device Management 

This section explains how to onboard devices to a Verity system. The most efficient approach for creating the system initially is to use the bulk configuration method via a system initialization file. However, devices can also be onboarded individually through the Verity UI.

## Adding Individual Devices

!!! Note

    This section describes how to manually add devices to the system. To add devices in bulk  please see the section titled [Onboarding Devices in Bulk](adding-devices.md)

Adding a new spine or leaf device is a multi-step process described by the following steps:



![alt text](media/device_management_diagram.png)

1. Create or select the provisioning object.
1. Configure the [Device Management Connection settings](/fabrics/#device-management) .
1. Prepare the physical switch.
1. Boot the device.
1. Connect the switch to the peers.


## Preprovision Object Creation
Preprovisioning lets the user set up the device before the hardware arrives. Zooming in allows the user to edit the details of the device.

![](media/spine_leaf_blue.png)


### Adding Leaf or Spine Devices
1. Click the **Topology** navigation item.
1. Click **Network View**.
1. In the upper right cornet of the **Network View** click the **Add Preprovisioned Switch** (![](media/buttons/6.2/button_add_new_preprovisioned_switch.png){: class="btn"}) icon.
1. Enter the name of the switch.
1. Set the number of **Expected Eth Ports**.
1. Set the **Rack** text (Optional).
1. Click-hold the **Type** field and select **Leaf**, **Spine**, **Superspine** or **Management**.
1. If the switchpoint is designated as a Leaf or Spine, Click hold the **POD** field and set its value.

The following section describes other switchpoint management features. These are not required for device onboarding, but do give the user the ability to create provisioning for the switchpoint before the phyical device is detected and brought into the system. To proceed with the new device creation skip to the Device controller section below.

#### Manage Rows Button
![](media/managed_rows_example_6_6.png)

The **Manage Rows** button (![](media/buttons/6.2/manage_rows_button.png){: class="btn"}) provides a convenient way to apply the same settings to multiple ports on a single switch. The settings include switch provisioning as well as the mass enabling/disabling of Edge ports. ![](media/manage_rows_buttons.png){: class="pop"}

##### Set Eth-Port Provisioning
This option lets you choose an **Eth-Port Profile** and apply it to a port or to a consecutive list of ports. ![](media/14a8cbd016650199367b861b01b5adb7.png){: class="pop"}

##### Set Eth-Port Setting
This option lets you choose an **Eth-Port Setting** and apply it to a port or to a consecutive list of ports. ![](media/c647603c0ec500f2be97b627a6ae06f5.png){: class="pop"}

##### Replace Eth-Port Provisioning
This option lets you choose all ports by their assigned **Eth-Port Profile** and replace the assignment with a different **Eth-Port Profile**. ![](media/565ec97f9110e4a5b628955b7f4b68ff.png){: class="pop"}

##### Replace Eth-Port Settings
This option lets you choose all ports by their assigned **Eth-Port Setting** and replace the assignment with a different **Eth-Port Setting**. ![](media/e139c97c4ec81160e121f20f187479d3.png){: class="pop"}

##### Clear All
This setting clears **Eth-Port Provisioning** values and sets **Eth-Port Profiles** to default for a port or a consecutive list of ports. ![](media/dfdb1dd0c2c83e6162c4d2410d263202.png){: class="pop"}

##### Enable Edge Ports
This setting lets you enable an **Edge Port** or enable a consecutive list of **Edge Ports**. ![](media/enable_ports_manage_row.png){: class="pop"}

##### Disable Edge Ports
This setting lets you disable an **Edge Port** or disable a consecutive list of **Edge Ports**. ![](media/disable_ports_manage_row_buttons.png){: class="pop"}



### Enable or Disable Individual Device Port
To enable or disable an individual port, zoom in on the port and click the **Enabled** checkbox to set the desired state.


![](media/how-to-enable-or-disable-a-port.png)



## Device Management


Device Management is used to create the interface between the Verity application and the switch. Based on the LLDP capabilities of the switch, it can be automatically discovered in the network topology, or it can be statically located. For systems containing many devices, the configuration settings in Device Management can be imported/exported from the Import/Export tool bench available from **Operations / Import/Export** ![](media/operations_import_export.png){: class="pop"}

### Configure Device Management Settings
1. Go to fabrics and select the device. Navigate to the section titled **Device Management**.
1. Enter the **LLDP Search String**. This value must be either the chassis ID or the serial number of the managed device. This value serves as a hardware identifier and is used to detect connections between managed devices. Later, this value will auto-populate in the pre-provisioned Device ID when the entries to the Device Management settings are saved.
1. Enter the Switch IP and Mask.
1. Enter the Gateway.
1. Enable the Device Management settings and save the changes.
1. **Verify the Hardware Identifier**. The Device Management LLDP Search String should appear on the provisioning object in the **Device ID** field. (![](media/lldp_device_id_example_update_2.png){: class="pop"})



!!! note "How Switch Hostnames are provisioned"

    ![](media/sonic_switch_cli.png)

    The Device Management settings for each switch includes both an LLDP Search String and a ZTP Identifier field. How these fields are populated determines how the hostname is assigned to the device. The hostname can be the set to the switchpoint name or to a hardware identifier (serial number or chassis ID).

    * If only the LLDP Search String is entered and the ZTP Identifier is left blank, Verity uses the LLDP Search String to create ZTP files, set the hostname and identify the device during network topology discovery.
    * If both fields are filled with different values, the ZTP Identifier is used to create ZTP files, the LLDP chassis ID is used to identify the device during network topology discovery, and the hostname is set to the switchpoint name.


## Physical Switch Preparation and Connection.

!!! warning "New Devices Starting Point"

    It is required that all SONiC devices being onboarded into Verity start in ONIE mode with no OS installed. This ensures that the device receives its load from the Partner Firmware Package installed on Verity and runs through the ZTP process. (If the current switch is running OS10 with DHCP enabled, OS10 is automatically removed when using DHCP options set up according to this documentation.)

When ready, connect the management port of the new device to the **Out-of-Band Management** network. Then, connect the device to the other relevant spine/leaf switches needed to integrate the device into the system.

## Zero Touch Provisioning
Verity’s ZTP feature is a way to remotely set up switches without having to manually configure them on a hop-by-hop basis. The process consists of two steps: ONIE Boot process and ZTP Provisioning portion.

The ONIE process starts when a switch boots up from the factory without a SONiC image and it connects to a remote server to download the necessary software image. The actual ZTP process starts with a switch that has SONiC loaded and a default configuration. The verity system creates a series of files that are used to prepare the SONiC switch with a minimal configuration to communicate with the Device controllers within Verity. DHCP options on the Verity SDLC server tells the switches the location of the remote server (vNetC) where the required files are stored. The system supports ZTP for both the management and spine/leaf switches.