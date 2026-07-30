---
hide:
- toc
---
# Network Operations
There are a number of common operations that operators may perform on their network.

## Network Read-Only Mode

1. Click **Topology** and navigate to the **Network View**, click the **Read-Only** icon to "on" (![](media/buttons/6.2/button_read_only_toggle.png){: class="btn"}) 

![](media/read_only_with_lable_6_5.png)

!!! Note 

    The read-only mode can be applied to the world and per switch. All levels are honored simultaneously and are displayed on each switch.

    World wide read only is automatically set during a CORE upgrade of the vNETC. It is recommended, but not required, to be set for firmware and other major system updates to allow the user to see what unexpected changes may be caused by those actions.

## Switch Replacement

The new device should be in ONIE mode.

1. Remove the old device from service (![](images/MOS%20Switch.png){:class="pop"}).
1. Delete the old device (![](images/Delete%20Switch.png){:class="pop"}).
1. In the option box, make sure "Preserve Switchpoint" and "Disable Controller" are selected (![](images/Preserve%20End%20and%20Ctl.png){:class="pop"}).
1. In the Preprovisioned Switchpoint, replace the Device ID field with the new Serial Number or Service Tag (![](images/Replace%20Service%20Tag-Serial.png){:class="pop"}).
1. Go the disabled controller, and update the Service Tag field with the new device Serial Number or Service Tag (![](images/chg%20ctl%20servicetag.png){:class="pop"}).
1. Re-enable the controller

Refer to the ZTP sections for the ZTP process for the switch role (ie Leaf, Spine or Management). The new switch shhould go through ONIE and ZTP process and start communicating with the Device Controller.

## Add New Site Note
1. Click Topology and navigate to **Network View**.
1. Click the **Note**  (![](media/buttons/6.2/button_edit_note.png){: class="btn"}) icon.
1. Enter the text of the new site note.
1. In the same popup, click the **Save** icon.


# Device Operations
Inspecting devices and performing operations on them is accomplished in the Switchpoint object in the Topology view.

![](media/device_operations_6_6_.png)

## Using Device Operations
Zoom to a device by double clicking on it in the topology map (![](media/switch_head.png){: class="pop"}).


### How to Reboot a Switch
From **Topology**, zoom into the network operations section (top lower right) of the device and click the reboot button.

![](media/reboot_this_switch_6_6.png)

### Device Locks
![](media/buttons/6.2/button_lock_unlock.png)


Locking a device restricts users without **[NW] Network** privileges from editing it.(![](media/admin_user_roles_nw_network.png){: class="pop"}) 




### To Lock a Device:

1. Click **Topology**
1. Zoom in to the top of the device ![](media/switch_head.png){: class="pop"} . 
1. Click the lock icon (![](media/buttons/6.2/button_switch_locked.png){: class="btn"}) .


### Device Operational Tools
| Icon      | Name | Function |
| --------  | ---- | ----     |
| ![](media/buttons/6.2/button_current_switch_configuration.png){: class="btn-large"}| Show the current switch configuration| Show current switch configuration |   
| ![](media/buttons/6.2/button_open_mac_address_workbench.png){: class="btn-large"}| MAC Address Search | Search for a MAC address on this device |   
| ![](media/buttons/6.2/button_open_system_logging.png){: class="btn-large"} | System Log | View the system log |
| ![](media/buttons/6.2/button_highlight.png){: class="btn-large"}| Highlighter | Highlight the device on the topology map |
| ![](media/buttons/6.2/button_open_for_edit.png){: class="btn-large"}| Edit | Edit the device settings |
| ![](media/buttons/6.2/button_lock_unlock.png)| Lock | [Locks the device](#device-locks)
| ![](media/buttons/6.2/button_delete.png){: class="btn-large"} | Delete | Delete object |
| ![](media/buttons/6.2/button_manage_switch_pairs.png){: class="btn-large"} | Manage Switch Pairs | Add Switch Pairs |
| ![](media/buttons/6.2/button_ping_traceroute.png){: class="btn-large"} | Opens Ping/Traceroute Dialog| Open Ping/Traceroute Dialog|
| ![](media/5ac6a3eebe48a95d0c2b4e6d9b5eeb50.png){: class="btn-large"} | Capture Snapshot | Capture a snapshot of this device for troubleshooting - press once to start capturing and then again when capture is complete (icon turns dark green)|
| ![](media/buttons/6.2/button_rescan.png){: class="btn-large"} | Rescan | Trigger a full rescan by the ACS of this device. |
| ![](media/buttons/6.2/button_open_remote_access_tunnel.png){: class="btn-large"} | Open Tunnel | Open a remote access tunnel |
| ![](media/buttons/6.2/button_open_report.png){: class="btn-large"} | Report | Open report |
| ![](media/buttons/6.2/button_reboot_device.png){: class="btn-large"} | Reboot Device | Reboots Device  |
| ![](media/buttons/6.2/button_out_of_service.png){: class="btn-large"} | Out of Service | Mark device out of service. |

## Badges
Badges are used to group devices visually. Badges are assigned a name, a color and a number.
To create a new badge or view all badges go to  **Operations/Badges**.

![](media/operations_badges_6_6.png)

### Create and Assign Badge to Device 

1. Click **Topology**. 
1. Enable focus of a selected device.
1. Click the **Edit** icon.
1. Click set badges icon (![](media/buttons/6.2/button_badge.png){: class="btn"})  ![](media/switch_badges_edit_example.png){: class="pop"} .
1. Enable the check-box next to the phrase **Create New Badge** ![](media/create_assign_badge_window.png){: class="pop"} .
1. Set a **Name**, **Color** and **Num** for the badge.
1. Click **Yes** to create the badge.