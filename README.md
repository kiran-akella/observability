# 🌐 Observability

Observability is the practice of understanding the internal state of a system based on the data it generates, such as logs, metrics, and traces. It is a crucial aspect of modern cloud-native and distributed systems, helping teams diagnose and resolve issues efficiently.

## 🔑 Key Components of Observability Stack

### 📊 1. Grafana
Grafana is an open-source visualization and monitoring tool that allows users to create dashboards and alerts based on time-series data. It supports various data sources, including Prometheus, Loki, and more.

### 📈 2. Prometheus
Prometheus is an open-source monitoring and alerting toolkit designed for reliability and scalability. It collects and stores metrics in a time-series database and provides a powerful query language (PromQL) for analysis.

#### 🚀 Features:
- ✅ Multi-dimensional data model
- ✅ Flexible query language (PromQL)
- ✅ Pull-based metric collection
- ✅ Alerting via Alertmanager

### 📜 3. Loki
Loki is a horizontally scalable, multi-tenant log aggregation system inspired by Prometheus. Unlike traditional log management tools, Loki does not index log content but instead indexes metadata, making it efficient for searching logs at scale.

#### 🔥 Features:
- 💰 Cost-effective log storage
- 🔍 Label-based log querying (LogQL)
- 📡 Seamless integration with Grafana
- 📌 Native support for Kubernetes logs

### 🔄 4. Promtail
Promtail is an agent that collects logs and forwards them to Loki. It is commonly used to scrape logs from Kubernetes pods and local files.

#### 🛠️ Features:
- 🏷️ Label-based log processing
- ⚡ Lightweight and easy to configure
- 🔗 Works seamlessly with Loki

### 🏗️ 5. Grafana Alloy
Grafana Alloy is a unified telemetry agent designed to collect, process, and export logs, metrics, and traces. It simplifies observability by reducing the need for multiple agents and integrates seamlessly with Grafana, Prometheus, and Loki.

#### ⚙️ Features:
- 🎛️ Supports logs, metrics, and traces
- 🔄 Configurable pipelines for data processing
- 🌱 Lightweight and efficient
- 🔗 Native support for OpenTelemetry
