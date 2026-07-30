# Installation of Verity for Enterprise Software Components in a VMWare Environment



## Introduction

The Verity management and orchestration system is comprised of two functional components, both of which are instantiated as Virtual Machines (VMs). This document describes the installation and configuration of these VMs within a VMWare ESXi server.

## Virtual Machine Overview

Verity’s two VM functional components are:

1.  Virtual Network Commander (vNetC) – Functions include the orchestration logic, UI hosting, northbound RESTful API, and databases.
2.  Software Defined LAN Controller (SDLC) – The SDLC VM is comprised of a series of containers that map one-to-one to the managed switch devices. Functions include network discovery, device provisioning, and network assurance. The SDLC serves as the abstraction layer between the managed switch and the vNetC by translating the native management protocols into the vNetC’s NETCONF interface and Yang model.

## Topology Overview

Below is the basic VM and hardware topology for reference.

### Recommended Network Management Architecture

Each system requires a management subnet that can support 4 system IP addresses as well as 3 IP addresses per managed switch. The breakdown is as follows:

| **IP address Allocations for Management Network** | **Component**                      | **Allocation**               |
|---------------------------------------------------|------------------------------------|------------------------------|
| Verity System components                          | vNETC LAN side, SDLC, ACS, GuiA    | 4 Static Addresses           |
| Managed Switches                                  | Verity Switch Controller\*         | 1 Dynamic Address per switch |
| Managed Switches                                  | Switch in ZTP Process (optional)\* | 1 Dynamic Address per switch |
| Managed Switches                                  | Switch Post ZTP Process\*          | 1 Static Address per switch  |

-   If applicable

The orchestration platform (vNETC) is configured on the customer’s network with one static IP address to be accessed by users.

The following diagram shows the recommended management network architecture. Variations are possible based on individual customer’s network needs. A second diagram follows with a version showing only one connection to the vNETC.

![A diagram of a computer server Description automatically generated](../media/730fda87b9cd45d7f60a91d8be6ce2ec.png)

![A picture containing text, screenshot, diagram, rectangle Description automatically generated](../media/8ca9dc45163636a83dddbab79922c5e8.png)

## Prerequisites

1.  vNetC
    1.  Resolvable, fully qualified domain name
    2.  Static IP address, gateway, DNS servers
    3.  Valid Verity license
2.  SDLC
    1.  IP addressing per table above.

        *NOTE: Must be routable to the vNetC*

3.  Controllers (within SDLC)
    1.  IP Addressing per table above.

        *NOTE: The diagram above shows that the controllers are bridged to NIC 2 of the SDLC. The IP MUST be on the same VLAN/subnet as the SDLC.*

4.  ESXi
    1.  Compute resources meeting Verity requirements based on the number of switches being managed. See Resource documentation for computing CPU and memory needs.
    2.  Virtual Switch
        1.  The vNetC and SDLC should be on the same virtual switch in ESXi or at minimum they must be routable.
        2.  Your system requires **promiscuous mode** will be set to enabled.

## Obtaining the vNetC and SDLC VM Images and Files

Obtain the following files from BeyondEdge:

| **Description**                  | **Filename Example**       | **File Type** | **Notes**                                                                                                                                                                                   |
|----------------------------------|----------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **vNetC VM Image**               | **vNetC-x_x_x_x.ova**      | VMWare OVA    | Resources including vCPU and memory should be adjusted based on iVN resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| **vNetC “core” Upgrade**         | **core-x_x_x_x- full.tar** | Tarball       | vNetC needs to be updated via UI SD-Admin immediately after configuration and boot                                                                                                         |
| **SDLC VM Image**                | SDLC-x_x_x_x.ova           | VMWare OVA    | Resources including vCPU and memory should be adjusted based on iVN resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| **SDLC Binary Firmware Upgrade** | sdlc-x_x_x_x.bin           | Binary        | SDLC should be upgraded via web page immediately after configuration and boot                                                                                                               |
| **License**                      | license.cms                | License file  | Is uploaded using UI (obtain from Beyond Edge Networks)                                                                                                                                    |


## Creating the Virtual Machines

The following instructions explain how to create virtual machines for both the vNetC and SDLC (once VMware is loaded into the desired server).

