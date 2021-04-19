Ansible Role: tftpd
====================

An Ansible role that installs and configures **tftpd**.

Table of Contents
-----------------

<!-- toc -->

- [Requirements](#requirements)
- [Role Variables](#role-variables)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
  * [Top-Level Playbook](#top-level-playbook)
  * [Role Dependency](#role-dependency)
- [License](#license)
- [Author Information](#author-information)

<!-- tocstop -->

Requirements
------------

- Ansible 2+

Role Variables
--------------

Whether to enable the service or not:

```yml
tftpd_service: no
```

The root directory that is served:

```yml
tftpd_root: '/var/lib/tftpboot'
```

The file containing file name mappings:

```yml
tftpd_mapfile: '/etc/tftp-mappings.conf'
```

The mappings themselves are unset by default. You can define your own list of mappings, e.g. to replace backslashes with forward slashes:

```yml
tftpd_mappings:
  - operation: 'rg'
    regex: '\\'
    replacement: '/'
```

Dependencies
------------

- [idiv-biodiversity.xinetd][]

Example Playbook
----------------

Add to `requirements.yml`:

```yml
---

- src: idiv-biodiversity.tftpd

...
```

Download:

```console
$ ansible-galaxy install -r requirements.yml
```

### Top-Level Playbook

Write a top-level playbook:

```yml
---

- name: head server
  hosts: head

  roles:
    - role: idiv-biodiversity.tftpd
      tags:
        - tftpd

...
```

### Role Dependency

Define the role dependency in `meta/main.yml`:

```yml
---

dependencies:

  - role: idiv-biodiversity.tftpd
    tags:
      - tftpd

...
```

License
-------

MIT

Author Information
------------------

This role was created in 2018 by [Christian Krause][author] aka [wookietreiber at GitHub][wookietreiber], HPC cluster systems administrator at the [German Centre for Integrative Biodiversity Research (iDiv)][idiv].


[author]: https://www.idiv.de/en/groups_and_people/employees/details/61.html
[idiv]: https://www.idiv.de/
[wookietreiber]: https://github.com/wookietreiber
[idiv-biodiversity.xinetd]: https://galaxy.ansible.com/idiv-biodiversity/xinetd/
