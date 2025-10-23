## QUESTION A
Displays the inventory that Ansible is currently using, in JSON format.

```json
{
    "_meta": {
        "hostvars": {
            "192.168.121.248": {
                "ansible_ssh_private_key_file": "~/.ssh/deploy_key",
                "ansible_user": "deploy"
            },
            "192.168.121.51": {
                "ansible_ssh_private_key_file": "~/.ssh/deploy_key",
                "ansible_user": "deploy"
            }
        }
    },
    "all": {
        "children": [
            "ungrouped",
            "db",
            "web"
        ]
    },
    "db": {
        "hosts": [
            "192.168.121.51"
        ]
    },
    "web": {
        "hosts": [
            "192.168.121.248"
        ]
    }
}
```
## QUESTION B
Displays the same inventory information but in the form of an ASCII graph.

```bash
@all:
  |--@ungrouped:
  |--@db:
  |  |--192.168.121.51
  |--@web:
  |  |--192.168.121.248
```

## QUESTION C
The `ansible_connection=local` parameter tells Ansible to run modules directly on the machine where you are running Ansible, without using SSH.

```bash
192.168.121.1 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.121.248 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
192.168.121.51 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

## BONUS QUESTION 
When you run `ansible-config dump` in your working directory where a local ansible.cfg exists, the output shows the effective configuration including your local values, for example: `host_key_checking = False` and `inventory = hosts`.

When you run it in your home directory, without a local `ansible.cfg`, the output reflects the system and user defaults and your local changes are not applied.

In other words, `ansible.cfg` in the working directory overwrites the default values while only the global and user values ​​are visible in the home directory.