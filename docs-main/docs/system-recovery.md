---
hide:
- toc
---

## System Recovery from POSTGRES Backup
### Verity 6.3.0 + 

If the vNETC is part of a high availability deployment, please refer to the instructions in the High Availability configuration section.

[Recovering an HA site from POSTGRES backup](high-availability.md#recovering-an-ha-site-from-postgres-backup)

Otherwise, proceed as follows:

1. Transfer a database backup of the system being recovered to the new system.  This would come from the SFTP backup server if configured, or from the old system under the directory: `/var/ns/backups/postgres/active/archive/`. The file will typically have a name like: **20240514T164709.116Z.tbz**
1. Place the backup file in a convenient location, such as `/tmp or /var/ns/direct`. 
1. Shut down the operations services using: ` service ns_init stop `
1. Run the restore command specifying the transferred file, eg:  `ns_restore -b /tmp/20240514T164709.116Z.tbz` . This restores the database and system configuration from the database backup.
1. Once complete, restart system services using: `service ns_init start`
1. `virsh console` into SDLC and run the setup to point to the vNetC.