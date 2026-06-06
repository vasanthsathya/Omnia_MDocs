# Reference

This section contains information-oriented technical reference material for Omnia v2.1. Every page is designed to be looked up rather than read end-to-end -- use the search bar or the table of contents below to find the specific specification you need.

## Support Matrix

Hardware, software, and topology compatibility tables that define the certified operating envelope for Omnia deployments.

- [Servers](SupportMatrix/servers.md) - Supported server models
- [Storage](SupportMatrix/storage.md) - Supported storage systems
- [Switches](SupportMatrix/switches.md) - Supported network switches
- [NICs](SupportMatrix/nics.md) - Supported network interface cards
- [Operating Systems](SupportMatrix/operating_systems.md) - Supported OS versions
- [Network Topologies](SupportMatrix/network_topologies.md) - Supported network configurations
- [Installed Software](SupportMatrix/installed_software.md) - Software components

## Configuration File Reference

Parameter-by-parameter documentation for every Omnia input file located under `/opt/omnia/input/project_default`.

- [Omnia Config](Configuration/omnia_config.md) - Main configuration file
- [Provision Config](Configuration/provision_config.md) - Provisioning settings
- [Network Spec](Configuration/network_spec.md) - Network configuration
- [Software Config](Configuration/software_config.md) - Software installation settings
- [Storage Config](Configuration/storage_config.md) - Storage configuration
- [Security Config](Configuration/security_config.md) - Security settings
- [Telemetry Config](Configuration/telemetry_config.md) - Telemetry configuration
- [Local Repo Config](Configuration/local_repo_config.md) - Local repository settings
- [BuildStreaM Config](Configuration/buildstream_config.md) - BuildStreaM configuration
- [HA Config](Configuration/ha_config.md) - High availability configuration

## Sample Files

Annotated examples of key input and configuration files, ready to copy and adapt.

- [PXE Mapping File](SampleFiles/pxe_mapping_file.md) - PXE boot mapping example
- [Software Config JSON](SampleFiles/software_config_json.md) - Software configuration example
- [Slurm Conf](SampleFiles/slurm_conf.md) - Slurm configuration example
- [Slurmdbd Conf](SampleFiles/slurmdbd_conf.md) - Slurm database configuration example

## Cluster Requirements

Minimum hardware, disk, and network port requirements for each deployment scenario.

- [Minimum Nodes](ClusterRequirements/minimum_nodes.md) - Node count requirements
- [Disk Space](ClusterRequirements/disk_space.md) - Storage requirements
- [Ports](ClusterRequirements/ports.md) - Network port requirements

## Playbook Reference

Quick-reference table covering every Omnia playbook, its purpose, where it runs, and what inputs it requires.

- [Playbook Reference](Playbooks/playbook_reference.md) - Complete playbook catalog

## Telemetry Metrics Reference

Catalog of every metric collected by the Omnia telemetry pipeline, organized by data source.

- [iDRAC Metrics](Metrics/idrac_metrics.md) - iDRAC server metrics
- [GPU Metrics](Metrics/gpu_metrics.md) - GPU performance metrics
- [LDMS Metrics](Metrics/ldms_metrics.md) - LDMS collector metrics

## Appendices

Supplementary reference material: naming rules, timezone values, and filesystem configuration details.

- [Hostname Requirements](Appendices/hostname_requirements.md) - Host naming conventions
- [Timezones](Appendices/timezones.md) - Supported timezone values
- [BeeGFS Server Setup](Appendices/beegfs_server_setup.md) - BeeGFS configuration details
