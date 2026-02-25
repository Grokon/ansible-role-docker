# ansible-role-docker

[![Molecule Test Status](https://github.com/Grokon/ansible-role-docker/actions/workflows/molecule.yml/badge.svg?branch=master)](https://github.com/Grokon/ansible-role-docker/actions/workflows/molecule.yml)
[![GitHub release](https://img.shields.io/github/release/Grokon/ansible-role-docker.svg)](https://github.com/Grokon/ansible-role-docker/release)
[![GitHub license](https://img.shields.io/github/license/Grokon/ansible-role-docker.svg)](https://github.com/Grokon/ansible-role-docker/blob/master/LICENSE)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-grokon.docker-blue.svg)](https://galaxy.ansible.com/grokon/docker/)
[![Downloads](https://img.shields.io/ansible/role/d/grokon.docker)](https://galaxy.ansible.com/grokon/docker/)

## Example Playbook

```yaml
- hosts: all
  roles:
    - grokon.docker
```

An Ansible Role that installs Docker on Debian

## Table of content

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [docker__apt_key](#docker__apt_key)
  - [docker__apt_key_url](#docker__apt_key_url)
  - [docker__apt_repository](#docker__apt_repository)
  - [docker__channel](#docker__channel)
  - [docker__daemon_json](#docker__daemon_json)
  - [docker__default_daemon_json](#docker__default_daemon_json)
  - [docker__package_dependencies](#docker__package_dependencies)
  - [docker__packages](#docker__packages)
  - [docker__registries](#docker__registries)
  - [docker__state](#docker__state)
  - [docker__version](#docker__version)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.17`

## Default Variables

### docker__apt_key

Path to store Docker's GPG signing key.

#### Default value

```YAML
docker__apt_key: /etc/apt/keyrings/docker.asc
```

### docker__apt_key_url

URL to download Docker's GPG signing key.

#### Default value

```YAML
docker__apt_key_url: https://download.docker.com/linux/debian/gpg
```

### docker__apt_repository

Docker APT repository definition in DEB822 format.
Written to /etc/apt/sources.list.d/docker.sources.

#### Default value

```YAML
docker__apt_repository: |
  Types: deb
  URIs: https://download.docker.com/linux/debian
  Suites: {{ ansible_facts['distribution_release'] }}
  Components: {{ docker__channel }}
  Signed-By: {{ docker__apt_key }}
```

### docker__channel

Docker repository channel to use (e.g. stable, test, nightly).

#### Default value

```YAML
docker__channel: stable
```

### docker__daemon_json

Custom Docker daemon configuration (dict).
Merged on top of docker__default_daemon_json, overriding matching keys.

#### Default value

```YAML
docker__daemon_json: {}
```

### docker__default_daemon_json

Default Docker daemon configuration (dict).
Merged with docker__daemon_json and rendered as /etc/docker/daemon.json.

#### Default value

```YAML
docker__default_daemon_json:
  log-driver: json-file
  log-opts:
    max-size: 10m
    max-file: '5'
    tag: "{{ '{{.ImageName}}|{{.Name}}' }}"
```

### docker__package_dependencies

List of APT packages required before installing Docker.

#### Default value

```YAML
docker__package_dependencies:
  - ca-certificates
  - curl
  - gnupg
```

### docker__packages

List of Docker APT packages to install.

#### Default value

```YAML
docker__packages:
  - docker-ce
  - docker-ce-cli
  - containerd.io
  - docker-compose-plugin
  - docker-buildx-plugin
```

### docker__registries

List of docker registries to configure.

#### Default value

```YAML
docker__registries: []
```

#### Example usage

```YAML
docker__registries:
 - registry_url: "https://index.docker.io/v1/"
   username: "your_docker_hub_username"
   password: "your_docker_hub_password"
   email: "your_docker_hub@emailaddress.com"
   reauthorize: false
   config_path: "$HOME/.docker/config.json"
   state: "present"
```

### docker__state

Desired package state:
- 'present' to install
- 'absent' to uninstall

#### Default value

```YAML
docker__state: present
```

### docker__version

Pin a specific Docker version. Leave empty to install the latest available.
Example: "5:24.0.7-1~debian.12~bookworm"

#### Default value

```YAML
docker__version: ''
```

## Dependencies

None.

## License

MIT

## Author

grokon
