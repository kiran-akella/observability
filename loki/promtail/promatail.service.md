# Promtail system service file

```status
root@docker:~# sudo systemctl status promtail
● promtail.service - Promtail service
     Loaded: loaded (/etc/systemd/system/promtail.service; enabled; preset: enabled)
     Active: active (running) since Tue 2025-03-25 16:18:19 UTC; 2min 7s ago
   Main PID: 1330 (promtail)
      Tasks: 8 (limit: 2349)
     Memory: 16.5M (peak: 16.8M)
        CPU: 891ms
     CGroup: /system.slice/promtail.service
             └─1330 /usr/bin/promtail -config.file /etc/promtail/config.yml
```
# sudo cat /etc/systemd/system/promtail.service

```service
root@docker:~# cat /etc/systemd/system/promtail.service
[Unit]
Description=Promtail service
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=promtail
ExecStart=/usr/bin/promtail -config.file /etc/promtail/config.yml
# Give a reasonable amount of time for promtail to start up/shut down
TimeoutSec = 60
Restart = on-failure
RestartSec = 2

[Install]
WantedBy=multi-user.target

```
# sudo journalctl -u promtail.service

```logs
Mar 25 16:18:19 docker.asia-south1-c.c.booming-entity-448213-v0.internal systemd[1]: Started promtail.service - Promtail service.
Mar 25 16:18:20 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:19.907893838Z caller=promtail.go:135 msg="Reloading configuration file" sha3sum=ae507851b76277753f10fb97b6317aaacaec3459076678d3bee6b4b62c021da9
Mar 25 16:18:20 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:19.91279738Z caller=server.go:351 msg="server listening on addresses" http=[::]:9080 grpc=[::]:35945
Mar 25 16:18:20 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:19.913056494Z caller=main.go:173 msg="Starting Promtail" version="(version=3.4.2, branch=release-3.4.x, revision=4fa045d3)"
Mar 25 16:18:20 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=warn ts=2025-03-25T16:18:19.91319272Z caller=promtail.go:265 msg="enable watchConfig"
Mar 25 16:18:25 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:24.912470205Z caller=filetargetmanager.go:372 msg="Adding target" key="/var/log/auth.log:{job=\"auth.log_from_docker_to_loki\"}"
Mar 25 16:18:25 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:24.91260896Z caller=filetarget.go:345 msg="watching new directory" directory=/var/log
Mar 25 16:18:25 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: level=info ts=2025-03-25T16:18:24.912816036Z caller=tailer.go:147 component=tailer msg="tail routine: started" path=/var/log/auth.log
Mar 25 16:18:25 docker.asia-south1-c.c.booming-entity-448213-v0.internal promtail[1330]: ts=2025-03-25T16:18:24.912849192Z caller=log.go:168 level=info msg="Seeked /var/log/auth.log - &{Offset:8279 Whence:0}"
```
