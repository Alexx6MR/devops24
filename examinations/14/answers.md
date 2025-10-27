## QUESTION A
In the `14-firewall.yml` file we gonna need 3 block.
Every block will make a change in the one or both server.


1. This block is to ensure that `firewalld` and `python3-firewall` are installed and running.
```yml
- name: Configure firewalld on all servers
  hosts: all
  become: true
  tasks:
    - name: Ensure firewalld and python3-firewall are installed
      ansible.builtin.package:
        name:
          - firewalld
          - python3-firewall
        state: present

    - name: Enable and start firewalld service
      ansible.builtin.service:
        name: firewalld
        state: started
        enabled: true
```
2. This block is to ensure that `http` and `http` are enabled in firewalld.
```yml
- name: Configure webserver firewall
  hosts: webserver
  become: true
  tasks:
    - name: Enable HTTP and HTTPS services in firewalld
      ansible.posix.firewalld:
        service: "{{ item }}"
        permanent: true
        state: enabled
        immediate: true
      loop:
        - http
        - https
```
3. This block is to ensure that `msql` is enabled in firewalld.
```yml
- name: Configure dbserver firewall
  hosts: dbserver
  become: true
  tasks:
    - name: Enable MySQL service in firewalld
      ansible.posix.firewalld:
        service: mysql
        permanent: true
        state: enabled
        immediate: true
```