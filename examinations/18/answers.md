## QUESTION A


```bash

```

## QUESTION B

1. Create the directory that appeared in the DEFAULT_MODULE_PATH(default)
```bash
mkdir -p ~/.ansible/plugins/modules
```
2. Copy the Ansible module to the new directory. We are in ansible folder.
```bash
cp library/anagrammer.py ~/.ansible/plugins/modules/anagrammer.py
```

## QUESTION  C

1. This is the playbook that gonna use the module we just copied.
```bash
---
- name: Test the Custom Anagrammer Module
  hosts: localhost
  become: true
  vars:
    message: "hello world"

  tasks:
    - name: Run anagrammer module with the message variable
      anagrammer:
        message: "{{ message }}"
      register: anagram_result

    - name: Display the results
      ansible.builtin.debug:
        msg:
          - "Original Message: {{ anagram_result.original_message }}"
          - "Reversed Message: {{ anagram_result.reversed_message }}"
          - "Changed Status: {{ anagram_result.changed }}"
```

2. run the playbook:
```bash
ansible-playbook --verbose --extra-vars message='"This is a whole other message"' ~/Desktop/devops24/examinations/18/18-anagrammer.yml --ask-become-pass
```
> note: Remember to pass the `--ask-become-pass` flag for it to run correctly.


## BONUS QUESTION 
What is the relationship between the booleans you can use in Python, and the various "truthy/falsy" values
you most often use in Ansible?

**Answer:**
Ansible use Jinja2 motor and that flexibility accepts strings like `"False"` or `"yes"` as booleans. But Python evaluates the string `"False"` as `True` because it is a non-empty string.

What modules/filters are there in Ansible that can safely test for "truthy/falsy" values, and return something
more stringent?

**Answer:** In Ansible, the safest way to test `truthy` and `falsy` values is by using filters and modules that force strict evaluation. The most common filter is `| bool`, which converts any variable into a real boolean.

for example:
```yml
when: my_var | bool
```
> If `my_var` is `yes`, `1`, or True, the condition passes; otherwise, it fails.