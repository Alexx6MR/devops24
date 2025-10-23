## QUESTION A


1. In the `tasks/main.yml` file, add the following code:

```yml
---
- name: Deploy nginx new websidan
  ansible.builtin.copy:
    src: files/index.html
    dest: /var/www/example.internal/html/index.html
    owner: root
    group: root
    mode: '0644'
  notify:
    - Reload nginx
```
2. In the `handlers/main.yml` file, add the following code:

```yml
---
- name: Reload nginx
  ansible.builtin.service:
    name: nginx
    state: reloaded
```

3. Inside the folder `files`, add a `index.html` file with some modifications.
4. Create the playbook file and run it. The content must be something like this:

```yml
---
- name: Configure the web server(s) according to specs
  hosts: webserver
  become: true
  roles:
    - webserver
```