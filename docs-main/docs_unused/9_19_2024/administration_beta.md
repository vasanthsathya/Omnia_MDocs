---
hide:
- toc
---
# Administration

Administrative settings are organized into two sections. These are **Admin** and **Installation Admin**.

##Admin 

To access the **Admin** settings click the **Admin** icon.

![](media/buttons/6.3/buttons_admin.png)



![](media/admin_tile_contents_6_3.png)


### Provisioning Reserved Ranges
To provision the underlay, the system requires the ability to assign ASNs and IP addresses. The exact number required depends upon the maximum expected size of the data center. Because changing these values later can severely affect the integrity of an operational data center, it is recommended that you set the expected maximums larger than any expected growth. The underlay Reserved Range page shows the reserved ranges. User assigned ASNs and IPs cannot be chosen from these ranges.

Verity assigns variables within these ranges as managed objects are created. The variables are marked as "auto" in the UI screens where they are used and can always be overridden in each use case if required.

**It is highly recommended that these are set up during system installation. They can be changed later, but it will be a service affecting change as most of the configuration needs to be replaced system wide.**




### Licensing 
The Licensing displays License Usage and Physical Port Usage bar graphs. While focused on the object, the user can see the date of licensing expiration, contact information for support, and reports of license and physical port usage. System licensing information is available in **Licensing**. To access this section click **Admin** and then click *Licensing*

![](media/731c8d157e28a4c4d49508964a9c64fd.png)

## Installation Admin
To access the features discussed below, go to **Support / Installation Admin**.

![](media/support_installation_admin_6_3.png)

![](media/installation_admin_6_3.png)

### Routing
Routing includes the following WAN IP information.

-   Hostname (fully qualified domain name)
-   RAT Port Range
-   WAN IP Source (DHCP or Static)
-   WAN Default Route
-   WAN IP Address
-   DNS Server


### Certificate Management
Certificate Management is a drag and drop control panel to import SSL Certificates.

#### How to Access the Certificate Management Options
To import a Certificate, go to the **Support** drop down menu and select **Installation Admin**. ![](media/installation_admin_6_3_highlight.png){: class="pop"}

In the window that appears double-click the section titled **Certificate Management**. ![](media/certificate_management_6_3.png){: class="pop"}  

In the window that appears, double-click the tile that describes the certificate you want to upload.You can either drag the certificate to the drag and drop section or click the browse button and select your certificate file to upload it.  


![](media/drag_drop_certificate_tile_6_3.png)


<!-- TODO need instructions for this feature -->

### Branding

Branding is where you apply custom business branding to your Verity application as it is shown in the browser.

Branding can be applied to:

  - Banner - large logo across the top of the UI display
  - Favicon - icon on tab header in browser
  - Top Logo - smaller logo displayed on top left of UI 


### Settings
Settings lets you configure the following:

-   vNetc Address on Management VLAN
-   Permissible IP Address Ranges on Managed Devices
-   Customized Download Address/FQDN

### Monitoring, Backups and Logging
Monitoring, Backups and Logging lets you configure status monitoring, backups, and loggings of the vNetc via SNMP, SFTP and SYSLOG.

### Report
Report lets you run scheduled service reports and export the data as a CSV file. 

![](media/schedule_reports_window.png)




The options and fields for the report are:

| **Field**               | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Run Daily      | Run the MAC address search every day                                                                                                                                                                                                                                                                                                              |
| Report Name               | Filename output by the system. Recommend using CSV extension | 
| Last Modified | Indicates last time report was run |
| Services | List of Services on the system. Check box indicates that the service should be included in the report |


## How to Access Feature Flags
To enable or disable feature flags, first enable SD-Admin by double-clicking the SD-Admin button icon.
In the window that appears, double click the tile titled "Settings". In the window that appears, the feature flag
options are presented as a collection of checkboxes. 

The feature flags are generally used to enable or disable visibilty of options in the UI and other system wide behaviors. Please consult with BE Networks regarding the usage of these settings beyond the defaults that are set upon installation.

## How to Access Radius Server Settings
To access the Radius Server settings, first click the **Support** menu and click **Installation Admin**. ![](media/installation_admin_6_3_highlight.png){: class="pop"}


In the window that appears double-click the tile named **Users**. Double-click the tile
named **Radius Logins**.

Add rows for up to 4 RADIUS servers that Verity will connect to when users login to validate their user name and credentials.

## How to access SYSLOG
Enable SD-Admin by double-clicking the SD-Admin button icon. Click the window titled "Monitoring, Backups and Logging".


## How to Automate Backups
Enable SD-Admin by double-clicking the SD-Admin button icon. Click the window titled "Monitoring, Backups and Logging". Under the heading "DB Backups" is where you automate system backups.

## Users and Permissions

Verity supports role based access (RBAC) permissions scheme to partition the various workflows to operational personnel.

