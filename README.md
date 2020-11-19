# ansible-role-evilginx2

[![Ansible Role Name](https://img.shields.io/ansible/role/51897?label=Role%20Name&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/51897?label=Ansible%20Quality%20Score&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Ansible Role Downloads](https://img.shields.io/ansible/role/d/51897?label=Ansible%20Role%20Downloads&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx2)
[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/ansible-role-evilginx2/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/ansible-role-evilginx2/actions)

A Ansible role that deploys the evilginx2 application and starts it in a tmux session. 

## Requirements

None.

## Variables

`defaults/main.yml`

| Variable                       | Description                                                                                    | Default value                                                                               |
| ------------------------------ | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| evilginx2_version              | The version of evilginx2 to install.                                                           | 2.4.0                                                                                       |
| evilginx2_platform             | The platform type.                                                                             | linux                                                                                       |
| evilginx2_arch                 | The architecture.                                                                              | amd64                                                                                       |
| evilginx2_sha256               | The sha256 sum of the downloaded file that matches the version, platform and arch combination. | sha256:595a77ddfb6f674bd5bc1c297ae912f5ebf6ba218a2f857ff46b7b37d1a9678b                     |
| evilginx2_download_destination | The download destination of the gophish release tar.gz file.                                   | /tmp/evilginx2-{{ evilginx2_version }}-{{ evilginx2_platform }}-{{ evilginx2_arch }}.tar.gz |
| evilginx2_install_destination  | The install destination of gophish.                                                            | /opt                                                                                        |

## Dependencies

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
