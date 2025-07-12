
## Promethous Kurulumu:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false prometheus
```

```shell
wget https://github.com/prometheus/prometheus/releases/download/v2.53.5/prometheus-2.53.5.linux-amd64.tar.gz
```


```shell
tar -xvf prometheus-2.53.5.linux-amd64.tar.gz
```

```shell
sudo mkdir -p /data /etc/prometheus
```

```shell
cd prometheus-2.53.5.linux-amd64
```

```shell
sudo cp prometheus promtool /usr/local/bin/
```

```shell
sudo cp consoles/console_libraries/ /etc/prometheus
```

```shell
sudo cp prometheus.yml /etc/prometheus/prometheus.yml
```

```shell
sudo chown -R prometheus:prometheus /etc/prometheus /data
```

```shell
prometheus --version
```

```shell
prometheus --help
```

```shell
sudo vim /etc/systemd/system/prometheus.service
```

```init
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=prometheus
Group=prometheus
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/prometheus \
	--config.file=/etc/prometheus/prometheus.yml \
	--storage.tsdb.path=/data \
	--web.console.templates=/etc/prometheus/consoles \
	--web.console.libraries=/etc/prometheus/console_libraries \
	--web.listen-address=0.0.0.0:9090
	--web.enable-lifecycle

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl enable prometheus.service
```

```shell
sudo systemctl start prometheus.service
```

```shell
sudo systemctl status prometheus.service
```

```shell
journalctl -u prometheus -f --no-pager
```

## Node Exporter Kurulumu:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false node_exporter
```

```shell
wget https://github.com/prometheus/node_exporter/releases/download/v1.9.1/node_exporter-1.9.1.linux-amd64.tar.gz
```

```shell
tar -xvf node_exporter-1.9.1.linux-amd64.tar.gz
```


```shell
sudo mv node_exporter-1.9.1.linux-amd64/node_exporter \
	/usr/local/bin/
```

```shell
node_exporter --help
```

```shell
sudo vim /etc/systemd/system/node_exporter.service
```

```systemd
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=node_exporter
Group=node_exporter
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/node_exporter \
	--collector.logind

[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl enable node_exporter.service
```

```shell
sudo systemctl start node_exporter.service
```

```shell
sudo systemctl status node node_exporter.service
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

```yml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export                   # <----
    static_configs:
      - targets: ["localhost:9100"]
```


```shell
promtool check config /etc/prometheus/prometheus.yml
```

```shell
curl -X POST http://localhost:9090/-/reload
```

## Grafana:

```shell
sudo apt-get install -y apt-transport-https software-properties-common wget
```

```shell
sudo mkdir -p /etc/apt/keyrings/
```

```shell
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```

+ stable

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```

+ Beta

```shell
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```



```shell
# Updates the list of available packages
sudo apt-get update
```

```shell
# Installs the latest OSS release:
sudo apt-get install grafana
```

```shell
# Installs the latest Enterprise release:
sudo apt-get install grafana-enterprise
```

```shell
sudo systemctl enable grafana-server
```

```shell
sudo systemctl start grafana-server
```

```shell
sudo vim /etc/grafana/provisioning/datasources/datasources/datasources.yaml
```

```yaml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    url: http://localhost:9090
    isDefault: true
```


```shell
sudo systemctl restart grafana-server
```


## Pushgateway:

```shell
sudo useradd \
	--system \
	--no-create-home \
	--shell /bin/false pushgateway
```

```shell
wget https://github.com/prometheus/pushgateway/releases/download/v1.11.1/pushgateway-1.11.1.linux-amd64.tar.gz
```

```shell
tar -xvf pushgateway-1.11.1.linux-amd64.tar.gz
```

```shell
sudo cp -v pushgateway-1.11.1.linux-amd64/pushgateway /usr/local/bin
```

```shell
sudo vim /etc/systemd/system/pushgateway.service
```

```systemd
[Unit]
Description=Pushgateway
Wants=network-online.target
After=network-online.target

StartLimitIntervalSec=500
StartLimitBurst=5

[Service]
User=pushgateway
Group=pushgateway
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=/usr/local/bin/pushgateway

[Install]
WantedBy=multi-user.target
```


```shell
sudo systemctl enable pushgateway.service
```

```shell
sudo systemctl start pushgateway.service
```

```shell
sudo vim /etc/prometheus/prometheus.yml
```

```yaml
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090"]


  - job_name: node_export
    static_configs:
      - targets: ["localhost:9100"]


  - job_name: pushgateway           # <<---
    honor_labels: true
    static_configs:
      - targets: ["localhost:9091"]
```

