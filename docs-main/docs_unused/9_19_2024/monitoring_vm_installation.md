# Create the Monitoring Virtual Machine

**Prerequisites:**

1.  Valid SSL Certificates for vNetC are installed
2.  DHCP server is configured for the subnet that vNetC is using
    1.  Monitoring uses DHCP initially to come online. Users will statically assign an IP address during configuration of the VM

**Procedure:**

1.  Go to **Virtual Machines**.
2.  Click **Create/Register VM**.

    ![](media/vm_create_register_vm.png)

3.  In the window that appears select **Deploy a virtual machine from an OVF or OVA file**.
4.  Click Next.

    ![](media/62d249fe65b817e959c663436478dca2.png)

5.  Enter a name for the VM and upload the Monitoring VM Image OVA file via the prompt that says **Click to Select file or drag/drop**.
6.  Click Next.

    ![](media/7d705ddd65e635d0f6b9d60b379b9a48.png)

7.  Select the desired data store options. Click **Next**.

    ![](media/3d62e00ee944f39284cb84b9bdba6b46.png)

8.  Set the Deployment options – Network mappings to the correct Port Group.
9.  This Port Group must be set to **promiscuous mode**.

    ![](media/96dbf8190a9a9431958e3867d3f7eff1.PNG)

10. Click **Next**.

    ![](media/0c64e55455ea1d10568e0c2375028418.png)

11. Review the settings and if they are correct, click **Finish**.

    ![](media/625d98d3467fbc50408a78a56591bfbd.png)

12. The VM creation process will start. When the process completes the progress bar in **Recent tasks** at the bottom of the screen will say **Completed Successfully**.

    ![](media/786193113bbdbd3c15eeccaf9477a366.png)

# Configure Monitoring from the Console

This step requires you to configure Monitoring with an IP address, default gateway, and DNS servers. Then the script will ask for the Fully Qualified Domain Name (FQDN) of the VNetC so it knows how to connect the monitoring dashboard. To do so, you need to open the VM console.

