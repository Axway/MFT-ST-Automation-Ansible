# SecureTransport Install, Configuration, and Tuning


## 1. Introduction

### Purpose

These playbooks are intended to be used:
* To deploy in TEST environments
* As a sample 
* To update existing ST deployments 

They have not been tested for production purposes. 
Use them at your own risk and make sure to validate all plays and tasks before deploying elsewhere.

### Deployment

When all plays  run, they will install and configure SecureTransport Enterprise Cluster deployment with:

- PostgreSQL database (version: 16)
- NFS storage to share between the core nodes (version: 3)
- OS prerequisites for ST Linux install (version: RHEL 9) -> valid for ST version Sept 2024 & later
- Two core server nodes in a cluster
- Two edge nodes
- Synchronization between the edges
- Streaming between edges and core servers
- SecureTransport, non-root install (version: 5.5, Dec 2024 & later)
- All available Axway Plugins (version: latest)
- Initial ST configuration
- Additional configuration such as repository encryption
- Base ST tuning

Additionally, you can opt to run the st_update playbook to update your existing install

### Security

These configuration files and plays all use plain text passwords and do not encrypt sensitive data for demonstration purposes.

To build at customer's sites, in production or using any sensitive information, you must update the playbooks to use Ansible Vault


## 2. Prerequisites

> [!CAUTION]
> Ansible 2.17 dropped support for Python 3.6, as a result, 2.16 will be the last version that works out of the box with RHEL 8

- ansible [core 2.14.3]
- Python 3.11 on the machine where ansible is installed
- ansible & python prerequisites installed


#### These playbooks are written and validated with:
> 
> ansible [core 2.16.14]
> 
> configured module search path = ['~/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
>
>  config file = ~/MFT-ST-Automation-with-Ansible-example/ansible.cfg
> 
>  configured module search path = ['~/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
> 
>  ansible python module location = /usr/local/lib/python3.11/site-packages/ansible
> 
>  ansible collection location = ~/.ansible/collections:/usr/share/ansible/collections
> 
>  executable location = /usr/local/bin/ansible
> 
>  python version = 3.11.11 (main, Dec  3 2024, 17:20:40) [Clang 16.0.0 (clang-1600.0.26.4)] (/usr/local/opt/python@3.11/bin/python3.11)
> 
>  jinja version = 3.1.5
> 
> libyaml = True

### Servers

You need a total of 6 host machines to run the installation playbooks.
All need to run RHEL 9, Rocky Linux 9, or RHEL 8

#### The release I have been testing with is:

> NAME="Red Hat Enterprise Linux"
>
> VERSION="9.3 (Plow)"
>
> ID="rhel"
>
> ID_LIKE="fedora"
>
> VERSION_ID="9.3"
>
> "Red Hat Enterprise Linux 9.3 (Plow)
> 
## 3. Before you begin

### Pull this repository

### Install Galaxy and Python3 requirements

<kbd>ansible-galaxy collection install -r galaxy-requirements.yml</kbd>

<kbd>pip install -r requirements.txt</kbd>


### Update inventory
- Update the inventory file with your password and hostnames
- rename the sample file to inventory.ini or pass it to ansible with -i my-filename.ini

### Update the variables

Open the file `files/external_vars.yml` and update the variables with all relevant information
Open the file `files/services_vars.yml` and  update the values to indicate which services you want to enable; where; and how much memory to allocate
Open the file `files/download_links.yml` and  update the values to indicate which files to use for install/update and where are they located

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
- `os_install` [role]: Installs and configures all RHEL 8 prerequisites for ST
- `st_install` [playbook]: Downloads and installs the ST software, plugins and services
- `st_configuration` [role]: Configures streaming, synchronization, and ST initial configuration
- `st_tuning`[role]: Applies the base ST tuning (memory allocation, c3p0 and relevant server configuration parameters)

Additionally, if you want to use the update role:

- `st_update`[role]: Applies the specified ST update


## 4. Build all


Run this to install

```bash
ansible-playbook st_deploy_master.yml
```

Run this to update

```bash
ansible-playbook st_update.yml
```

It will connect to the configured servers and install all the software. It will also start the appropriate services.


## Authors
- [Hristina Stoykova](mailto:hstoykova@axway.com)