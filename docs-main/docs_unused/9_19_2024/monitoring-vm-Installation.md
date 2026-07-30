# NOTE: For Luke - Delete this message. This is a more recent version of the document by the name "monitoring_vm_installation.md

# Verity VM Installation (VMware 7.0.3)

## Introduction

The Verity management and orchestration system is comprised of three functional components, all of which are instantiated as Virtual Machines (VMs). This document describes the installation and configuration of these VMs within a VMWare ESXi server.

## Virtual Machine Overview

Verity’s three VM functional components:

| Virtual Machine                        | Function                                                                                                                                                                                                                                                                                                                                                 |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Virtual Network Commander (vNetC)      | Orchestration logic, UI hosting, northbound RESTful API, and databases.                                                                                                                                                                                                                                                                                 |
| Software Defined LAN Controller (SDLC) | The SDLC VM is comprised of a series of containers that map one-to-one to the managed switch devices. Network discovery, device provisioning, and network assurance. The SDLC serves as the abstraction layer between the managed switch and the vNetC by translating the native management protocols into the vNetC’s NETCONF interface and Yang model. |
| Monitoring                             | The Monitoring VM is comprised of various containers that collect, process and display the network device details that are managed by Verity.                                                                                                                                                                                                            |

## Virtual Machine Topology

Below is the basic VM and hardware topology for reference: ![](media/bb4e05c67eb9715f4c3dd9ccd1d5006d.png)

**Recommended Network Management Architecture**

Each system requires a management subnet that can support 5 system IP addresses as well as 3 IP addresses per managed switch. The breakdown is as follows:

| IP address Allocations for Management | Component                                   | Allocation                   |
|---------------------------------------|---------------------------------------------|------------------------------|
| Verity System components              | vNETC LAN side, SDLC, ACS, GuiA, Monitoring | 5 Static Addresses           |
| Managed Switches                      | Verity Switch Controller                    | 1 Dynamic Address per switch |
| Managed Switches                      | Switch in ZTP Process                       | 1 Dynamic Address per switch |
| Managed Switches                      | Switch post ZTP Process                     | 1 Static Address per switch  |

The orchestration platform (vNETC) is configured on the customer’s network with one static IP address to be accessed by users.

The following diagram shows the recommended management network architecture. Variations are possible based on individual customer’s network needs. A second diagram follows with a version showing only one connection to the vNETC.

![](media/6263b9748880a3fe027085a8bf3a903d.png)

## Prerequisites

1.  **vNetC**
    1.  Resolvable, fully qualified domain name
    2.  Static IP address, gateway, DNS servers
    3.  Valid Verity license
2.  **SDLC**
    1.  IP addressing per table above. *NOTE: Must be routable to the vNetC*
3.  **Controllers (within SDLC)**
    1.  IP Addressing per table above. *NOTE: The diagram above shows that the controllers are bridged to NIC 2 of the SDLC. The IP MUST be on the same VLAN/subnet as the SDLC.*
4.  **Monitoring**
    1.  IP addressing per table above. *NOTE: Must be routable to the vNetC*
5.  **ESXi**
    1.  Compute resources meeting Verity requirements based on the number of switches being managed. See Resource documentation for computing CPU and memory needs.
    2.  Virtual Switch
        1.  The vNetC and SDLC should be on the same virtual switch in ESXi or at minimum they must be routable.
        2.  Your system requires **promiscuous mode** to be set to enabled.
6.  **Routable or switched network between Verity components and managed switching devices**
    1.  If using a router or firewall between Verity and the switches, the following ports must be allowed to pass.
        1.  Port 8080 for gNMI
        2.  Port 80 - HTTP
        3.  Port 443 - HTTPS
        4.  Port 22 - SSH

# Obtaining the vNetC, SDLC and Monitoring VM Images and Files

Obtain the following files from BE Networks:

