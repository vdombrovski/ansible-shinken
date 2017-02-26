Shinken
=======

This role is to install Shinken and configure your hosts and services.
Currently at an early stage and not quite ready for other peoples networks.

virtualenv support was coded but since shinken doesn't play nicely in a
virtualenv those code paths have been disabled.

Requirements
------------


Role Variables
--------------

The following are set via defaults/main.yml *and currently usable* (some things
have not been implemented yet)


    # How should things be installed, 'packages' or 'pip'
    shinken_install_from: 'pip'

    # Path of broker configuration
    shinken_config_broker: /etc/shinken/brokers/

    # Do we want the web UI?
    shinken_enable_web_ui2: true

    # List of modules to enable in the broker. 'webui2' enables web interface.
    shinken_broker_modules: 'webui2'

    # Shinken web UI configuration, only changed items are here so far.
    shinken_broker_webui_host: 0.0.0.0
    shinken_broker_webui_port: 7767
    shinken_broker_webui_auth_secret: SiteSpecificAuthSecret # MUST BE CHANGED

    # Where are contacts placed
    shinken_config_contacts: /etc/shinken/contacts/

    # Details of the available contacts (include password for internal authentication)
    # This example shows both expanded and single line list format for admin and guest.
    shinken_contacts:
     - contact_name: 'admin'
       email: 'shinken@localhost'
       password: 'password'
       is_admin: 1
       expert: 1
       can_submit_commands: 1
     - { contact_name: 'guest', email: 'guest@localhost', password: 'password'}

    # where does service configuration go?
    shinken_config_services: /etc/shinken/services/

    # What services are we monitoring? which hostgroups do they apply to?
    shinken_services:
     - { service_description: 'ping test', command: 'check_ping', hostgroup_name: [] }

    # Where should the host configuration go
    shinken_config_hosts: /etc/shinken/hosts/
    shinken_config_hostgroups: /etc/shinken/hostgroups/

    # Which hosts are we monitoring? NOTE: hostgroups list is a required field, even if empty.
    shinken_hosts:
     - { host_name: 'router.local' , hostgroups: [ 'infrastructure' ]}
     - { host_name: 'modem.local', parent: 'router.local', hostgroups: [ 'appliances' ] }
     - { host_name: 'shinken.io', parent: 'modem.local', hostgroups: [ 'remote-server', 'web-server' ] }


Dependencies
------------

This module requires epel on centos for virtualenvs and shinken packages. Roles
to perform these tasks are below, but any roles / tasks to organise the
dependenies will work.

    ansible-galaxy install wtanaka.virtualenv
    ansible-galaxy install geerlingguy.repo-epel

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: shinken
      roles:
         - { role: goetz.shinken, shinken_broker_modules: webui }

License
-------

GPL2+

Author Information
------------------

Issues or feedback can be reported to the author at karl@kgoetz.id.au; please
prefix the subject with 'ansible' or 'role'.

