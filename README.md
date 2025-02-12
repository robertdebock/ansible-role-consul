# [Ansible role consul](#consul)

Install and configure consul on your system.

|GitHub|GitLab|Downloads|Version|
|------|------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-consul/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-consul/actions)|[![gitlab](https://gitlab.com/robertdebock-iac/ansible-role-consul/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-consul)|[![downloads](https://img.shields.io/ansible/role/d/robertdebock/consul)](https://galaxy.ansible.com/robertdebock/consul)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-consul.svg)](https://github.com/robertdebock/ansible-role-consul/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/robertdebock/ansible-role-consul/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: robertdebock.consul
      consul_bootstrap_expect: 1
      consul_encrypt: "6r73CP0icJrap1tsQ17yuqzVguho4/yz+aI/dkVg2Kk="
      consul_bind_addr: "0.0.0.0"
      consul_services:
        - name: web
          tags:
            - rails
          port: 80
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/robertdebock/ansible-role-consul/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
    - role: robertdebock.hashicorp
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/robertdebock/ansible-role-consul/blob/master/defaults/main.yml):

```yaml
---
# defaults file for consul

# You can install consul using a package in this role. If you have installed
# consul manually, set this to `false`.
consul_install_package: true

# Consul requires a license. Without setting a license (or an empty license), some steps are skipped.
consul_license: ""

# This flag controls the datacenter in which the agent is running.
consul_datacenter: my-dc-1

# This flag provides a data directory for the agent to store state.
consul_data_dir: /opt/consul

# The address to which Consul will bind client interfaces, including the HTTP and DNS servers
consul_client_addr: "0.0.0.0"

# Enables the built-in web UI server and the required HTTP routes.
consul_ui: true

# This flag is used to control if an agent is in server or client mode.
consul_server: true

# This flag provides the number of expected servers in the datacenter.
# consul_bootstrap_expect: 3

# Specifies the secret key to use for encryption of Consul network traffic.
# consul_encrypt: "6r73CP0icJrap1tsQ17yuqzVguho4/yz+aI/dkVg2Kk="

# Similar to -join but allows retrying a join until it is successful.
# consul_retry_join:
#   - consul.domain.internal

# The address that should be bound to for internal cluster communications.
# consul_bind_addr: "{{ ansible_default_ipv4.address }}"

# The advertise address is used to change the address that we advertise to other nodes in the cluster.
# consul_advertise_addr: "{{ ansible_default_ipv4.address }}"

# You can define service that Consul should manage.
# consul_services:
#   - name: web
#     tags:
#       - rails
#     port: 80

# In same cases you may not want to start Consul as a service, because you are "bootstrapping" for example.
consule_service_started_and_enabled: true
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-consul/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-bootstrap)|
|[robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-core_dependencies)|
|[robertdebock.hashicorp](https://galaxy.ansible.com/robertdebock/hashicorp)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-hashicorp/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-hashicorp/actions)|[![Build Status GitLab](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp/badges/master/pipeline.svg)](https://gitlab.com/robertdebock-iac/ansible-role-hashicorp)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-consul/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|[Amazon](https://hub.docker.com/r/robertdebock/amazonlinux)|Candidate|
|[Debian](https://hub.docker.com/r/robertdebock/debian)|bullseye|
|[EL](https://hub.docker.com/r/robertdebock/enterpriselinux)|9|
|[Fedora](https://hub.docker.com/r/robertdebock/fedora)|40|
|[Ubuntu](https://hub.docker.com/r/robertdebock/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-consul/issues).

## [License](#license)

[Apache-2.0](https://github.com/robertdebock/ansible-role-consul/blob/master/LICENSE).

## [Author Information](#author-information)

[robertdebock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
