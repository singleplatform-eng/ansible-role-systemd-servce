
SErvice
=========

This role is designed to provide all the needed directories, config files, service units, and service handlers for managing generic services using systemd on Ubuntu. It does not manage the installation of any service dependencies.


Requirements 
------------

Ubuntu 18.04+


Role Variables
--------------
Defaults
```
TODO
```
Required Vars
```
TODO
```

Dependencies
------------

None

Example Playbook
----------------

    - hosts: localhost
      vars:
      roles:
         - { role: ansible-role-systemd-service }

Author Information
------------------

[SinglePlatform Engineering](http://engineering.singleplatform.com/)

License
-------

BSD 3-Clause
