# Prometheus/Grafana/Node_expporter in Docker
Данная конфигурация **НЕ ВКЛЮЧАЕТ в себя установку docker и docker copmpose**

---
#### Первоначальная подготовка
Создаём директорию проекта 
``` bash
mkdir -p /prometheus 
mkdir -p /prometheus/configuration 
mkdir -p /prometheus/data
chown 65534:65534 /prometheus/data
```
сюда же мы клонируем наш docker compose файл

```bash
cd /prometheus
git clone git@github.com:WhitePavel/prometheus_docker.git
```
---
#### здесь мы создаём конфигурационный файл prometheus для получения метрик
изначально метрики идут только с хоста, если нужно выбрать другие отредактируйте файл как вам нужно, я оставил подключение к хосту
⬇️⬇️⬇️
``` bash
cat <<EOF> /prometheus/configuration/prometheus.yml
scrape_configs:
  - job_name: node
    scrape_interval: 10s
    static_configs:
    - targets: ['node-exporter:9100']
EOF
```
---
Осталось только поднять наш файл через docker compose
``` bash
cd /prometheus 
docker-compose up -d 
```
---
### [Основа данной конфигурации взята с источника](https://dockerhosting.ru/blog/zapusk-prometheus-v-docker/)
