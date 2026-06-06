Best Practices Checklist 

[ ](javascript:void\(0\) "Share")



 * [ Home ](../index.md)

[ ![logo](../assets/omnia-logo.png) ](../index.md "Dell Omnia") Dell Omnia 



 * [ Home ](../index.md)

Overview 
 * [ Architecture ](../Overview/architecture.md)

Get Started 
 * [ Prerequisites Checklist ](../GetStarted/prerequisites_checklist.md)

How-to Guides 
 * Setup Setup 
 * [ Prepare OIM ](../HowTo/Setup/prepare_oim.md)
 * Slurm Slurm 
 * [ Set Up Slurm ](../HowTo/Slurm/setup_slurm.md)
 * Kubernetes Kubernetes 
 * [ Set Up Kubernetes ](../HowTo/Kubernetes/setup_service_k8s.md)
 * Storage Storage 
 * [ Configure NFS ](../HowTo/Storage/configure_nfs.md)
 * Networking Networking 
 * [ Configure InfiniBand ](../HowTo/Networking/configure_infiniband.md)
 * Authentication Authentication 
 * [ Set Up OpenLDAP ](../HowTo/Authentication/setup_openldap.md)
 * Telemetry Telemetry 
 * [ Set Up Telemetry ](../HowTo/Telemetry/setup_telemetry.md)
 * Containers Containers 
 * [ Use Apptainer ](../HowTo/Containers/use_apptainer.md)
 * BuildStreaM BuildStreaM 
 * [ Deploy GitLab ](../HowTo/BuildStreaM/deploy_gitlab.md)

Reference 
 * Support Matrix Support Matrix 
 * [ Servers ](../Reference/SupportMatrix/servers.md)
 * Configuration Configuration 
 * [ Omnia Config ](../Reference/Configuration/omnia_config.md)
 * Sample Files Sample Files 
 * [ PXE Mapping File ](../Reference/SampleFiles/pxe_mapping_file.md)
 * Cluster Requirements Cluster Requirements 
 * [ Minimum Nodes ](../Reference/ClusterRequirements/minimum_nodes.md)
 * Playbooks Playbooks 
 * [ Playbook Reference ](../Reference/Playbooks/playbook_reference.md)
 * Metrics Metrics 
 * [ iDRAC Metrics ](../Reference/Metrics/idrac_metrics.md)
 * Appendices Appendices 
 * [ Hostname Requirements ](../Reference/Appendices/hostname_requirements.md)

