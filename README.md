# kubectl (Ansible Role)

[![CI](https://github.com/averagebit/ansible-role-kubectl/workflows/CI/badge.svg?event=push)](https://github.com/averagebit/ansible-role-kubectl/actions?query=workflow%3ACI)

## Description

Ansible role to install [kubectl](https://kubernetes.io/docs/reference/kubectl/kubectl/).

## Requirements

The role was developed and tested with the following Ansible versions.

| Name                                                   | Version     |
| ------------------------------------------------------ | ----------- |
| [ansible](https://pypi.org/project/ansible-base/)      | `>= 2.9.13` |
| [ansible-base](https://pypi.org/project/ansible-base/) | `>= 2.10.1` |
| [ansible-core](https://pypi.org/project/ansible-core/) | `>= 2.11.2` |

## Platforms

The role was tested on the following distributions and releases.

| Name   | Version |
| ------ | ------- |
| Ubuntu | `jammy` |

## Installation

`ansible-galaxy install averagebit.kubectl` will install the latest
stable release.

`ansible-galaxy install -r requirements.yml` will install the role
from a requirements file.

```yaml
# requirements.yml
---
roles:
  - name: averagebit.kubectl
    version: 1.0.0
```

## Variables

- `kubectl_os`
  - Default: `"linux"`
  - Description: The OS target for the binary.
- `kubectl_version`
  - Default: `"latest"`
  - Description: The version of the binary can be a specific version such as: `"1.25.0"`.
- `kubectl_owner`
  - Default: `"root"`
  - Description: The owner of the installed binary.
- `kubectl_group`
  - Default: `"root"`
  - Description: The group of the installed binary.
- `kubectl_mode`
  - Default: `"0755"`
  - Description: The permissions of the installed binary.
- `kubectl_bin_dir_mode`
  - Default: `"0755"`
  - Description: The permissions of the binary directory.
- `kubectl_bin_dir`
  - Default: `"/usr/local/share/kubectl"`
  - Description: The directory to install the binary in.
- `kubectl_bin_path`
  - Default: `"{{ kubectl_bin_dir }}/kubectl"`
  - Description: The full path to the binary.
- `kubectl_link_path`
  - Default: `"/usr/local/bin/kubectl"`
  - Description: The symlink path created to the binary.
- `kubectl_repo_url`
  - Default: `"https://dl.k8s.io"`
  - Description: The URL to the repository.
- `kubectl_file_url`
  - Default: `"{{ kubectl_repo_url }}/release/v{{ kubectl_version }}/bin/{{ kubectl_os }}/{{ kubectl_architecture }}/kubectl"`
  - Description: The URL to the file.
- `kubectl_version_url`
  - Default: `"https://dl.k8s.io/release/stable.txt"`
  - Description: The URL to fetch the latest version from.
- `kubectl_checksum_url`
  - Default: `"{{ kubectl_file_url }}.sha256"`
  - Description: The URL to the checksum of the file.
- `kubectl_architecture`
  - Default: `"{{ kubectl_architecture_map[ansible_architecture] }}"`
  - Description: The architecture target for the binary.
- `kubectl_architecture_map`
  - Default: `{"aarch": "arm64", "aarch64": "arm64", "amd64": "amd64", "arm64": "arm64", "armhf": "armhf", "armv7l": "armhf", "ppc64le": "ppc64le", "s390x": "s390x", "x86_64": "amd64"}`
  - Description: The architecture map used to set the correct name
    according to the repository binary naming.

## Usage

```yaml
# playbook.yml
- hosts: servers
  roles:
    - role: averagebit.kubectl
      become: true # required unless specified at the playbooks top level
      tags: kubectl # (optional) convenience tag
  vars:
    - kubectl_version: latest # or a specific version such as: 1.25.0
```

## Legal

Copyright 2022 averagebit <[averagebit@pm.me](mailto:averagebit@pm.me)>

Licensed under the Apache License, Version 2.0 (the "License"); you may
not use this file except in compliance with the License. You may obtain
a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
