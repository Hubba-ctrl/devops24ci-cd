# QUESTION 1 
-------
I created the following task for the directory
```
 - name: create directory structure 
      ansible.builtin.file:
        path: /var/www/example.internal/html/
        state: directory 
        owner: root
        group: root
        mode: "0755"
        settype: httpd_sys_content_t
        recurse: yes
```

and for the upload task i wrote the following task
```
- name: Upload index.html into var
      ansible.builtin.copy:
        src: files/index.html
        dest: /var/www/example.internal/html/index.html
        owner: root
        group: root
        mode: "0644"
        setype: httpd_sys_content_t
```



# QUESTION 2
-------------
I feel like this way is usable for small playbooks, but if you have larger ones you might need to think of other ways. I have read about handlers
but the issue for me right this second is that the docs for ansible seems to be down, but I can see through google searchs that handlers are alot
more common for big production playbooks. 

# BONUS QUESTION
--------------
As mentioned earlier, if i had a huge playbook, I would use handlers in Ansible to minimize the amount of restarts. By seperating my change
operations and restart operations, I would make sure that all my changes are made, before a restart happens. I did something similar in this assignment
by using registers. First time I ran it, it restart nginx, but the second time it did not. But to answer the question my ideal flow would be the following:
**1.** Apply all of my configurations
**2.** Validate that my configuration syntax is correct which --check or --syntax-check and ansible-lint 
**3.** Make sure that the services in question only get restarted once everything is ready to be updated, installed