Operations 
 * [ Add / Remove Nodes ](add_remove_nodes.md)
 * Best Practices Checklist [ Best Practices Checklist ](best_practices_checklist.md) Table of contents 
 * [ BIOS and firmware ](#bios-and-firmware)

Troubleshooting 
 * [ General ](../Troubleshooting/general.md)

Contributing 
 * [ Pull Requests ](../Contributing/pull_requests.md)

Table of contents 

 * [ BIOS and firmware ](#bios-and-firmware)

 1. [ Home ](../index.md)
 2. [ Operations ](index.md)

# Best Practices Checklist[¶](#best-practices-checklist "Permanent link")

A consolidated checklist of recommendations for deploying and operating an Omnia cluster. Each item links to the relevant documentation section for detailed procedures.

## BIOS and firmware[¶](#bios-and-firmware "Permanent link")

| Best Practice | Reference 
---|---|--- 
☐ | **Disable PowerCap** on all compute nodes to ensure maximum CPU performance. PowerCap can throttle compute-intensive HPC workloads. | [Prerequisites Checklist](../GetStarted/prerequisites_checklist.md) 
☐ | **Set BIOS to Performance mode** on all compute nodes. The `Performance` power profile maximizes clock speeds and disables power-saving C-states that introduce latency. | [Prerequisites Checklist](../GetStarted/prerequisites_checklist.md) 
☐ | **Keep iDRAC firmware current** on all nodes. Firmware updates fix bugs, improve Redfish API reliability, and patch security vulnerabilities. Use Dell Repository Manager or `racadm` for updates. | [Security Hardening](security_hardening.md) 
 
## Playbook execution[¶](#playbook-execution "Permanent link")

| Best Practice | Reference 
---|---|--- 
☐ | **Run playbooks from their directory** using `cd`. Omnia playbooks use relative paths for roles and configuration files. Always `cd /omnia` before running `ansible-playbook`. | [Index](../HowTo/index.md) 
☐ | **Review prerequisites before running playbooks.** Each playbook has specific input files and environment requirements. Check the corresponding how-to guide before execution. | [Index](../HowTo/index.md) 
 
## Storage and telemetry[¶](#storage-and-telemetry "Permanent link")

| Best Practice | Reference 
---|---|--- 
☐ | **Provision sufficient NFS storage for telemetry.** The telemetry pipeline (VictoriaMetrics, Kafka) can generate significant data volumes. Allocate at least 500 GB of NFS-backed persistent storage for telemetry retention. | [Setup Telemetry](../HowTo/Telemetry/setup_telemetry.md) 
☐ | **Prefer the PowerScale CSI driver over external NFS** for Kubernetes persistent volumes. The CSI driver provides dynamic provisioning, better performance, and snapshot support compared to static NFS mounts. | [Deploy Powerscale Csi](../HowTo/Kubernetes/deploy_powerscale_csi.md) 
☐ | **Ensure external NFS is accessible via the admin network.** If using external NFS (not PowerScale), verify that the NFS server is reachable from all nodes on the admin network and that firewall rules allow NFS traffic (ports 2049, 111). | [Configure Nfs](../HowTo/Storage/configure_nfs.md) 
 
## System administration[¶](#system-administration "Permanent link")

| Best Practice | Reference 
---|---|--- 
☐ | **Minimize OIM reboots.** The OIM hosts critical Podman containers that provide provisioning, DHCP, and management services. Rebooting the OIM interrupts these services and may cause hostname or IP changes. Plan reboots during maintenance windows only. | [General](../Troubleshooting/general.md) 
☐ | **Keep Firefox updated on RHEL OIM.** If you use the AWX web UI on the OIM, ensure Firefox (the default RHEL browser) is updated to avoid TLS compatibility and rendering issues. | [Security Hardening](security_hardening.md) 
☐ | **Run** `yum update --security` **routinely.** Apply security patches on the OIM and all cluster nodes on a regular schedule (monthly recommended). Drain Slurm nodes before applying updates. | [Security Hardening](security_hardening.md) 
☐ | **Sync system time across the OIM and all nodes.** Use `chrony` or `ntpd` to maintain synchronized clocks. Time drift causes Kerberos authentication failures, Slurm scheduling issues, and inaccurate telemetry timestamps. | [Prerequisites Checklist](../GetStarted/prerequisites_checklist.md) 
 
## Pre-deployment summary[¶](#pre-deployment-summary "Permanent link")

Use this condensed list as a quick pre-flight check before running any Omnia deployment:

 1. ☐ BIOS: PowerCap disabled, Performance mode set.
 2. ☐ iDRAC firmware updated to the latest supported version.
 3. ☐ Network: admin and BMC VLANs configured, NFS accessible.
 4. ☐ System clocks synchronized (chrony/NTP).
 5. ☐ OIM meets minimum requirements (4+ cores, 32+ GB RAM, 256+ GB disk).
 6. ☐ Input files reviewed and populated (mapping file, config files).
 7. ☐ Credentials encrypted with Ansible Vault.
 8. ☐ Sufficient NFS storage allocated for telemetry.
 9. ☐ Firefox updated (if using AWX web UI).
 10. ☐ Security updates applied: `yum update --security`.

Info

 * [Prerequisites Checklist](../GetStarted/prerequisites_checklist.md) \-- Detailed prerequisites for all deployment paths.
 * [Security Hardening](security_hardening.md) \-- Full security hardening procedures.
 * [Log Management](log_management.md) \-- Log monitoring and rotation configuration.
