---
hide:
- toc
---
# Inter-Tenant Routing
## Single Tenant-to-Tenant Routing
Before you perform this feature, the selected Tenants must [enable their Layer-3 Anycast IP/Mask on a service](services.md#enable-layer-3-anycast-ipmask-on-a-service).

1. Click **Tenancy**.
1. Click your chosen **Tenant** from the tree.
1. View the section titled **Inter-Tenant Routing**. 

You create Tenant-to-Tenant associations, set Route Maps, and apply Route Target and Distinguisher settings here.
To create an inter-tenant connection, you first need to select a Tenant to connect with.
In the Imports field, select a Tenant of your choice and click the **Enable** checkbox next to it. To add more Tenants, repeat the Import process.

### Bidirectional Tenant-to-Tenant Routing
To configure two-way Tenant Routing, complete the above steps to enable single Tenant-to-Tenant Routing. 

1. Under the **Inter-Tenant Routing** section, click the Object button next to the selected Tenant.
1. In the Tenant window that appears, click **Inter-Tenant Routing** and assign the Tenant from the previous window. Click **Enable** to confirm the selection.

When you view the Tenant-Tenant Routing for bidirectional Tenants, both Tenants display their connection to one another in their Imports window.




### Tenant-to-Tenant Routing with Route Maps
You need to create Route Maps before you apply them to Tenant-to-Tenant routing. [Creating Route Maps](route-maps.md) is a separate process. Additionally, applying Route Maps to Tenant-to-Tenant routing requires that you already configured Tenant-to-Tenant routing.

1. Click **Tenancy** and click the Tenant you want to work with.
1. View the **Inter-Tenant Routing** section.
1. Set the values of the following five form fields as needed for your configuration:

* Route Distinguisher
* Route Target Import
* Import Route Map
* Route Target Export
* Export Route Map