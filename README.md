cloud9
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-cloud9.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-cloud9)

Installs the Cloud9 IDE on a machine.

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-cloud9) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-cloud9/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many scenarios available, please have a look in the `molecule/` directory.

Context
--------
This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cloud9.png "Dependency")

Requirements
------------

- A system installed with required packages to run Ansible. Hint: [bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap).
- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)
- Buildtools installed. Hint: [buildtools](https://galaxy.ansible.com/robertdebock/buildtools).
- NPM available. Hint: [npm](https://galaxy.ansible.com/robertdebock/npm).

Role Variables
--------------

- cloud9_parameter: Description of values. [default: value]
- cloud9_user: The user to run under. [default: cloud9]
- cloud9_group: The group to run under. [default: cloud9]
- cloud9_username: The username used to authenticate in the IDE. [default: username]
- cloud9_password: The password used to authenticate in the IDE. [default: password]
- cloud9_bind_address: The TCP port to bind to. [default: {{ ansible_default_ipv4.address }}]
- cloud9_installer: Where to place the installer files. [default: /home/{{ cloud9_user }}/c9sdk]
- cloud9_workspace: What directory to use a a workspace. [default: /home/{{ cloud9_user }}/workspace]

Dependencies
------------

- None known.

Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|
|------------|-----------|-----------|-----------|
|alpine-edge|no|no|no|
|alpine-latest|no|no|no|
|archlinux|no|no|no|
|centos-6|no|no|no|
|centos-latest|yes|yes|yes|
|debian-latest|yes|yes|yes|
|debian-stable|yes|yes|yes|
|debian-unstable|yes|yes|yes|
|fedora-latest|yes|yes|yes|
|fedora-rawhide|yes|yes|yes|
|opensuse-leap|no|no|no|
|opensuse-tumbleweed|no|no|no|
|ubuntu-artful|yes|yes|yes|
|ubuntu-devel|yes|yes|yes|
|ubuntu-latest|yes|yes|yes|

Example Playbook
----------------

A minimal example:
```
---
- name: cloud9
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.buildtools
    - role: robertdebock.npm
    - role: robertdebock.cloud9
      cloud9_username: someuser
      cloud9_password: S3cr3t
```

A more realistic example:
```
---
- hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.update
    - role: robertdebock.firewall
      firewall_services:
        - name: ssh
        - name: http
        - name: https
    - role: robertdebock.python_pip
    - role: robertdebock.httpd
      httpd_applications:
        - name: cloud9
          location: /
          backend_url: http://localhost:8181/
    - role: robertdebock.buildtools
    - role: robertdebock.npm
    - role: robertdebock.cloud9
      cloud9_bind_address: 127.0.0.1
```

To install this role:
- Install this role individually using `ansible-galaxy install robertdebock.cloud9`

Sample roles/requirements.yml: (install with `ansible-galaxy install -r roles/requirements.yml
```
---
- name: robertdebock.bootstrap
- name: robertdebock.buildtools
- name: robertdebock.npm
- name: robertdebock.cloud9
```

License
-------

Apache License, Version 2.0

Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
