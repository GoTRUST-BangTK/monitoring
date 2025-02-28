
# 📊 Monitoring Stack (Prometheus + Grafana + Alertmanager + cAdvisor + Node Exporter)

This project provides a **monitoring solution** using **Prometheus**, **Grafana**, **Alertmanager**, **cAdvisor**, and **Node Exporter** to collect, visualize, and manage system and container performance.

---

## 🚀 Components

1. **Prometheus** - A powerful time-series database and monitoring system.
2. **Grafana** - A visualization tool to create dashboards from Prometheus metrics.
3. **Alertmanager** - Manages alerts sent by Prometheus and routes them to various notification channels.
4. **cAdvisor** - Monitors resource usage of running containers.
5. **Node Exporter** - Collects system-level metrics (CPU, memory, disk, network, etc.).

---

## 📌 Deployment

### **2️⃣ Run Services with Docker Compose**

Navigate to the project directory and run: `docker-compose up` 

✅ This will start **Prometheus, Grafana, Alertmanager, cAdvisor, and Node Exporter** as Docker containers.


## 🛠️ Configuration

### **📍 Prometheus**

-   **Configuration file:** `prometheus/conf/prometheus.yml`
-  **Rule file**: ` container-rules.yml, linux-rules.yml `
-   **Default URL:** http://localhost:9090
-   **Check monitored targets:** http://localhost:9090/targets

### **📍 Grafana**

-   **Configuration file:** `grafana/conf`
-   **Default URL:** http://localhost:3000
-   **Default credentials:**
    -   **Username:** `admin`
    -   **Password:** `admin` _(can be changed in settings)_

### **📍 Alertmanager**

-   **Configuration file:** `alertmanager/alertmanager.yml`
-   **Default URL:** http://localhost:9093
-   Used to send notifications via **Slack, Email, Telegram, etc.**

### **📍 cAdvisor**

-   **Monitors running Docker containers' performance.**
-   **Default URL:** http://localhost:8080
-   Provides container-level CPU, memory, disk, and network statistics.

### **📍 Node Exporter**

-   **Collects system-level metrics (CPU, memory, disk, network, etc.).**
-   **Default URL:** http://localhost:9100/metrics

----------

## 📊 Accessing Grafana Dashboard

1.  Open **Grafana** at: http://localhost:3000
2.  Log in using the default admin credentials.
3.  Add **Prometheus Data Source**:
    -   Navigate to **Settings → Data Sources**
    -   Select **Prometheus**
    -   Enter URL: `http://prometheus:9090`
    -   Click **Save & Test**
4.  Import a **Prebuilt Dashboard**:
    -   Go to **Dashboard → Import**
    -   Enter **Dashboard ID**:
        -   **Node Exporter Dashboard ID:** `1860`
        -   **cAdvisor Dashboard ID:** `14282`

----------

## 📢 Alert Configuration

### **Example: Sending Alerts to Slack**


Modify `alertmanager/alertmanager.yml` to include **Slack webhook** , **Telegram webhook**:

```yaml
receivers:
  - name: 'slack'
    slack_configs:
      - send_resolved: true
        channel: '#monitoring'
        api_url: 'https://hooks.slack.com/services/your-slack-webhook'

  - name: 'telegram'
    telegram_configs:
      - api_url: 'https://api.telegram.org'
        bot_token: 'xx'
        chat_id: xxx
        send_resolved: true
        message: "{{ range .Alerts }}{{ .Annotations.description }}{{ .Annotations.timestamp }}\n{{ end }}"
