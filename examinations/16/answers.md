## QUESTION A

1. Here you can download the latest PDF with the checks that need to be done: https://downloads.cisecurity.org/#/

2. I separated the tests into two fairly simple roles, 

- `cis_packages`: Checks that have to do with programs.
- `cis_services`: Checks that have to do with services.

3. run the playbook:
```bash
ansible-playbook ~/Desktop/devops24/examinations/16/16-compliance-check.yml
```

## BONUS QUESTION 

To be able to separate them into roles you just have to run the following command:
```bash
ansible-galaxy init ~/Desktop/devops24/examinations/16/roles/cis_packages
ansible-galaxy init ~/Desktop/devops24/examinations/16/roles/cis_services
```