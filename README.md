cloud9
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-cloud9"><img src="https://travis-ci.org/robertdebock/ansible-role-cloud9.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure cloud9 IDE on your system.

<img src="https://img.shields.io/ansible/role/d/29418"/>
<img src="https://img.shields.io/ansible/quality/29418"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.cloud9
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - robertdebock.bootstrap
    - robertdebock.buildtools
    - robertdebock.epel
    - robertdebock.npm
    - robertdebock.git
    - robertdebock.locale
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
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
cloud9_bind_address: "{{ ansible_default_ipv4.address | default('127.0.0.1') }}"
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.git
- robertdebock.locale
- robertdebock.npm
- robertdebock.service

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/cloud9.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tag|allow_failures|
|---------|---|--------------|
|fedora|latest|no|
|fedora|rawhide|yes|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '\~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible\~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.6.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Python version 2.7 is required |
| Archlinux | Python version 2.7 is required |
| CentOS latest | Python version 2.7 is required |
| Debian | Python version 2.7 is required |
| openSUSE Leap | Python version 2.7 is required |
| Ubuntu | Python version 2.7 is required |



Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-cloud9) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-cloud9/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

Modules
-------

This role uses the following modules:
```yaml
---
- command
- file
- git
- group
- import_role
- package
- service
- systemd
- user
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