## Create the vNetC Virtual Machine

1.  Go to **Virtual Machines**. Click **Create/Register VM** ![](../media/vmware_create_register_highlight.png){:class="pop"} .

2.  In the window that appears select **Deploy a virtual machine from an OVF or OVA file**. Click Next.![](../media/b442ae0cc7b0d78f52d2898e394c6b54.jpeg){:class="pop"}

3.  Enter a name for the VM and upload the vNetC VM Image OVA file via the prompt that says **Click to Select file or drag/drop**. Click Next ![](../media/3916e04247d0d17a17201b89e10bac50.PNG){:class="pop"}.

4.  Select the desired data store options. Click **Next** ![](../media/fd0fd497a2295fae21345f0e4dcd5a08.jpeg){:class="pop"} . 

5.  Set the Deployment options – Network mappings to the correct Port Group.
6.  This Port Group must be set to **promiscuous mode**.
7.  Click **Next** ![](../media/e7ad33d3a69c0e6cd15423af2102ea4e.jpeg){:class="pop"} .



![](../media/96dbf8190a9a9431958e3867d3f7eff1.PNG)



8.  Click on Finish ![](../media/09df623860eef0c4263fe78995ac4303.PNG){:class="pop"}.



!!!Notice  
    Ignore "A required disk image was missing" message.

The VM creation process will start. When the process completes the progress bar in **Recent tasks** at the bottom of the screen will say **Completed Successfully.**

**![](../media/822cbfa3515c2824a164ee5af14f3e2f.PNG)**

**![](../media/bcc526fae6e7a47076c9e461539f8561.PNG)**

## Configure the vNetC from the Console.

