# Grafana-Loki
In the context of Linux, Loki (specifically Grafana Loki) is an open-source log aggregation system designed to collect, store, and query logs from applications and infrastructure

******
It is frequently described as "like Prometheus, but for logs" because it uses the same label-based approach for organizing data, making it a popular choice for monitoring Linux system logs and Kubernetes environments
**********

Key Characteristics
Cost-Efficient Indexing: Unlike systems like Elasticsearch that index the full text of every log, Loki only indexes metadata (labels). This significantly reduces storage costs and makes it easier to operate.
LogQL: It uses its own query language, LogQL, which is inspired by Prometheus's PromQL.
Seamless Integration: It is built to work natively with Grafana for visualization and often uses agents like Promtail or Grafana Alloy to ship logs from Linux servers to the central Loki instance.


**********************************
How to install LOKI

fist install Grafana then start with loki

Run in terminal
1-
wget https://github.com/grafana/loki/releases/latest/download/loki-linux-amd64.zip
unzip loki-linux-amd64.zip
chmod +x loki-linux-amd64
./loki-linux-amd64

2-
wget https://github.com/grafana/loki/releases/latest/download/promtail-linux-amd64.zip
unzip promtail-linux-amd64.zip
chmod +x promtail-linux-amd64

3- Configure logs
&&&
scrape_configs:
  - job_name: system
    static_configs:
      - targets:
          - localhost
        labels:
          job: varlogs
          __path__: /var/log/*.log
&&&&

4- Run:
./promtail-linux-amd64 -config.file=promtail.yaml

5- Connect Loki to Grafana
http://localhost:3100

6- Query:

{job="varlogs"}

scp file.txt user@receiver:/path/


****************************************
&&&&& important&&&&&&&&&&&&&&&&&
nano promtail.yaml
&&&
server:
  http_listen_port: 9080

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://localhost:3100/loki/api/v1/push

scrape_configs:
  - job_name: system_logs
    static_configs:
      - targets:
          - localhost
        labels:
          job: varlogs
          __path__: /var/log/*.log

&&&&&&&
Make sure:

clients:
  - url: http://localhost:3100/loki/api/v1/push

    ************************************
    
start measure 
http://localhost:3100/ready


