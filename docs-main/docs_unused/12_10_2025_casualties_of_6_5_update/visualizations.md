---
hide:
- toc
---

# Visualizations
The **Visualization** feature provides graphical representations of various device details. 

![](media/visualizations.png)

## Open Visualizations
The Visualizations feature can be accessed in three different ways.

1. Open **Visualizations** via the **Reports** icon and click the **Visualizations** menu tab.

![](media/visualization_6_3_data_center.png)

2. Right Click a Hex button that provides **Visualizations** as an option in the form of menus titled **Visualization Used For** and **Visualization Used By**.

![](media/visualization_hex_button_6_3.png)

3.Click the Visualization icon (![](media/buttons/6.3/button_open_visualizations.png){:class="btn"}) on a device port .

![](media/device_port_6_3.png)

### Diagrams
The following sections describe the data representation of each diagram.

### Provisioning Tree
The **Provisioning Tree** lets you visualize what provisioning objects or interfaces are used for / used by.

![](media/0fc8eafdc404ed7ce6e33f0ecbd8047e.png)

There are three ways to access the **Provisioning Tree** diagram.

- You select **Provisioning Tree** from the Mini-Map**.**
- You click the **Visualization Button** directly on a UI device port.
- You select **Visualize Used For** or **Visualize Used By** in the provisioning objects Hex button selection menu.

These three choices are described in detail below.

#### Access Provisioning Tree Visualization from Device Port
Click the ports **Open Visualization** button (![](media/buttons/6.3/button_open_visualizations.png){:class="btn"}) .

![](media/device_port_6_3.png)

The **Access Provisioning** diagram opens for the selected port.![](media/74.png){: class="pop"}

### Select Access Provisioning via Visualize Used For or Visualize Used By
When you right-click a provisioning object's Hex button, the menus “**Visualize Used For**” and “**Visualize Used By**” are presented to you. These options allow you to view the role of the selected object in relation to other objects.

![](media/75.png)

**Visualize Used For:**  This visual representation illustrates the interconnections among objects using the selected provisioning object. The selected provisioning object is on the left, and its hierarchical relationships with the other objects are displayed to the right of it.

In this example **Visualize Used For** is selected on an Eth-Port-Profile named **Finance Department and Ops**.

![](media/76.png) 

In the diagram below, the object representing the Eth-Port Profile named **Finance Department and Ops** is rendered to the far left of the diagram and is composed of the objects to the right of it.

![](media/77.png)

**Visualize Used By:** This visualization shows objects that are used by the selected object. In this diagram, the selected provisioning object is positioned to the far right, and its hierarchical relationships with objects that use it are presented to the left.

![](media/78.png)

### Tenant Route

**Tenant Route** is a diagram that shows Tenant-Tenant Routing relationships.

![](media/tenant_route_visualization.png)

Hovering over an individual Tenant highlights its Tenant-to-Tenant routing relationships in *green*.

![](media/tenant_visualization_hover_device.png)

These relationships are reflected in the **Tenant Slice** window in **Tenant-Tenant Routing**.![](media/80.png){: class="pop"}