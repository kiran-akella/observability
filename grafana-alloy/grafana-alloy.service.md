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

# cat /usr/lib/systemd/system/alloy.service

```service
root@k8-master-node:~# cat /usr/lib/systemd/system/alloy.service
[Unit]
Description= Vendor-agnostic OpenTelemetry Collector distribution with programmable pipelines
Documentation=https://grafana.com/docs/alloy
Wants=network-online.target
After=network-online.target

[Service]
Restart=always
User=alloy
Environment=HOSTNAME=%H
Environment=ALLOY_DEPLOY_MODE=deb
EnvironmentFile=/etc/default/alloy
WorkingDirectory=/var/lib/alloy
ExecStart=/usr/bin/alloy run $CUSTOM_ARGS --storage.path=/var/lib/alloy/data $CONFIG_FILE
ExecReload=/usr/bin/env kill -HUP $MAINPID
TimeoutStopSec=20s
SendSIGKILL=no

[Install]
WantedBy=multi-user.target
```

# sudo journalctl -u alloy.service

```logs
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.166691096Z level=info msg="finished node evaluation" controller_path=/ controller_id="" trace_id=adb64dd077ad4db390637f349ce3c0eb node_id=labelstore duration=4.64µs
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.166739666Z level=info msg="finished node evaluation" controller_path=/ controller_id="" trace_id=adb64dd077ad4db390637f349ce3c0eb node_id=local.file_match.tmplogs duration=41.15µs
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.166944476Z level=info msg="finished node evaluation" controller_path=/ controller_id="" trace_id=adb64dd077ad4db390637f349ce3c0eb node_id=loki.source.file.local_files duration=194.4µs
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.166958426Z level=info msg="finished complete graph evaluation" controller_path=/ controller_id="" trace_id=adb64dd077ad4db390637f349ce3c0eb duration=1.57285ms
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167060656Z level=info msg="scheduling loaded components and services"
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167400556Z level=info msg="starting cluster node" service=cluster peers_count=0 peers="" advertise_addr=127.0.0.1:12345
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167633576Z level=info msg="peers changed" service=cluster peers_count=1 peers=k8-master-node
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167646346Z level=info msg="tail routine: started" component_path=/ component_id=loki.source.file.local_files component=tailer path=/var/log/auth.log
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167727426Z level=info msg="Seeked /var/log/auth.log - &{Offset:4904 Whence:0}" component_path=/ component_id=loki.source.file.local_files component=tailer
Mar 26 16:41:23 k8-master-node alloy[5444]: ts=2025-03-26T16:41:23.167943976Z level=info msg="now listening for http traffic" service=http addr=127.0.0.1:12345
```