1.  Select your VM under the **Virtual Machine** column and click **Console**/**Open browser console**.

    ![](media/7da934f751071b413f49bc966dabecdd.png)

2.  The VM console appears. The Monitoring initialization may take several minutes. While waiting you can press **Enter** and wait for login prompt.

    ![](media/0fb62280a0a4662030b21e7ba6ccac42.png)

3.  Login to Monitoring with username **verity** and password **vnc1234**.
4.  Enter a new password if prompted. If not prompted for the password, you can continue to use the default password or change it with the **passwd** command.
5.  Run the setup application from the shell by typing **sudo ./setup.sh** and pressing Enter.

    ![](media/78387507ff9feb68e35c7b66ded8699a.png)

6.  Enter the following information:

    ![](media/c800c57b7ce83e2d7c3dd9e11dc6e6a5.png)

    1.  IPv4 Address and subnet in CIDR format (x.x.x.x/\#)
    2.  Default Route (Gateway)
    3.  DNS Servers seperated by a comma
7.  Enter the FQDN of vNetC.

    ![](media/0624356aa8ed9c8be189e82d62af1093.png)

**Certificates are Required**

Make sure that the SSL certificates for Verity's web server are installed and working correctly. Monitoring connects to the vNetC with 'https' and if the vNetC returns a certificate error, Monitoring will fail to connect.

1.  Press **Enter**.
2.  Setup of monitoring is complete. The display will show the current settings and provide a note about if you need to make changes in the future, re-run this script.

    ![](media/1d2df8998a60dc5faf754cca7cd9e4d2.png)

3.  Type **sudo reboot** to reboot the VM for all the settings to take effect. After the reboot, it takes about 3 minutes for the Docker containers to start up and to announce itself to the vNetC.
4.  When the Monitoring VM connects to the vNetC, in Verity, a Growl with the MAC Address of the Monitoring VM will appear. Once this does, use the refresh button on Chrome. ![A blue rectangle with white text Description automatically generated](media/3a927482efb0677fd1930cd56ed7f543.png)
5.  There will be a new dashboard icon in the top left corner showing the Monitoring Dashboard. Also, the Monitoring Dashboard will be the new startup screen.

    ![](media/b51f152864043ab3a79d5959808c405e.png)

# Upgrade to the Latest Monitoring Software

1.  Upgrade the Monitoring software via the vNetC Web Administration.
2.  Use Chrome Web Browser to access the vNetC IP address that was just configured.
3.  At the login prompt enter username **admin** and the administration password configured in the menu during installation. These are the credentials you entered in step 3 of **Configure the vNetC from the Console**.

    ![](media/84b32ecf2d4c0f3cafa29d9506b6715b.png)

4.  From the Admin web page, select the **Software Packages and Licensing** section by double clicking and zooming in.

    ![](media/f78139b93bb359956bcb9cef14c87aa0.png)

5.  Click **Application Packages**.

    ![](media/application_package_tile.png)

6.  Using the **Browse Files** (or drag and drop) field, import the **Monitoring Upgrade** file provided by BE Networks.

    ![](media/47469124383e394b94f7c900db8c525c.png) ![](media/2bff0367520d06b1b85ede32326bc1b0.png)

7.  When the process is complete you are presented with a success message.

    ![](media/9527d2b99eb7bf328d381688383d8bf1.png) ![](media/e96f006d3b414724f8b4a614e33b2927.png)

8.  Click the **Deploy** button.
9.  When prompted to continue, click Yes. The software updates.

    ![](media/df679ed723ae86020b8462db0de5cb83.png)

**NOTE:** It take about 5 minutes for the tarball to be uploaded to the Monitoring VM, and the changes to be applied and the new containers started up. If you SSH into the Monitoring VM, and go to the /be_install directory, you will see the tarball uploaded. If you run sudo docker ps you will see the uptime of the containers to be less than 5 minutes online letting you know that everything is updated. We are working on adding a panel to Monitoring Dashboard that will show the latest installed Version.

# Monitoring VM Troubleshooting
This list of questions is here to help Verity customers and partners diagnose and resolve Verity deployment problems. Steps are numbered to ensure that the most basic and common issues are addressed first. Follow the steps in sequence, as their order is important.

## Verify the Verity Monitoring VM is Running and Configured Correctly
1. Is the dashboard icon available on the global navigation bar?  

    ![](media/dashboard_icon_diagram.png)


    - **No**: 
        This may be a sign that the initial setup steps were not completed correctly.
        1. Rerun the setup steps [**Configure Monitoring VM from the Console**](../monitoring-kvm-install/#configure-monitoring-from-the-console).
        1. Restart the VM to ensure all configuration changes take effect.
    - **Yes**:
        This indicates that the Monitoring VM is running and configured correctly.


1. Is the **Dashboards** page available after clicking on the dashboard icon?
     ![](media/dashboard_diagram_populated.png)


    - **No**:
        This may be a sign that the Monitoring VM is not running. 
        1. Restart the VM to ensure all configuration changes take effect.
    - **Yes**:
        This indicates that the Monitoring VM is running and configured correctly.
## Verify the Verity ETL services is running and configured correctly

1. At **Dashboards/Site** verify the following panels are performing as designed:

    -  **Alarm Count By Severity** panel is displaying the correct data
    -  **Switch Connectivity** panel is displaying the correct data
    -  **Switch Connectivity History** panel is displaying the correct data.

        ![](media/dashboard_site_select_items.png)

    - **No**:
        This may be a sign that the ETL processes and timeseries databases are not performing as designed. 
        1. Restart the VM to ensure all configuration changes take effect.
        1. From **Dashboards/Verity**, you will now  gather the logs from the services listed below by following the provided instructions.
            - **Monitoring Logs: verity-ml-python/knowledge_graph**
            - **Monitoring Logs: verity-ml-python/verity_fastapi**
            - **Monitoring Logs: telegraf** 

            For each item listed above, follow these steps:

            1. Click on the ellipse to the right of the log panel and select **View**.  This will open a *new window* displaying the logs for the corresponding service.  
            1. Click on the ellipse to the right of the expanded log view and select **Inspect > Data**. *This will open the inspect panel*. 
            1. Click on the **Download logs** button. This will download a text file containing the logs to your local machine.
            ![](media/dashboards_verity_download_logs.png)
            

        Next, create a snapshot of the vNetC environment.

        Send the collected monitoring logs and the vNetC snapshot to Verity Support for further analysis.

    - **Yes**, all panels are displaying the correct data:
      This indicates that the system is running and configured correctly. If you are still experiencing issues, please contact Verity Support.
