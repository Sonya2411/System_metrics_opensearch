# System_metrics_opensearch
Этот проект разворачивает стек для мониторинга и визуализации системных метрик с использованием:

- **Metricbeat** — сбор метрик системы
- **Logstash** — маршрутизация и обработка данных
- **OpenSearch** — хранилище и движок поиска
- **OpenSearch Dashboards** — визуализация

## Установка

### 1. Установка зависимостей 

Убедитесь, что у вас установлены:

- `Java 17+` (для Logstash и OpenSearch)
- `tar`, `curl`, `systemd`, `wget`

Используемые технологии:

- OpenSearch 2.18.0
- Logstash 8.9.0
- Metricbeat 8.13.4
- OpenSearch Dashboards 2.18.0

### 2. Настройка конфигураций

#### Установка сервисов

- Переместите opensearch.service и opensearch_dashboards.service по пути /lib/systemd/system
- Переместите logstash.service и metricbeat.service по пути /etc/systemd/system

Все технологии устанавливать в директорию /opt

#### Metricbeat
- Замените файл metricbeat.yml в папке metricbeat

#### Logstash
- Файл `metricbeat.conf` содержит pipeline, принимающий данные от Metricbeat и отправляющий их в OpenSearch
- Замените файл `pipelines.yml` по пути logstash/config и поместите файл `metricbeat.conf` по пути logstash/config/conf.d

### 4. Настройка сервисов

```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl start opensearch
sudo systemctl start opensearch_dashboards
sudo systemctl start logstash
sudo systemctl start metricbeat
```
### 5. Визуализация

1. Перейдите в http://localhost:5601
2. Создайте Index Puttern metricbeat-YYYY.MM.DD
3. Постройте визуализации
