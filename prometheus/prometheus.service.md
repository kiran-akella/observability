# prometheus system service file

```status
[root@redhat ~]# sudo systemctl status prometheus
● prometheus.service - Prometheus
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; preset: disabled)
     Active: active (running) since Tue 2025-03-25 16:17:07 UTC; 46min ago
   Main PID: 928 (prometheus)
      Tasks: 15 (limit: 48884)
     Memory: 117.9M
        CPU: 3.550s
     CGroup: /system.slice/prometheus.service
             └─928 /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ --web.config.file /etc/prometheus/web.yml
```
# sudo cat /etc/systemd/system/prometheus.service

```service
[root@redhat ~]# sudo cat /etc/systemd/system/prometheus.service
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file /etc/prometheus/prometheus.yml \
    --storage.tsdb.path /var/lib/prometheus/ \
    --web.config.file /etc/prometheus/web.yml
[Install]
WantedBy=multi-user.target
```
# sudo cat /etc/prometheus/prometheus.yml

```yml
global:
  scrape_interval: 10s

scrape_configs:
  - job_name: 'prometheus'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9090']
    basic_auth:
      username_file: '/etc/prometheus/username_file'
      password_file: '/etc/prometheus/password_file'
  - job_name: 'node-exporter'
    scrape_interval: 5s
    static_configs:
      - targets: ['localhost:9100']
    basic_auth:
      username_file: '/etc/prometheus/username_file'
      password_file: '/etc/prometheus/password_file'
```
# sudo cat /etc/prometheus/web.yml

```yml
basic_auth_users:
  kiran: $2b$12$DLTQ.j0oK7lkmnUOsjrtl.R4EAdiYgS.jXTiR6H85flP2ezT49Wuq
```
# sudo journalctl -u prometheus.service

```logs
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.755Z level=INFO source=main.go:1248 msg="TSDB started"
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.757Z level=INFO source=main.go:1433 msg="Loading configuration file" filename=/etc/prometheus/prometheus.yml
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.758Z level=INFO source=main.go:1472 msg="updated GOGC" old=100 new=75
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.758Z level=INFO source=main.go:1482 msg="Completed loading of configuration file" db_storage=1.375µs remote_storage=1.819µs web_handler=484ns query_engine=1.03µs scrape=193.435µs scrape_sd=36.104µs notify=1.018µs notify_sd=770ns rules=1.24µs tracing=4.903µs filename=/etc/prometheus/prometheus.yml totalDuration=3.05048ms
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.758Z level=INFO source=main.go:1209 msg="Server is ready to receive web requests."
Mar 25 16:17:08 redhat prometheus[928]: time=2025-03-25T16:17:08.759Z level=INFO source=manager.go:169 msg="Starting rule manager..." component="rule manager"
Mar 25 16:17:18 redhat prometheus[928]: time=2025-03-25T16:17:18.388Z level=INFO source=compact.go:582 msg="write block resulted in empty block" component=tsdb mint=1742882400000 maxt=1742889600000 duration=32.499833ms
Mar 25 16:17:18 redhat prometheus[928]: time=2025-03-25T16:17:18.389Z level=INFO source=head.go:1371 msg="Head GC completed" component=tsdb caller=truncateMemory duration=1.377416ms
Mar 25 16:17:18 redhat prometheus[928]: time=2025-03-25T16:17:18.389Z level=INFO source=checkpoint.go:99 msg="Creating checkpoint" component=tsdb from_segment=44 to_segment=45 mint=1742889600000
Mar 25 16:17:18 redhat prometheus[928]: time=2025-03-25T16:17:18.408Z level=INFO source=head.go:1333 msg="WAL checkpoint complete" component=tsdb first=44 last=45 duration=18.899918ms

```
