# QUESTION A 

---
- name: Checking Cis security benchmarks
  hosts: all
  become: true
  tasks:
    - name: Get package facts
      ansible.builtin.package_facts: 

    - name: Get service facts
      ansible.builtin.service_facts:

    - name: Assert SELinux is enforcing
      ansible.builtin.assert:
        that: ansible_facts.selinux.mode == "enforcing"
        success_msg: "SELinux is enforcing."
        fail_msg: "SELinux is not enforcing."

    - name: Assert sudo is installed
      ansible.builtin.assert:
        that: "'sudo' in ansible_facts.packages"
        fail_msg: "sudo is NOT installed."
        success_msg: "sudo is installed."

    - name: Assert rsh-server is not installed
      ansible.builtin.assert:
        that: "'rsh-server' not in ansible_facts.packages"
        fail_msg: "rsh-server is installed"
        success_msg: "rsh-server is not installed."

    - name: Assert tftp-server is not installed
      ansible.builtin.assert:
        that: "'tftp-server' not in ansible_facts.packages"
        fail_msg: "tftp-server is installed."
        success_msg: "tftp-server is not installed."

    - name: Assert talk-server is not installed
      ansible.builtin.assert:
        that: "'talk-server' not in ansible_facts.packages"
        fail_msg: "talk-server is installed."
        success_msg: "talk-server is not installed"

    - name: Assert sshd package exists
      ansible.builtin.assert:
        that: "'openssh-server' in ansible_facts.packages"
        success_msg: "SSH server is installed."
        fail_msg: "SSH server is not installed."

    - name: Check that firewalld is installed
      ansible.builtin.assert:
        that:
          - "'firewalld.service' in ansible_facts.services"
        success_msg: "Firewalld service is installed."
        fail_msg: "Firewalld service is not installed"

    - name: Assert firewalld service is running
      ansible.builtin.assert:
        that:
          - ansible_facts.services['firewalld.service'].state == 'running'
        success_msg: "Firewalld is running."
        fail_msg: "Firewalld is NOT running."

    - name: Assert chrony is installed
      ansible.builtin.assert:
        that: "'chrony' in ansible_facts.packages"
        fail_msg: "chrony is NOT installed."
        success_msg: "chrony is installed."

    - name: Assert root user exists
      ansible.builtin.assert:
        that: "'root' in ansible_facts['user_id']"
        success_msg: "Root user exists"
        fail_msg: "Root user does not exist"


# BONUS QUESTION FOR ENLIGHTMENT 
---
- name: Configure the web server(s) according to specs
  hosts: web
  gather_facts: true
  become: true
  roles:
    - webserver

- name: Configure the database server(s) according to specs
  hosts: db
  become: true
  roles:
    - dbserver

- name: Run cis security check
  import_playbook: 16-compliance-check.yml