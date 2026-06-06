Configure LDMS 

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
 * [ Set Up Slurm ](../Slurm/setup_slurm.md)
 * Kubernetes Kubernetes 
 * [ Set Up Kubernetes ](../Kubernetes/setup_service_k8s.md)
 * Storage Storage 
 * [ Configure NFS ](../Storage/configure_nfs.md)
 * Networking Networking 
 * [ Configure InfiniBand ](../Networking/configure_infiniband.md)
 * Authentication Authentication 
 * [ Set Up OpenLDAP ](../Authentication/setup_openldap.md)
 * Telemetry Telemetry 
 * [ Set Up Telemetry ](setup_telemetry.md)
 * Configure LDMS [ Configure LDMS ](configure_ldms.md) Table of contents 
 * [ Overview ](#overview)
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
 3. [ Telemetry ](setup_telemetry.md)

# Configure LDMS[¶](#configure-ldms "Permanent link")

Fine-tune LDMS (Lightweight Distributed Metric Service) sampler plugins and aggregation configuration for custom metric collection on compute nodes.

## Overview[¶](#overview "Permanent link")

LDMS runs two types of daemons:

 * **Samplers** (on compute nodes) -- Collect OS-level metrics at regular intervals.
 * **Aggregators** (on K8s service cluster) -- Collect samples from all compute nodes and forward them to the storage backend (Kafka/VictoriaMetrics).

This guide shows how to configure sampler plugins (`meminfo`, `vmstat`, `procstat`, and others) and adjust aggregation parameters.

## Prerequisites[¶](#prerequisites "Permanent link")

 * The [Setup Telemetry](setup_telemetry.md) procedure is complete (LDMS is deployed).
 * LDMS agents are running on compute nodes.
 * Aggregators are running on the K8s service cluster.

## Procedure[¶](#procedure "Permanent link")

 1. **Review available LDMS sampler plugins** :

Run on: compute node
 
 
 ldms_ls -h localhost -p 411 -v
 

Common sampler plugins:

.. list-table:: :header-rows: 1 :widths: 25 75
 
 
 * - Plugin
 - Metrics Collected
 * - `meminfo`
 - Memory usage (MemTotal, MemFree, Buffers, Cached, SwapTotal, etc.)
 * - `vmstat`
 - Virtual memory statistics (page faults, swaps, context switches)
 * - `procstat`
 - Per-CPU usage statistics (user, system, idle, iowait)
 * - `lustre_client`
 - Lustre filesystem client statistics
 * - `ibnet`
 - InfiniBand network counters
 * - `slurm_sampler`
 - Slurm job-level metrics
 

 1. **Configure sampler plugins** on a compute node:

Run on: compute node
 
 
 vi /etc/ldms/ldmsd.conf
 

Example sampler configuration:

File: /etc/ldms/ldmsd.conf on compute node
 
 
 # Transport and authentication
 auth_add name=munge plugin=munge
 
 # Listen for connections
 listen xprt=sock port=411 auth=munge
 
 # Load sampler plugins
 load name=meminfo
 config name=meminfo producer=${HOSTNAME} instance=${HOSTNAME}/meminfo \
 schema=meminfo component_id=${COMPONENT_ID}
 start name=meminfo interval=10000000
 
 load name=vmstat
 config name=vmstat producer=${HOSTNAME} instance=${HOSTNAME}/vmstat \
 schema=vmstat component_id=${COMPONENT_ID}
 start name=vmstat interval=10000000
 
 load name=procstat
 config name=procstat producer=${HOSTNAME} instance=${HOSTNAME}/procstat \
 schema=procstat component_id=${COMPONENT_ID}
 start name=procstat interval=10000000
 

!!! note
 
 
 The `interval` is in microseconds. `10000000` = 10 seconds.
 

 1. **Restart the LDMS sampler daemon** after configuration changes:

Run on: compute node
 
 
 systemctl restart ldmsd
 

 1. **Configure the LDMS aggregator** on the K8s cluster:

Run on: K8s control plane node
 
 
 kubectl edit configmap -n telemetry ldms-aggregator-config
 

Example aggregator configuration:

ConfigMap: ldms-aggregator-config in telemetry namespace
 
 
 # Authentication
 auth_add name=munge plugin=munge
 
 # Listen for downstream connections
 listen xprt=sock port=411 auth=munge
 
 # Add each compute node as a producer
 prdcr_add name=compute01 host=10.5.0.101 port=411 xprt=sock \
 auth=munge type=active interval=30000000
 prdcr_start name=compute01
 
 prdcr_add name=compute02 host=10.5.0.102 port=411 xprt=sock \
 auth=munge type=active interval=30000000
 prdcr_start name=compute02
 
 # Start the updater to collect from all producers
 updtr_add name=all_nodes interval=30000000 offset=100000
 updtr_prdcr_add name=all_nodes regex=.*
 updtr_start name=all_nodes
 

 1. **Restart the aggregator pod** :

Run on: K8s control plane node
 
 
 kubectl rollout restart deployment -n telemetry ldms-aggregator
 

 1. **(Bulk configuration) Deploy to all compute nodes** via Ansible:

Run on: omnia_core container
 
 
 ansible slurm_node -m copy -a "src=/tmp/ldmsd.conf dest=/etc/ldms/ldmsd.conf"
 ansible slurm_node -m service -a "name=ldmsd state=restarted"
 

## Verification[¶](#verification "Permanent link")

 1. **Verify sampler data** on a compute node:

Run on: compute node
 
 
 ldms_ls -h localhost -p 411 -v
 

Expected: list of active metric sets (meminfo, vmstat, procstat).

 1. **Query specific metrics** :

Run on: compute node
 
 
 ldms_ls -h localhost -p 411 -l -v | grep MemFree
 

 1. **Verify the aggregator is collecting** from compute nodes:

Run on: K8s control plane node
 
 
 AGG_POD=$(kubectl get pod -n telemetry -l app=ldms-aggregator -o jsonpath='{.items[0].metadata.name}')
 kubectl exec -n telemetry $AGG_POD -- ldms_ls -h localhost -p 411 -v
 

 1. **Verify data reaches VictoriaMetrics** :

Run on: K8s control plane node
 
 
 VM_POD=$(kubectl get pod -n telemetry -l app=victoriametrics -o jsonpath='{.items[0].metadata.name}')
 kubectl exec -n telemetry $VM_POD -- curl -s "http://localhost:8428/api/v1/query?query=meminfo_MemFree"
 

## Next Steps[¶](#next-steps "Permanent link")

 * [Verify Telemetry](verify_telemetry.md) \-- End-to-end telemetry verification.
 * [Configure External Kafka](configure_external_kafka.md) \-- Route LDMS data through external Kafka.

## Troubleshooting[¶](#troubleshooting "Permanent link")

**ldmsd fails to start** Check configuration syntax:

Run on: compute node
 
 
 ldmsd -c /etc/ldms/ldmsd.conf -F -v DEBUG 2>&1 | head -50
 

**"Connection refused" from aggregator to sampler** Verify the sampler is listening:

Run on: compute node
 
 
 ss -tlnp | grep 411
 

Check firewall:

Run on: compute node
 
 
 firewall-cmd --add-port=411/tcp --permanent
 firewall-cmd --reload
 

**Munge authentication failure** Ensure the Munge key is the same on compute nodes and aggregator:

Run on: omnia_core container
 
 
 ansible slurm_node -m shell -a "md5sum /etc/munge/munge.key"
 

**Metrics not appearing in VictoriaMetrics** Check the Kafka-to-VictoriaMetrics consumer logs:

Run on: K8s control plane node
 
 
 kubectl logs -n telemetry -l app=kafka-consumer --tail=30
 
