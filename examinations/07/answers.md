## QUESTION A
To ensure that mariadb-server starts when the server is powered on, we need to add the following line:

```bash
- name: Ensure MariaDB-server is started at boot
      ansible.builtin.service:
        name: mariadb-server
        enabled: true
        state: started
```

## QUESTION B

To ensure that the mariadb service is started and running, you can do it in two ways. Connect to mariadb using the command `ansible db -m command -a "systemctl status mariadb"`.

**Expected Result**
```bash
192.168.121.51 | CHANGED | rc=0 >>
● mariadb.service - MariaDB 10.11 database server
     Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-10-21 13:49:36 UTC; 42s ago
 Invocation: b276df54cd774cb9bf8a2e600044ce90
       Docs: man:mariadbd(8)
```

## BONUS QUESTION 

There are several different ways to verify that the MariaDB service is running and you can see a feew below:

1. With systemd commands:
    * `systemctl is-active mariadb` -> should return active.
    * `systemctl status mariadb` -> shows process info and uptime.

2. With Ansible:
    * `ansible dbserver -m command -a "mysqladmin ping"` -> returns mysqld is alive.