# Reserved Ranges

!!! warning

    If your system's network identifiers require custom ranges, it is strongly recommended to configure these settings *immediately after* installing the Verity software and *before* beginning the preprovisioning process. The preprovisioning process involves adding devices using the system initialization file and/or manually adding devices. Changing the network identifier ranges later may require reprovisioning the entire network.

The **Provisioning Reserved Ranges** section displays a set of editable value ranges for networking identifiers used in the provisioning process. On a new system, it populates with working default values, so the user doesn't need to perform any custom configuration to have a working system.

To tailor the network setup to specific requirements, you may need to customize the allocated ranges of network identifiers. Customizing these settings allows for more precise control over network configurations and ensures compatibility with your network environment. To view this section go to **Operations -> Fabric Configuration -> Provisioning Reserved Ranges**. To change the values click the edit icon ![](media/buttons/6.2/btn_edit.png){:class="btn"} .

![](media/provisioning_reserved_ranges_2.png)

### Example of Reserved Range Values

Verity uses reserved range values across the system. Certain values are shown in specific windows with the **Auto** prefix, signaling that the user can change them if needed.

![](media/reserved_range_values_6_6.png)
