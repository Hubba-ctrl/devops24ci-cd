---
- name: Node export for Prometheus
  hosts: all
  become: true
  tasks:
    - name: Create node_exporter user
      ansible.builtin.user:
        name: node_exporter
        system: true
        shell: /usr/sbin/nologin
        create_home: false

    - name: Create directory structure
      ansible.builtin.file:
        path: /var/lib/node_exporter/textfile_collector
        state: directory
        owner: node_exporter
        group: node_exporter
        mode: "0755"
        recurse: true

    - name: Copy systemd files to servers
      ansible.builtin.copy:
        src: "{{ item }}"
        dest: /etc/systemd/system/
        group: root 
        owner: root
        mode: "0644"
      loop: [files/node_exporter.service, 
             files/node_exporter.socket]

    - name: Copy sysconfig files to servers
      ansible.builtin.copy:
        src: files/sysconfig.node_exporter
        dest: /etc/sysconfig/node_exporter
        group: root 
        owner: root
        mode: "0644"

    - name: Download node exporter binaries
      ansible.builtin.get_url: 
        url: https://github.com/prometheus/node_exporter/releases/download/v1.10.0/node_exporter-1.10.0.linux-amd64.tar.gz
        dest: /tmp/
        group: deploy
        owner: deploy
        mode: "0644"

    - name: Unzip downloaded package
      ansible.builtin.unarchive:
        src: /tmp/node_exporter-1.10.0.linux-amd64.tar.gz
        dest: /tmp/
        remote_src: true 

    - name: Copy binary file to usr/local
      ansible.builtin.copy:
        src: /tmp/node_exporter-1.10.0.linux-amd64/node_exporter
        dest: /usr/sbin/node_exporter
        remote_src: true
        owner: root 
        group: root
        mode: "0755"

    - name: Enable and start socket
      ansible.builtin.systemd:
        name: node_exporter.socket
        enabled: true
        state: started
        daemon_reload: true

    - name: Open port 9100/tcp on servers
      ansible.posix.firewalld:
        port: 9100/tcp
        permanent: true
        immediate: true
        state: enabled
