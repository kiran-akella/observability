# Promtail Documentation

![Promtail](https://raw.githubusercontent.com/grafana/loki/main/docs/sources/logo.png)

[![Promtail](https://img.shields.io/badge/Promtail-Log%20Collector-blue?style=for-the-badge&logo=grafana)](https://grafana.com/docs/loki/latest/clients/promtail/)
[![Docker](https://img.shields.io/badge/Docker-Container-blue?style=for-the-badge&logo=docker)](https://hub.docker.com/r/grafana/promtail)
[![GitHub](https://img.shields.io/badge/Source-GitHub-black?style=for-the-badge&logo=github)](https://github.com/grafana/loki/tree/main/clients/cmd/promtail)

## 📌 Introduction

Promtail is an agent that ships the contents of local logs to a private or Grafana Cloud Loki instance. It is usually deployed alongside Loki to automatically detect and scrape logs from Kubernetes pods or other sources.

## 🚀 Features

- 🔍 **Log Discovery:** Auto-discovers logs from Kubernetes and other environments.
- 📡 **Labeling:** Attaches metadata to logs for efficient searching.
- 🔗 **Integration with Loki:** Works seamlessly with Loki for log aggregation.
- 🛠 **Lightweight & Easy-to-use:** Minimal resource consumption and simple configuration.

## 🔧 Installation

### Using Docker
```sh
docker run -d --name=promtail \
  -v /var/log:/var/log:ro \
  -v /etc/promtail:/etc/promtail \
  grafana/promtail:latest
```

### Using Binary
1. Download the latest release from [Promtail GitHub Releases](https://github.com/grafana/loki/releases).
2. Extract and move the binary to `/usr/local/bin`.
3. Run Promtail with your configuration file:
   ```sh
   promtail -config.file=/etc/promtail/config.yml
   ```

## 📜 Configuration Example

```yaml
server:
  http_listen_port: 9080

positions:
  filename: /var/log/positions.yaml

clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:
  - job_name: system-logs
    static_configs:
      - targets:
          - localhost
        labels:
          job: varlogs
          __path__: /var/log/*.log
```

## 📚 Documentation & Resources

- 📖 [Official Promtail Docs](https://grafana.com/docs/loki/latest/clients/promtail/)
- 🐳 [Promtail Docker Image](https://hub.docker.com/r/grafana/promtail)
- 🏗️ [Loki GitHub Repository](https://github.com/grafana/loki)

---
