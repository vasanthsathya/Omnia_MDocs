HA Config 

[ ](javascript:void\(0\) "Share")



 * [ Home ](../../index.md)

[ ![logo](../../assets/omnia-logo.png) ](../../index.md "Dell Omnia") Dell Omnia 



 * [ Home ](../../index.md)

Overview 
 * [ Architecture ](../../Overview/architecture.md)

Get Started 
 * [ Prerequisites Checklist ](../../GetStarted/prerequisites_checklist.md)

How-to Guides 
 * Setup Setup 
 * [ Prepare OIM ](../../HowTo/Setup/prepare_oim.md)
 * Slurm Slurm 
 * [ Set Up Slurm ](../../HowTo/Slurm/setup_slurm.md)
 * Kubernetes Kubernetes 
 * [ Set Up Kubernetes ](../../HowTo/Kubernetes/setup_service_k8s.md)
 * Storage Storage 
 * [ Configure NFS ](../../HowTo/Storage/configure_nfs.md)
 * Networking Networking 
 * [ Configure InfiniBand ](../../HowTo/Networking/configure_infiniband.md)
 * Authentication Authentication 
 * [ Set Up OpenLDAP ](../../HowTo/Authentication/setup_openldap.md)
 * Telemetry Telemetry 
 * [ Set Up Telemetry ](../../HowTo/Telemetry/setup_telemetry.md)
 * Containers Containers 
 * [ Use Apptainer ](../../HowTo/Containers/use_apptainer.md)
 * BuildStreaM BuildStreaM 
 * [ Deploy GitLab ](../../HowTo/BuildStreaM/deploy_gitlab.md)

Reference 
 * Support Matrix Support Matrix 
 * [ Servers ](../SupportMatrix/servers.md)
 * Configuration Configuration 
 * [ Omnia Config ](omnia_config.md)
 * HA Config [ HA Config ](ha_config.md) Table of contents 
 * [ Parameter reference ](#parameter-reference)
 * Sample Files Sample Files 
 * [ PXE Mapping File ](../SampleFiles/pxe_mapping_file.md)
 * Cluster Requirements Cluster Requirements 
 * [ Minimum Nodes ](../ClusterRequirements/minimum_nodes.md)
 * Playbooks Playbooks 
 * [ Playbook Reference ](../Playbooks/playbook_reference.md)
 * Metrics Metrics 
 * [ iDRAC Metrics ](../Metrics/idrac_metrics.md)
 * Appendices Appendices 
 * [ Hostname Requirements ](../Appendices/hostname_requirements.md)

Operations 
 * [ Add / Remove Nodes ](../../Operations/add_remove_nodes.md)

Troubleshooting 
 * [ General ](../../Troubleshooting/general.md)

Contributing 
 * [ Pull Requests ](../../Contributing/pull_requests.md)

Table of contents 

 * [ Parameter reference ](#parameter-reference)

 1. [ Home ](../../index.md)
 2. [ Reference ](../index.md)
 3. [ Configuration ](omnia_config.md)

# high_availability_config.yml Reference[¶](#high_availability_configyml-reference "Permanent link")

File path: `/opt/omnia/input/project_default/high_availability_config.yml` (also referred to as `ha_config.yml`)

This file configures Kubernetes control plane high availability (HA) using a virtual IP address and load-balanced API servers.

## Parameter reference[¶](#parameter-reference "Permanent link")

Parameter | Type | Required | Default | Description 
---|---|---|---|--- 
`ha_enabled` | Boolean | No | `false` | Enable Kubernetes control plane high availability. When `true`, multiple `kube_control_plane` nodes share a virtual IP. 
`ha_virtual_ip` | String (IP) | Conditional | (none) | Virtual IP address for the Kubernetes API server. Clients and worker nodes connect to this IP instead of a single control plane node. Required when `ha_enabled` is `true`. Must be on the same subnet as the control plane nodes' admin network. 
`ha_load_balancer` | String | No | `kube-vip` | Load balancer technology for the control plane virtual IP. Accepted values: `kube-vip`. Additional options may be supported in future releases. 
`ha_control_plane_port` | Integer | No | `6443` | Port on which the Kubernetes API server listens. The virtual IP forwards traffic to this port on all control plane nodes. 
`ha_etcd_external` | Boolean | No | `false` | Use an external etcd cluster instead of the embedded etcd that runs on each control plane node. When `true`, provide etcd endpoints via `ha_etcd_endpoints`. 
`ha_etcd_endpoints` | List | Conditional | `[]` | List of external etcd endpoints (e.g., `["https://10.5.0.10:2379", "https://10.5.0.11:2379"]`). Required when `ha_etcd_external` is `true`. 
 
## HA architecture overview[¶](#ha-architecture-overview "Permanent link")

Component | Description 
---|--- 
**kube-vip** | Runs as a static pod on each control plane node. One node is elected leader and holds the virtual IP. If the leader fails, another control plane node takes over within seconds. 
**Virtual IP** | A floating IP that is always routable to the current leader. All `kubelet` and `kubectl` connections target this IP. 
**etcd** | By default, each control plane node runs its own etcd instance (stacked topology). Alternatively, an external etcd cluster can be specified. 
 
## Prerequisites[¶](#prerequisites "Permanent link")

 * Minimum **3 control plane nodes** for a quorum-based HA deployment.
 * The `ha_virtual_ip` must be a free IP on the admin network subnet -- it must not be assigned to any physical server or DHCP range.
 * All control plane nodes must have L2 connectivity on the admin network for ARP-based virtual IP failover.

## Usage example[¶](#usage-example "Permanent link")

File: /opt/omnia/input/project_default/high_availability_config.yml
 
 
 ha_enabled: true
 ha_virtual_ip: "10.5.0.250"
 ha_load_balancer: "kube-vip"
 ha_control_plane_port: 6443
 ha_etcd_external: false
 

Info

 * [Omnia Config](omnia_config.md) \-- Kubernetes deployment settings.
 * [Minimum Nodes](../ClusterRequirements/minimum_nodes.md) \-- Minimum node counts for HA deployments.
 * [Ports](../ClusterRequirements/ports.md) \-- Kubernetes ports including the API server.
