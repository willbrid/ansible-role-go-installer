Ansible-role-go-installer
=========

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/willbrid/ansible-role-go-installer/blob/main/LICENSE) [![CI](https://github.com/willbrid/ansible-role-go-installer/actions/workflows/ci.yml/badge.svg)](https://github.com/willbrid/ansible-role-go-installer/actions/workflows/ci.yml)

The **ansible-role-go-installer** role allows you to install the **Go** development tool on Linux environments. It automatically detects the existing version of **Go** (if present), downloads and installs the desired version from the official **Go** website, and configures the system environment (PATH variable). This role is compatible with Linux distributions.

Requirements
------------

- This role has been tested with some distributions. **Debian** (Ubuntu 22.04,24.04, Debian 11,12) and **RedHat** (Rhel 9).

Description of Variables
--------------

|Nom|Type|Description|Obligatoire|Valeur par défaut|
|---|----|-----------|-----------|-----------------|
`go_version`|str|Go version number. Format: x.y.z|no|`"1.23.10"`
`go_checksum`|str|checksum string of characters from the Go archive file to download|no|`""`

Dependencies
------------

None.

Example Playbook
----------------

- Role installation

```bash
mkdir -p $HOME/install-go
```

```bash
vim $HOME/install-go/requirements.yml
```

```yaml
- name: ansible-role-go-installer
  src: git+https://github.com/willbrid/ansible-role-go-installer.git
  version: v0.0.1
```

```
cd $HOME/install-go && ansible-galaxy install --force -r requirements.yml
```

- Using the role in a playbook

```bash
vim $HOME/install-go/playbook.yml
```

--- Example of the content of the **playbook.yml** file without configuring the variable `go_checksum`

```yaml
---
- hosts: localhost
  become: true

  vars:
    go_version: "1.23.10"

  roles:
    - ansible-role-go-installer
```

--- Example of the content of the **playbook.yml** file when configuring the variable `go_checksum`

> Note: To configure the `go_checksum` variable, you first need to know your system architecture using the command `uname -m` (`x86_64` = `amd64`). This will allow you to better choose the `sha256 checksum` string that corresponds to your architecture. <br> Link to the string retrieval site `sha256 checksum` : [https://go.dev/dl/](https://go.dev/dl/)

```yaml
---
- hosts: localhost
  become: true

  vars:
    go_version: "1.23.10"
    go_checksum: "77e5da33bb72aeaef1ba4418b6fe511bc4d041873cbf82e5aa6318740df98717" # for amd64 (please update as this value is only an example)

  roles:
    - ansible-role-go-installer
```

- Playbook execution

```bash
cd $HOME/install-go && ansible-playbook playbook.yml
```

License
-------

MIT

Author Information
------------------

William Bridge NGASSAM
