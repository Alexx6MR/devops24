## QUESTION A

The ansible.builtin.debug module prints messages or variable values to help see what Ansible is doing.

```bash
ok: [webserver] => {
    "ansible_facts.hostname": "webserver"
}
```

## QUESTION B
ansible_facts is a dictionary of system information that Ansible automatically collects from each host before running tasks (via the setup module).

```bash

```

## QUESTION  C
To remove the same software you installed, set state: absent in the playbook.

```bash
---
- name: Uninstall packages
  hosts: all
  tasks:
    - name: Remove vim, bash-completion, and qemu-guest-agent
      become: true
      ansible.builtin.package:
        name: vim,bash-completion,qemu-guest-agent
        state: absent
```

## BONUS QUESTION 
Examples of Ansible playbook options:

* `--verbose`: increases the amount of information Ansible shows while running.
* `-v`: basic details.
* `-vv`: adds connection info.
* `-vvv`: shows full stask data.
* `-vvvv`: includes SSH debugging.
* `--check`: Runs a dry run. Shows what changes would happen without actually changing anything.
* `--syntax-check`: Checks if the playbooks syntax is valid before running it.
