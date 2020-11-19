# ansible-role-evilginx2

[![Ansible Role Name](https://img.shields.io/ansible/role/51897?label=Role%20Name&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/51897?label=Ansible%20Quality%20Score&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Ansible Role Downloads](https://img.shields.io/ansible/role/d/51897?label=Ansible%20Role%20Downloads&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/ansible-role-evilginx2/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/ansible-role-evilginx2/actions)


## Requirements

None.

## Variables

`defaults/main.yml`

| Variable | Description | Default value |
| -------- | ----------- | ------------- |

## Dependencies

[geerlingguy.pip](https://github.com/geerlingguy/ansible-role-pip)
[robertdebock.update_package_cache](https://github.com/robertdebock/ansible-role-update_package_cache)
[robertdebock.core_dependencies](https://github.com/robertdebock/ansible-role-core_dependencies)

## Example Playbooks

### Default role installation

```yaml
---
- hosts: evilginx2_hosts
  become: yes
  roles:
    - role: justin_p.evilginx2
```

### Deployment playbook

This playbook is tested as part of the role CI.

```yaml
---
- name: Deploy Evilginx2
  hosts: evilginx2_hosts
  tasks:
    - include_role:
        name: robertdebock.update_package_cache
      tags: molecule-idempotence-notest
    - include_role:
        name: robertdebock.bootstrap
    - include_role:
        name: robertdebock.update
      vars:
        update_reboot: no
    - include_role:
        name: robertdebock.firewall
      vars:
        firewall_services:
          - name: ssh
          - name: http
          - name: https
    - include_role:
        name: robertdebock.hostname
      vars:
        hostname: evilginx.local
        hostname_reboot: no
    - include_role:
      name: justin_p.evilginx2
```

## Local Development

This role includes molecule that will spin up a local docker environment to deploy, configure and test this role.

Development requirements:

- Docker
- Molecule
- Molecule-docker
- yamllint
- ansible-lint

or simply use a VM with [this](https://github.com/justin-p/ansible-terraform-workstation) configuration.

## License

MIT

## Authors

Justin Perdok ([@justin-p](https://github.com/justin-p/)), Orange Cyberdefense

## Contributing

Feel free to open issues, contribute and submit your Pull Requests. You can also ping me on Twitter ([@JustinPerdok](https://twitter.com/JustinPerdok))
