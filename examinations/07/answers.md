# QUESTION A
-------
I created the following tasks for mariadb-service 

```
    - name: Ensure MariaDB is started at boot
      ansible.builtin.service:
	      name: mariadb
	      enabled: true

    - name: Ensure MariaDB is started
      ansible.builtin.service:
	      name: mariadb
	      state: started
```



# QUESTION B
-------------
One of the ways is to use `ssh deploy@dbserver(or ip ad) "systemctl status mariadb"` or ` " ps aux | grep mariadb "` to ensure that the service is
up and running. In our case, with vagrant enviorment i had to do the following command `vagrant ssh dbserver -c "systemctl status mariadb(or ps aux | grep mariadb)"` 
# BONUS QUESTION
--------------
I mentioned two of the ways above, but both through the same mean. Using commands on the server directly through ssh. I can log  into the server
and try to check if the service is running by using the commands above or similar ones. I can also use `ansible.builtin.commands` in a playbook
to ensure that Mariadb is running if I want. 
