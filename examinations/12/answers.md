## QUESTION A

Create two different roles and then email the playbook, if everything goes well it is because they are installed correctly if it does not go well it is because the roles were created incorrectly.

1. Create both roles.
```bash
ansible-galaxy role init dbserver
ansible-galaxy role init webserver
```
2. Run playbook
```bash
ansible-playbook ~/Desktop/devops24/examinations/12/12-roles.yml
```