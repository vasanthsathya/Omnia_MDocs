---
hide:
- toc
---

## Create the Monitoring Virtual Machine

!!! warning "vNetC and SDLC must be fully installed and configured"

    The vNetC and SDLC Virtual Machines must be installed and fully configured before installing the Monitoring VM. 
    Also, DHCP must be available for initial setup and configuration. This procedure must follow after Verity is fully 
    online and operational with DHCP available for the initial VM Network setup.

1. Go to **Virtual Machines**. 
1. Click **Create/Register VM**. ![](media/monitoring_ova_create.png){: class="pop"}
1.  In the window that appears select **Deploy a virtual machine from an OVF or OVA file**. 
1. Click Next. ![](media/monitoring_ova_deploy.png){: class="pop"}
1. Enter a name for the VM and upload the Monitoring VM Image OVA file via the prompt that says **Click to Select file or drag/drop**.
1. Click Next. ![](media/monitoring_ova_image_upload.png){: class="pop"}
1. Select the desired data store options. Click **Next**. ![](media/monitoring_ova_datastore.png){: class="pop"}
1. Set the Deployment options – Network mappings to the correct Port Group.
1. This Port Group must be set to **promiscuous mode**. ![](media/96dbf8190a9a9431958e3867d3f7eff1.PNG){: class="pop"}
1. Click **Next**. ![](media/monitoring_network.png){: class="pop"}
1. Review the settings and if they are correct, click **Finish**. ![](media/monitoring_confirm.png){: class="pop"}
1. The VM creation process will start. When the process completes the progress bar in **Recent tasks** at the bottom of the screen will say **Completed Successfully**. ![](media/monitoring_vm_complete.png){: class="pop"}

---

### Configure Monitoring from the Console
This step requires you to configure Monitoring with an IP address, default gateway, and DNS servers. Then the script will ask for the Fully Qualified Domain Name (FQDN) or IP address of the VNetC so it knows how to connect the monitoring dashboard. To do so, you need to open the VM console. 

1. Select your VM under the **Virtual Machine** column and click **Console**/**Open browser console**. ![](media/monitoring_console.png){: class="pop"}
1. The VM console appears. The Monitoring initialization may take several minutes. While waiting you can press **Enter** and wait for login prompt. ![](media/monitoring_login.png){: class="pop"}
1. Login to Monitoring with username **verity** and password **vnc1234**. 
1. Enter a new password if prompted. If not prompted for the password, you can continue to use the default password or change it with the **passwd** command. 
1. Run the setup application from the shell by typing **sudo ./setup.sh** and pressing Enter. ![](media/monitoring_setup_script.png){: class="pop"}
1. Enter the following information: ![](media/monitoring_networking_script.png){: class="pop"}
    1. IPv4 Address and subnet in CIDR format (x.x.x.x/#)
    1. Default Route (Gateway)
    1. DNS Servers seperated by a comma
1. Enter the FQDN or IP Address of the vNetC. ![](media/monitoring_vnetc_ip.png){: class="pop"}

!!! warning "Certificates are Required"

    Make sure that the SSL certificates for Verity's web server are installed and working correctly. Monitoring connects to the vNetC with 'https' and if the vNetC returns a certificate error, Monitoring will fail to connect.

8. Press **Enter**.
1. Setup of monitoring is complete. The display will show the current settings and provide a note about if you need to make changes in the future, re-run this script. ![](media/monitoring_vnetc_complete.png){: class="pop"}
1. Type **exit** to logout of the console and close the console window
1. Use Chrome Web Browser to access the vNetC IP address that was just configured.
1. At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**. ![](media/aab2e9cc425873f4e6fbd016f8f60f47.png){: class="pop"}
1. There will be a new dashboard icon in the top left corner showing the Monitoring Dashboard. Also, the Monitoring Dashboard will be the new startup screen. ![](media/monitoring_dashboard.png){: class="pop"}

---

### Upgrade to the Latest Monitoring Software

1. Upgrade the Monitoring software via the vNetC Web Administration.

1. Use Chrome Web Browser to access the vNetC IP address that was just configured.
1. At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**. ![](media/aab2e9cc425873f4e6fbd016f8f60f47.png){: class="pop"}
1. From the Admin web page, select the **Software Packages and Licensing** section by double clicking and zooming in. ![](media/software_packages_and_licensing_tile.png){: class="pop"}
1. Click **Application Packages**. ![](media/application_packages.png){: class="pop"}
1. Using the **Browse Files** (or drag and drop) field, import the **Monitoring Upgrade** file provided by BE Networks. ![](media/monitoring_update_application_package.png){: class="pop"} ![](media/monitoring_update_application_upload.png){: class="pop"}
1. When the process is complete you are presented with a success message. ![](media/monitoring_update_application_upload_success.png){: class="pop"}
![](media/monitoring_update_application_deploy.png){: class="pop"}
1. Click the **Deploy** button. 
1. When prompted to continue, click Yes. The software updates. ![](media/monitoring_update_deploy.png){: class="pop"}