| Description                  | Filename Example            | File Type    | Notes                                                                                                                                                                                       |
|------------------------------|-----------------------------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| vNetC VM Image               | **vNetC-x_x_x_x.ova**       | VMware OVA   | Resources including vCPU and memory should be adjusted based on iVN resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| vNetC “core” Upgrade         | **core-x_x_x_x- full.tar**  | tarball      | vNetC needs to be updated via UI SD-Admin immediately after configuration and boot                                                                                                         |
| SDLC VM Image                | SDLC-x_x_x_x.ova            | VMware OVA   | Resources including vCPU and memory should be adjusted based on iVN resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| SDLC Binary Firmware Upgrade | firmware-x_x_x_x.tar        | tarball      | SDLC should be upgraded via web page immediately after configuration and boot                                                                                                               |
| Monitoring VM Image          | verity-monitoring_x.x.x.ova | VMware OVA   | Resources including vCPU and memory should be adjusted based on iVN resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| Monitoring Software Upgrade  | verity-monitoring_x.x.x.tar | tarball      | Monitoring needs to be updated via UI SD-Admin immediatly after configuration and boot                                                                                                     |
| License                      | license.cms                 | License file | Is uploaded using UI                                                                                                                                                                       |

# Create the Monitoring Virtual Machine

**Prerequisites:**

1.  Valid SSL Certificates for vNetC are installed
2.  DHCP server is configured for the subnet that vNetC is using
    1.  Monitoring uses DHCP initially to come online. Users will statically assign an IP address during configuration of the VM

**Procedure:**


1.  Go to **Virtual Machines**.
2.  Click **Create/Register VM**. ![](media/e801db929a33cdc36fb19c8d514da826.png){: class="pop"}
3.  In the window that appears select **Deploy a virtual machine from an OVF or OVA file**.
4.  Click Next. ![](media/62d249fe65b817e959c663436478dca2.png){: class="pop"}
5.  Enter a name for the VM and upload the Monitoring VM Image OVA file via the prompt that says **Click to Select file or drag/drop**.
6.  Click Next. ![](media/7d705ddd65e635d0f6b9d60b379b9a48.png){: class="pop"}
7.  Select the desired data store options. Click **Next**. ![](media/3d62e00ee944f39284cb84b9bdba6b46.png){: class="pop"}
8.  Set the Deployment options – Network mappings to the correct Port Group.
9.  This Port Group must be set to **promiscuous mode**. ![](media/96dbf8190a9a9431958e3867d3f7eff1.PNG){: class="pop"}
10. Click **Next**. ![](media/0c64e55455ea1d10568e0c2375028418.png){: class="pop"}
11. Review the settings and if they are correct, click **Finish**. ![](media/625d98d3467fbc50408a78a56591bfbd.png){: class="pop"}
12. The VM creation process will start. When the process completes the progress bar in **Recent tasks** at the bottom of the screen will say **Completed Successfully**. ![](media/786193113bbdbd3c15eeccaf9477a366.png){: class="pop"}

# Configure Monitoring from the Console

This step requires you to configure Monitoring with an IP address, default gateway, and DNS servers. Then the script will ask for the Fully Qualified Domain Name (FQDN) of the VNetC so it knows how to connect the monitoring dashboard. To do so, you need to open the VM console.

