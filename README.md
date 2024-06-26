# PromGraf

This repository provides a guide for setting up Grafana, Loki, Promtail, Prometheus, and cAdvisor for monitoring and visualization purposes. Below are the steps to install and configure these tools.

## Install Grafana on Debian or Ubuntu
```bash
sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key
```
## Stable release
```
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

```bash
sudo apt-get update
sudo apt-get install grafana
sudo systemctl status grafana-server
Install Loki and Promtail using Docker
```
## Download Loki Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml
```
## Run Loki Docker container
```
docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml
```
## Download Promtail Config
```
wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml
```
## Run Promtail Docker container
```
docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml
```
Install Prometheus and cAdvisor
## Download the prometheus config file

```bash
wget https://raw.githubusercontent.com/prometheus/prometheus/main/documentation/examples/prometheus.yml
```
## Install Prometheus using Docker
```
docker run -d --name=prometheus -p 9090:9090 -v <PATH_TO_prometheus.yml_FILE>:/etc/prometheus/prometheus.yml prom/prometheus --config.file=/etc/prometheus/prometheus.yml
```
## Check Config

## Using Docker Compose
## Check docker-compose.yml

## Verify
```
docker-compose up -d
docker-compose ps
```

-------------------------------------------------------------------------

[Prometheus Docs]("https://prometheus.io/docs/introduction/overview/")

[Grafana Docs]("https://grafana.com/docs/grafana/latest/")

## Pre-Requisite

- Kubernetes Cluster - Minikube for Testing
- Helm 

If you don't have them installed. Follow the below links:

[Install Minikube]("https://minikube.sigs.k8s.io/docs/start/")

[Install Helm]("https://helm.sh/docs/intro/install/")

<br></br>

## It all starts with Monitoring 

Monitoring your Kubernetes cluster is essential for ensuring the health and performance of your applications and infrastructure. Here are some reasons why monitoring your Kubernetes cluster is important:

- Identify issues and troubleshoot: By monitoring your Kubernetes cluster, you can quickly identify issues such as application crashes, resource bottlenecks, and network problems. With real-time monitoring, you can troubleshoot issues before they escalate and impact your users.

- Optimize performance and capacity: Monitoring allows you to track the performance of your applications and infrastructure over time, and identify opportunities to optimize performance and capacity. By understanding usage patterns and resource consumption, you can make informed decisions about scaling your infrastructure and improving the efficiency of your applications.

- Ensure high availability: Kubernetes is designed to provide high availability for your applications, but this requires careful monitoring and management. By monitoring your cluster and setting up alerts, you can ensure that your applications remain available even in the event of failures or unexpected events.

- Security and compliance: Monitoring your Kubernetes cluster can help you identify potential security risks and ensure compliance with regulations and policies. By tracking access logs and other security-related metrics, you can quickly detect and respond to potential security threats.

<br></br>

## Using Prometheus for monitoring

Prometheus is an open-source monitoring and alerting system that helps you collect and store metrics about your software systems and infrastructure, and analyze that data to gain insights into their health and performance. It provides a powerful query language, a flexible data model, and a range of integrations with other tools and systems. With Prometheus, you can easily monitor metrics such as CPU usage, memory usage, network traffic, and application-specific metrics, and use that data to troubleshoot issues, optimize performance, and create alerts to notify you when things go wrong.

<br></br>

## Why Prometheus over other monitoring tools ?

Prometheus is a popular choice for Kubernetes monitoring for several reasons:

- Open-source: Prometheus is an open-source project that is free to use and has a large community of contributors. This means that you can benefit from ongoing development, bug fixes, and feature enhancements without paying for a commercial monitoring solution.

- Native Kubernetes support: Prometheus is designed to work seamlessly with Kubernetes, making it easy to deploy and integrate with your Kubernetes environment. It provides pre-configured Kubernetes dashboards and supports auto-discovery of Kubernetes services and pods.

- Powerful query language: Prometheus provides a powerful query language that allows you to easily retrieve and analyze metrics data. This allows you to create custom dashboards and alerts, and to troubleshoot issues more easily.

- Scalability: Prometheus is designed to be highly scalable, allowing you to monitor large and complex Kubernetes environments with ease. It supports multi-node architectures and can handle large volumes of data without significant performance degradation.

- Integrations: Prometheus integrates with a wide range of other tools and systems, including Grafana for visualization, Alertmanager for alerting, and Kubernetes API server for metadata discovery.

<br></br>

## Prometheus Architecture

<br></br>
![Alt text](https://prometheus.io/assets/architecture.png)

<br></br>

## What is Grafana ?

Grafana is a popular open-source data visualization and analytics platform that allows you to create custom dashboards and visualizations based on a variety of data sources. Grafana is often used for monitoring and analyzing metrics and logs in real-time, making it an ideal tool for monitoring systems and applications, including Kubernetes environments.

Grafana supports a wide range of data sources, including databases, time-series databases, and other data storage systems. It provides a powerful query language that allows you to retrieve and analyze data from these sources, and to create custom dashboards and alerts based on that data.

In addition to its powerful data visualization and analysis capabilities, Grafana is also highly extensible. It supports a wide range of plugins and integrations, including integrations with popular monitoring and logging tools like Prometheus, Elasticsearch, and InfluxDB.
