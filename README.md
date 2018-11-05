cloud9
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-cloud9.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-cloud9)

The purpose of this role is to install and configure cloud9 IDE on your system.

Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```
---
- name: Converge
  hosts: all
  gather_facts: false
  become: true

  roles:
    - robertdebock.bootstrap
    - robertdebock.buildtools
    - robertdebock.epel
    - robertdebock.npm
    - robertdebock.cloud9

```

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```
---
# defaults file for cloud9

# Create this user and group and run the software under this user.
cloud9_user: cloud9
cloud9_group: cloud9

# The webinterface requires authentication, these are the login details.
cloud9_username: username
cloud9_password: password

# Where to place the installer and workspace.
cloud9_installer: /home/{{ cloud9_user }}/c9sdk
cloud9_workspace: /home/{{ cloud9_user }}/workspace

# What IP address to listen on.
cloud9_bind_address: "{{ ansible_default_ipv4.address }}"

# To update all packages installed by this roles, set `cloud9_package_state` to `latest`.
cloud9_package_state: present

```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

---
- robertdebock.bootstrap
- robertdebock.epel
- robertdebock.buildtools
- robertdebock.npm


Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cloud9.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|no|no|no|no|no*|
|alpine-latest|no|no|no|no|no*|
|archlinux|no|no|no|no|no*|
|centos-6|no|no|no|no|no*|
|centos-latest|yes|yes|yes|no|no*|
|debian-latest|yes|yes|yes|no|no*|
|debian-stable|yes|yes|yes|no|no*|
|debian-unstable*|yes|yes|yes|no|no*|
|fedora-latest|yes|yes|yes|no|no*|
|fedora-rawhide*|yes|yes|yes|no|no*|
|opensuse-leap|no|no|no|no|no*|
|opensuse-tumbleweed|no|no|no|no|no*|
|ubuntu-artful|yes|yes|yes|no|no*|
|ubuntu-devel*|yes|yes|yes|no|no*|
|ubuntu-latest|yes|yes|yes|no|no*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-cloud9) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-cloud9/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many specific scenarios available, please have a look in the `molecule/` directory.


License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
