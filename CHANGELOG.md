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