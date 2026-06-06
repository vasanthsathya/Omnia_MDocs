NICs 

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
 * [ Servers ](servers.md)
 * NICs [ NICs ](nics.md) Table of contents 
 * [ NIC support matrix ](#nic-support-matrix)
 * Configuration Configuration 
 * [ Omnia Config ](../Configuration/omnia_config.md)
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

 * [ NIC support matrix ](#nic-support-matrix)

 1. [ Home ](../../index.md)
 2. [ Reference ](../index.md)
 3. [ Support Matrix ](servers.md)

# Supported Network Interfaces[¶](#supported-network-interfaces "Permanent link")

Omnia v2.1 supports the following network interface cards (NICs) for admin, BMC, compute, and high-speed data networks.

## NIC support matrix[¶](#nic-support-matrix "Permanent link")

Manufacturer | Model | Speed | Ports | Notes 
---|---|---|---|--- 
NVIDIA (Mellanox) | ConnectX-6 | Up to 200 Gb/s | 1--2 | HDR InfiniBand and Ethernet modes. Supports SR-IOV, RDMA (RoCEv2 and InfiniBand), and GPUDirect. Recommended for high-speed compute and storage networks. 
Intel | E810 | Up to 100 Gb/s | 1--4 | Ethernet only. Supports SR-IOV, RDMA (RoCEv2), and ADQ (Application Device Queues). Suitable for admin, compute, and storage networks. 
 
## NIC role mapping[¶](#nic-role-mapping "Permanent link")

Network | ConnectX-6 | Intel E810 | Configuration Notes 
---|---|---|--- 
Admin network | Yes | Yes | Specified as `oim_nic_name` in `network_spec.yml`. Typically a 1 GbE or 10 GbE port. 
BMC network | \-- | \-- | BMC uses the iDRAC dedicated NIC (built-in); not a PCIe add-in card. 
Compute / data network | Yes | Yes | High-speed fabric for MPI, NCCL, and storage traffic. 
Public / external network | Yes | Yes | Internet-facing or campus-facing network. Optional depending on topology. 
 
## Firmware requirements[¶](#firmware-requirements "Permanent link")

NIC | Minimum Firmware | How to Update 
---|---|--- 
ConnectX-6 | Consult NVIDIA firmware release notes | Use `mlxfwmanager` from the Mellanox OFED package or Dell Update Package (DUP). 
Intel E810 | Consult Intel Ethernet release notes | Use `nvmupdate64e` from the Intel NVM Update Tool or Dell Update Package (DUP). 
 
Warning

Running mismatched firmware across NICs in the same cluster can cause intermittent link failures. Update all NICs to the same firmware version before running `discovery.yml`.

## InfiniBand considerations (ConnectX-6)[¶](#infiniband-considerations-connectx-6 "Permanent link")

When using ConnectX-6 in InfiniBand mode:

 * An InfiniBand subnet manager (e.g., OpenSM) must be running on at least one node in the fabric.
 * Omnia does not deploy or configure the InfiniBand subnet manager automatically; this must be set up independently.
 * RDMA and GPUDirect require the NVIDIA OFED driver stack, which can be included in the provisioning image via `software_config.json`.

Note

For Ethernet-mode deployments, ConnectX-6 supports RoCEv2 (RDMA over Converged Ethernet). Priority Flow Control (PFC) and ECN must be configured on the switch ports to avoid packet loss under RDMA workloads.

## LOM (LAN on Motherboard) support[¶](#lom-lan-on-motherboard-support "Permanent link")

Most Dell PowerEdge servers include onboard 1 GbE or 10 GbE LOM ports. These are supported for admin and BMC networks but are **not** listed as separately qualified NICs. LOM ports are referenced by their system interface name (e.g., `eno1`, `eno2`) in `network_spec.yml`.

Info

 * [Network Spec](../Configuration/network_spec.md) \-- Network specification parameters including NIC names.
 * [Switches](switches.md) \-- Supported switches for connecting NIC ports.
 * [Network Topologies](network_topologies.md) \-- How NICs map to network topology models.
