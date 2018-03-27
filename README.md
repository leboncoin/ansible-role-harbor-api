# [WIP] Ansible Role: Harbor API Codifying

[![License:MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

An Ansible Role to manage Harbor API


<!-- TOC -->

- [Ansible Role: Harbor API condifying](#wip-ansible-role-harbor-api-condifying)
- [Requirements](#requirements)
- [Role Variables](#role-variable)
- [Usage](#usage)
    - [Roles](#roles)
    - [Projects](#projects)
- [Dependencies](#dependencies)
- [Example Playbook](#example-playbook)
- [Contributing](#contributing)
- [License](#license)
<!-- /TOC -->

# Requirements

Have one or more [Harbor](https://github.com/vmware/harbor) instances

# Installation

Harbor-API  is an Ansible role distributed globally using [Ansible Galaxy](https://galaxy.ansible.com/). In order to install Harbor-API role you can use the following command.

```
$ ansible-galaxy install leboncoin.harbor-api
```

# Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

    harbor_directory_api: "{{ role_path }}/files/config/"
    harbor_directory_api_projects: "{{ role_path }}/files/config/projects/"

Another variables can be used from [harbor.cfg](https://github.com/vmware/harbor/blob/master/make/harbor.cfg), prefixed by *harbor_*

    harbor_auth_mode: ldap_auth
    harbor_harbor_admin_password: Harbor12345

# Usage

You can create json files to configure your harbor, based on swagger implementation ([swagger editor]( https://editor.swagger.io/?url=https://raw.githubusercontent.com/vmware/harbor/master/docs/swagger.yaml ))


### Sysadmins

Resources:
- Put (/users/{user_id}/sysadmin)

_admins_removed is required because "harbor api" doesn't implement the research of admin [#PR4388](https://github.com/vmware/harbor/pull/4388)_

files/config/roles.json

    {
        "admins":[
            "sysadmin@mycompany.com"
        ],
        "admins_removed":[
            "oldsysadmin@mycompany.com"
        ]
    }

### Projects

Resources:
- Add (/projects)
- Put (/projects/{project_id})

files/config/projects/myproject.json

    {
        "name": "myproject",
        "metadatas": {
            "public": false
        },
        "members" [
            developer@mycompany.com
        ],
        "admins": [
            sysadmin@mycompany.com
        ]
    }


# Dependencies

None.

# Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: harbor
      roles:
         - { role: leboncoin.harbor } # install harbor instance
         - { role: leboncoin.harbor-api } # populate api

# Contributing

Please, see [TODO.md](TODO.md) to get ideas to contribute or implement your own things.

# License

MIT
