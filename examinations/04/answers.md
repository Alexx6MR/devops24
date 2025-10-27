## QUESTION A
If we add `state:started` to the service module. 
This tells Ansible that the service should be active (running).

```yml
- name: Ensure nginx is started at boot
  ansible.builtin.service:
    name: nginx
    enabled: true
    state: started #<-- add this line
```

## QUESTION B
Moving the `become: true` statement for a specific task to the top of the playbook allowed us to run each task as root and saved us from a lot of code repetition.


## QUESTION  C
To uninstall a service without breaking the server, the first thing we must do is disable and shut down the service. That's why we changed the order of things, first stopping and disabling the service and then uninstalling it. If you uninstall it while it's running, you could leave orphaned processes or errors in the system.

```yml
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

Examples of good names
```yml
Ensure nginx is installed 
Remove vim, bash-completion, and qemu-guest-agent
```