| **Permission**               | **Parameters**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |     **Role**          |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------|
| [DEV] Device Management      | Add device controller, Swap switchpoints,  Set read only mode,  Capture device snapshot,  Trigger a full device rescan by ACS, Open a remote access tunnel, Reboot switch,  Mark device out of service.                                                                                                                                                                                                                                                                                                                             |  Device Operations    |
| [NW] Network                 | Edit POD name,  Add a new preprovisioned switch  Designate LAN TORs (Management Network),  Lock switch Edit site, Create switch pairs,  Create a static connection, Delete device controller, Edit device controller, Site Settings (DHCP snooping, Aggressive Reporting, CRC Failure Threshold) , Underlay Fabric Configuration  |  Network Operations  |
| [SEP] Switch Endpoint        | Edit Switch Name and type (spine/leaf)  Delete Switch Edit switch Note, Port Provisioning                                                                                                                                                                                                                                                                                                                                                                         |  Day-Day Service Management  |
| [BP] Base Provisioning       | Manage Tenants, Gateways, LAGS, Route map assignments                                                                                                                                                                                                                                        |      Infrastructure |
| [GBL] Globals                | Manage badges, Radius servers for 802.1x                                                                                                                                                                                                                                                                                                                                                                                                                     | Security       |
| [IE] Import                  | Import snapshots, Clear system                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |  Global Provisioning |
| [SVC] Services               | Manage services, Change assigned tenant                                                                                                                                                                                                                                                                                                                                                                                                                                                      |  Service Creator               |
| [SET] Sets                   | Manage Firmware Update Sets                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |  Software Manager   |
| [VIEW] Views                 |Manage Views                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Monitoring   |



### User Roles
This feature lets you grant or restrict features to selected user roles.

#### Assigning Users to Roles
1. Select the **User Accounts** item box. ![](media/71e08a77fee80b76a17e5b52657b3b79.png){: class="pop"} 
1. In the window that appears, click the Access Level menu item twice for the chosen user. ![](media/b7fd8578cdc1f859a4d652c02adb997f.png){: class="pop"}  You can also select the edit icon (![](media/762938c4d2a53ea9622dad7040002ede.png){: class="btn"}) in the upper right corner of the **User Accounts** window to edit the page.
1. Choose the Username you want to change and set the **Access Level** to the desired role. ![](media/5e5c24b0af7804c6deda92bbed4ff548.png){: class="pop"} 
1. To complete the process, click the checkmark ( ![](media/51ff4d9f4c07cf2999a6033ab24ec47a.png){: class="btn"} ) in the upper right corner of the **User Accounts** window to save your work.

### VNFs
This section of the map focuses on the management of the virtual machine installations of the vNetc and SDLC. This includes the ACS, GuiA and DHCP server. Device Controller settings are also in this section. ![](media/53d3010397780b4ce03544ebf148c9f8.png){: class="pop"}

### vNetC Commander
This section is composed of important processes working within the vNetC virtual machine. ![](media/57e33c41f1f5a35f1b073e958dd22084.png){: class="pop"}

### System Applications
System applications are ACS and GuiA. To create a new system application:

1. Click the **Add a System Application** button. (![](media/buttons/6.2/button_add_item.png){: class="btn"}) ![](media/58.png){: class="pop"}

### GuiA
**GuiA** stands for UI Acceleration and is a new system application that increases UI performance. To add **GuiA** to your application:

1. Open the Admin tab and click **Settings**. ![](media/59.png){: class="pop"}
1. In **Feature Flags** check the box next to **Enable GuiA** and save your selection. You are only allowed 1 **GuiA** instance for your application. ![](media/60.png){: class="pop"}
1. Go to **Verity**. ![](media/d570e9c6246e8766da2ec8866742d5c0.png){: class="pop"}
1. Click **VNFs**. ![](media/60.1.png){: class="pop"}
1. In the window that appears, click to open the **SDLC** contents. ![](media/61.png){: class="pop"}
1. In the window that appears click the create button (![](media/buttons/6.2/button_add_item.png){: class="btn"}) ![](media/62.png){: class="pop"}.
1. Choose **GuiA** from the prompt that appears.
1. In the window that appears enable the application and fill out the fields with the relevant IP information. ![](media/63.png){: class="pop"}
1. Save your work by clicking the checkbox icon(![](media/9bc0cdaa2797b2a57868072c2f8c30bd.png){: class="btn"}).
1. The yellow **Status** box text reads **Awaiting Status**. When it changes to **Connected**, the process is complete. ![](media/64.png){: class="pop"}

## Export Selected Provisioning as JSON for Later Import
1. Enable the world view by clicking the World icon.
1. Open **Import/Export** Workbench.
1. Click **Export** Button.
1. Select the JSON option.
1. Click **Export** button.