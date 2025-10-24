---
- name: Configure both servers firewalls
  hosts: all
  become: true
  tasks:

    - name: Install firewalld and python3-firewall
      ansible.builtin.package:
        name: "{{ item }}"
        state: present
      loop: [firewalld, python3-firewall]

    - name: Enable and start firewalld
      ansible.builtin.service:
        name: firewalld
        enabled: true
        state: started

    - name: Enable http,https webserver
      ansible.posix.firewalld:
        service: "{{ item }}"
        permanent: true
        state: enabled
      loop: [http, https]
      when: "'web' in group_names"
      notify: Reload firewalld

    - name: Enable mariadb dbserver
      ansible.posix.firewalld:
        service: mysql
        permanent: true
        state: enabled
      when: "'db' in group_names"
      notify: Reload firewalld

  handlers:
    - name: Reload firewalld
      ansible.builtin.service:
        name: firewalld
        state: reloaded
