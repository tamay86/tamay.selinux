Ansible Role: tamay.selinux
=========

This role configures SELinux state, booleans, ports and file contexts. 

Requirements
------------

None.

Role Variables
--------------

List of all variables, including default values.

    selinux_state: 'enforcing'
    selinux_policy: targeted

Sets selinux to *enforcing*, *permissive* or *disabled*. Default policy is *targeted*.    
    
    selinux_boolean:
      - name: httpd_can_network_connect
        state: yes
        persistent: yes

Contains a list of SELinux booleans, with their state (on or off) and whether it should be persistent. *State* and *persistent* defaults to *yes*, so it can be omitted.
    
    selinux_port:
      - ports: 8888
        proto: tcp
        setype: http_port_t
        state: present

A list of ports with the wanted context. *State* defaults to *yes*, so it can be omitted.
    
    selinux_fcontext:
      - target: '/srv/git_repos(/.*)?'
        setype: httpd_sys_rw_content_t
        state: present

List with paths and their wanted file context. *State* defaults to *yes*, so it can be omitted.

Dependencies
------------

None.

Example Playbook
----------------

    ---
    
    - hosts: all
    
      vars:
        selinux_state: 'enforcing'
        selinux_policy: targeted
    
        selinux_boolean:
          - name: httpd_can_network_connect
          - name: httpd_can_network_connect_db
    
        selinux_port:
          - ports: 8888
            proto: tcp
            setype: http_port_t
            state: present
    
        selinux_fcontext:
          - target: '/srv/git_repos(/.*)?'
            setype: httpd_sys_rw_content_t
            state: present
    
      roles:
      - tamay.selinux

License
-------

MIT

Author Information
------------------

tamay.mueller@gmail.com