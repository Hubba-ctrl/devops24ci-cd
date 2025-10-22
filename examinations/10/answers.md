# QUESTION A
-------
Took some time to get through the docs, but I did not find anything about how to reference the fact of the default ipv4-address. I just did a quick 
google search and found how to reference the fact in my .j2 template. The way my template looks right now is the code below. 
```
server {
    listen {{ ansible_default_ipv4.address }}:80;
    listen {{ ansible_default_ipv4.address }}:443 ssl;
    root /var/www/example.internal/html;
    index index.html;
    server_name example.internal;

    ssl_certificate "/etc/pki/nginx/server.crt";
    ssl_certificate_key "/etc/pki/nginx/private/server.key";
    ssl_session_cache shared:SSL:1m;
    ssl_session_timeout  10m;
    ssl_ciphers PROFILE=SYSTEM;
    ssl_prefer_server_ciphers on;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

In my playbook, i made sure to put `gather_facts: true` at the top. I then changed only changed one task, which was the one where i copied the static
config to the webserver. Instead i used the builtin.template and referenced the jinja2 file above, with the following task 
```
    - name: Use nginx example.internal template to webserver
      ansible.builtin.template:
        src: templates/example.internal.conf.j2
        dest: /etc/nginx/conf.d/example.internal.conf
        owner: root
        group: root
        mode: "0644"
      register: exampleconf

´´´ 
