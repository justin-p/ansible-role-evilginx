# ansible-role-gophish

[![Ansible Role Name](https://img.shields.io/ansible/role/51375?label=Role%20Name&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/gophish)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/51375?label=Ansible%20Quality%20Score&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/gophish)
[![Ansible Role Downloads](https://img.shields.io/ansible/role/d/51375?label=Ansible%20Role%20Downloads&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/gophish)
[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/ansible-role-chisel/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/ansible-role-gophish/actions)

A Ansible role that deploys the [gophish](https://github.com/gophish/gophish) application as a systemd service. This role does not install any mail services for relaying or web services for proxing gophish. You are expected to handle this in your own playbooks, see [Deployment playbook](#Deployment-playbook) for an example.

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
