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
- Change the Edges install parameters to accomodate the modernized SC
- Validated install with RHEL 9
- Changed the DB version to PostgreSQL 16