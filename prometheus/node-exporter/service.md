[root@redhat ~]# sudo systemctl status node_exporter
● node_exporter.service - Prometheus Node Exporter
     Loaded: loaded (/etc/systemd/system/node_exporter.service; disabled; preset: disabled)
     Active: active (running) since Tue 2025-03-25 17:42:18 UTC; 10min ago
   Main PID: 2690 (node_exporter)
      Tasks: 5 (limit: 48884)
     Memory: 24.3M
        CPU: 1.155s
     CGroup: /system.slice/node_exporter.service
             └─2690 /usr/bin/node_exporter --web.config.file /etc/prometheus/web.yml

Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=time
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=timex
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=udp_queues
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=uname
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=vmstat
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=watchdog
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=xfs
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.293Z level=INFO source=node_exporter.go:141 msg=zfs
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.298Z level=INFO source=tls_config.go:347 msg="Listening on" address=[::]:9100
Mar 25 17:42:18 redhat node_exporter[2690]: time=2025-03-25T17:42:18.299Z level=INFO source=tls_config.go:386 msg="TLS is disabled." http2=false address=[::]:9100
[root@redhat ~]# cat /etc/systemd/system/node_exporter.service
[Unit]
Description=Prometheus Node Exporter
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/bin/node_exporter --web.config.file /etc/prometheus/web.yml
[Install]
WantedBy=multi-user.target

[root@redhat ~]# cat /etc/prometheus/web.yml
basic_auth_users:
  kiran: $2b$12$DLTQ.j0oK7lkmnUOsjrtl.R4EAdiYgS.jXTiR6H85flP2ezT49Wuq
[root@redhat ~]# 
