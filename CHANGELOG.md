### Updates from 07/05/23  [hstoykova]
- Updated the inventory sample with the correct variables
- Set more restrictive (0750) permissions on the new directories
- Disabled the SELinux policies as they are not currently needed

### Updates from 02/12/24
- exposed the SSL_ADMIN_PORT variable to allow customization of the admin port
- Fixed owner/group parameters in the os_install to resolve to the variables instead of the hardcoded 'axway'
- Changed the posgres tablespace owner to {{ DB_USER }}
- Refactored the install properties files generation
- Parameterized the JRE version

### Updates from 01/24/25
- Removed the 32-bit library requirements and the MariaDB requirements for edges
- Added a task to stop firewalld before mounting. In production, please add nfs:tcp as a firewall exception instead
- Changed the jre pattern from jre1 to jre to account for jre2+
- Changed the Edges install parameters to accomodate the modernized SC
- Validated installation with RHEL 9
- Changed the DB version to PostgreSQL 16
- Optimized tablespace creation
- Moved the download links to a separate file

### Updates from 01/29/25
- Supressed interpreter warnings by adding interpreter_python=auto_silent
- Added configuration to create service unit files
- Added configuration to enable monitord
- Added configuration to allow using a preinstalled/preconfigured DB
- Updated the REST API requests to reuse the cookies and CSRF token upon login
- Created tasks to deploy service unit files

### Updates from 02/05/2025
- Published a playbook (st_update.yml) and a role (st_update) to install an update for ST