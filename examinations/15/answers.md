## QUESTION A

1. To make this possible you just have to change the data within the Prometheus playbook for the following:
```bash
static_configs:
    - targets:
        - 'node-exporter:9100'
        - '192.168.121.248:9100'
        - '192.168.121.51:9100'
```

1. Once changed, you just have to run the 10-node_exporter.yml playbook and that's it.