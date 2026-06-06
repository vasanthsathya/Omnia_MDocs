Reprovision Cluster 

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
 * Reprovision Cluster [ Reprovision Cluster ](reprovision_cluster.md) Table of contents 
 * [ When to re-provision ](#when-to-re-provision)

Troubleshooting 
 * [ General ](../Troubleshooting/general.md)

Contributing 
 * [ Pull Requests ](../Contributing/pull_requests.md)

Table of contents 

 * [ When to re-provision ](#when-to-re-provision)

 1. [ Home ](../index.md)
 2. [ Operations ](index.md)

# Re-provision Cluster Nodes[¶](#re-provision-cluster-nodes "Permanent link")

Re-provisioning replaces the operating system and software stack on existing cluster nodes. This is a full-cycle operation: nodes are re-imaged from the OIM and then reconfigured with the appropriate Omnia roles (Slurm, Kubernetes, or both).

## When to re-provision[¶](#when-to-re-provision "Permanent link")

Re-provisioning is the correct approach when:

 * **Operating system update** \-- You need to move nodes from one OS version to another (for example, RHEL 8.8 to RHEL 9.4).
 * **Configuration drift** \-- Nodes have accumulated manual changes that diverge from the desired state and a clean slate is simpler than incremental fixes.
 * **Recovery** \-- A node's OS is corrupted or a critical service has been misconfigured beyond easy repair.
 * **Role change** \-- A node is being reassigned from the Slurm cluster to the Kubernetes cluster (or vice versa).

Warning

Re-provisioning destroys all data on the target node's local disks. Ensure any important data is backed up to shared storage (NFS, PowerScale) before proceeding.

## Prerequisites[¶](#prerequisites "Permanent link")

 * The OIM is healthy and all OIM services are running (verify with [Verify Oim Services](../HowTo/Setup/verify_oim_services.md)).
 * Shared storage (NFS or PowerScale) is accessible for any data that must survive the re-provision.
 * Updated OS images have been built and are available in the Pulp repository (see [Build Cluster Images](../HowTo/Setup/build_cluster_images.md)).
 * The mapping file has been updated if node roles are changing.

## Procedure[¶](#procedure "Permanent link")

### Step 1: Drain workloads[¶](#step-1-drain-workloads "Permanent link")

Before re-provisioning, gracefully drain all workloads from the target nodes.

**For Slurm nodes:**

Run on: Slurm control node
 
 
 scontrol update NodeName=compute-03 State=DRAIN Reason="Re-provisioning"
 

Wait for running jobs to complete, or cancel them if immediate action is needed:

Run on: Slurm control node
 
 
 # Check for running jobs on the node
 squeue -w compute-03
 
 # Cancel if necessary
 scancel <job_id>
 

**For Kubernetes nodes:**

Run on: Kubernetes control plane
 
 
 kubectl drain kube-worker-02 --ignore-daemonsets --delete-emptydir-data
 

### Step 2: Update configuration[¶](#step-2-update-configuration "Permanent link")

 1. Review and update the input configuration files as needed:

 
 
 ssh omnia_core
 cd /omnia/input
 

 * `mapping_file.csv` \-- Update node roles if changing.
 * `provision_config.yml` \-- Update OS image or provisioning parameters.
 * `omnia_config.yml` \-- Update cluster-level settings.

 * If building a new OS image, run the image-build process:

 
 
 cd /omnia
 ansible-playbook playbooks/build_cluster_images.yml
 

### Step 3: Re-image the nodes[¶](#step-3-re-image-the-nodes "Permanent link")

Run `discovery.yml` to re-discover and PXE-boot the target nodes with the updated OS image:

Run on: OIM host
 
 
 cd /omnia
 ansible-playbook playbooks/discovery.yml
 

The nodes will:

 1. Reboot into the PXE environment.
 2. Receive the new OS image from the OIM.
 3. Complete the cloud-init first-boot configuration.

Note

The re-imaging process typically takes 15--30 minutes per node, depending on image size and network speed.

### Step 4: Redeploy cluster software[¶](#step-4-redeploy-cluster-software "Permanent link")

After the nodes have been re-imaged and are accessible via SSH, redeploy the Omnia cluster software:

Run on: OIM host
 
 
 cd /omnia
 ansible-playbook playbooks/omnia.yml
 

This playbook applies the full cluster configuration, including:

 * Slurm controller and compute daemon setup
 * Kubernetes control plane and worker configuration
 * GPU drivers (CUDA / ROCm)
 * Authentication (OpenLDAP client)
 * Telemetry agents

## Verification[¶](#verification "Permanent link")

After re-provisioning is complete:

Run on: OIM host
 
 
 # Verify Slurm nodes are back online
 sinfo
 
 # Verify Kubernetes nodes are Ready
 kubectl get nodes
 
 # Check for any failed Ansible tasks in the log
 cat /opt/omnia/log/core/playbooks/omnia.log | grep -i "failed"
 
 # Run a test Slurm job
 srun -N 1 hostname
 

Info

 * [Add Remove Nodes](add_remove_nodes.md) \-- Add or remove nodes without re-imaging.
 * [Oim Cleanup](oim_cleanup.md) \-- Full teardown and rebuild of the OIM itself.
 * [Discover Nodes](../HowTo/Setup/discover_nodes.md) \-- Detailed node discovery procedure.
