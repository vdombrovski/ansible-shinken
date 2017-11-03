Shinken playbook
===

This role allows for a modular install of Shinken.

Features:
---

- Customizable hosts, services, contacts
- Mods:
    - openio_import: Compatibility module with openio services
    - influxdb: Push results into influxdb
    - redis-retention: Temporary store results in redis
    - forward_nagios: forward alerts to nagios NSCA server (requires Nagios + ng-nsca-server)
    - named-pipe: linux pipe for passing commands to shinken
    - webui: WIP, not yet available

Requirements
---

This role requires ansible and git to be installed

List of compatible distros:
- Ubuntu 16.04 (xenial)
- CentOS 7 (openio_import module is not available)

Example:
---

An example playbook can be found [here](./example.yml)


License
---

GPL2+
