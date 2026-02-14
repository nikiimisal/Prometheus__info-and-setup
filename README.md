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

# 🚀 Prometheus Monitoring Setup with Node Exporter and Python App

This project demonstrates how to set up:

- Prometheus
- Node Exporter
- Python Application with custom metrics
- System monitoring on AWS EC2 (Ubuntu 22.04)

---

# 🚀 Installation of Prometheus + Node Exporter + Python App 

---

## 🔹 Step 1: Launch EC2 Instance

### Why manually launch EC2?

For learning and real infrastructure understanding:

- You understand networking
- You understand security groups
- You understand Linux setup
- You understand real-world infrastructure

### Instance Configuration

| Setting | Value | Why |
|----------|--------|------|
| Instance Type | t3.micro | Free tier eligible |
| OS | Ubuntu 22.04 LTS | Stable & widely used |
| Name | prometheus | Easy identification |

---

## 🔹 Step 2: Configure Security Group (Important)

### Open these ports:

| Port | Purpose | Why Needed |
|------|----------|------------|
| 22 | SSH | Connect via terminal |
| 9090 | Prometheus | Access Prometheus UI |
| 9100 | Node Exporter | Server metrics |
| 5000 | Python App | Application monitoring |
| 3000 | Grafana | Dashboard (optional) |

Allow source:

```
0.0.0.0/0
```

👉 Public access for learning only  
👉 In production, always restrict IP

---

## 🔹 Step 3: Connect to Server

```
ssh -i your-key.pem ubuntu@your-public-ip
sudo hostnamectl hostname Prometheus
exit
```

### Why?
To access EC2 terminal remotely.

Update system:

```
sudo apt update -y
```

### Why?
To refresh package index before installing software.

---

## 🔹 Step 4: User Types (Security Concept)

In Linux, 3 types of users exist:

1. Root user → Full access  
2. Local user → Regular login  
3. System user → For running services  

👉 Prometheus should NOT run as root  
👉 We create a dedicated system user for security

---

## 🔹 Step 5: Install Prometheus

### Create Prometheus System User

```
sudo useradd --no-create-home --shell /bin/false prometheus
```

### Why?

- No home directory
- Cannot login
- More secure
- Used only to run service

---

### Create Required Directories

```
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

| Directory | Purpose |
|------------|----------|
| /etc/prometheus | Configuration files |
| /var/lib/prometheus | Time-series database storage |

Prometheus stores monitoring data inside `/var/lib/prometheus`.

---

### Set Ownership

```
sudo chown prometheus:prometheus /var/lib/prometheus
```

### Why?
Prometheus must have write permission for storing metrics.

---

### Download Prometheus

```
cd /tmp

wget https://github.com/prometheus/prometheus/releases/download/v2.53.1/prometheus-2.53.1.linux-amd64.tar.gz

tar -xvf prometheus-2.53.1.linux-amd64.tar.gz

cd prometheus-2.53.1.linux-amd64
```

### Why download manually?

- Understand binaries
- Production-style installation
- Avoid package manager dependency

---

### Move Required Files

```
sudo mv prometheus /usr/local/bin/
sudo mv promtool /usr/local/bin/

sudo mv consoles /etc/prometheus
sudo mv console_libraries /etc/prometheus

sudo mv prometheus.yml /etc/prometheus
```

### Why?

- `/usr/local/bin` → Standard executable location
- `/etc/prometheus` → Configuration directory

---

### Set Ownership

```
sudo chown -R prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /usr/local/bin/prometheus
```

---

### Create Prometheus Service File

```
sudo vim /etc/systemd/system/prometheus.service
```

Paste:

```
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
 --config.file=/etc/prometheus/prometheus.yml \
 --storage.tsdb.path=/var/lib/prometheus \
 --web.console.templates=/etc/prometheus/consoles \
 --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```

### Why systemd?

- Auto start on reboot
- Manage service status
- Production best practice

---

### Start Prometheus

```
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
sudo systemctl status prometheus
```

Access:

```
http://YOUR_PUBLIC_IP:9090
```


---
---


>The above steps were focused on monitoring the server infrastructure.
>From this point onward, we will configure application-level monitoring.
>Follow the steps below to instrument and monitor the application.



---
---

## 🔹 Step 6: Install Node Exporter

```
cd /tmp

