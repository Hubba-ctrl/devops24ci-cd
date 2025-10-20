# QUESTION 1 
-------
By adding state: started we can make sure that the webserver is started when running the playbook. This variable makes sure that the server is started, by checking if it is it does nothing, or if it's not started it makes sure that it starts up. 

# QUESTION 2
-------------
By adding become=true before the tasks, and as the same indention as task, you make sure that all tasks in that playbook are run as sudo, instead of just having a specific task run as sudo

# QUESTION 3 
----------
The reason to why we change the order of the task is because the fact that you have to disable the service before uninstalling it, whereas when you start the service you have to make sure it's installed before starting it. 


# BONUS QUESTION
--------------
By making sure that the name of both the playbook and the task within the playbook accurately describes what it's doing, we make sure that there is no confusion when running different playbooks. 
