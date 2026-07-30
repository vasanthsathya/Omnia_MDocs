---
hide:
- toc
---
# Ethernet Port Settings (Eth-Port Settings)
Eth-Port Settings allow the operator to define settings specific to a port related to Layer-1 and Layer-2 features such as port speed, speed/duplex negotiation, and Power-over-Ethernet (PoE).

The following figure shows the detail within an Ethernet Port Settings dialog box:

![](media/eth-port-settings-example.png)

## Create an Eth-Port Setting
1. Navigate to the Eth-Port Settings tile by clicking **Templates** and from the **Templates** tab double-click **Eth-Port-Settings**.
1. Create an Eth-Port Setting instance by clicking the **Add** button (![](media/buttons/6.2/add.png){:class="btn"}).
1. In the prompt that appears, enter a name for the **Eth-Port Setting**.
1. Apply desired settings.
1. Enable the settings by clicking the **Enable** checkbox.

## Apply an Eth-Port Setting
1. Determine the port you wish to apply the Eth-Port Setting on.![](media/eth_port_settings_on_port.png){: class="pop"}
1. Open the port editing window and assign the Eth-Port Setting in the right most dropdown menu. ![](media/choose_an_eth_port_setting.png){: class="pop"}

## RoCEv2

![](media/rocev2_device_settings_6_5.png)

**RoCEv2** provides a routable, lossless data transport over standard Ethernet, crucial for GPU-intensive workloads. By operating over UDP/IP, it scales across subnets. Its reliance on **Explicit Congestion Notification** (ECN) and **Priority-based Flow Control** (PFC) guarantees reliable data delivery, thereby avoiding performance bottlenecks in demanding GPU applications like AI/ML.

### Enable WRED Tuning
Enable custom tuning of WRED (Weighted Random Early Detection) values. Uncheck to use switch default values.
#### Minimum WRED Threshold
A value between 1 and 12480 (in Kilobytes)
#### Maximum WRED Threshold
A value between 1 and 12480 (in Kilobytes)
#### WRED Drop Probability
A value between 0 and 100
### Enable Watchdog Tuning
Enable custom tuning of watchdog values. Uncheck to use switch default values.
#### Priority Flow Control Watchdog Action
Ports with this setting will be disabled when link state tracking takes effect.
#### Priority Flow Control Watchdog Detect Time
A value between 100 to 5000.
#### Priority Flow Control Watchdog Restore Time
A value between 100 to 60000.

!!! info 

    Applying port speeds below 10G to ports within a Port Group (discussed below) requires additional configuration. Please read [How to Configure a Port Group Member to Operate Below a Speed of 10G](ethernet-port-settings.md#how-to-configure-port-group-members-to-operate-below-a-speed-of-10g)

## Port Groups

Port groups provide a way to manage multiple ports collectively based on their underlying hardware constraints. On certain networking switches ports are organized into groups that must maintain uniform speeds—either 10G or 25G across all ports in the group. To change the speed of any port in the group, you must reconfigure the entire group using the command ` port-group 2 speed 10000 `, which would set all ports in group 2 to 10G operation.

### How to Set the Port Group Speed From Verity
To set the port group speed from Verity you use the **Port Group Speed** settings of your selected group from the Topology window.
The Port Group Speed settings are only visible on the first port of each port group. If ports 1-4 belong to the same group, the field appears only on port 1.

![](media/port_group_speed.png)

The available values are:

* 10G
* 25G
* None

### How to Configure Port Group Members to Operate Below a Speed of 10G

1. Set the Port Group Speed to 10G.  ![](media/port_group_speed.png){: class="pop"}
1. Configure the individual port speed to below 10G in the Eth-Port-Settings assigned to the port. ![](media/eth-port-settings-speed.png){: class="pop"}
