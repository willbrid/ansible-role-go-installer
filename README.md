Ansible-role-go-installer
=========

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/willbrid/ansible-role-go-installer/blob/main/LICENSE)

Le rôle **ansible-role-go-installer** permet d’installer l'outil de développement **Go** sur des environnements Linux. Il détecte automatiquement la version existante de **Go** (si présente), télécharge et installe la version souhaitée depuis le site officiel de **Go**, et configure l’environnement système (variable **PATH**). Ce rôle est compatible avec les distributions linux.

Exigences
------------

- Ce rôle a été testé avec certaines distributions **Debian** (Ubuntu 22.04,24.04, Debian 11,12) et **RedHat** (Rhel 9).

Description des Variables
--------------

|Nom|Type|Description|Obligatoire|Valeur par défaut|
|---|----|-----------|-----------|-----------------|
`go_version`|str|numéro de version de Go. Format : x.y.z|non|`"1.23.10"`
`go_checksum`|str|chaine de caractères checksum du fichier archive Go à télécharger|non|`""`

Dépendances
------------

Aucune.

Exemple Playbook
----------------

- Installation du rôle

```bash
mkdir -p $HOME/install-go/roles
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
cd $HOME/install-go && ansible-galaxy install -r requirements.yml --roles-path roles
```

- Utilisation du rôle dans un playbook

```bash
vim $HOME/install-go/playbook.yml
```

--- Exemple de contenu du fichier playbook.yml sans configurer la variable `go_checksum`

```yaml
---
- hosts: localhost
  become: true

  vars:
    go_version: "1.23.10"

  roles:
    - ansible-role-go-installer
```

--- Exemple de contenu du fichier playbook.yml en configurant la variable `go_checksum`

> Note: Pour configurer la variable `go_checksum`, il faudrait au préalable connaitre l'architecture de votre système via la commande `uname -m` (`x86_64` = `amd64`). Ainsi vous pourrez mieux choisir la chaine de caractères `sha256 checksum` qui correspond à votre architecture. <br>
Lien du site de récupération de la chaine `sha256 checksum` : [https://go.dev/dl/](https://go.dev/dl/)

```yaml
---
- hosts: localhost
  become: true

  vars:
    go_version: "1.23.10"
    go_checksum: "77e5da33bb72aeaef1ba4418b6fe511bc4d041873cbf82e5aa6318740df98717" # pour amd64

  roles:
    - ansible-role-go-installer
```

- Exécution du playbook

```bash
cd $HOME/install-go && ansible-playbook playbook.yml
```

License
-------

MIT

Informations sur l'auteur
------------------

William Bridge NGASSAM
