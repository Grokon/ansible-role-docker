# ansible-role-docker

[![Mocelule Test Status](https://github.com/Grokon/ansible-role-docker/actions/workflows/molecule.yml/badge.svg?branch=master)](https://github.com/Grokon/ansible-role-docker/actions/workflows/molecule.yml)
[![GitHub release](https://img.shields.io/github/release/Grokon/ansible-role-docker.svg)](https://github.com/Grokon/ansible-role-docker/release)
[![GitHub license](https://img.shields.io/github/license/Grokon/ansible-role-docker.svg)](https://github.com/Grokon/ansible-role-docker/blob/master/LICENSE)
[![Ansible Galaxy](https://img.shields.io/badge/galaxy-grokon.docker-blue.svg)](https://galaxy.ansible.com/grokon/docker/)
[![Downloads](https://img.shields.io/ansible/role/d/grokon.docker)](https://galaxy.ansible.com/grokon/docker/)

An Ansible Role that installs Docker and docker-compose-plugin on Debian

## Table of content

- [Default Variables](#default-variables)
  - [docker__apt_key](#docker__apt_key)
  - [docker__apt_key_url](#docker__apt_key_url)
  - [docker__apt_repository](#docker__apt_repository)
  - [docker__channel](#docker__channel)
  - [docker__daemon_json](#docker__daemon_json)
  - [docker__default_daemon_json](#docker__default_daemon_json)
  - [docker__edition](#docker__edition)
  - [docker__package_dependencies](#docker__package_dependencies)
  - [docker__packges](#docker__packges)
  - [docker__registries](#docker__registries)
  - [docker__state](#docker__state)
  - [docker__version](#docker__version)
- [Open Tasks](#open-tasks)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### docker__apt_key

#### Default value

```YAML
docker__apt_key: /usr/share/keyrings/docker-archive-keyring.gpg
```

### docker__apt_key_url

#### Default value

```YAML
docker__apt_key_url: https://download.docker.com/linux/debian/gpg
```

### docker__apt_repository

#### Default value

```YAML
docker__apt_repository: |
  deb [arch=amd64 signed-by={{ docker__apt_key }}]
  https://download.docker.com/linux/debian
  {{ ansible_distribution_release }} {{ docker__channel | join(' ') }}
```

### docker__channel

#### Default value

```YAML
docker__channel: [stable]
```

### docker__daemon_json

#### Default value

```YAML
docker__daemon_json: ''
```

### docker__default_daemon_json

#### Default value

```YAML
docker__default_daemon_json: |
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "5",
    "tag": "{% raw %}{{.ImageName}}|{{.Name}}{% endraw %}"
  }
```

### docker__edition

Wanted Docker Edition - can be one of: - 'ce' (Community Edition) - 'ee' (Enterprise Edition)

#### Default value

```YAML
docker__edition: ce
```

### docker__package_dependencies

#### Default value

```YAML
docker__package_dependencies:
  - apt-transport-https
  - ca-certificates
  - curl
  - gnupg
  - software-properties-common
  - lsb-release
```

### docker__packges

#### Default value

```YAML
docker__packges:
  - docker-{{ docker__edition }}
  - docker-{{ docker__edition }}-cli
  - containerd.io
  - docker-compose-plugin
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

Install or remove docker_package : - 'present' for install - 'absent' to uninstall

#### Default value

```YAML
docker__state: present
```

### docker__version

#### Default value

```YAML
docker__version: ''
```


## Open Tasks

- (improvement): Add doc for all variables
- (improvement): Add description for all tasks

## Dependencies

None.

## License

MIT

## Author

grokon
