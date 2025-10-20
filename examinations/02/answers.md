# QUESTION 1 
-------
If i run ansible-inventory --list, what happens is that i get an overview of my servers and their information.
I can see the ip-addresses that are written in my hostfile, and also see what the path for my keys are and also what user that is used. 


# QUESTION 2
-------------
What happens if i use the --graph instead of --list is that i see a simpler to read version (graph) of my servers and their ip-addresses. 
It serves as a quick overview of my servers and the groupings, instead of seeing all the information I can use this to quickly check my servers
addresses and groupings.

# QUESTION 3 
----------
The ```ansible_connection=local
```
means that it should look for a localhost instead of an virtual connection. Instead of providing ip-addresses i can simply point to my host by using 
this parameter. If i try to use the ip-address it will instead refuse the connection cause of the fact that it cant connect to itself through ssh. 

# BONUS QUESTION
--------------
So from what I can gather, the dump is showing different values depending on where it's run. In my ansible dir, I can see what file ansible 
reads for hosts, and also see that my host_key_checking is off. I can also see that it is reading the config file from /home/hubba/ansible-conf/ansible.cfg
and as mentioned earlier see what file it reads hosts from. Whereas when I run it in my home directory without any ansible configuration, it only shows
that it has no config file to read from. Since it is unconfigured. 
