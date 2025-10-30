---
- name: Require sudo password for deploy
  hosts: all
  become: true
  gather_facts: false
  tasks:
    - name: Set password for deploy
      ansible.builtin.user:
        name: deploy
        password: "$6$PMzGuXmepawNyFjf$HnZHZut9bAPc3LpejCtqtHatZNmgke1BdKpVHBBqxAn95GN38EgQ8pSBcm6110AqNl.ZwAoyQOgF/H5ja21"
        update_password: always

    - name: Enable password required sudo
      ansible.builtin.copy:
        dest: /etc/sudoers.d/deploy
        owner: root
        group: root
        mode: '0440'
        content: |
          deploy ALL=(ALL) ALL
        validate: "visudo -cf %s"
