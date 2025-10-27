## QUESTION A

Each role that is created has a complete version of the last examinations, but in a more simplified form, which means that if we run the roles we should have the same results as if we had run the examinations in order.

1. Create both roles.
```bash
ansible-galaxy role init webserver
ansible-galaxy role init dbserver
```
- `webserver`: In the webserver/tasks/main role, add the content of exams 4, 5, 6, 10
- `dbserver`: In the dbserver/tasks/main role, add the content of exams 7, 8, 

2. Run playbook
```bash
ansible-playbook ~/Desktop/devops24/examinations/12/12-roles.yml
```
>note: I recommend to use `--check` to see the result without changing nothing.