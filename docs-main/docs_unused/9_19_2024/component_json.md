# Component JSON

**Component JSON** is a feature of the **Import/Export Workbench.**

This feature lets you export a JSON file containing data associated with a selected component. Components include Tenants and Route Maps.

## Introduction

Components such as Tenants make references to other user-configured tools like Services and BGP-Gateways. Component JSON is a tool used to bundle components with their user-configured dependencies in an exported JSON file. Importing components into a system using this feature will include all related dependencies and user settings.

To use this feature, follow these steps:

## Export Process

1.  Open the **Import/Export Workbench**.

![](media/import_export_workbench.png)


2.  Click **Export.**

![A screenshot of a phone Description automatically generated](media/ba65f104cbcf45a370cbcfceb981c238.png)

3.  Select **Component** and the component type, such as **Tenant** or **Route Map**. In the image below, the component type selected is **Tenant**. If the component type has not been created, it is *grayed out*. After you’ve made your selections, click Export.

![Component JSON](media/4103563f39bfdf950e9481286b150612.png)

4.  You will be provided with a list of all components of your chosen type. Select the one you want and click **Export**. The JSON file is immediately downloaded to your local machine.

![A screenshot of a computer Description automatically generated](media/0ccf07161de0e2c22fa689fcb5c5c25a.png)

## Import Process

Data saved in the JSON file is imported by following these steps:

5.  Open the **Import/Export Workbench**.

![Import export workbench](media/import_export_workbench.png)

6.  Click **Import.**

![Import](media/ba65f104cbcf45a370cbcfceb981c238.png)

7.  A prompt will appear to select the JSON file from a directory on your computer.
