# How-to Guides

Task-oriented procedures for deploying, configuring, and managing Omnia clusters. Each guide follows a consistent structure: **Overview**, **Prerequisites**, **Procedure**, **Verification**, **Next Steps**, and **Troubleshooting**.

!!! tip
    If you are new to Omnia, start with the [Get Started](../GetStarted/index.md) tutorials first. How-to guides assume you understand Omnia's architecture and have a working OIM.

## Initial Setup & Provisioning

Get Omnia installed on your OIM and provision bare-metal servers into a working cluster.

- [Prepare OIM](Setup/prepare_oim.md) - Prepare the Omnia Installation Manager
- [Configure Credentials](Setup/configure_credentials.md) - Set up authentication credentials
- [Configure Inputs](Setup/configure_inputs.md) - Configure deployment parameters
- [Create Mapping File](Setup/create_mapping_file.md) - Create PXE boot mapping
- [Create Local Repos](Setup/create_local_repos.md) - Set up local software repositories
- [Build Cluster Images](Setup/build_cluster_images.md) - Build cluster deployment images
- [Deploy Omnia Core](Setup/deploy_omnia_core.md) - Deploy core Omnia services
- [Discover Nodes](Setup/discover_nodes.md) - Discover and register compute nodes
- [PXE Boot Nodes](Setup/pxe_boot_nodes.md) - Boot nodes via PXE
- [Verify Cluster](Setup/verify_cluster.md) - Verify cluster deployment
- [Verify OIM Services](Setup/verify_oim_services.md) - Verify OIM service health

## Slurm Job Scheduling

Deploy and manage Slurm-based HPC clusters, including GPU-accelerated workloads and dynamic node management.

- [Set Up Slurm](Slurm/setup_slurm.md) - Deploy and configure Slurm
- [Build Slurm Repo](Slurm/build_slurm_repo.md) - Create Slurm software repository
- [Add Slurm Nodes](Slurm/add_slurm_nodes.md) - Add nodes to Slurm cluster
- [Remove Slurm Nodes](Slurm/remove_slurm_nodes.md) - Remove nodes from Slurm cluster
- [Slurm Config Backup](Slurm/slurm_config_backup.md) - Backup Slurm configuration
- [Slurm with GPU](Slurm/slurm_with_gpu.md) - Configure GPU support in Slurm
- [Run HPC Benchmarks](Slurm/run_hpc_benchmarks.md) - Run performance benchmarks

## Kubernetes Services

Deploy and configure the Kubernetes service cluster used for platform services, monitoring, and storage.

- [Set Up Kubernetes](Kubernetes/setup_service_k8s.md) - Deploy Kubernetes service cluster
- [Configure HA](Kubernetes/configure_ha.md) - Configure high availability
- [Deploy PowerScale CSI](Kubernetes/deploy_powerscale_csi.md) - Deploy PowerScale CSI driver

## Storage

Configure shared storage for your cluster, including NFS and PowerVault block storage.

- [Configure NFS](Storage/configure_nfs.md) - Set up NFS shared storage
- [Configure PowerVault](Storage/configure_powervault.md) - Configure PowerVault storage

## Networking

Set up high-performance interconnects for your compute fabric, including InfiniBand and RoCE.

- [Configure InfiniBand](Networking/configure_infiniband.md) - Set up InfiniBand networking
- [Configure RoCE](Networking/configure_roce.md) - Configure RoCE networking

## Authentication

Configure centralized user authentication across your cluster using LDAP.

- [Deploy External LDAP](Authentication/deploy_external_ldap.md) - Integrate with external LDAP
- [Replicate LDAP](Authentication/replicate_ldap.md) - Set up LDAP replication
- [Set Up OpenLDAP](Authentication/setup_openldap.md) - Deploy OpenLDAP server
- [Set Up OpenLDAP Proxy](Authentication/setup_openldap_proxy.md) - Configure LDAP proxy

## Telemetry & Monitoring

Deploy and configure the telemetry pipeline for cluster-wide metrics collection, aggregation, and visualization.

- [Set Up Telemetry](Telemetry/setup_telemetry.md) - Deploy telemetry services
- [Configure External Kafka](Telemetry/configure_external_kafka.md) - Use external Kafka
- [Configure External Victoria](Telemetry/configure_external_victoria.md) - Use external VictoriaMetrics
- [Configure LDMS](Telemetry/configure_ldms.md) - Configure LDMS collector
- [Telemetry from OME](Telemetry/telemetry_from_ome.md) - Integrate with OpenManage Essentials
- [Verify Telemetry](Telemetry/verify_telemetry.md) - Verify telemetry data flow

## Containers & Packages

Run containerized workloads and deploy additional software packages on provisioned nodes.

- [Deploy Additional Packages](Containers/deploy_additional_packages.md) - Install extra software
- [Use Apptainer](Containers/use_apptainer.md) - Run containers with Apptainer

## BuildStreaM (CI/CD)

Automate cluster deployment using GitLab CI/CD pipelines and the BuildStreaM catalog-driven workflow.

- [Deploy GitLab](BuildStreaM/deploy_gitlab.md) - Deploy GitLab for CI/CD
- [Update Catalog Pipeline](BuildStreaM/update_catalog_pipeline.md) - Update BuildStreaM catalog
- [BuildStreaM Troubleshooting](BuildStreaM/buildstream_troubleshooting.md) - Troubleshoot BuildStreaM issues
