<h1 align="center">Prometheus</h1>


##  1️⃣ Prometheus

Prometheus is an open-source systems monitoring and alerting toolkit originally developed at SoundCloud in 2012. It provides a powerful time-series database optimized for storing metrics and enables flexible, multi-dimensional data collection and analysis. Prometheus has become a cornerstone of cloud-native observability, widely used in conjunction with container orchestration platforms like Kubernetes.

---

###  Key facts

- **Initial release**: 2012
- **Developer**: Originally SoundCloud; now part of the Cloud Native Computing Foundation
- **Primary language**: Go
- **Data model**: Multi-dimensional time series identified by metric name and labels
- **License**: Apache License 2.0

---

###  Architecture and operation

Prometheus works on a pull model: it periodically scrapes metrics from instrumented targets via HTTP endpoints.<br>
These metrics are stored locally in a custom time-series database.<br>
A powerful query language, PromQL, allows users to aggregate and visualize metrics, create dashboards, or define alert conditions.

---

###  Ecosystem and integrations

Prometheus is often deployed with complementary tools. Grafana provides visualization and dashboarding, while the Alertmanager <br>
component routes alerts to email, chat, or incident management systems.<br>
Exporters extend Prometheus to gather metrics from third-party systems like databases, message queues, or hardware devices.

---

###  Importance in observability

Prometheus has become a de facto standard for metrics in modern observability stacks.<br>
It is cloud-native by design, supporting service discovery for dynamic environments such as Kubernetes. <br>
Its simplicity, powerful data model, and rich ecosystem have made it central to monitoring microservices, infrastructure, and application performance across industries.


---

## 2️⃣ Prometheus vs CloudWatch

###  🔹 Amazon CloudWatch

- AWS managed service
- Limited to AWS environment
- No installation required
- Fully managed (PaaS)
- Limited customization

###  🔹 Prometheus

- Open-source tool
- Works on all cloud platforms
  - AWS
  - Azure
  - GCP
  - On-premise
- Needs manual setup
- Highly customizable
- You manage infrastructure (IaaS type)<br>
👉 CloudWatch is AWS-specific.<br>
👉 Prometheus is cloud-agnostic (multi-cloud support).


Example:<br>
CloudWatch monitors EC2 only inside AWS.<br>
Prometheus can monitor:<br>
- EC2
- Azure VM
- GCP VM
- On-prem server
- Kubernetes

---

## 3️⃣ Types of Monitoring

Monitoring is divided into 2 main types:


---

###  🖥️ 1. Server Monitoring (Infrastructure Monitoring)

This monitors machine-level metrics like:<br>
- CPU usage
- Memory (RAM)
- Disk space
- Disk I/O
- Network incoming traffic
- Network outgoing traffic
- System load

Example:<br>
If EC2 CPU goes above 80%, Prometheus can trigger an alert.

Server monitoring answers:<br>
👉 Is the machine healthy?


---

###  🌐 2. Application Monitoring

This monitors application-level metrics like:<br>
- HTTP request count
- Error rate
- Response time
- API latency
- Database query time

Applications can be:<br>
- Python
- Node.js
- WordPress
- Java
- .NET

Application monitoring answers:<br>
👉 Is the application healthy?

---

##  4️⃣ How Prometheus Works (Architecture)


Prometheus follows a Pull-Based Model.

Instead of agents pushing data, Prometheus:

1. Scrapes metrics from targets
2. Stores them in its time-series database
3. Allows querying using PromQL
4. Sends alerts using Alertmanager
5. Visualizes dashboards using Grafana

Main components:<br>
- Prometheus Server
- Exporters
- Alertmanager
- Grafana
- PromQL
- Service Discovery

---

##  5️⃣ How Server Monitoring Works in Prometheus

Prometheus does NOT automatically monitor servers by default.

To monitor a server (like EC2), you install:

###  🔹 Node Exporter

Node Exporter is an open-source software component that collects hardware and operating system metrics for monitoring with Prometheus.<br>
It exposes system-level statistics—such as CPU usage, memory, disk, and network metrics—in a format Prometheus can scrape and store for analysis and alerting.

