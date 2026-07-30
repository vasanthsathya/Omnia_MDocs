---
hide:
- toc
---
# UI Navigation

## Verity Workspace
Verity Workspace is the "single pane of glass" through which you can configure [Tenant Services](tenants.md/#tenants), [BGP gateways](gateways.md/#gateways), [Layer-3 instances](tenants.md/#tenant-layer-3-configuration), and apply these settings to network leaf ports.

![](media/workspace_6_5.png)

## Main Navigation Bar
The Main Navigation Bar provides quick access to the different work areas in Verity:

![](media/navigation_menu_6_5.png) 

## Basic UI Navigation
The Verity UI is designed to behave like Google Maps in that it uses a zoomable user interface. Panning and zooming is how you view sections in more detail. The more you zoom in, the more context is shown. You zoom in/out by scrolling with your mouse wheel or double clicking to focus on a section. A single mouse click lets you see one layer deeper without zooming in.

- Pan - Hold-click on any point of the map and move the mouse. Keyboard arrow keys also support panning.
- Zoom - Double-click on an object to go to a defined view.  You can also drag and scroll the page to navigate. The + and - keyboard buttons also control zoom.

### Icon Links
Clicking Icons referencing related objects within a given pane moves the user to the referenced object where it can be viewed or edited. All icons are described in mouse pop up tool tips, this helps you learn the options as you become more proficient in using the UI.

## Topology Navigation

### Network Representation
The devices are described in a Spine Plane configuration [Spine Plane Configuration](spine-plane.md)

- PODs are composed of Spine and Leaf switches
- Spine Planes are composed of Superspines
- One Spine per POD connects upward to all Superspines in its assigned Spine Plane
- Multiple PODs can connect to the same Spine Plane, enabling inter-POD communication

![](media/spine_plane_image-with-border.png)

#### Leaf Pairs
Leaf Pairs are represented by a border encapsulating the paired switches.

![](media/be61da0e2b2c96238845a98e496c7e61.png)

When zoomed in, the fabric connection is represented by the following image.

![](media/8c9a57aaaa033a165ba8797e468c4da1.png)

#### Color Connections
The state of devices is depicted by colored connection lines. The available state is depicted by a green color icon, while the down state is denoted by red, provisioning by gold and unstable by yellow. 

**Toggle Color Connections of Leafs**
When in Topology/Topology you can toggle the visibility of connection lines by clicking the line visibility toggle button.

![](media/buttons/6.3/button_toggle_visibility_of_lines.png)

## Buttons
There are two types of [buttons in the Verity UI, **Regular** buttons and **Hex** buttons](icon-reference.md/#verity-ui-icon-reference).

### Regular Buttons
Regular buttons are scattered throughout the application and are used to perform different actions. If a button is not a Hex button it is a regular button. To perform an action with a regular button you left click it. There are many more regular buttons than those shown in the example above. A more detailed description of buttons is presented later in this document.
![](media/regular_buttons.png)

### Hex Buttons
Hex buttons represent tangible objects such as switches or other devices and respond to both right and left click mouse button actions.

![](media/cf5ec92e7ce08abf92282362f28b7ba5.png)

Clicking a hex button causes the window view to center on the Hex button container. Right-clicking a hex button gives you additional options that apply to the object.

![](media/visualization_hex_button_6_3.png)

##### Jumping Views
When you click the hex button a window “jump” is performed moving your view to the respective **Provisioning** section of the application. In the example below, a “jump” is made to the **Eth Port Profile** after clicking the hex button.

![](media/19.png)

![](media/2cbdb59d4d0c5ce2d2f42c9f5f113a6f.png)

#### Navigation Depth Tracker
On the top left of the screen, there is a navigation depth tracker. You can click on the level you would like to directly navigate back to. An example is shown below.

![](media/navigation_depth_tracker_6_5.png)

### Badges
Badges are used to group devices visually.

![](media/badges_6_5.png)


## Network View
The Network View window resides inside the **Topology** and displays virtual devices and connections that represent hardware devices in the physical network configuration.

![](media/network_view_6_5.png)

### Search Workbench
Search Workbench is used to search objects in the UI.

![](media/search_filed_6_5.png)

### Growl History
Growls are errors that occur between the client browser and the Verity orchestration platform. Holding the mouse over the growl gives the user more detail about the error. The Growl history can be viewed at **Alarms/Growl History**.

![](media/growls_6_5.png)

### Alarms

Alarms are notifications that inform the administrator about changes to the network state. These notifications are displayed in the **Events** view under the **Active Alarms** tab.

![](media/alarms_6_5_diagram_3.png)

### Highlighter

![](media/buttons/6.2/button_highlight.png)

Highlighter ![](media/195559eb1239038be9f0875a5d21ac7d.png){: class="btn"}
is a powerful tool for tracing an object usage anywhere in the UI. It is shown within the various objects and at the bottom center of the map. When you use the highlight tool, a purple hue is applied to the selected object. The user cannot use highlighter in the world view.

## Groups

Provisioning Objects can be organized into collections called **Groups**. Groups do not affect the behavior of Provisioning Objects and are used only for aesthetic and organizational purposes.

### How to Create Groups

Open the tile of an object that you want to include in a group. In the example below, a Service tile is used.

The upper right corner of the window contains a field named Group.

![](media/group_field_annotate.png)

Double-click the field to edit it. Click **Create New Group**.

![](media/group_field_annotate_2.png)

Click the checkmark button.

![](media/group_annotate_and_arrow.png)

A window appears prompting you to name your Group.

![](media/fb8ecb68b102818bbb703fc1db8c6c85.png)

Type and submit a name by clicking the checkbox button. The Service is automatically placed in the Group. Any Groups you create are available in the Group drop down menu. As an example, the following image contains 2 custom Groups, one named Accounting East and the other named Accounting West.

![](media/5316fefdeb9fe5cc6a3c8584df12ea0c.png)

The parent tile window renders a new tile for each Group.

**![](media/groups_example_78245628gbt6wbe97t.png)**

### Creating Groups from Reports

Groups can be created via the Reports window. To do this you need to first navigate to the Reports window of the object(s) you want to group.

![](media/reports_groups.png)

Here, Actions are used to create Groups. To create a Group using Actions, click **Actions**, click **Set Group**, name the Group**,** click **Accept Changes.**

![](media/actions_button_with_arrows.png)

!!!Note 
    **Action** menus differ between objects. Depending on your selection, the **Set Group** option may appear differently (e.g., "Set Bundle") or not at all.

The changes are made and visible in the Group column.

![](media/group_report_column.png)


### Default Objects
Windows throughout the application that are used to edit device parameters have a default object. This object is displayed in light-green and is editable.


![](media/default-object-example.png)