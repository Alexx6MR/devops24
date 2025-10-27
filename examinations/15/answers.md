## QUESTION A

1. To make this possible you just have to change the data within the Prometheus playbook for the following:
```bash
static_configs:
    - targets:
        - 'node-exporter:9100'
        - '<dbserver_ip>:9100'
        - '<webserver_ip>:9100'
```

2. Download the `node_exporter` executable and unzip it, then copy the contents to the correct folder. Make sure you give the executable privileges are correct.
```yml
- name: Ensure the node exporter installation file is on the server
    ansible.builtin.copy:
        src: "./files/node_exporter-1.9.1.linux-amd64/node_exporter"
        dest: "/usr/sbin/node_exporter"
        owner: root
        group: root
        mode: '0755'
```

3. Once changed, you just have to run the 15-node_exporter.yml playbook and that's it.

```bash
ansible-playbook ~/Desktop/devops24/examinations/15/15-node_exporter.yml
```