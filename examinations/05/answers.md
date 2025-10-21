## QUESTION A

The first output shows that the playbook successfully copied the file to the remote machine.
The task result includes `changed: true`, meaning Ansible detected that `/etc/nginx/conf.d/https.conf` did not exist before and created it.

```bash
Using /home/alexei/Desktop/devops24/ansible/ansible.cfg as config file

PLAY [Configure nginx from http to https] ********************************************************************

TASK [Gathering Facts] ***************************************************************************************
ok: [192.168.121.248]

TASK [Copy https file into nginx] ****************************************************************************
changed: [192.168.121.248] => {"changed": true, "checksum": "4928f5d40694d15bf3e276596d47b8fc75544d59", "dest": "/etc/nginx/conf.d/https.conf", "gid": 0, "group": "root", "md5sum": "a3bb0c727d3e156afa3a11d78b406c83", "mode": "0644", "owner": "root", "secontext": "system_u:object_r:httpd_config_t:s0", "size": 465, "src": "/home/deploy/.ansible/tmp/ansible-tmp-1761046895.8166173-11365-104684179706764/source", "state": "file", "uid": 0}

PLAY RECAP ***************************************************************************************************
192.168.121.248            : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

The second output shows that the playbook detected no changes were needed on the remote machine.
The task result includes `changed: false`, meaning Ansible verified that `/etc/nginx/conf.d/https.conf` already existed and was identical to the source file, so it did not copy it again.


```bash
PLAY [Configure nginx from http to https] ********************************************************************

TASK [Gathering Facts] ***************************************************************************************
ok: [192.168.121.248]

TASK [Copy https file into nginx] ****************************************************************************
ok: [192.168.121.248] => {"changed": false, "checksum": "4928f5d40694d15bf3e276596d47b8fc75544d59", "dest": "/etc/nginx/conf.d/https.conf", "gid": 0, "group": "root", "mode": "0644", "owner": "root", "path": "/etc/nginx/conf.d/https.conf", "secontext": "system_u:object_r:httpd_config_t:s0", "size": 465, "state": "file", "uid": 0}

PLAY RECAP ***************************************************************************************************
192.168.121.248            : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

```
## QUESTION B
state: restarted → restarts the service.
Allows nginx to reload the new HTTPS configuration without you having to do it manually.

```bash
 - name: Restart nginx to apply new configuration
      ansible.builtin.service:
        name: nginx
        state: restarted
```

## QUESTION  C

If the service is constantly restarted, even unnecessarily:

* Active connections are dropped unnecessarily.
* This may cause brief downtime.
* This may cause increased system load or errors in production.
* This violates Ansible's idempotence philosophy (only change if necessary).

**Better solution:**
Use `handlers` to restart only when the file changes.

## BONUS QUESTION 

1. `systemd` Controls services directly.

```bash
- name: Restart nginx using systemd
  ansible.builtin.systemd:
    name: nginx
    state: restarted
```

2. `command` They execute manual commands. It's not the "cleanest" way, but it's possible.

```bash
- name: Restart nginx manually
  ansible.builtin.command: systemctl restart nginx
```