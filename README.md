# SecureTransport Install, Configuration, and Tuning


## 1. Introduction

### Purpose

These playbooks are intended to be used:
* To deploy in TEST environments
* As a sample 

They have not been tested for production purposes. 
Use them at your own risk and make sure to validate all plays and tasks before deploying elsewhere.

### Deployment

When all plays  run, they will install and configure SecureTransport Enterprise Cluster deployment with:

- PostgreSQL database (version: 14)
- NFS storage to share between the core nodes (version: 3)
- OS prerequisites for ST Linux install (version: RHEL 8)
- Two core server nodes in a cluster
- Two edge nodes
- Synchronization between the edges
- Streaming between edges and core servers
- SecureTransport, non-root install (version: 5.5, any update)
- All available Axway Plugins (version: latest)
- Initial ST configuration
- Additional configuration such as repository encryption
- Base ST tuning

### Security

These configuration files and plays all use plain text passwords and do not encrypt sensitive data for demonstration purposes.

To build at customer's sites, in production or using any sensitive information, you must update the playbooks to use Ansible Vault


## 2. Prerequistes

- ansible [core 2.14.3]
- Python 3.11 on the machine where ansible is installed
- ansible & python prerequisites installed

> These playbooks are written with:
> 
> ansible [core 2.14.3]
> 
> config file = ~/Library/CloudStorage/ansible.cfg
> 
> configured module search path = ['~/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
> 
>  ansible python module location = /Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages/ansible
> 
>  ansible collection location = ~/.ansible/collections:/usr/share/ansible/collections
> 
>  executable location = /Library/Frameworks/Python.framework/Versions/3.11/bin/ansible
> 
>  python version = 3.11.2 (v3.11.2:878ead1ac1, Feb  7 2023, 10:02:41) 
> 
> [Clang 13.0.0 (clang-1300.0.29.30)] (/Library/Frameworks/Python.framework/Versions/3.11/bin/python3.11)
> 
>  jinja version = 3.1.2
> 
>  libyaml = True

### Servers

You need a total of 6 host machines to run these playbooks.
All need to run RHEL 8

> The release I have been testing with is:

> NAME="Red Hat Enterprise Linux"

> VERSION="8.7 (Ootpa)"

> ID="rhel"

> ID_LIKE="fedora"

> VERSION_ID="8.7"

> Red Hat Enterprise Linux release 8.7 (Ootpa)
## 3. Before you begin

### Pull this repository

### Update inventory
- Update the inventory file with your password and hostnames
- rename the sample file to inventory.ini

### Update the variables

Open the file `files/external_vars.yml` and update the variables with all relevant information
Open the file `files/services_vars.yml` and  update the values to indicate which services you want to enable; where; and how much memory to allocate

### Upload your licenses

Place both CORE and FEATURES licenses under `files/licenses/`
### Decide which playbooks you want to run

There is a master playbook that runs each of the roles or playbooks in order. If you want to skip parts of the configuration, 
comment out the roles or playbooks you don't want to run. 
Additionally, you can choose to run or skip specific tasks, using the Ansible tasks. 
More information is available here: https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_tags.html

The list of playbooks and roles that will run by default is:

- `storage_install` [playbook]: Installs the nfs-server binaries, configures the server and exports the shared folder
- `postgres-config` [role]: Installs and configures the shared database
- `os_install` [playbook]: Installs and configures all RHEL 8 prerequisites for ST
- `st_install` [playbook]: Downloads and installs the ST software, plugins and services
- `st_configuration` [role]: Configures streaming, synchronization, and ST initial configuration
- `st_tuning`[role]: Applies the base ST tuning (memory allocation, c3p0 and relevant server configuration parameters)

## 4. Build all


Run this to install

```bash
ansible-playbook st_deploy_master.yml
```


It will connect to the configured servers and install all the software. It will also start the appropriate services.


## Authors
- [Hristina Stoykova](mailto:hstoykova@axway.com)