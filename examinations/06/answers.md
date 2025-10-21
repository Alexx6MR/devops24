## QUESTION A

1. One task to create the directory structure under `/var/www/example.internal/html/`.

```bash
 - name: Create directory structure for example.internal
      ansible.builtin.file:
        path: /var/www/example.internal/html
        state: directory
        mode: '0755'
```
2. One task to upload our `files/index.html` file to `/var/www/example.internal/html/index.html`.

```bash
 - name: Ensure the index.html file is uploded for nginx
      ansible.builtin.copy:
        src: files/index.html
        dest: /var/www/example.internal/html/index.html
        owner: root
        group: root
        mode: '0644'
        backup: true
```

## QUESTION B
Using "register+when" works for small cases, but in a real production environment, using controllers is recommended. Using "register+when" repeats logic, is fragile, and can cause unnecessary or multiple restarts in the same run. Controllers add changes and restart only once.


## BONUS QUESTION 
Personally, I would store the results of tasks that might require a restart in variables and prioritize them from most to least important. Then, I would place the restart step at the end of the playbook and only perform it if necessary.