1.  Select your VM under the **Virtual Machine** column and click **Console**/**Open browser console**. ![](media/7da934f751071b413f49bc966dabecdd.png){: class="pop"}
2.  The VM console appears. The Monitoring initialization may take several minutes. While waiting you can press **Enter** and wait for login prompt. ![](media/0fb62280a0a4662030b21e7ba6ccac42.png){: class="pop"}
3.  Login to Monitoring with username **verity** and password **vnc1234**.
4.  Enter a new password if prompted. If not prompted for the password, you can continue to use the default password or change it with the **passwd** command.
5.  Run the setup application from the shell by typing **sudo ./setup.sh** and pressing Enter. ![](media/78387507ff9feb68e35c7b66ded8699a.png){: class="pop"}
6.  Enter the following information: ![](media/c800c57b7ce83e2d7c3dd9e11dc6e6a5.png){: class="pop"}
    1.  IPv4 Address and subnet in CIDR format (x.x.x.x/\#)
    2.  Default Route (Gateway)
    3.  DNS Servers seperated by a comma
7.  Enter the FQDN of vNetC. ![](media/0624356aa8ed9c8be189e82d62af1093.png){: class="pop"}

**Certificates are Required**

Make sure that the SSL certificates for Verity's web server are installed and working correctly. Monitoring connects to the vNetC with 'https' and if the vNetC returns a certificate error, Monitoring will fail to connect.

1.  Press **Enter**.
2.  Setup of monitoring is complete. The display will show the current settings and provide a note about if you need to make changes in the future, re-run this script. ![](media/1d2df8998a60dc5faf754cca7cd9e4d2.png){: class="pop"}
3.  Type **sudo reboot** to reboot the VM for all the settings to take effect. After the reboot, it takes about 3 minutes for the Docker containers to start up and to announce itself to the vNetC.
4.  When the Monitoring VM connects to the vNetC, in Verity, a Growl with the MAC Address of the Monitoring VM will appear. Once this does, use the refresh button on Chrome. ![A blue rectangle with white text Description automatically generated](media/3a927482efb0677fd1930cd56ed7f543.png){: class="pop"}
5.  There will be a new dashboard icon in the top left corner showing the Monitoring Dashboard. Also, the Monitoring Dashboard will be the new startup screen. ![](media/b51f152864043ab3a79d5959808c405e.png){: class="pop"}

# KVM Installation

## Introduction

The Verity management and orchestration system is comprised of three functional components, all of which are instantiated as Virtual Machines (VMs). This document describes the installation and configuration of these VMs within a KVM environment.

## Virtual Machine Overview

Verity’s three VM functional components are:

1.  Virtual Network Commander (vNetC) – Functions include the orchestration logic, UI hosting, northbound RESTful API, and databases.
2.  Software Defined LAN Controller (SDLC) – The SDLC VM is comprised of a series of containers that map one-to-one to the managed switch devices. Functions include network discovery, device provisioning, and network assurance. The SDLC serves as the abstraction layer between the managed switch and the vNetC by translating the native management protocols into the vNetC’s NETCONF interface and Yang model.
3.  Monitoring - The Monitoring VM is comprised of a series of containers that collect, process and display the network device details that are managed by Verity.

## Topology Overview

Below is the basic VM and hardware topology for reference.

## Recommended Network Management Architecture

Each system requires a management subnet that can support 5 system IP addresses as well as 3 IP addresses per managed switch. The breakdown is as follows:

| IP address Allocations for Management Network | Component                                   | Allocation                   |
|-----------------------------------------------|---------------------------------------------|------------------------------|
| Verity System components                      | vNETC LAN side, SDLC, ACS, GuiA, Monitoring | 5 Static Addresses           |
| Managed Switches                              | Verity Switch Controller                    | 1 Dynamic Address per switch |
| Managed Switches                              | Switch in ZTP Process                       | 1 Dynamic Address per switch |
| Managed Switches                              | Switch Post ZTP Process                     | 1 Static Address per switch  |

The orchestration platform (vNETC) is configured on the customer’s network with one static IP address to be accessed by users.

The following diagram shows the recommended management network architecture. Variations are possible based on individual customer’s network needs. A second diagram follows with a version showing only one connection to the vNETC.

![](media/fcd245a468fc4a2e2dd1078d8f34b21e.png)

![](media/bb4e05c67eb9715f4c3dd9ccd1d5006d.png)

## Prerequisites

1.  **vNetC**
    1.  Resolvable, fully qualified domain name
    2.  Static IP address, gateway, DNS servers
    3.  Valid Verity license
2.  **SDLC**
    1.  IP addressing per table above

*NOTE: Must be routable to the vNetC*

1.  **Devcice Controllers (within SDLC)**
    1.  IP Addressing per table above.

*NOTE: The diagram above shows that the controllers are bridged to NIC 2 of the SDLC. The IP MUST be on the same VLAN/subnet as the SDLC.*

1.  **Monitoring**
    1.  IP Addressing per table above.

*NOTE: Must be routable to the vNetC*

1.  **KVM**
    1.  Compute resources meeting Verity requirements based on the number of switches being managed. See Resource documentation for computing CPU and memory needs.
    2.  Virtual Switch
        1.  The vNetC, SDLC and Monitoring should be on the same bridge or at minimum they must be routable.
2.  **Routable or switched network between Verity components and managed switching devices**
    1.  If using a router or firewall between Verity and the switches, the following ports must be allowed to pass.
        1.  Port 8080 for gNMI
        2.  Port 80 - HTTP
        3.  Port 443 - HTTPS
        4.  Port 22 - SSH

Obtaining the vNetC and SDLC VM Images and Files[🔗](http://127.0.0.1:8000/BE-Network/docs/docs/kvm-install/#obtaining-the-vnetc-and-sdlc-vm-images-and-files)

Obtain the following files from BeyondEdge:

| Description                | Filename Example                       | File Type    | Notes                                                                                                                                                                                   |
|----------------------------|----------------------------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| vNetC VM Image             | vNetC-x_x_x_x.qcow2                    | KVM qcow     | Resources including vCPU and memory should be adjusted based on resource needs documentation. Networking will need to be altered to the correct bridge names used in the server         |
| vNetC “core” Upgrade       | core-x_x_x_x- full.tar                 | Tarball      | vNetC needs to be updated via UI SD-Admin immediately after configuration and boot                                                                                                     |
| SDLC VM Image              | SDLC-x_x_x_x.qcow2                     | KVM qcow     | Resources including vCPU and memory should be adjusted based on resource needs documentation. Networking will need to be altered to the correct virtual switch names used in the server |
| Firmware Upgrade Package   | firmware-x_x_x_x.tar                   | Tarball      | SDLC should be upgraded via system upgrader immediately after configuration and boot                                                                                                    |
| Monitoring VM Image        | verity-monitoring_x.x.x.qcow2          | KVM qcow     | Resources including vCPU and memory should be adjusted based on resource needs documentation. Networking will need to be altered to the correct bridge names used in the server         |
| Monitoring Upgrade Package | verity-monitoring_x.x.x.tar            | Tarball      | Monitoring should be updated via UI AS-Admin immediatly after configuration and boot                                                                                                   |
| License                    | license.cms or sitexxxxx.tar           | License file | Is uploaded using UI                                                                                                                                                                   |
| XML Parameters             | vnetc.xml, SDLC.xml and monitoring.xml | xml          | Default files are provided and are edited during the installation process                                                                                                               |

# Upgrade to the Latest Monitoring Software

1.  Upgrade the Monitoring software via the vNetC Web Administration.
2.  Use Chrome Web Browser to access the vNetC IP address that was just configured.
3.  At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**. ![](media/84b32ecf2d4c0f3cafa29d9506b6715b.png){: class="pop"}
4.  From the Admin web page, select the **Software Packages and Licensing** section by double clicking and zooming in. ![](media/f78139b93bb359956bcb9cef14c87aa0.png){: class="pop"}
5.  Click **Application Packages**. ![](media/c0cb1f0331c02823dea4718f1e8931ae.png){: class="pop"}
6.  Using the **Browse Files** (or drag and drop) field, import the **Monitoring Upgrade** file provided by BE Networks. ![](media/47469124383e394b94f7c900db8c525c.png){: class="pop"} ![](media/2bff0367520d06b1b85ede32326bc1b0.png){: class="pop"}
7.  When the process is complete you are presented with a success message. ![](media/9527d2b99eb7bf328d381688383d8bf1.png) ![](media/e96f006d3b414724f8b4a614e33b2927.png){: class="pop"}
8.  Click the **Deploy** button.
9.  When prompted to continue, click Yes. The software updates. ![](media/df679ed723ae86020b8462db0de5cb83.png){: class="pop"}

# Configure Monitoring from the Console

Monitoring must be configured with a Static IP address and the vNetC FQDN.

**virsh start monitoring**

(Domain 'monitoring' started)

**virsh console monitoring**

The VM console appears. The Monitoring initialization may take several minutes. While waiting you can press **Enter** and wait for login prompt. ![](media/46a48dadb3a9e26771565a43778c4852.png){: class="pop"}

1.  Login to Monitoring with username **verity** and password **vnc1234**.
2.  Enter a new password if prompted. If not prompted for the password, you can continue to use the default password or change it with the **passwd** command.
3.  Run the setup application from the shell by typing **sudo ./setup.sh** and pressing Enter. ![](media/8cdf9c21f5a9479eb54fa4cf0c0ae630.png){: class="pop"}
4.  Enter the following information: ![](media/c6720850a7725da8a38f2686e52a8269.png){: class="pop"}
    1.  IPv4 Address and subnet in CIDR format (x.x.x.x/\#)
    2.  Default Route (Gateway)
    3.  DNS Servers seperated by a comma
5.  Enter the FQDN or IP Address of the vNetC. ![](media/0624356aa8ed9c8be189e82d62af1093.png){: class="pop"}

**Certificates are Required**

Make sure that the SSL certificates for Verity's web server are installed and working correctly. Monitoring connects to the vNetC with 'https' and if the vNetC returns a certificate error, Monitoring will fail to connect.

1.  Press **Enter**.
2.  Setup of monitoring is complete. The display will show the current settings and provide a note about if you need to make changes in the future, re-run this script. ![](media/1d2df8998a60dc5faf754cca7cd9e4d2.png){: class="pop"}
3.  Type **sudo reboot** to reboot the VM for all the settings to take effect. After the reboot, it takes about 3 minutes for the Docker containers to start up and to announce itself to the vNetC.
4.  When the Monitoring VM connects to the vNetC, in Verity, a Growl with the MAC Address of the Monitoring VM will appear. Once this does, use the refresh button on Chrome. ![A blue rectangle with white text Description automatically generated](media/3a927482efb0677fd1930cd56ed7f543.png){: class="pop"}
5.  There will be a new dashboard icon in the top left corner showing the Monitoring Dashboard. Also, the Monitoring Dashboard will be the new startup screen. ![](media/b51f152864043ab3a79d5959808c405e.png){: class="pop"}

# Upgrade to the Latest Monitoring Software

1.  Upgrade the Monitoring software via the vNetC Web Administration.
2.  Use Chrome Web Browser to access the vNetC IP address that was just configured.
3.  At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**. ![](media/84b32ecf2d4c0f3cafa29d9506b6715b.png){: class="pop"}
4.  From the Admin web page, select the **Software Packages and Licensing** section by double clicking and zooming in. ![](media/f78139b93bb359956bcb9cef14c87aa0.png){: class="pop"}
5.  Click **Application Packages**. ![](media/c0cb1f0331c02823dea4718f1e8931ae.png){: class="pop"}
6.  Using the **Browse Files** (or drag and drop) field, import the **Monitoring Upgrade** file provided by BE Networks. ![](media/47469124383e394b94f7c900db8c525c.png){: class="pop"} ![](media/2bff0367520d06b1b85ede32326bc1b0.png){: class="pop"}
7.  When the process is complete you are presented with a success message. ![](media/9527d2b99eb7bf328d381688383d8bf1.png) ![](media/e96f006d3b414724f8b4a614e33b2927.png){: class="pop"}
8.  Click the **Deploy** button.
9.  When prompted to continue, click Yes. The software updates. ![](media/df679ed723ae86020b8462db0de5cb83.png){: class="pop"}

The installation and updates of Verity for Cloud software components is now complete.
