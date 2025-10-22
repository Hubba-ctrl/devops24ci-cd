# QUESTION A
----------
```
---
- name: Add multiple users and groups
  hosts: web
  become: true
  tasks:
    - name: Adding users to groups
      ansible.builtin.user:
        name: "{{ item.name }}"
        groups: "{{ item.groups }}"
        state: present
      loop:
        - {name: "alovelace", groups: ["wheel,audio,video"]}
        - {name: "ghopper", groups: ["wheel,audio"]}
        - {name: "aturing", groups: "tape"}
        - {name: "edijkstra", groups: "tcpdump"}

```
# QUESTION B
------
```
---
- name: Copy .md files to deploy
  hosts: db
  become: true
  tasks:
    - name: copying the files
      ansible.builtin.copy:
        src: "{{ item }}"
        dest: /home/deploy
        owner: deploy
        mode: "0644"
      with_fileglob:
        - "files/*.md"
```
# BONUS QUESTION
I used `openssl passwd -6`to generate a hashed password. I used notasecret
as a password. 
```
---
- name: Add multiple users and groups
  hosts: web
  become: true
  tasks:
    - name: Adding users to groups
      ansible.builtin.user:
        name: "{{ item.name }}"
        groups: "{{ item.groups }}"
        password: $6$0OKJBevDHxE636wl$l26Y0ttVrVa98wnDQ6ahgU1moy1tuEwv1qwc0HYwMEXQ2QtGiYoSA7X0SFVeWGu1ls9rAPTtFZ/2gYMicLiya0
        state: present
      loop:
        - {name: "alovelace", groups: ["wheel,audio,video"]}
        - {name: "ghopper", groups: ["wheel,audio"]}
        - {name: "aturing", groups: "tape"}
        - {name: "edijkstra", groups: "tcpdump"}

```
# BONUS BONUS QUESTION

```
---
- name: Add multiple users and groups
  hosts: web
  become: true
  tasks:
    - name: Adding users to groups
      ansible.builtin.user:
        name: "{{ item.name }}"
        groups: "{{ item.groups }}"
        password: $6$0OKJBevDHxE636wl$l26Y0ttVrVa98wnDQ6ahgU1moy1tuEwv1qwc0HYwMEXQ2QtGiYoSA7X0SFVeWGu1ls9rAPTtFZ/2gYMicLiya0
        comment: "{{ item.realname }}"
        state: present
      loop:
        - {name: "alovelace", groups: ["wheel,audio,video"], realname: "Ada Lovelace"}
        - {name: "ghopper", groups: ["wheel,audio"], realname: "Grace Hopper"}
        - {name: "aturing", groups: "tape", realname: "Alan Turing"}
        - {name: "edijkstra", groups: "tcpdump", realname: "Edsger W. Dijkstra"}
```