>Node Exporter is a small software installed on the server you want to monitor.

Key facts
- Initial release: 2015
- Developer: Prometheus Authors
- Programming language: Go
- License: Apache License 2.0
- Primary use: Export Linux system metrics to Prometheus



Example Process:

1. Install Node Exporter on EC2
2. Update `prometheus.yml`
3. Prometheus scrapes metrics from that server

Node Exporter collects:
```
node_cpu_seconds_total
node_memory_MemAvailable_bytes
node_network_receive_bytes_total
```

So:

👉 If you want to monitor 5 servers<br>
👉 Install Node Exporter on all 5 servers<br>
👉 Add them in Prometheus config

---

##  6️⃣ How Application Monitoring Works

Application monitoring requires configuration changes.

For example:<br>
- Python app → Install Prometheus client library
- Node.js app → Install prom-client package
- WordPress → Use exporter plugin

Steps:<br>
1. Add Prometheus library inside application
2. Expose /metrics endpoint
3. Update Prometheus YAML config

So yes, for applications:<br>
✔ Server monitoring → Install exporter<br>
✔ Application monitoring → Code changes + library install


---

##  7️⃣ Configuration (Imp)

Prometheus uses a configuration file:
```
prometheus.yml
```

Inside this file, we define:<br>
- Which servers to monitor
- Which apps to monitor
- Scrape interval
- Target IPs and ports<br>
Example concept:

```
scrape_configs:
  - job_name: "node"
    static_configs:
      - targets: ["192.168.1.10:9100"]
```

So Prometheus mainly depends on:<br>
👉 Correct YAML configuration<br>
👉 Proper integration

If you know how to modify YAML and add scrape targets — you can manage Prometheus properly.


---

##  8️⃣ What is the Main Job of Prometheus?

Prometheus does not fix problems.

Its job is:<br>
✔ Collect metrics<br>
✔ Store data<br>
✔ Show dashboards<br>
✔ Generate alerts<br>
✔ Help you analyze system behavior<br>

In simple words:<br>
>Prometheus shows what your system is doing now and what might happen next.

You sit and observe dashboards — Prometheus continuously monitors everything.


---

##  9️⃣ Advantages

✔ Multi-cloud support<br>
✔ Open-source<br>
✔ Powerful querying (PromQL)<br>
✔ Strong Kubernetes support<br>
✔ Highly scalable<br>
✔ Custom alerting

---

##  🔟 Limitations

❌ Needs manual setup<br>
❌ Not a log monitoring tool<br>
❌ Local storage by default<br>
❌ Requires configuration knowledge<br>

---








---
---


##  ✅ Conclusion

Prometheus is mainly a monitoring tool whose core purpose is:

>To continuously observe what your system or application is doing and display those metrics on Prometheus dashboards.

It does not fix problems.<br>
It does not automatically optimize systems.<br>
It simply:<br>
- Collects metrics<br>
- Stores time-series data<br>
- Shows dashboards<br>
- Generates alerts

You monitor everything from the dashboard.



---
Prometheus is an open-source monitoring and alerting system that collects metrics from servers and applications through proper configuration and integration.<br>
Its primary purpose is to provide visibility into system behavior via dashboards and alerts. <br>
To use Prometheus effectively, one must understand how to configure exporters, instrument applications, and update the YAML configuration file correctly.
---

###  🎯 In Simple Words

Whatever you are running:<br>
- Server (CPU, RAM, Disk, Network)<br>
- Application (Python, Node.js, WordPress, APIs)<br>
- Containers<br>
- Kubernetes<br>
Prometheus monitors it — if it is properly integrated.

---

###  🔹 The Most Important Skill in Prometheus

The main thing you must understand is:

✔ How to integrate targets<br>
✔ How to configure exporters<br>
✔ How to update the prometheus.yml file<br>
✔ How to add scrape configurations

Because Prometheus works only if:

- You correctly configure targets
- You update YAML properly
- You expose `/metrics` endpoints
- You install exporters where required

If integration is wrong → No metrics<br>
If YAML is wrong → Prometheus will not scrape

So yes, the real skill in Prometheus is:

>Understanding integration and configuration.


---
---
---








































































