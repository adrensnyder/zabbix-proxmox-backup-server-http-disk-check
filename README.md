# Proxmox Backup Server by HTTP – Disk check

This repository provides a Zabbix add-on template to monitor disk health (SMART) and related checks on Proxmox Backup Server (PBS) nodes.
The template also includes checks related to Ceph where applicable.

This template is designed to be linked together with the [Proxmox Backup Server by HTTP](https://github.com/ismvru/zbx-tmplt-pbs) template, as it reuses the same macros.
It has been tested with Zabbix Server 6.0 LTS and the official Proxmox Backup Server by HTTP template.

All required macros are documented directly inside the template.

## Setup instructions

1. Create a dedicated monitoring user (for example `zabbix`) in:
   Configuration → Access Control → User Management

2. Create an API token for the user:
   Configuration → Access Control → API Tokens

3. Assign permissions to the user and API token:
   - Path: `/`
   - Role: `Audit`
   - Menu: Configuration → Access Control → Permissions

   Note:
   The template queries the following API endpoints:
   - `/datastore`
   - `/system/status`
   - `/system/tasks`

   The user associated with the API token must have sufficient rights to access these endpoints.
   It is currently not possible to create a more granular custom permission group in Proxmox Backup Server.

4. Configure the required host macros:

   - `{$PBS.NODE.NAME}`
   - `{$PBS.TOKEN.ID}`
   - `{$PBS.TOKEN.SECRET}`

## Notes
Ceph-related checks refer to storage health information visible from the PBS node environment, when applicable.
