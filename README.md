[![Build_Status](https://travis-ci.org/singleplatform-eng/ansible-role-systemd-service.svg?branch=master)](https://travis-ci.org/singleplatform-eng/ansible-role-systemd-service)
ansible-role-systemd-service
=========

This role is designed to provide all the needed directories, config files, service units, and service handlers for managing generic services using systemd on Ubuntu. It does not manage the installation of any service dependencies.


Requirements 
------------

Systemd
ansible 2.5+

Role Variables
--------------
Defaults
```
service_config_dir: "/etc/{{service_name}}"
service_systemd_service_dir: /etc/systemd/system
service_log_dir: "/var/log/{{service_name}}"

```

Required Vars
```
service (dict) - dictionary defining the contents of the environmentfile and the unit, service, and install sections of the service unit. The unit_config, service_config, and install_config keys must contain the required directives for a functional system service unit or the unit will be malformed. 

service_name (string) - The name of the service. This needs to be passed in via a role var and cannot be interpreted from any variable set via host identity, i.e. group_vars. By default this will be used for the name of the service unit e.g. example.service and the directory where the environment file and service unit are written. With the default service_config_dir this would be /etc/{{service_name}}/{{service_name}}.env and /etc/{{service_name}}/{{service_name}}.service.

Note that environment variables that need to be enclosed by quotes should have them explicitly defined.
```

Optional Vars
```
service_config_dir (string, /etc/{{service_name}}) - The directory where the environment file and service unit definition will be written.

service_systemd_service_dir (string, /etc/systemd/system) - The systemd directory the service unit will be symlinked into.

service_log_dir (string, /var/log/{{service_name}}) - The log directory for the service. This will be owned by the user and group defined in service_config or root if no user has been configured.
```

Dependencies
------------

None

Example Playbook
----------------

```
- hosts: localhost
  remote_user: root
  vars:
    service_name: example # NOTE: This must be passed to the role as a string for handlers to function properly
    service:
      unit_config: {}
      environment:
        EXAMPLE_ARGS: 'testing'
      service_config:
        ExecStart: /bin/echo "${EXAMPLE_ARGS}"
        Type: oneshot
        EnvironmentFile: "{{service_config_dir}}/{{service_name}}.env"
      install_config: {}
  roles:
    - { role: role_under_test }
  tasks:
    - name: Handle example
      command: /bin/true
      changed_when: false
      notify: "Start {{service_name}}.service"
```
Author Information
------------------

[SinglePlatform Engineering](http://engineering.singleplatform.com/)

License
-------

BSD 3-Clause
