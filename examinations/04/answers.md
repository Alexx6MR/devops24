## QUESTION A
Add `state:started` to the service module.
This tells Ansible that the service should be active (running) and enabled.

```bash
- name: Ensure nginx is started at boot
  ansible.builtin.service:
    name: nginx
    enabled: true
    state: started #<-- add this line
```

## QUESTION B
Causes all tasks within the playbook to run as superuser (root), without having to type `become: true` in each task.


## QUESTION  C
Because you can't first uninstall a service that's still running. You must stop and disable it before removing it.
If you uninstall it while it's running, you may leave orphaned processes or errors in the system.

```bash
---
- name: Uninstall a webserver
  hosts: web
  become: true
  tasks:
    - name: Ensure nginx is not started at boot
      ansible.builtin.service:
        name: nginx
        state: stopped
        enabled: false
    
    - name: Ensure nginx is uninstalled
      ansible.builtin.package:
        name: nginx
        state: absent
```

## BONUS QUESTION 
The name should clearly describe the action and purpose of the task, not what the code does internally.
It should answer the question: "What does this task accomplish?"

Exemepl
```bash
Ensure nginx is installed 
Remove vim, bash-completion, and qemu-guest-agent
```