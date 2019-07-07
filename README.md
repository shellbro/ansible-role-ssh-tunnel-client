shellbro.ssh_tunnel_client
==========================

[![Build Status](https://travis-ci.org/shellbro/ansible-role-ssh-tunnel-client.svg?branch=master)](https://travis-ci.org/shellbro/ansible-role-ssh-tunnel-client)

Ansible role for setting up SSH tunnel between two CentOS 7 machines (client
side). Uses autossh and systemd for persistance.

Before applying this role to a client machine use `shellbro.ssh_tunnel_server`
role on a server machine so it is configured to allow port forwarding and has
correct client SSH public key installed.

Requirements
------------

Ansible version >= 2.4

Role Variables
--------------

* server - server hostname or IP address (required)
* server_port - server's SSH port (by default 22)
* user - run tunnel as this user. This option implies that specified user
exists on the client side, has SSH key pair generated and public SSH key is
installed on the server side using `shellbro.ssh_tunnel_server` role. (required)
* server_alive_interval - SSH connection setting (by default 15 seconds)
* server_alive_count_max - SSH connection setting (by default 3)
* restart_sec - `autossh` takes care of tunnel persistence using
`server_alive_interval` and `server_alive_count_max` settings. This option
instructs systemd to restart `autossh` itself when it exits. (by default 15
seconds)
* remote_port_forwarding - enable remote port forwarding (by default `false`)
* local_port_forwarding - enable local port forwarding (by default `false`)

When either `remote_port_forwarding` or `local_port_forwarding` variable is set
to `true` then four additional variables are required:

* bind_address - address to bind to on the server side (if
`remote_port_forwarding` is `true`) or on the client side (if
`local_port_forwarding` is `true`)
* forward_port - port to be forwarded on the server side (if
`remote_port_forwarding` is `true`) or on the client side (if
`local_port_forwarding` is `true`)
* target_host - host to forward to
* target_port - port to forward to

Dependencies
------------

* shellbro.epel

Example Playbook
----------------

    - name: Configure server side
      hosts: server-side
      roles:
        - role: shellbro.ssh-tunnel-server
          open_port: 12222

    - name: >-
        Set up persistent SSH tunnel for accessing SSH server
        (running on the client side) behind firewall
      hosts: client-side
      roles:
        - role: shellbro.ssh-tunnel-client
          host: server-side
          user: devops
          remote_port_forwarding: true
          bind_address: 0.0.0.0
          forward_port: 12222
          target_host: 127.0.0.1
          target_port: 22

License
-------

BSD

Author Information
------------------

Jakub Gorczyca
