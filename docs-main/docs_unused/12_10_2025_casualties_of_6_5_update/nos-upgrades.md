---
hide:
- toc
---

# NOS Upgrades

Successful device software upgrades typically necessitate a device reboot. However, forcing a full network-wide restart for each device update is impractical and unacceptable. The solution to this problem is **Image Update Sets**.

**Image Update Sets** allow you to organize devices into user-defined groups and target these distinct groups for software updates. This approach enables the system to leverage the redundancy of active switches to maintain network availability during the update process. The trade-off for this approach is that during the update the system may have reduced capacity, but it allows you to safely upgrade sections of your network without shutting down the entire system.

## Upgrade by Image Update Sets

!!! NOTICE 

    This section describes the mechanics of using Image Update Sets; it does not cover how to apply them to any specific configuration or deployment scenario.

To access Image Update Sets, go to **Operations/Image Updates**. 

![](media/9d775e9a14ab58eaee07630a297c3c3e.png)

The presented window is composed of rows and columns, with each row representing an Image Update Set and each column representing information specific to that Image Update Set. The **Members** field displays how many devices are in the Image Update Set. The columns titled **Name**, **Rules** and **Upgrader** are user defined values. The last column **Pie Charts** contains graphs that detail the state of the installation.

### Members
**Members** shows the device count for the Image Update Set. Double-clicking area opens a Report listing all devices in the set.

### Name
**Name** is where you name your Image Update Set.

### Rules
Devices are grouped into Image Update Sets by using conditional logic in the **Rules** column. A Rule contains a **Not** clause, a condition (named **Rule Type**), and a field containing values contingent on the condition (named **Rule Value**). The Rule value options change depending on the selected Rule type. All three fields are shown in the following image.



![](media/9c48b396e85cb6dce67f44d877bec3a1.png)

Each Image Update Set can have up to three Rules.



![](media/three_image_update_sets.png)


There are many conditions to choose from. Clicking the conditional field provides a scrollable list.

![](media/2f50f011a243d8197b445d99fbb2a15c.png)

**Rule Example**

The example in the following image selects all devices assigned a **Badge Color** of **blue**.

![](media/895a4571349935018d06e7609b9ea276.png)

This more complex example selects all devices in the network with a blue **Badge Color** that are in **POgit pull
D C** and are **Not** of the product class ONT.

![](media/7a0a86832ceb019d6c5a983b5543c039.png)

When writing Image Update Sets, it is important to understand that order matters. If a device is included in an Image Update Set, it cannot be included in subsequent Image Update Sets further down the page.

In this example, the conditions are the same for both Image Update Sets but only the first Image Update Set contains members.

![](media/83d75f0d049bb8993ee00e0f47b882f5.png)

Any devices not explicitly assigned to an Image Update Set are assigned to  **All Others** on the bottom row.

![](media/ba28309143c5ea3345508262fbe74b1e.png)

## Upgrader

The Upgrader column is where you select the software version package and schedule the reboot time. This action is applied to all devices that fall within the Image Update Set Rules.

![](media/a1c9eeef14a254c1ba996760da674167.png)

The first field specifies the software version, followed by three options for selecting the device's restart time.

**Now**

This performs the image transfer and reboots immediately.

**Month/Day/Year, Hour: Minute: Second AM/PM**

When you select this option, the image file is transferred and written to the standby partition of the device. The device then reboots at the scheduled time.

!!! Notice 

     Switch Devices have active and standby partitions. This allows you to load device image software during normal operation and reboot at a scheduled time.

**Next Reboot**

When you select this option, the image file is transferred and written to the standby partition of the device and updates on the next *manual* reboot.

## Pie Charts

The last column of information, titled Pie Charts, consists of pie charts that present device states as visual graphs. 

![](media/image_update_sets_pie_charts.png)

There are four metrics that are expressed:  **Installation**, **Comm**, **Provisioning** and **Upgrader**.
Individual pie charts can be hidden by unchecking the checkboxes at the top-left of the Image Updates tile.

![](media/pie_chart_show_hide_checkboxes.png)

# Upgrade by Device
Each device can be upgraded individually independent of Image Update Set. To do so, zoom into the device **SW Version** tile.![](media/c6ec2dde4551db953e974a2ad134519a.png){: class="pop"}

In the window that appears you have the choice to choose **Target Package** by **Set** and **By Device**. Select **By Device**. The drop-down menu lists the available upgrade packages. Choose the one you desire. Save the choice by clicking the save button.

!!! Warning 

    The moment you save, the device will reboot!

![](media/1a29dcb5dc307840254a37de65b3fbb3.png)


### Enable/Disable Devices from Receiving Software Updates.

In Network View, the **Image Upgrades of all Devices Enable/Disable** button ![](media/buttons/6.3/button_firmware_upgrade_enable_disable.png){: class="btn"} determines if a system will accept software updates.



![](media/image_upgrades_icon_6_5.png)