This step requires you to configure the vNetC with an IP address and Fully Qualified Domain Name (FQDN). To do so, you need to open the VM console. Select your VM under the **Virtual Machine** column and click **Console**/**Open browser console**.

![](../media/692477910705d9f1eb08ddf358ab155d.PNG)

The VM console appears. The vNetc initialization may take several minutes. While waiting you can press **Enter** and wait for login prompt.

![](../media/dbcb931946cc6c80954c1957b45ecedf.jpeg)

1.  Login to the vNetC with username **root** and password **vnc1234**. Enter a new password if prompted. If not prompted for the password, you can continue to use the default password or change it with the **passwd** command.
2.  Run the administration application from the shell by typing **ns_admin** and pressing Enter ![](../media/00af5b91fc99fd941a2820875081b661.jpeg){:class="pop"}

1.  You are prompted to enter a web user interface admin account password. Document the password you choose as it will be required for UI authentication later in the process. It is very important that you remember the password! When done press Enter.
1.  In the Admin Menu, select **Network Configuration**. Press Enter ![](../media/50f08a925821190e6f54d3058f68167f.jpeg){class="pop"}

5.  Select **FQDN (Fully Qualified Domain Name).** Press Enter and set to the desired **Fully Qualified Domain Name.** If the field is prepopulated, it is required that you replace the default text with your own FQDN.
6.  Verify that WAN IP DHCP is disabled. If WAN IP DHCP is enabled, disable it using the menu or…
7.  Select **WAN Static IP Settings,** press enter.
    -   Enter: IPv4 Address and subnet in CIDR format (x.x.x.x/\#\#) where x.x.x.x is the IPv4 address and \#\# is the CIDR subnet mask prefix
    -   Enter: Default Route (Gateway)
    -   Enter: DNS Server 1
    -   Enter: DNS Server 2 (if required)
8.  Return to the network configuration menu.
9.  Save Settings

Follow the prompt and the VM will reboot with the new settings configured.

# Install the License and Upgrade to the Latest vNetC Core Software

Upgrade the vNetC Core software via the vNetC Web Administration.

1.  Use Chrome Web Browser to access the vNetC IP address that was just configured.
2.  At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**![](../media/sine_in_prompt.png){:class="pop"} .

3.  From the Admin web page, select the **Software Packages and Licensing** section by double clicking and zooming in
![](../media/software_packages_and_licensing_tile.png){:class="pop"} . 

4.  Select **License**![](../media/0a8e17ba3bbbe30be671dda200582728.png){:class="pop"}.

![](../media/deb23d66a3fc3a04aa64cbdcc7ca9cd2.PNG)

5.  When the window appears, record the information on the **Licensing tied to** line. Provide this information to BeyondEdge to obtain your license file

6.  After you obtain your license.cms file you are required to upload it to the application. Use the drag and drop palette to upload the file or browse for the file. The license file may also be embedded in a \<filename\>.tar file and this can also be directly imported, and the system will extract the license.cms file ![](../media/8f8b5a86c069537deee487a63f88f407.png){class="pop"} .

After you upload the file make sure a success message is presented ![](../media/9b3cba410b78f60acee4cab8458e5145.png){:class="pop"} .

After you upload the license, a tab titled Verity appears at the upper right of the screen (refresh the page if you do not see the tab). Click **Verity** and let the screen populate ![](../media/96bce08e2e33e8fbdfb9711a3a26ca1a.jpeg){:class="pop"}

After the **Verity** window has fully completed populating select the **Admin** tab. Select **Software Packages and Licensing** and click **vNetC Packages.**![](../media/vnetc_packages.png){:class="pop"} .

Using the **Browse Files** (or drag and drop) field, import the **vNetC Core Upgrade** file provided by BeyondEdge ![](../media/94609d9c3082e641c84666dc36310cbd.png){:class="pop"}

![](../media/28623c1b1e46685b5c960763bb328b7c.png)

When the process is complete you are presented with a success message ![](../media/8294513f9471453183dde5332a5e8d10.png){:class="pop"}.


Click the **Deploy** button ![](../media/buttons/6.2/deploy.png){:class="btn"}. When prompted to continue, click Yes ![](../media/2242c0169d4e29944e7cda29952c05a8.jpeg){:class="pop"}


The software updates.

![](../media/918c49596f254b6e4d22d58ee9577472.png)

You may see an error titled **Fatal Error WebSocket Error: Connection lost -2** appear, this is normal. The browser may temporarily say that the site cannot be reached. When the process is done, the landing page will render.

**Save Settings**

While in Admin, go to the Settings box.

1.  Add Management VLAN.
2.  Add Management address with mask.
3.  Verify Permissible IP Address Ranges on Managed Devices are assigned ![](../media/878c4fe54ff51ef4746adb2378e6dd80.PNG){:class="pop"}.

Use the VMWARE interface to **Power Off** the vNetC. Later, after you install the SDLC VM, you will restart (**Power on**) the vNetC ![](../media/vm_ware_power_off_on.png){:class="pop"} . 

# Create Optional NIC LAG

1.  Select “Networking”.
2.  Select “Virtual switches”.
3.  Select “Add standard virtual switch” ![](../media/009824b841b2e1f0d6506604b98c8984.PNG){:class="pop"}.

4.  Give the virtual switch a name then click on the ADD button.
5.  Edit settings on same.
6.  Add a second uplink.
7.  Configure remaining options as shown below. Pay particular attention to the Uplink Security, and NIC Teaming assignments ![](../media/cd1eb33baa46d0fca504154e400375ce.PNG){:class="pop"}.

8.  Verify both link’s Status indicate Active.
9.  Click on “SAVE” button.
10.  Select “Networking".
11.  Select Port Groups.
12.  Select “Add port group”.
13.  Port Group “SDLAN_MGMT_2000” is created with VLAN 2000 and Virtual switch LAN-2000

!!!Notice

    In the listed examples, SDLAN_MGMT_2000 is untagged and SDLAN_MGMT_TRUNK is tagged.




![](../media/022083a04bff286b764986c097d73c29.PNG)

14.  Enter name, VLAN and Virtual switch.
15.  Click on Add.
16.  Select “Add port group”. To create the 2nd Port Group, SDLAN_MGMT_TRUNK.
17.  Input name, VLAN and Virtual switch.
18.  Click on Add ![](../media/502fe6e78c34de236d9b628faffde5ff.PNG){:class="pop"}.

19.  Go back to the ESXi Host Client page. Select Virtual Machines.
20.  Select the VNetC FQDN (gatorland in this example).
21.  Select Actions.
22.  From the pull-down menu select Edit settings ![](../media/2b212856f09bbf7972640e18f4442e18.PNG){:class="pop"}.

23.  Click on the pull-down menu for Network Adaptor 3.
24.  Select “SDLAN_MGMT_TRUNK.
25.  Click on the check box to Connect. Also verify Network Adaptor 1 is configured as shown.
26.  Save.

## Create the SDLC Virtual Machine

1.  Go to **Virtual Machines**. Click **Create/Register VM.** ![](../media/vmware_create_register.png){:class="pop"}

2.  In the window that appears select **Deploy a virtual machine from an OVF or OVA file**. Click Next ![](../media/b442ae0cc7b0d78f52d2898e394c6b54.jpeg){:class="pop"}.



3.  Enter a name for the VM and upload the SDLC VM Image OVA file via the prompt that says **Click to Select file or drag/drop**. Click Next ![](../media/e25f811196082592efed2600b0f5be67.jpeg){:class="pop"}.

4.  Select the desired data store options. Click **Next** ![](../media/fd0fd497a2295fae21345f0e4dcd5a08.jpeg){:class="pop"} .

5.  Set the deployment options. Click **Next** ![](../media/e25f811196082592efed2600b0f5be67.jpeg){:class="pop"} .

6.  Review the settings and if they are correct, click **Finish** ![](../media/3fca8bcfd8e437bc3a2f222768d0874f.jpeg){:class="pop"} .

The VM creation process will start. When the process completes the progress bars at the bottom of the screen will say **Completed Successfully** ![](../media/493014afb45c1396d0263a207aaa89d9.jpeg){:class="pop"} .

## Configure the SDLC from the Console

The SDLC must be configured with a Static IP address and the vNetC FQDN.

Select the SDLC from the VMWARE ESXi interface and click the **Console** tab. Select **Open browser console** ![](../media/vm_ware_open_browser_console.png){:class="pop"} .

The console appears ![](../media/fcfa7d033b791505b95bf5b1e0932952.jpeg){:class="pop"} .

During the following process DHCP errors may appear. They should be ignored.

-   Press **Enter** to get the login prompt, enter username: **admin** and password: **admin.**
-   As you access the internal command line interface (CLI) press **Enter** to see a list of options.
-   Select **Admin** and press **Enter.**
-   Type **Wizard**. Press Enter
-   In response to the prompt **“do you want to modify hostname**”, select **Y.**
-   You are prompted for the hostname. Type **SDLC** (uppercase) and press **Enter.**
-   You are prompted to change **hostname**. Select **Y.**
-   **Advertise the Site Management VLAN ? [y/n]** 2000 **Y.**
-   **Initial Site Management VLAN [1-4093] [Enter for default (1)] (q to quit): 2000**
-   You are prompted to **Use DHCP for management uplink configuration,** select **N.**
-   You are prompted to enter the **MGMT IP**. Enter management IP and press **Enter**. If vNetC and SDLC (GAIA, ACS and DHCP) are on different subnets, it is recommended to have three consecutive static IP addresses on the same subnet for GAIA, ACS and DHCP. However, if vNetC is on the same subnet as GAIA, ACS and DHCP, it is recommended to use four sequential IP addresses.
-   You are prompted to enter the **Default Gateway in CIDR format**. Enter the default gateway and press **Enter** or select **Y** to accept.
-   You are prompted to enter the suggested **ACS IP**, select **Y.** Press **Enter.**
-   You are prompted to enter the suggested **GAIA IP**, select **Y.** Press **Enter.**
-   You are prompted to enter the **DNS server**. Enter the DNS server and press **Enter**.
-   You are prompted to enter **Comma Separated NTP Server(s**). Enter **vNetC’s IP address** and press **Enter.**
-   You are Prompted to enter the **vNetC FQDN** or **IP**. Submit the information and Press **Enter**. (Use IP only)
-   You are Prompted to **enter ACS connection path** as **URL**. Select **N.**
-   You are Prompted to enter the **ACS FQDN** or **IP**. Press **Enter**.
-   You are Prompted to enter **ACS connection protocol**. Choose **http or https.** Press **Enter**
-   You are Prompted to enter **ACS connection port number**. Press **Enter.**
-   You are prompted to enter **VCF connection path URL**. Select **N.**
-   You are prompted to enter **VCF FQDN or IP**. Press **Enter. (Use IP only)**
-   You are prompted to enable **DHCP on management VLAN**. Select **Y**.
-   Enter DHCP lowest range IP
-   Enter DHCP high range IP.
-   Review the information. You are prompted to save the configuration. Select **Y**.
-   The Wizard results should look like the picture below.
-   Reboot is required for any changes to take effect. In the console, type **reboot** and press **Enter** ![](../media/2b597e1dc14aba72f4a1eed7a34febd2.PNG){:class="pop"} .

1.  Power down the SDLC
2.  Go back to the ESXi Host Client page.
3.  Select the VNetC FQDN (SDLC in this example).
4.  Select Edit ![](../media/daacabeae271c5a953d8127812cace20.PNG){:class="pop"}

5.  Click on the pull-down menu for Network Adaptor 2
6.  Select “SDLAN_MGMT_2000
7.  Click on the check box to Connect.
8.  Click on the pull-down menu for Network Adaptor 3
9.  Select “SDLAN_MGMT_TRUNK
10.  Click on the check box to Connect.
11.  Save

**Power On the vNetC.**

In the VMware ESXi interface power on the vNetC. This takes a few minutes.

**Power On the SDLC.**

In the VMware ESXi interface power on the vNetC. This takes a few minutes.

Go to the Verity tab.

![](../media/794dc77d7cd4004039c98a46bb62dc31.png)

Wait until the process is finished. The application landing page resembles the image below when all processes have been completed. 

![](../media/vnf_system_apps_green.png)

## Update SDLC

Double click the **Admin** tab, double click **Software Packages and Licensing**. Double click **Firmware Packages**. Select and place the SDLC Binary Firmware Upgrade firmware file on the **Drag & Drop** area or use the **Browse Files** button to select the file.

If upgrades are disabled, enable for update.

![](../media/478d40d88c5aa513aad9b2adedcd16fe.png)

When uploaded, you are prompted with a green success message.

![](../media/962410031cfb6ddb8cb7e36f99957359.jpeg)

Deploy the firmware by clicking the **Deploy** button ![](../media/buttons/6.2/deploy.png){:class="btn"} ![](../media/a74aa3f6497dcf606d55417463f3654d.jpeg){:class="pop"} . 


A validation message appears. Click **Yes** ![](../media/3ab83b02e72a59c324f2b377e3b3ac2f.png){:class="pop"} .


![](../media/79f24bd99c7a9930b37521d706f457d8.png)

Click the **Verity** tab ![](../media/850a667bb30b5e49fcd29dddb87393c8.png){:class="pop"}

Double click the **VNFs** window ![](../media/vnf_highlight.png){:class="pop"}

Double click the **SDLC** section ![](../media/sdlcs_tile_highlight.png){:class="pop"}

Double click the box with the title of **SW Version** ![](../media/sdlc_software_version_tile.png){:class="pop"}

Set the **Target Package** field to the Firmware version ![](../media/e855591b313c3b57306c4974e1ce4432.png){:class="pop"}

Click the **Check** button ![](../media/e7c7b399d960a2c5e07265e06d384e57.png){:class="btn"}

Go to **Endpoint Sets** ![](../media/endpoint_sets_highlight.png){:class="pop"}

Uncheck the box titled **Disable Upgrades** ![](../media/disable_all_upgrades.png){:class="pop"}

![](../media/44448dab4ec6047cf589baf1585ea5e8.png)

![](../media/8cf84f1ef9cdef7276b9e18eb9dfdf50.jpeg)

In the window that appears titled **GuiA Disconnected**, click the icon to refresh.

![](../media/f0815d366b871acfca28690ea7f2629a.jpeg)

Let the process complete.

![](../media/8518546915747e1f255fc01151d0a326.png)

When the window appears the initial state of **System Applications** are offline. This is expressed by their red LED icons.

When the **System Applications** come online their LED icons render green. This may take up to 5 minutes.

![](../media/ee3a98987c1ec9abea4299f17e43a9fc.png)

![](../media/47d0b2e268ea5ed6cceebd456f3b65c1.png)

The installation and updates of Verity for Enterprise software components is now complete.

Disable (check) All Upgrades Disabled
