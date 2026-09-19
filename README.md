# Monitoring Task

## Objective
Install Prometheus and Grafana on a Linux EC2 instance, configure Node Exporter for system metrics, connect Prometheus to Grafana, and create a monitoring dashboard.

## Technologies Used
- AWS EC2
- Ubuntu Linux
- Prometheus
- Grafana
- Node Exporter
- Git and GitHub

## Architecture
Linux EC2
- Node Exporter: 9100
- Prometheus: 9090
- Grafana: 3000

Node Exporter collects Linux system metrics.
Prometheus scrapes the metrics from Node Exporter.
Grafana connects to Prometheus and visualizes the metrics.

## Node Exporter
Node Exporter was installed and configured as a system service.

The metrics endpoint was verified at:
http://localhost:9100/metrics

Node Exporter was confirmed to be running on port 9100.

## Prometheus
Prometheus was installed on the Ubuntu EC2 instance.

Prometheus was configured to scrape Node Exporter using:

job_name: node_exporter
scrape_interval: 15s
target: localhost:9100

The configuration was validated successfully using promtool.

Prometheus was restarted and confirmed ready.

The Prometheus targets API was checked and the node_exporter target was verified as UP.

## Grafana
Grafana OSS was installed and configured as a system service.

Grafana was accessed through port 3000.

The Prometheus data source was configured with:

http://localhost:9090

Grafana successfully queried the Prometheus API.

## Monitoring Dashboard
A Grafana dashboard named Linux Server Monitoring was created.

The dashboard contains:

- CPU Usage
- Memory Usage
- Disk Usage

All three panels display metrics collected from Node Exporter through Prometheus.

## PromQL Queries

### CPU Usage
100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)

### Memory Usage
100 * (1 - (node_memory_MemAvailable_bytes{job="node_exporter"} / node_memory_MemTotal_bytes{job="node_exporter"}))

### Disk Usage
100 * (1 - (node_filesystem_avail_bytes{job="node_exporter",mountpoint="/",fstype!="rootfs"} / node_filesystem_size_bytes{job="node_exporter",mountpoint="/",fstype!="rootfs"}))

## Verification
- Node Exporter service running
- Node Exporter metrics endpoint accessible
- Prometheus service running
- Prometheus configuration validated
- Node Exporter target UP
- Grafana service running
- Grafana connected to Prometheus
- CPU metrics displayed
- Memory metrics displayed
- Disk metrics displayed
- Linux Server Monitoring dashboard created

## Project Structure
Monitoring-Task/
- README.md
- prometheus.yml
- .gitignore
- screenshots/

## Result
Prometheus successfully collects Linux system metrics from Node Exporter, and Grafana visualizes the metrics through the Linux Server Monitoring dashboard.
