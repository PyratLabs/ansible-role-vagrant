# Ansible Role: vagrant

Ansible role for installing vagrant.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-vagrant.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-vagrant)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - SUSE/openSUSE 15
  - Ubuntu 18.04 LTS

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                          | Description                                                                  | Default Value    |
|-----------------------------------|------------------------------------------------------------------------------|------------------|
| `vagrant_version`                 | Use a specific version of vagrant, eg. `2.2.6`. Specify `false` for latest.  | `false`          |
| `vagrant_install_os_dependencies` | Allow role to install OS dependencies.                                       | `false`          |
| `vagrant_projects_dir`            | Directory to put Vagrant projects. Specify `false` to skip.                  | `$HOME/projects` |
| `vagrant_projects`                | List of Vagrant projects to be cloned with `git`. See notes.                 | _NULL_           |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing the latest vagrant version globally:

```yaml
---
- hosts: workstation
  become: true
  vars:
    vagrant_projects_dir: /opt/vagrant/projects
  roles:
    - role: xanmanning.vagrant
```

### Note about `vagrant_projects`

This is a list of git repositories to be cloned into the projects directory.
If this is empty, no projects will be cloned.

Below is an example of a project:

```yaml
vagrant_projects:
    - name: vagrant-examples                             # Directory name to clone into
      repo: git@github.com:patrickdlee/vagrant-examples  # Repository to clone
      update_repo: true                                  # Always update local copy of repo
      version:  master                                   # Check out this version of the repo
      force: false                                       # Discard any existing working copy of the repo
      key_file: "{{ ansible_user_dir }}/.ssh/id_rsa"     # Key file to use to clone the repo
      recursive: true                                    # Include submodules in clone
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
