# QUESTION A 
-----------------
The permissions set in ~/.ssh directory are rwx for user and no other permissions for groups or others. UG is deploy deploy, and the reason to why the permissions is set in this way is because ssh required strict mode. 
If the permissions in my file would allow for group or other to login, sshd would refuse the connection. This is a security parameter taken by ssh. 

# QUESTION B
-----------------
autorized_keys has a list of public keys, these are the keys that are allowed to login to the account without a password. Not much else to say about this one


# QUESTION C
--------------
The way I would go about this assignment is to create a key using my deploy user in webserver, and then copy the key to dbserver directly using ssh. So basically using 
```bash
ssh-keygen -t ed25519 
```

and then to copy the ssh key to dbserver through ssh. 

```bash 
ssh-copy-id deploy@192.168.121.188
```

I had one issue, and that was that i had no possibility to use the command above, without providing the deploy@dbserver accounts password. I do not know if i did it the correct way, but i decided to login to dbserver and then used 
```bash 
sudo passwd deploy
```
to change the password. After that i could copy the ssh-key using ssh-copy-id and from there on i was able to login to  dbserver without providing a passphrase. 
I am fully aware that i could just cat my -pub key from one server to the others authorized_keys, but i wanted to use ssh-copy-id since it was provdided as a tip in the readme

# BONUS QUESTION 
--------------
Yes, one of the easiest ways to do it is through using ssh deploy@dbserver "insert_command" 


