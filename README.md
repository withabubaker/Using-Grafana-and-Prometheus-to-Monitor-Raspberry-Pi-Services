# Using Grafana and Prometheus to Monitor Raspberry Pi Services

![alt text](https://github.com/withabubaker/Using-Grafana-and-Prometheus-to-Monitor-Raspberry-Pi-Services/blob/main/img/GrafanaDash.jpg)


## Project Goal
In this tutorial, we will install and set up Grafana dashboard and Prometheus to monitor specific services running on a Raspberry pi.

## Flow Chart
![alt text](https://github.com/withabubaker/Using-Grafana-and-Prometheus-to-Monitor-Raspberry-Pi-Services/blob/main/img/GrafanaFlowChart.jpg)

## Targeted Services
1. nodered.service
3. pareto-anywhere-pi.service
4. barnowl-hci-forwarder-pi.service
5. ControlKasaSmartPlug.service

## Install and Configure Prometheus (windows 11)

1. Download and run the setup file from [here](https://prometheus.io/download/)
2. Edit ***prometheus.yml***, replace ***<raspberry_pi_ip>*** with your pi's IP address
```yaml
scrape_configs:
  - job_name: 'raspberrypi'
    static_configs:
      - targets: ['<raspberry_pi_ip>:9100']
```

3. Run Prometheus
```bash
cd C:\Prometheus
```
start the service
```bash
prometheus.exe --config.file=prometheus.yml
```
