## QUESTION A
To do this step, use a basic methodology of separating the "logic" into different files.

1. Create a folder called `vars` and inside a files with the following names and contents.

- `users.yml`: It stores all user information, so if more users are added in the future, the source code remains intact.
```yml
users:
  - username: alovelace
    groups: wheel,audio,video
  - username: aturing
    groups: tape
  - username: edijkstra
    groups: tcpdump
  - username: ghopper
    groups: wheel,audio
```


2. Create the playbook and add the following code.
```yml
---
- name: Users creator into the web server
  hosts: webserver
  become: true
  vars_files:
    - vars/users.yml

  tasks:
    - name: Ensure users exist with required supplementary groups
      ansible.builtin.user:
        name: "{{ item.username }}"
        state: present
        groups: "{{ item.groups }}"
        append: false # secures exactly those groups (idempotent)
        create_home: true

      loop: "{{ users }}"
```

3. Run the command:

```bash
ansible-playbook ~/Desktop/devops24/examinations/11/11-users-creator.yml
```

## QUESTION B

1. Create a folder called files and add 3 empty files that end with `.md`.

```bash
bar.md
baz.md
foo.md
```

2. Create a playbook and paste the follwing code.
```yml
---
- name: Copy all .md files to deploy's home on dbserver
  hosts: dbserver
  become: true
  tasks:
    - name: Transfer files to dbserver
      ansible.builtin.copy:
        src: "{{ item }}"
        dest: "/home/deploy/{{ item | basename }}"
        owner: deploy
        group: deploy
        mode: '0644'
      with_fileglob:
        - "files/*.md"
```
>note: The destination is `/home/deploy/` so that the files are saved on the `deploy` user's home directory.

3. Run the playbook.

## BONUS QUESTION 
In the previously created directory `vars`, add another file called `user_passwords.yml`. The file will store the users password. I don't see it as a good practice to have the passwords for each user in plain text, although they will later be encrypted using `sha512`.

1. Add the following content to the file.
```bash
users_passwords:
  alovelace: "Password"
  aturing:   "Password"
  edijkstra: "Password"
  ghopper:   "Password"
```

2. Add new lines to the previus playbook.
```yml
---
- name: Users creator into the web server
  hosts: webserver
  become: true
  vars_files:
    - vars/users_passwords.yml #(new) This line is to know where to get the password
    - vars/users.yml

  tasks:
    - name: Ensure users exist with required supplementary groups
      ansible.builtin.user:
        name: "{{ item.username }}"
        password: "{{ users_passwords[item.username] | password_hash('sha512', item.username) }}" #(new) The explanation is below in a note.
        state: present
        groups: "{{ item.groups }}"
        append: false # secures exactly those groups (idempotent)
        create_home: true

      loop: "{{ users }}"
```
> note: If you look in the password field, we've created a way for the password to be encrypted on the fly and sent to the server already encrypted.

## BONUS BONUS QUESTION 
1. In the `users` file we created, add a `realname` field to each user.

```yml
users:
  - username: alovelace
    realname: alfred lovelace
    groups: wheel,audio,video
  - username: aturing
    realname: anhia turing
    groups: tape
  - username: edijkstra
    realname: eddie dijkstra
    groups: tcpdump
  - username: ghopper
    realname: george hopper
    groups: wheel,audio
```

2. Add this line of code below the `name` field in the playbook you made.

```yml
name: "{{ item.username }}"
comment: "{{ item.realname }}" # <- GECOS is here
password: "{{ users_pa....."
```
3. Run the playbook for the last time and check in the server to se the results.