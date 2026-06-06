Add Slurm Nodes 

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
 * [ Prepare OIM ](../Setup/prepare_oim.md)
 * Slurm Slurm 
 * [ Set Up Slurm ](setup_slurm.md)
 * Add Slurm Nodes [ Add Slurm Nodes ](add_slurm_nodes.md) Table of contents 
 * [ Overview ](#overview)
 * Kubernetes Kubernetes 
 * [ Set Up Kubernetes ](../Kubernetes/setup_service_k8s.md)
 * Storage Storage 
 * [ Configure NFS ](../Storage/configure_nfs.md)
 * Networking Networking 
 * [ Configure InfiniBand ](../Networking/configure_infiniband.md)
 * Authentication Authentication 
 * [ Set Up OpenLDAP ](../Authentication/setup_openldap.md)
 * Telemetry Telemetry 
 * [ Set Up Telemetry ](../Telemetry/setup_telemetry.md)
 * Containers Containers 
 * [ Use Apptainer ](../Containers/use_apptainer.md)
 * BuildStreaM BuildStreaM 
 * [ Deploy GitLab ](../BuildStreaM/deploy_gitlab.md)

Reference 
 * Support Matrix Support Matrix 
 * [ Servers ](../../Reference/SupportMatrix/servers.md)
 * Configuration Configuration 
 * [ Omnia Config ](../../Reference/Configuration/omnia_config.md)
 * Sample Files Sample Files 
 * [ PXE Mapping File ](../../Reference/SampleFiles/pxe_mapping_file.md)
 * Cluster Requirements Cluster Requirements 
 * [ Minimum Nodes ](../../Reference/ClusterRequirements/minimum_nodes.md)
 * Playbooks Playbooks 
 * [ Playbook Reference ](../../Reference/Playbooks/playbook_reference.md)
 * Metrics Metrics 
 * [ iDRAC Metrics ](../../Reference/Metrics/idrac_metrics.md)
 * Appendices Appendices 
 * [ Hostname Requirements ](../../Reference/Appendices/hostname_requirements.md)

Operations 
 * [ Add / Remove Nodes ](../../Operations/add_remove_nodes.md)

Troubleshooting 
 * [ General ](../../Troubleshooting/general.md)

Contributing 
 * [ Pull Requests ](../../Contributing/pull_requests.md)

Table of contents 

 * [ Overview ](#overview)

 1. [ Home ](../../index.md)
 2. [ How-to Guides ](../index.md)
 3. [ Slurm ](setup_slurm.md)

# Add Slurm Nodes[¶](#add-slurm-nodes "Permanent link")

Dynamically add new compute nodes to a running Slurm cluster without disrupting existing workloads.

## Overview[¶](#overview "Permanent link")

Omnia supports dynamic node addition to expand a running Slurm cluster. The process involves:

 1. Provisioning the new server(s) using the standard Omnia workflow.
 2. Adding the new node(s) to the mapping file.
 3. Running the add-node playbook to configure Slurm on the new nodes and update the controller's `slurm.conf`.

## Prerequisites[¶](#prerequisites "Permanent link")

 * A working Slurm cluster deployed via [Setup Slurm](setup_slurm.md).
 * New server(s) are physically racked, cabled, and have BMC connectivity.
 * The new server(s) have been provisioned and are reachable on the admin network.
 * New node entries have been added to the `pxe_mapping_file.csv`.

## Procedure[¶](#procedure "Permanent link")

 1. **Update the mapping file** with new node entries:

Run on: omnia_core container
 
 
 vi /opt/omnia/input/project_default/pxe_mapping_file.csv
 

Add new rows for each new compute node:

File: /opt/omnia/input/project_default/pxe_mapping_file.csv
 
 
 slurm_node,slurm_cluster,NEWSVCTG1,,,aa:bb:cc:dd:ee:10,10.5.0.110,aa:bb:cc:dd:ff:10,10.3.0.110
 slurm_node,slurm_cluster,NEWSVCTG2,,,aa:bb:cc:dd:ee:11,10.5.0.111,aa:bb:cc:dd:ff:11,10.3.0.111
 

 1. **Provision the new nodes** if not already provisioned:

Run on: omnia_core container
 
 
 cd /omnia/discovery
 ansible-playbook discovery.yml --ask-vault-pass
 

 1. **Run the add-node playbook** :

Run on: omnia_core container
 
 
 cd /omnia
 ansible-playbook omnia.yml --ask-vault-pass --limit "new_nodes"
 

!!! note
 
 
 If a dedicated `add_node.yml` playbook is available in your Omnia
 version, use it instead:
 
 ```bash title="Run on: omnia_core container"
 ansible-playbook utils/add_node.yml --ask-vault-pass \
 -e "target_nodes=10.5.0.110,10.5.0.111"
 ```
 

 1. **Update the Slurm configuration** on the control node to include the new nodes:

Run on: Slurm control node
 
 
 # Reconfigure Slurm to pick up new nodes
 scontrol reconfigure
 

## Verification[¶](#verification "Permanent link")

 1. **Check that new nodes appear in the cluster** :

Run on: Slurm control node
 
 
 sinfo
 

New nodes should appear in the `normal` partition with `idle` state.

 1. **Run a test job on the new nodes** :

Run on: Slurm control node
 
 
 srun -w <new-node-hostname> hostname
 

 1. **Verify Munge authentication** on the new nodes:

Run on: Slurm control node
 
 
 munge -n | ssh <new-node-ip> unmunge
 

 1. **Check slurmd is running** on the new nodes:

Run on: new compute node
 
 
 systemctl status slurmd
 

## Next Steps[¶](#next-steps "Permanent link")

 * [Slurm With Gpu](slurm_with_gpu.md) \-- Configure GPU support on the new nodes if they have GPUs.
 * [Configure Nfs](../Storage/configure_nfs.md) \-- Mount shared storage on new nodes.
 * [Setup Openldap](../Authentication/setup_openldap.md) \-- Ensure LDAP clients are configured on new nodes.

## Troubleshooting[¶](#troubleshooting "Permanent link")

**New nodes show "down" in sinfo** \- Verify `slurmd` is running:
 
 
 ```bash title="Run on: new compute node"
 systemctl status slurmd
 journalctl -u slurmd --no-pager -n 20
 ```
 

 * Check that `slurm.conf` on the new node matches the control node's version:

Run on: new compute node
 
 grep "SlurmctldHost" /etc/slurm/slurm.conf
 

 * Resume the node from the controller:

Run on: Slurm control node
 
 scontrol update nodename=<node> state=resume reason="added"
 

**Munge key mismatch** Re-distribute the Munge key from the control node:

Run on: omnia_core container
 
 
 ansible new_nodes -m copy -a "src=/etc/munge/munge.key dest=/etc/munge/munge.key owner=munge group=munge mode=0400"
 ansible new_nodes -m service -a "name=munge state=restarted"
 

**New nodes not in Ansible inventory** Re-run discovery or manually add the nodes to the Ansible inventory:

Run on: omnia_core container
 
 
 ochami node list
 