wget https://github.com/prometheus/node_exporter/releases/download/v1.8.1/node_exporter-1.8.1.linux-amd64.tar.gz

tar -xvf node_exporter-1.8.1.linux-amd64.tar.gz

sudo mv node_exporter-1.8.1.linux-amd64/node_exporter /usr/local/bin/

sudo useradd -rs /bin/false node_exporter
```

### Why Node Exporter?

Prometheus cannot read OS metrics directly.

Node Exporter collects:

- CPU
- Memory
- Disk
- Network

Exposes metrics on:

```
http://IP:9100/metrics
```

---

### Create Node Exporter Service

```
sudo vim /etc/systemd/system/node_exporter.service
```

Paste:

```
[Unit]
Description=Node Exporter
After=network.target

[Service]
User=node_exporter
Group=node_exporter
Type=simple
ExecStart=/usr/local/bin/node_exporter

[Install]
WantedBy=multi-user.target
```

---

### Start Node Exporter

```
sudo systemctl daemon-reload
sudo systemctl start node_exporter
sudo systemctl enable node_exporter
sudo systemctl status node_exporter
```

---
---

>We have installed Node Exporter, but Prometheus is not yet scraping its metrics.
>If Node Exporter is not integrated with Prometheus, no node-related metrics will appear in the metrics section.
>Now we need to integrate Node Exporter with Prometheus.
>This integration is required so that Prometheus can pull server-level metrics such as CPU, memory, disk, and network usage.

---
---

## 🔹 Step 7: Configure Prometheus (Pull Model)

Edit:

```
sudo vim /etc/prometheus/prometheus.yml
```

Add under `scrape_configs:`:

```
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```

### Why?

Prometheus follows Pull Model.  
We must define scrape targets manually.

Restart:

```
sudo systemctl restart prometheus
```

---
---

>With server monitoring configured, we will now deploy the Python application as the final step to enable application-level monitoring.


---
---

## 🔹 Step 8: Deploy Python Application

Install dependencies:

```
sudo apt install python3-pip python3-venv -y
```

Create virtual environment:

```
python3 -m venv myenv
source myenv/bin/activate
```

Install packages:

```
pip install flask prometheus_client
```

### Why prometheus_client?

It exposes `/metrics` endpoint for application monitoring.

---

### Create Python App

```
vim app.py
```

Add:

```python
from flask import Flask
from prometheus_client import Counter, generate_latest, CONTENT_TYPE_LATEST

app = Flask(__name__)

REQUESTS = Counter('hello_world_total', 'Total Hello World Requests')

@app.route('/')
def hello():
    REQUESTS.inc()
    return "Hello, World!"

@app.route('/metrics')
def metrics():
    return generate_latest(), 200, {'Content-Type': CONTENT_TYPE_LATEST}

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

---

### Run Application

```
nohup python3 app.py > app.log 2>&1 &
```

Test:

```
http://YOUR_PUBLIC_IP:5000
```

---

## 🔹 Step 9: Add Python App to Prometheus

Edit:

```
sudo vim /etc/prometheus/prometheus.yml
```

Add:

```
  - job_name: 'python_app'
    static_configs:
      - targets: ['localhost:5000']
```

Restart:

```
sudo systemctl restart prometheus
```

Now Prometheus monitors:

- Server metrics
- Application metrics

---

## 🔹 Step 10: Verify Metrics

Open:

```
http://YOUR_PUBLIC_IP:9090
```

Search:

```
hello_world_total
```

You should see increasing values.

To calculate CPU usage:

```
100 - (avg by (instance) (irate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

---

# 🔥 What You Built

You created a complete monitoring architecture:

EC2  
↳ Prometheus  
↳ Node Exporter (Server Monitoring)  
↳ Python App (Application Monitoring)

This demonstrates:

- Pull-based monitoring
- Secure system users
- systemd service management
- Application instrumentation
- Production-style installation













