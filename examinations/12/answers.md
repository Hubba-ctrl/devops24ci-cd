# QUESTION A
----------
```
---
# tasks file for dbserver
- name: Ensure MariaDB-server is installed.
  ansible.builtin.package:
        name: mariadb-server
        state: present

- name: Ensure MariaDB is started at boot
  ansible.builtin.service:
        name: mariadb
        enabled: true

- name: Ensure MariaDB is started
  ansible.builtin.service:
        name: mariadb
        state: started

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


- name: Create Mariadb user and grant * privileges on webbappd
  community.mysql.mysql_user:
        name: webappuser
        password: "{{ webappdb_password }}"
        priv: webappdb.*:ALL
        login_unix_socket: /var/lib/mysql/mysql.sock

```

```
---
- name: Ensure nginx is installed
  ansible.builtin.package:
    name: nginx
    state: present
    # changed from latest to present to make it production-level

- name: Ensure nginx is enabled at boot
  ansible.builtin.service:
    name: nginx
    enabled: true

- name: Ensure nginx is started
  ansible.builtin.service:
    name: nginx
    state: started

- name: Copy nginx https conf to webserver
  ansible.builtin.copy:
    src: https.conf
    dest: /etc/nginx/conf.d/https.conf
    owner: root
    group: root
    mode: "0644"
  register: httpsconf

- name: Copy nginx example.internal configuration to webserver (TEMPLATE)
  ansible.builtin.template:
    src: example.internal.conf.j2
    dest: /etc/nginx/conf.d/example.internal.conf
    owner: root
    group: root
    mode: "0644"
  register: exampleconf

- name: Create directory structure
  ansible.builtin.file:
    path: /var/www/example.internal/html/
    state: directory
    owner: root
    group: root
    mode: "0755"
    recurse: true
  register: webdir

- name: Copy index.html into web root
  ansible.builtin.copy:
    src: index.html
    dest: /var/www/example.internal/html/index.html
    owner: root
    group: root
    mode: "0644"
  register: indexfile

- name: Restart nginx service if something changed
  ansible.builtin.service:
    name: nginx
    state: restarted
  when: httpsconf.changed or exampleconf.changed or webdir.changed or indexfile.changed
```
