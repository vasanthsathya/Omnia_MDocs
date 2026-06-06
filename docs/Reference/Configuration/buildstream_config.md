BuildStreaM Config 

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
 * BuildStreaM Config [ BuildStreaM Config ](buildstream_config.md) Table of contents 
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

# build_stream_config.yml Reference[¶](#build_stream_configyml-reference "Permanent link")

File path: `/opt/omnia/input/project_default/build_stream_config.yml`

This file configures the BuildStreaM catalog-driven CI/CD deployment pipeline, including GitLab integration and pipeline behavior settings.

## Parameter reference[¶](#parameter-reference "Permanent link")

### GitLab settings[¶](#gitlab-settings "Permanent link")

Parameter | Type | Required | Default | Description 
---|---|---|---|--- 
`gitlab_enabled` | Boolean | No | `false` | Enable GitLab deployment for BuildStreaM CI/CD pipelines. 
`gitlab_server` | String | Conditional | (none) | Hostname or IP of the GitLab server. Required when `gitlab_enabled` is `true`. 
`gitlab_port` | Integer | No | `443` | HTTPS port for the GitLab web interface and API. 
`gitlab_external_url` | String | Conditional | (none) | Public-facing URL of the GitLab instance (e.g., `https://gitlab.hpc.example.com`). Used in pipeline configuration and webhook URLs. 
`gitlab_admin_password` | String | Conditional | (vault-managed) | GitLab root/admin password. Set via `credentials_utility.yml`. 
`gitlab_runner_token` | String | Conditional | (vault-managed) | Registration token for GitLab Runners. Set via `credentials_utility.yml`. 
 
### Pipeline settings[¶](#pipeline-settings "Permanent link")

Parameter | Type | Required | Default | Description 
---|---|---|---|--- 
`buildstream_catalog_path` | String | No | `/opt/omnia/buildstream/catalog` | Path to the BuildStreaM declarative catalog on the OIM. The catalog defines the desired cluster state. 
`buildstream_pipeline_branch` | String | No | `main` | Git branch in the BuildStreaM repository that triggers pipeline execution. 
`buildstream_auto_trigger` | Boolean | No | `true` | Automatically trigger pipelines when catalog changes are pushed. Set to `false` for manual pipeline execution only. 
`buildstream_retry_count` | Integer | No | `3` | Number of retry attempts for failed pipeline stages. 
`buildstream_timeout` | Integer | No | `3600` | Maximum pipeline execution time in seconds (default: 1 hour). 
 
### GitLab Runner settings[¶](#gitlab-runner-settings "Permanent link")

Parameter | Type | Required | Default | Description 
---|---|---|---|--- 
`runner_executor` | String | No | `shell` | GitLab Runner executor type. Accepted values: `shell`, `docker`, `kubernetes`. 
`runner_concurrent` | Integer | No | `4` | Maximum number of concurrent pipeline jobs per runner. 
`runner_tags` | List | No | `["omnia", "buildstream"]` | Tags assigned to the runner for job matching. 
 
## Usage example[¶](#usage-example "Permanent link")

File: /opt/omnia/input/project_default/build_stream_config.yml
 
 
 gitlab_enabled: true
 gitlab_server: "10.5.0.100"
 gitlab_port: 443
 gitlab_external_url: "https://gitlab.hpc.example.com"
 
 buildstream_catalog_path: "/opt/omnia/buildstream/catalog"
 buildstream_pipeline_branch: "main"
 buildstream_auto_trigger: true
 buildstream_retry_count: 3
 buildstream_timeout: 3600
 
 runner_executor: "shell"
 runner_concurrent: 4
 runner_tags:
 - omnia
 - buildstream
 

Info

 * [Playbook Reference](../Playbooks/playbook_reference.md) \-- BuildStreaM-related playbooks.
 * [Minimum Nodes](../ClusterRequirements/minimum_nodes.md) \-- Minimum nodes for BuildStreaM deployments (8+).
