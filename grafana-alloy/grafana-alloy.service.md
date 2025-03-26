# grafana-alloy system service file

```output
root@k8-master-node:~# sudo systemctl status alloy
● alloy.service - Vendor-agnostic OpenTelemetry Collector distribution with programmable pipelines
     Loaded: loaded (/usr/lib/systemd/system/alloy.service; enabled; preset: enabled)
     Active: active (running) since Wed 2025-03-26 16:41:23 UTC; 5min ago
       Docs: https://grafana.com/docs/alloy
   Main PID: 5444 (alloy)
      Tasks: 12 (limit: 9516)
     Memory: 35.8M (peak: 38.2M)
        CPU: 885ms
     CGroup: /system.slice/alloy.service
             └─5444 /usr/bin/alloy run --storage.path=/var/lib/alloy/data /etc/alloy/config.alloy
```
