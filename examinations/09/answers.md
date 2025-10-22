## QUESTION A
To complete this part we just have to follow the steps below but Before continuing, remember to create the `vars` folder and inside a file called `secret.yml`:

1. Add the following line to the playbook `09-mariadb-password.yml`.

```yml
    become: true

    vars_files:
        - vars/secret.yml

    tasks:
```
> note: This prevents us from having to pass the variable through parameters in the command.


2. Change the password to a variable that we have in the file `vars/secret.yml`.
```yml
 - name: Create user webappuser with password from var
      community.mysql.mysql_user:
        name: webappuser
        password: "{{ webapp_password }}"
        priv: "webappdb.*:ALL"
        host: "%"
        state: present
        login_unix_socket: /var/lib/mysql/mysql.sock
        check_implicit_admin: true
```
3. Create a variables file (unencrypted for now) to test:
```yml
# vars/secret.yml
webapp_password: secretpassword
```
4. Run command:
```bash
ansible-playbook 09-mariadb-password.yml
```

## QUESTION B

1. Encrypts the existing variables file.

```bash
ansible-vault encrypt vars/secret.yml
```
> note: It will ask you for a Vault password (example: vaul123).

2. Save that password in plain text so the teacher can use it.

```bash
echo "vaul123" > vault_pass.txt
```
3. check that the file is encrypted.

```bash
cat vars/secret.yml
```
**Expected result**
```bash
$ANSIBLE_VAULT;1.1;AES256
6537323931663434623439336337356363363366623030303230636136623338...
```
4. Run command:
```bash
ansible-playbook 09-mariadb-password.yml --vault-password-file vault_pass.txt
```



