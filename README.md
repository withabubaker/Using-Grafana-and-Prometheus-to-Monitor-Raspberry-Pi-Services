# Using Grafana and Prometheus to Monitor Raspberry Pi Services

![alt text](https://github.com/withabubaker/Using-Grafana-and-Prometheus-to-Monitor-Raspberry-Pi-Services/blob/main/img/GrafanaDash.jpg)


## Project Goal
In this tutorial, I installed and set up Grafana dashboard and Prometheus to monitor specific services running on my Raspberry pi.

## Flow Chart
![alt text](https://github.com/withabubaker/Using-Grafana-and-Prometheus-to-Monitor-Raspberry-Pi-Services/blob/main/img/GrafanaFlowChart.jpg)


## Install and Configure Prometheus on wondows 11

Download and run the setup file from [here](https://prometheus.io/download/)
Edit ***prometheus.yml***, replace ***<raspberry_pi_ip>*** with your pi's IP address
```yaml
scrape_configs:
  - job_name: 'raspberrypi'
    static_configs:
      - targets: ['<raspberry_pi_ip>:9100']
```

Run Prometheus
```bash
cd C:\Prometheus
```
```bash
prometheus.exe --config.file=prometheus.yml
```

## Install and Configure Node Exporter, this will grab the metrics from the Raspberry Pi

Install the node on your Raspberry Pi
```bash
wget https://github.com/prometheus/node_exporter/releases/download/v1.6.0/node_exporter-1.6.0.linux-armv7.tar.gz
tar xvfz node_exporter-1.6.0.linux-armv7.tar.gz
cd node_exporter-1.6.0.linux-armv7
./node_exporter
```
Now you should be able to navigate to ***http://<raspberry_pi_ip>:9100/metrics***

Run it as a service to keep it running in the background continuously
Create a service file
```bash
sudo nano /etc/systemd/system/node_exporter.service
```
  Add the following to the file
```ini
[Unit]
Description=Node Exporter

[Service]
ExecStart=/home/pi/node_exporter-1.6.0.linux-armv7/node_exporter

[Install]
WantedBy=multi-user.target
```

Enable the service, this will let the service run automatically after reboot then start the service
```bash
sudo systemctl enable node_exporter
sudo systemctl start node_exporter
```

## Install Grafana on windows 11

Download and install the file from [here](https://grafana.com/grafana/download?pg=get&plcmt=selfmanaged-box1-cta1&platform=windows).
you should be able to navigate ***http://localhost:3000*** with the default credential admin/admin

Go to Configuration > Data Source and add Prometheus as a data source

Now you can create the dashboard and play around. That's it!!!

