Add LDAP Support
================

**(Optional, but recommended)**

LDAP support allows for your users to log in using their local username and
password. It also removes the need for the sys admin to keep updating the
``.htpasswd`` file.

Requirements:

- an LDAP server preferably with SSL support (``cts06.osc.edu:636``)

#. Install the necessary Apache module to use LDAP:

   .. code-block:: sh

      sudo yum install httpd24-mod_ldap.x86_64

#. Update the Apache config with LDAP Basic Authentication support.

   .. code-block:: sh

      cd ~/ood/src/ood-portal-generator

#. Create or edit the ``config.yml`` as such:

   .. code-block:: yaml

      ---

      auth:
        - 'AuthType Basic'
        - 'AuthName "private"'
        - 'AuthBasicProvider ldap'
        - 'AuthLDAPURL "ldaps://cts06.osc.edu:636/ou=People,ou=hpc,o=osc?uid" SSL'
        - 'AuthLDAPGroupAttribute memberUid'
        - 'AuthLDAPGroupAttributeIsDN off'
        - 'RequestHeader unset Authorization'
        - 'Require valid-user'

   .. note::

      For documentation on LDAP directives please see:
      https://httpd.apache.org/docs/2.4/mod/mod_authnz_ldap.html

#. Re-build the Apache config:

   .. code-block:: sh

      scl enable rh-ruby22 -- rake

#. Copy it over to the default location:

   .. code-block:: sh

      sudo scl enable rh-ruby22 -- rake install

#. Restart the Apache server:

   .. code-block:: sh

      sudo service httpd24-httpd restart

Close your browser so that you are properly logged out. Then open your browser
again and access the portal. You should now be able to authenticate with your
local username and password.