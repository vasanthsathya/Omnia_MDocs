Disk Space 

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
 * [ Omnia Config ](../Configuration/omnia_config.md)
 * Sample Files Sample Files 
 * [ PXE Mapping File ](../SampleFiles/pxe_mapping_file.md)
 * Cluster Requirements Cluster Requirements 
 * [ Minimum Nodes ](minimum_nodes.md)
 * Disk Space [ Disk Space ](disk_space.md) Table of contents 
 * [ Disk space summary ](#disk-space-summary)
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

 * [ Disk space summary ](#disk-space-summary)

 1. [ Home ](../../index.md)
 2. [ Reference ](../index.md)
 3. [ Cluster Requirements ](minimum_nodes.md)

# Disk Space Requirements[¶](#disk-space-requirements "Permanent link")

This page documents the minimum disk space requirements for each node role in an Omnia deployment.

## Disk space summary[¶](#disk-space-summary "Permanent link")

Node Role | Minimum Disk | Breakdown 
---|---|--- 
**OIM (Management Node)** | 256 GB | OS: ~20 GB. Pulp repo mirror: ~150 GB. Container images: ~30 GB. Logs and working space: ~56 GB. SSD recommended for Pulp performance. 
**Slurm Control Node** | 50 GB | OS: ~10 GB. Slurm state (`StateSaveLocation`): ~5 GB. MariaDB (job accounting): ~20 GB. Logs: ~15 GB. 
**Slurm Compute Node** | 50 GB | OS: ~10 GB. Slurm spool: ~5 GB. Temporary job data: ~30 GB. GPU drivers (if applicable): ~5 GB. 
**Login Node** | 50 GB | OS: ~10 GB. User tools and compilers: ~20 GB. Logs: ~20 GB. 
**K8s Control Plane** | 200 GB | OS: ~10 GB. etcd data: ~20 GB. Container images: ~50 GB. Telemetry data (VictoriaMetrics): ~100 GB. Logs: ~20 GB. 
**K8s Worker Node** | 200 GB | OS: ~10 GB. Container images: ~50 GB. Persistent volumes (local): ~120 GB. Logs: ~20 GB. 
**Auth Server** | 50 GB | OS: ~10 GB. LDAP database: ~5 GB. Logs: ~35 GB. 
**NFS Server (external)** | 200 GB+ | Repository mirror data (if serving as Pulp mirror target): ~150 GB. Shared home directories and scratch: remainder. 
 
## Detailed OIM disk allocation[¶](#detailed-oim-disk-allocation "Permanent link")

Component | Space | Notes 
---|---|--- 
RHEL 10.0 OS | ~20 GB | Server with GUI installation profile. 
Pulp repository mirror | ~150 GB | Mirrors RHEL BaseOS, AppStream, EPEL, CUDA/ROCm, K8s repos. Size varies with enabled repositories. 
Container images (Podman) | ~30 GB | OpenCHAMI, Pulp, omnia_core, and other OIM containers. 
ISO images | ~10 GB | RHEL 10.0 ISO(s) used for image building. 
Provisioning images | ~20 GB | Built images (x86_64 and/or AArch64). 
Logs and temp | ~26 GB | Ansible logs, OpenCHAMI logs, DHCP/TFTP logs. 
 
Note

The 256 GB minimum assumes a single architecture (x86_64). If provisioning both x86_64 and AArch64 nodes, add approximately 80 GB for the second repository mirror and image.

## Telemetry data sizing[¶](#telemetry-data-sizing "Permanent link")

Component | Growth Rate | Notes 
---|---|--- 
Kafka logs | ~1 GB/day per 100 nodes | Retained for `kafka_retention_hours` (default 168 hours). Purged automatically. 
VictoriaMetrics | ~500 MB/day per 100 nodes | Retained for `victoriametrics_retention` months. Compressed on disk. 
Grafana | Negligible | Dashboard definitions only; no metric data stored in Grafana. 
 
Tip

For clusters with 200+ nodes and 6-month retention, allocate at least 500 GB on the telemetry K8s node for VictoriaMetrics data.

## Filesystem recommendations[¶](#filesystem-recommendations "Permanent link")

Mount Point | Recommended FS | Notes 
---|---|--- 
`/` (root) | XFS | Default RHEL filesystem. Supports large files efficiently. 
`/var/lib/pulp` | XFS on SSD | High I/O during repository sync. SSD strongly recommended. 
`/var/lib/victoria-metrics` | XFS on SSD | Sequential write workload benefits from SSD. 
`/home` (shared) | NFS (PowerScale) | Shared across all nodes via NFS. 
 
Info

 * [Minimum Nodes](minimum_nodes.md) \-- Minimum node counts per scenario.
 * [Storage Config](../Configuration/storage_config.md) \-- NFS and BeeGFS mount configuration.
 * [Local Repo Config](../Configuration/local_repo_config.md) \-- Pulp repository storage path.
