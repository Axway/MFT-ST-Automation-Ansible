st_update
=========
This Ansible role updates Axway SecureTransport to the latest version. It performs various tasks such as checking the current version, downloading the update, and applying the update.


Requirements
------------
- Ansible 2.9+
- Access to the SecureTransport server
- Proper permissions to execute commands and manage services on the SecureTransport server

> [!NOTE]
> If your ST host(s) are running RHEL 8, the maximum Ansible version is 2.16


## Role Variables

- `sources_location`: Location of the sources (e.g., 'artifactory').
- `artifactory`: URL of the artifactory to download the update from.
- `ST_USER`: User to run the SecureTransport commands.
- `AXWAY_INSTALLER_HOME`: Path to the Axway installer home directory.
- `st_update_file`: Filename of the SecureTransport update.
- `st_backup_location`: Directory to store backups.
- `INSTALLER_DIR`: Directory to store the update files.
- `SSL_ADMIN_PORT`: SSL admin port for SecureTransport.
- `FILEDRIVEHOME`: Home directory for the file drive.

## Dependencies

None.

## Example Playbook

```yaml
- hosts: ST_NODES
  become: yes
  roles:
    - role: st_update
      vars:
        sources_location: "artifactory"
        artifactory: "https://artifactory.your-company.com"
        ST_USER: "axway"
        AXWAY_INSTALLER_HOME: "/opt/axway/"
        st_update_file: "SecureTransport_5.5-20250327_Update_allOS_BN3226.zip"
        st_backup_location: "/opt/axway/backups"
        INSTALLER_DIR: "/opt/axway/installer"
        SSL_ADMIN_PORT: 444
        FILEDRIVEHOME: "/opt/axway/SecureTransport"
```

Or you can use the sample file provided, [st_update.yml](../../st_update.yml)

## License

MIT

