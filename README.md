# ansible-role-evilginx

[![Ansible Role Name](https://img.shields.io/ansible/role/51897?label=Role%20Name&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/51897?label=Ansible%20Quality%20Score&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx)
[![Ansible Role Downloads](https://img.shields.io/ansible/role/d/51897?label=Ansible%20Role%20Downloads&logo=ansible&style=flat-square)](https://galaxy.ansible.com/justin_p/evilginx)
[![Github Actions](https://img.shields.io/github/workflow/status/justin-p/ansible-role-evilginx/CI?label=Github%20Actions&logo=github&style=flat-square)](https://github.com/justin-p/ansible-role-evilginx/actions)

A Ansible role that clones and builds the [evilginx](https://github.com/kgretzky/evilginx) application, clones a (configurable) additional [phishlet repository](https://github.com/An0nUD4Y/Evilginx2-Phishlets) and starts evilginx in a tmux session.

## Requirements

None.

## Variables

`defaults/main.yml`

| Variable                               | Description                                                                | Default value                                                                                  |
| -------------------------------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| evilginx_repo_author                   | Used to built evilginx_url, can be updated to a alternative repo           | `kgretzky`                                                                                     |
| evilginx_repo_name                     | Used to built evilginx_url,can be updated to a alternative repo            | `evilginx2`                                                                                    |
| evilginx_version                       | Tag/Release/Branch to install                                              | `v3.1.0`                                                                                       |
| evilginx_url                           | URL to clone evilginx repo from                                            | `"https://github.com/{{ evilginx_repo_author }}/{{ evilginx_repo_name }}"`                     |
| evilginx_install_destination           | Installation directory                                                     | `/opt/{{ evilginx_repo_name }}`                                                                |
| evilginx_phishlets_repo_author         | Used to built evilginx_phishlets_url, can be updated to a alternative repo | `An0nUD4Y`                                                                                     |
| evilginx_phishlets_repo_name           | Used to built evilginx_phishlets_url, can be updated to a alternative repo | `Evilginx2-Phishlets`                                                                          |
| evilginx_phishlets_version             | Tag/Release/Branch to install                                              | `master`                                                                                       |
| evilginx_phishlets_url                 | URL to clone evilginx phishlet repo from                                   | `"https://github.com/{{ evilginx_phishlets_repo_author }}/{{ evilginx_phishlets_repo_name }}"` |
| evilginx_phishlets_install_destination | Location where phishlets will be installed                                 | `"/opt/{{ evilginx_phishlets_repo_name }}"`                                                    |
## Dependencies

[robertdebock.update_package_cache](https://github.com/robertdebock/ansible-role-update_package_cache)

[robertdebock.core_dependencies](https://github.com/robertdebock/ansible-role-core_dependencies)

## Example Playbooks

### Default role installation

```yaml
---
- hosts: evilginx_hosts
  become: yes
  tasks:
    - name: Run 'gantsign.golang'-role
      ansible.builtin.include_role:
        name: gantsign.golang
      vars:
        golang_install_dir: /opt/go

    - name: Run 'justin_p.evilginx'-role
      ansible.builtin.include_role:
        name: justin_p.evilginx
        apply:
          environment:
            PATH: "{{ ansible_env.PATH }}:/opt/go/bin"
```

### Deployment playbook

This playbook is tested as part of the role CI.

```yaml
---
- name: Deploy evilginx
  hosts: evilginx_hosts
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
         name: gantsign.golang
        vars:
          golang_install_dir: /opt/go
    - include_role:
        name: justin_p.evilginx
        apply:
          environment:
            PATH: "{{ ansible_env.PATH }}:/opt/go/bin"
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
