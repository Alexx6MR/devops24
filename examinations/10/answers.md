## QUESTION A
To complete this task we just need to convert the static nginx configuration file into a Jinja2 template and then use the template module instead of copy.

1. Create a new folder called `templates` inside your working directory and copy the original configuration file `example.internal.conf` from examination 6.
Rename it as:

```bash
    templates/example.internal.conf.j2
```
2. Edit that file and replace the static IPs in the listen directives with the dynamic variable `{{ ansible_default_ipv4.address }}`:

```bash
    listen {{ ansible_default_ipv4.address }}:80;
    listen {{ ansible_default_ipv4.address }}:443 ssl;
```
> note: `ansible_default_ipv4.address` is automatically discovered by Ansible when it gathers system facts. It contains the main IPv4 address of the remote host.

3. Make a new playbook and add something like this:

```yml
---
- name: Configure nginx using a template
  hosts: webserver
  become: true
  tasks:
    - name: Ensure the that nginx render the vhost from template
      ansible.builtin.template:
        src: ./templates/example.internal.conf.j2
        dest: /etc/nginx/conf.d/example.internal.conf
        owner: root
        group: root
        mode: '0644'
      notify: Reload nginx

  handlers:
    - name: Reload nginx
      ansible.builtin.service:
        name: nginx
        state: restarted
```
> note: It is a good practice to use `handlers` so we gonna use it in every playbook now on.

4. Run the command and check the website.
```bash
    ansible-playbook 10-web-template.yml
```

5. To verify that everything went well, you just need to connect to the server and then verify the file.
```bash
    ssh webserver
    cat /etc/nginx/conf.d/example.internal.conf
```
> note: `ssh webserver` is the way I configured it, enter the way you have done it.