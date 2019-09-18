K3S installation role
=========

Installs latest (or specific) version of k3s on defined target(s)

Requirements
------------

Linux with systemd

Role Variables
--------------

Variables used by this role are:
- k3s_version - which version you would like to be installed, if not set will default to latest published on github
- k3s_bin_path - location where k3s binary will be installed, if not set defaults to /usr/local/bin

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Usage
----------------

Simplest playbook to be used for example could look like bellow. 

      ---

      - hosts: k3s_cluster
        gather_facts: yes
        user: root
        become: yes
        roles:
          - { role: k3s }

        environment:
          - http_proxy: "{{ proxy_env|default('') }}"
          - https_proxy: "{{ proxy_env|default('') }}"
          - no_proxy: "{{ ansible_host }}"


Inventory file that accompanies example playbook;

      [master]
      localhost


      [node]
      #node-01

      [k3s_cluster:children]
      master
      node

      [k3s_cluster:vars]
      #k3s_version=0.8.1

Example run;

      ansible-playbook -i inventory example.yml

Example run with use of proxy

      ansible-playbook -i inventory example.yml -e proxy_env=http://proxy-host.example.com:8080/


License
-------

Apache 2.0

