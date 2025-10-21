# QUESTION A
-------
This is the entire playbook I ran for this assignment 
```
---
- name: Ensure Mariadb is installed, running and enabled on boot
  hosts: db
  become: true
  tasks:
    - name: Ensure MariaDB-server is installed.
      ansible.builtin.package:
        name: mariadb-server
        state: present

    - name: Ensure python3-PyMySQl is installed
      ansible.builtin.package:
        name: python3-PyMySQL
        state: present

    - name: Ensure MariaDB is started at boot
      ansible.builtin.service:
        name: mariadb
        enabled: true

    - name: Ensure MariaDB is started
      ansible.builtin.service:
        name: mariadb
        state: started

    - name: Create Mariadb DB webappdb
      community.mysql.mysql_db:
        name: webappdb
        state: present
        login_unix_socket: /var/lib/mysql/mysql.sock

    - name: Create Mariadb user and grant * privileges on webbappd
      community.mysql.mysql_user:
        name: webappuser
        password: secretpassword
        priv: webappdb.*:ALL
        login_unix_socket: /var/lib/mysql/mysql.sock
```
