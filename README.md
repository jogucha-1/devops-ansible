## Content

- Playbook samples
- Ansible Role sample to Install Tomcat on HREL, Debian and Ubuntu Linux.
## Role info
## Tasks in the role

This role contains tasks to:

- Install basic packages required
- Install Java
- Add tomcat user and group
- Download tomcat and install - configure systemd
- Configure firewall

## How to use this role

- Update your inventory, e.g:

```
$ sudo hosts
[tomcat_nodes]
192.168.10.10       # Remote user to act on
```

- Update variables in playbook file - Set Tomcat version, remote user and Tomcat UI access credentials

```
$ sudo tomcat-installation.yml
- name: Tomcat deployment playbook
  hosts: tomcat_nodes       # Inventory hosts group / server to act on
  become: yes               # If to escalate privilege
  become_method: sudo       # Set become method
  remote_user: root         # Update username for remote server
  vars:
    tomcat_ver: 9.0.64                          # Tomcat version to install
    ui_manager_user: manager                    # User who can access the UI manager section only
    ui_manager_pass: Str0ngManagerP@ssw3rd      # UI manager user password
    ui_admin_username: admin                    # User who can access bpth manager and admin UI sections
    ui_admin_pass: Str0ngAdminP@ssw3rd          # UI admin password
  roles:
    - tomcat
```

If you are using non root remote user, then set username and enable sudo:

```
become: yes
become_method: sudo
```

## Running Playbook

Once all values are updated, you can then run the playbook against your nodes.

Playbook executed as root user - with ssh key:

```
$ ansible-playbook -i hosts tomcat-installation.yml --ask-vault-pass
```
