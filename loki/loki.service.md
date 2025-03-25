# Promtail system service file

```output
[root@redhat ~]# sudo systemctl status loki
● loki.service - Loki service
     Loaded: loaded (/etc/systemd/system/loki.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-03-25 16:17:07 UTC; 25s ago
   Main PID: 911 (loki)
      Tasks: 13 (limit: 48884)
     Memory: 122.7M
        CPU: 231ms
     CGroup: /system.slice/loki.service
             └─911 /usr/bin/loki -config.file /etc/loki/config.yml
```
# sudo /etc/systemd/system/loki.service

```service
[root@redhat ~]# cat /etc/systemd/system/loki.service
[Unit]
Description=Loki service
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=loki
ExecStart=/usr/bin/loki -config.file /etc/loki/config.yml
# Give a reasonable amount of time for the server to start up/shut down
TimeoutSec = 120
Restart = on-failure
RestartSec = 2

[Install]
WantedBy=multi-user.target
```

# sudo journalctl -u loki.service

```logs
Mar 25 16:17:31 redhat loki[911]: level=debug ts=2025-03-25T16:17:31.796678367Z caller=mock.go:186 msg="Get - deadline exceeded" key=collectors/ring
Mar 25 16:17:31 redhat loki[911]: level=debug ts=2025-03-25T16:17:31.7966846Z caller=mock.go:150 msg=Get key=collectors/ring wait_index=16
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796636683Z caller=mock.go:186 msg="Get - deadline exceeded" key=collectors/scheduler
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796696863Z caller=mock.go:150 msg=Get key=collectors/scheduler wait_index=12
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796709036Z caller=mock.go:186 msg="Get - deadline exceeded" key=collectors/distributor
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.79671794Z caller=mock.go:150 msg=Get key=collectors/distributor wait_index=14
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796723526Z caller=mock.go:186 msg="Get - deadline exceeded" key=collectors/pattern-ring
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.79672776Z caller=mock.go:150 msg=Get key=collectors/pattern-ring wait_index=13
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796731776Z caller=mock.go:186 msg="Get - deadline exceeded" key=collectors/compactor
Mar 25 16:17:32 redhat loki[911]: level=debug ts=2025-03-25T16:17:32.796735565Z caller=mock.go:150 msg=Get key=collectors/compactor wait_index=15
```
