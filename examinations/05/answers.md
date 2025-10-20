# QUESTION 1 
-------
While running the play the first time, I can see that changes has been made, whereas running it the second time, nothing is changed.
The output while running it the first time is yellow to show that it's changed whereas the second time it's green to show that everything was ok.

# QUESTION 2
-------------
I used the following task to ensure that nginx restarted  ```
- name: Restart nginx service and enable autostart 
      ansible.builtin.service:
        name: nginx
        state: restarted
```

# QUESTION 3 
----------
It goes against the ansible way, where things should only restart if there are changes made to the service in question. Since working in ansible 
you should strive for idempotency, which is defined by the meaning above. Also there is risks for downtime, which is something you would like to avoid
in production enviroments.

# BONUS QUESTION
--------------
I could find two other modules to use, one is ansible.builtin.systemd and the newer version one which is ansible.builtin.systemd_service.
