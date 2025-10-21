# QUESTION A
-------
I made sure to only keep the diffrences compared to the previous assignment in this question 
```
---
    - name: Create Mariadb user and grant * privileges on webbappd
      community.mysql.mysql_user:
        name: webappuser
        password: "{{ webappdb_password }}"
        priv: webappdb.*:ALL
        login_unix_socket: /var/lib/mysql/mysql.sock

  vars_files:
    - vars/dbvault.yml
```

# QUESTION B
-------
For this question, I just used `ansible-vault encrypt vars/vaultdb.yml`. 
The password to decrypt the vault is "notsosecretpassword"

