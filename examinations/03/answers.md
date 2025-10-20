# QUESTION 1 
-------
ansible.builtin.debug is a module used to debug ur tasks. Depending on what type of variables you set it has the possibility to give you different type of debug messages. 
By using this module, you can debug your tasks while running them, which makes it alot easier to debug the problems that could occur when running your playbook. 
You can both use set parameters but also use variables, while using the module to debug. 

# QUESTION 2
-------------
ansible_facts variable is a variable used in the ansible.builtin.debug, which can show you different type of facts. In the assigment, we use ansible_facts.nodename which shows us the different name for our nodes, in this case hosts. 
You can use another type of variable such as type or any of the variables you can find under the docs site. 

# QUESTION 3 
----------
The easiest way for me to uninstall the previously installed packages is by chaning the state to absent instead of present. I copied everything from the site.yml to the 03-uninstall-software-yml and only changed the state from present to absent. I then ran the playbook and it uninstalled all the previously installed packages.
 

# BONUS QUESTION
--------------
By using the different verbose option -v -vv -vvvv I can get more detailed information of the tasks running. By that i mean that you get more thorough information by each -v added. This is not something used only by ansible, it is a function that is used by alot of tools. 

By using --check, it doesnt actually execute the playbook, it instead tries to check what would happened if you ran the playbook. It seems like a useful tool to check your playbooks before executing them.

By using --syntax-check we can check that the structure and the format of the playbook is correctly formed. It doesnt actually connect to hosts, but instead just checks the syntax. In some cases, --checks won´t get you that far since it actually connects to hosts, instead of just checking the formatation fo the playbook.
