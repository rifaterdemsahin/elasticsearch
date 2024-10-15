# 🚀 Logging OpenShift Events to Elasticsearch/LokiStack: A Proof of Concept
# Logging OpenShift Events to Elasticsearch or LokiStack

🔍 This guide walks you through building a **Proof of Concept (PoC)** application that logs **OpenShift events** from a **CRC** (CodeReady Containers) environment to **Elasticsearch** or **LokiStack**. The goal is to ensure that all events are searchable and easily retrievable for monitoring and troubleshooting purposes.

---

## 💡 Objectives
Log OpenShift events from a local **CRC OpenShift** setup into a searchable format using **Elasticsearch** or **LokiStack** for real-time monitoring.

---

## 🛠️ Tools & Setup

- **CRC (CodeReady Containers)**: Simulates an OpenShift cluster locally.
- **Elasticsearch/LokiStack**: Indexes and searches logs.
- **Kibana/Grafana**: Visualizes logs (depending on the stack used).
- **Fluentd**: Collects and forwards logs.

---

## 🚀 Steps to Build the PoC

### 1. Set up CRC and Access OpenShift Console
Ensure CRC is installed and running. Open the OpenShift console:

```bash
crc start
crc console
```

### 2. Configure Fluentd to Collect Events
Install **Fluentd** as the logging agent within the OpenShift cluster. Configure Fluentd to route events to Elasticsearch or LokiStack.

For **Elasticsearch**:

```yaml
<source>
    @type openshift_events
    tag openshift.event
</source>

<match openshift.event>
    @type elasticsearch
    host YOUR_ELASTICSEARCH_HOST
    port 9200
    index_name openshift-logs
</match>
```

For **LokiStack**:

```yaml
<match openshift.event>
    @type loki
    url http://YOUR_LOKISTACK_HOST:3100
</match>
```

### 3. Verify Logs in Elasticsearch/LokiStack
Check logs through **Kibana** or **Grafana** dashboards to ensure they are searchable and displayed in real-time.

💡 **Pro Tip**: Create indices or log streams with proper time filters to avoid missing critical event data.

---

## ⏸️ Pause and Check the Logs
Verify the data in **Kibana** (Elasticsearch) or **Grafana** (LokiStack) to ensure events are searchable and displayed in real-time.

🖼️ *Example screenshot of event log display*:

![Screenshot](./screenshot-of-logs.png) *(Logs in Kibana with searchable fields).*

---

## 📊 Visualizing Logs

- **Kibana**: Create detailed dashboards for monitoring OpenShift event streams with Elasticsearch.
- **Grafana**: Track logs and monitor trends with LokiStack.

---

## 🔧 Troubleshooting Tips
- **Fluentd Not Logging?**: Check Fluentd permissions and configuration.
- **No Data in Elasticsearch/LokiStack?**: Verify networking configuration between CRC and the logging system.
- **Logs Missing Timestamps?**: Ensure Fluentd configuration includes timestamping for log entries.

---

## 🚀 Conclusion
This PoC demonstrates logging **OpenShift events** from a **CRC OpenShift** cluster to **Elasticsearch** or **LokiStack**, enhancing monitoring and issue identification in your OpenShift environment.

---

**🔗 Connect with me:**

- 💼 [LinkedIn](https://www.linkedin.com/in/rifaterdemsahin/)
- 🐦 [Twitter](https://x.com/rifaterdemsahin)
- 🎥 [YouTube](https://www.youtube.com/@RifatErdemSahin)
- 💻 [GitHub](https://github.com/rifaterdemsahin)

Let’s connect and explore more about Kubernetes, logging, and cloud technologies!
