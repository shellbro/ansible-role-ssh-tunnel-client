ssh-tunnel-client
=================

[![Build Status](https://travis-ci.org/shellbro/ansible-role-ssh-tunnel-client.svg?branch=master)](https://travis-ci.org/shellbro/ansible-role-ssh-tunnel-client)

Ansible role for setting up SSH tunnel on Fedora and CentOS 7 (client side). Uses autossh for persistance.

Requirements
------------

Ansible version >= 2.0.

Role Variables
--------------

None

Dependencies
------------

- shellbro.epel

Example Playbook
----------------

    - hosts: servers
      roles:
         - shellbro.ssh-tunnel-client

License
-------

BSD

Author Information
------------------

Jakub Gorczyca
