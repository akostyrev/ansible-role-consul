consul
=======

Installs and configures Consul

Requirements
------------

This role requires Ansible 1.4 or higher.

Role Variables
--------------

See [defaults/main.yml](defaults/main.yml) for a list and description of
variables used in this role.

Dependencies
------------

- kbrebanov.unzip

Example Playbook
----------------

Install Consul
```
- hosts: all
  roles:
    - { role: kbrebanov.consul }
```

Install Consul specifying version and checksum
```
- hosts: all
  roles:
    - { role: kbrebanov.consul, consul_version: 0.4.1, consul_sha256sum: 2cf6e59edf348c3094c721eb77436e8c789afa2c35e6e3123a804edfeb1744ac }
```

Install Consul with webui
```
- hosts: all
  roles:
    - { role: kbrebanov.consul, consul_webui: true }
```

Install Consul as a server
```
- hosts: all
  roles:
    - { role: kbrebanov.consul, consul_server: true }
```

Install Consul and configure a service
```
- hosts: all
  vars:
    consul_services:
      - name: "web"
        tags:
          - "rails"
        port: 80
  roles:
    - kbrebanov.consul
```

Install Consul and configure a check
```
- hosts: all
  vars:
    consul_checks:
      - name: "Web check"
        http: "http://localhost"
        interval: "10s"
        timeout: "1s"
  roles:
    - kbrebanov.consul
```

Install Consul and configure a watch
```
- hosts: all
  vars:
    consul_watches:
      - type: "service"
        service: "redis"
        handler: "/usr/bin/my-service-handler.sh"
  roles:
    - kbrebanov.consul
```

License
-------

BSD

Author Information
------------------

Inspired by:
- Kevin Brebanov's [consul role](https://github.com/kbrebanov/ansible-consul)
- Brian Shumate's [consul role](https://github.com/brianshumate/ansible-consul)
