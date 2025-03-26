# grafana systemd service file

```output
[root@redhat ~]# systemctl status grafana-server
● grafana-server.service - Grafana instance
     Loaded: loaded (/usr/lib/systemd/system/grafana-server.service; enabled; preset: disabled)
     Active: active (running) since Wed 2025-03-26 04:58:28 UTC; 46min ago
       Docs: http://docs.grafana.org
   Main PID: 894 (grafana)
      Tasks: 19 (limit: 48884)
     Memory: 247.7M
        CPU: 17.701s
     CGroup: /system.slice/grafana-server.service
             └─894 /usr/share/grafana/bin/grafana server --config=/etc/grafana/grafana.ini --pidfile=/var/run/grafana/grafana-server.pid --packaging=rpm cfg:default.paths.logs=/var/log/grafana cfg:default.paths.data=/var/lib/grafana cfg:default.paths.plugins=/var/lib/grafana/plugins cfg:default.paths.provisioning=/etc/grafana/provisioning
```
# cat /usr/lib/systemd/system/grafana-server.service
```service
[root@redhat ~]# cat /usr/lib/systemd/system/grafana-server.service
[Unit]
Description=Grafana instance
Documentation=http://docs.grafana.org
Wants=network-online.target
After=network-online.target
After=postgresql.service mariadb.service mysqld.service influxdb.service

[Service]
EnvironmentFile=/etc/sysconfig/grafana-server
User=grafana
Group=grafana
Type=notify
Restart=on-failure
WorkingDirectory=/usr/share/grafana
RuntimeDirectory=grafana
RuntimeDirectoryMode=0750
ExecStart=/usr/share/grafana/bin/grafana server                                     \
                            --config=${CONF_FILE}                                   \
                            --pidfile=${PID_FILE_DIR}/grafana-server.pid            \
                            --packaging=rpm                                         \
                            cfg:default.paths.logs=${LOG_DIR}                       \
                            cfg:default.paths.data=${DATA_DIR}                      \
                            cfg:default.paths.plugins=${PLUGINS_DIR}                \
                            cfg:default.paths.provisioning=${PROVISIONING_CFG_DIR}

LimitNOFILE=10000
TimeoutStopSec=20
CapabilityBoundingSet=
DeviceAllow=
LockPersonality=true
MemoryDenyWriteExecute=false
NoNewPrivileges=true
PrivateDevices=true
PrivateTmp=true
ProtectClock=true
ProtectControlGroups=true
ProtectHome=true
ProtectHostname=true
ProtectKernelLogs=true
ProtectKernelModules=true
ProtectKernelTunables=true
ProtectProc=invisible
ProtectSystem=full
RemoveIPC=true
RestrictAddressFamilies=AF_INET AF_INET6 AF_UNIX
RestrictNamespaces=true
RestrictRealtime=true
RestrictSUIDSGID=true
SystemCallArchitectures=native
UMask=0027

[Install]
WantedBy=multi-user.target
```


# sudo journalctl -u grafana-server.service
```logs
Mar 26 04:59:28 redhat grafana[894]: logger=infra.usagestats t=2025-03-26T04:59:28.334564627Z level=info msg="Usage stats are ready to report"
Mar 26 05:08:28 redhat grafana[894]: logger=cleanup t=2025-03-26T05:08:28.329749321Z level=info msg="Completed cleanup jobs" duration=33.332267ms
Mar 26 05:08:28 redhat grafana[894]: logger=plugins.update.checker t=2025-03-26T05:08:28.883091182Z level=info msg="Update check succeeded" duration=267.654155ms
Mar 26 05:18:28 redhat grafana[894]: logger=cleanup t=2025-03-26T05:18:28.298673359Z level=info msg="Completed cleanup jobs" duration=2.393788ms
Mar 26 05:18:28 redhat grafana[894]: logger=plugins.update.checker t=2025-03-26T05:18:28.880270569Z level=info msg="Update check succeeded" duration=264.624751ms
Mar 26 05:28:28 redhat grafana[894]: logger=cleanup t=2025-03-26T05:28:28.299816053Z level=info msg="Completed cleanup jobs" duration=3.146022ms
Mar 26 05:28:28 redhat grafana[894]: logger=plugins.update.checker t=2025-03-26T05:28:28.878893857Z level=info msg="Update check succeeded" duration=263.728422ms
Mar 26 05:29:28 redhat grafana[894]: logger=infra.usagestats t=2025-03-26T05:29:28.340247614Z level=info msg="Usage stats are ready to report"
Mar 26 05:38:28 redhat grafana[894]: logger=cleanup t=2025-03-26T05:38:28.298885126Z level=info msg="Completed cleanup jobs" duration=2.251452ms
Mar 26 05:38:28 redhat grafana[894]: logger=plugins.update.checker t=2025-03-26T05:38:28.875908295Z level=info msg="Update check succeeded" duration=260.947359ms
```
