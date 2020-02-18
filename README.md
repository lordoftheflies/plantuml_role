# Ansible Role: PlantUML

Ansible Galaxy role for PlantUML server and libraries.

## State

[![Build Status](https://travis-ci.org/lordoftheflies/plantuml_role.svg?branch=master)](https://travis-ci.org/lordoftheflies/plantuml_role)

## Requirements

Production:
* [Ansible 2.9+](https://docs.ansible.com/ansible/latest/roadmap/ROADMAP_2_9.html)
* [Python 3.4+](https://www.python.org/downloads/release/python-340/)

Development:
* Virtualenv
* [Tox 3.4+](https://tox.readthedocs.io/en/3.4.0/index.html)

## Role Variables


| Name | Description | Default |
| :--- | :--- | :--- |
| `plantuml_role_domain` | Primary domain of organization. | `cherubits.hu` |
| `plantuml_role_subdomain` | Subdomain of service | `plantuml` |

<p>
<details>
<summary> `plantuml_role_plantuml_limit_size` </summary>

Limits image width and height.

Default value: Environment variable `PLANTUML_LIMIT_SIZE`=4096

</details>
</p>

<p>
<details>
<summary> `plantuml_role_graphviz_dot` </summary>

Link to `dot` executable.

Default value: Environment variable `GRAPHVIZ_DOT`=/usr/bin/dot

</details>
</p>

<p>
<details>
<summary> `plantuml_role_plantuml_stats` </summary>

Set it to `on` to enable [statistics report](http://plantuml.com/statistics-report)

Default value: Environment variable `PLANTUML_STATS`=`off`

</details>
</p>

<p>
<details>
<summary> `plantuml_role_plantuml_stats` </summary>

When calling the proxy endpoint, the value of `HTTP_AUTHORIZATION` will be used to set the HTTP Authorization header

Default value: Environment variable HTTP_AUTHORIZATION=`null`

</details>
</p>

<p>
<details>
<summary> `plantuml_role_allow_plantuml_include` </summary>

Enables `!include` processing which can read files from the server into diagrams. Files are read relative to the current working directory.
Default value: Environment variable ALLOW_PLANTUML_INCLUDE=`false`

</details>
</p>


## Dependencies

This role depends on:
* [lordoftheflies.python](https://galaxy.ansible.com/lordoftheflies/python_role) [![Build Status](https://travis-ci.org/lordoftheflies/python_role.svg?branch=master)](https://travis-ci.org/lordoftheflies/python_role)
* [lordoftheflies.java](https://galaxy.ansible.com/lordoftheflies/java_role) [![Build Status](https://travis-ci.org/lordoftheflies/python_role.svg?branch=master)](https://travis-ci.org/lordoftheflies/java_role)

Group and host variables:
* Business-service domain is mandatory (`organization_domain`)
* Business-service subdomain is mandatory (`organization_subdomain`)

## Example Playbooks

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

Install role hosts
```yamlex
- hosts: plantuml_servers
      roles:
         - role: lordoftheflies.plantuml_role
           vars: 
             organization_domain: 'acme.org'
             organization_subdomain: 'plantuml'
```

Uninstall role hosts:
```yamlex
- hosts: plantuml_servers
      roles:
         - role: lordoftheflies.plantuml_role
           state: absent

```

Backup role hosts configuration:
```yamlex
- hosts: plantuml_servers
      roles:
         - role: lordoftheflies.plantuml_role
           vars:
               - export_config: true
               - backup_data: false
```
Reconfigure role hosts:
```yamlex
- hosts: plantuml_servers
      roles:
         - role: lordoftheflies.plantuml_role
           vars:
               - import_config: true
```

## Integration

### For Local Testing

* [Vagrant](https://www.vagrantup.com/) - (Tested using version 2.1.1)
* Vagrant plugins:
  * [vagrant-disksize (0.1.2)](https://github.com/{{ lookup('pipe', 'git config user.name') }}/vagrant-disksize)
  * [vagrant-libvirt](https://github.com/{{ lookup('pipe', 'git config user.name') }}/vagrant-libvirt)
  * vai (0.9.3) - For testing with multiple vms [vagrant-plugin-vai](https://github.com/{{ lookup('pipe', 'git config user.name') }}/vagrant-plugin-vai)
  * [vagrant-vbguest (0.15.2) - Recommended vagrant-vbguest](https://github.com/{{ lookup('pipe', 'git config user.name') }}/vagrant-vbguest)
* [Virtual Box](https://www.virtualbox.org/)
  * Tested using Version 5.2.14 r123301 (Qt5.6.1)

### Set up Molecule environment
```shell script
virtualenv --python=/usr/bin/python3.7 .env
source .env/bin/activate
pip install molecule docker molecule[lint] molecule[docker] molecule[vagrant]
```

### Set up your Molecule scenarios
```shell script
molecule init scenario -s default -d docker -r plantuml_role
molecule init scenario -s lxd -d lxd -r plantuml_role
molecule init scenario -s vagrant -d vagrant -r plantuml_role
```

### Testing

To test with all VM's defined in Vagrantfile run the following:

```shell
vagrant up
```

To run on a specific VM's
```shell
vagrant up xenial
```

### Supported platforms

| OS | Version | Distribution | Supported | Results  |
| :--- | :---: | :---: | :---: | :---: |
| Ubuntu | 19.10 | disco | supported | * |
| Ubuntu | 19.10 | eoan | supported | * |

## License

Apache 2.0

## Author Information

* [László Hegedűs](https://github.com/lordoftheflies) [:envelope:](mailto:laszlo.hegedus@cherubits.hu)
* [Jeff Geerling](https://github.com/geerlingguy) [:envelope:](mailto:laszlo.hegedus@cherubits.hu)
* [Christopher Steel](https://github.com/csteel) [:envelope:](mailto:christopher.steel@mcgill.ca)
> **NOTE**: `plantuml_role` generated using `skeleton` from [ansible_role_skeleton](https://github.com/lordoftheflies/ansible_role_skeleton).

#### Referencies

* [PlantUML](https://github.com/lordoftheflies/plantuml)
* [PlantUML Documentation](https://github.com/lordoftheflies/plantuml-documentation)
* [PlantUML Library](https://github.com/lordoftheflies/plantuml-stdlib)
* [PlantUML Server](https://github.com/lordoftheflies/plantuml-server)
* [PlantUML Wiki](https://github.com/lordoftheflies/plantuml-wiki)
