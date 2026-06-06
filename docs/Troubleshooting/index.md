# Troubleshooting

Symptom-driven guides for diagnosing and resolving issues with your Omnia cluster. Each entry follows a consistent **Symptom > Cause > Resolution** format so you can quickly identify the problem and apply the fix.

## Troubleshooting Approach

When you encounter an issue, follow this general diagnostic flow:

1. **Check logs first.** Most issues leave a clear trace in the logs. See [Log Management](../Operations/log_management.md) for log locations.
   - Playbook logs: `/opt/omnia/log/core/playbooks/`
   - Container logs: `podman logs <container_name>`
   - Slurm logs: `/var/log/slurm/`

2. **Verify prerequisites.** Many failures stem from unmet prerequisites (missing packages, wrong OS version, misconfigured networks). Re-check the [Prerequisites Checklist](../GetStarted/prerequisites_checklist.md) for your deployment path.

3. **Use the ochami CLI.** For provisioning issues, the `ochami-cli` provides direct access to the OpenCHAMI state manager for inspecting node inventory, boot status, and hardware state:
   ```bash
   ssh omnia_core
   ochami-cli smd components list
   ochami-cli bss bootscript list
   ```

4. **Search this section.** Browse the topic-specific pages below or use your browser's search (Ctrl+F) to find your symptom.

## Topics

- [General](general.md) - Common issues and general troubleshooting
- [Authentication](authentication.md) - LDAP and authentication problems
- [BuildStreaM](buildstream.md) - BuildStreaM CI/CD issues
- [Kubernetes](kubernetes.md) - Kubernetes service cluster problems
- [Provisioning](provisioning.md) - Node provisioning and PXE boot issues
- [Slurm](slurm.md) - Slurm job scheduler problems
- [Telemetry](telemetry.md) - Telemetry and monitoring issues
- [Known Limitations](known_limitations.md) - Known product limitations and workarounds