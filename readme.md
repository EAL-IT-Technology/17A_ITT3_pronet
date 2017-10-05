17A project network
=========================

This repo is about provisioning relevant servers.

There ought to be a network diagram - PR anyone?

Design decisions
----------------------

* 1 monitoring server running nagios

    It will pull what to monitor from the inventory file


Configuration
----------------

The directory `inventory` contains the inventory information for the development setup and for the groups.

For the nagios specific things see [the repository](https://github.com/moozer/ansible-role-nagios)

### `inventory/development`

This is the information used for devlopment, and is not intended to be rolled out in production.

It is used e.g. when doing `vagrant up` in the base directory

### `inventory/grp1`

This is the inventory information for group 1.

The intention is that other groups may add a new submodule that links to their own inventory directory structure.

### `inventory/<subdir>/group_vars/all/*`

Contains configuration that is applied to all groups

### `inventory/<subdir>/group_vars/servers/*`

Contains configuration that is applied to the `servers` group

### `inventory/<subdir>/group_vars/host_vars/srv-mon/*`

Contains configuration that is applied to the server called `srv-mon`

### `inventory/<subdir>/inventory`

This is the list of server and other devices that ansbiel is aware of.


Usage
-------------------

To pull the latest config (includin submodules)

1. `git pull`
2. `git submodule update --remote`

To test the configuration (to everything defined in `inventory` and `site.yml`)

    `ansible-playbook -i inventory/<subdir>/inventory site.yml --check -D`

To apply the configuration (to everything defined in `inventory` and `site.yml`)

    `ansible-playbook -i inventory/<subdir>/inventory site.yml`
