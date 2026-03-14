# Настройка дашборда Grafana для ML-сервиса

## 1. Источник данных

1. Откройте Grafana: http://localhost:3000 (admin/admin)
2. Меню слева → **Connections** → **Data sources** → **Add data source**
3. Выберите **Prometheus**
4. URL: `http://prometheus:9090` (если docker-compose.full) или `http://host.docker.internal:9090`
5. **Save & test**

## 2. Создание дашборда

1. Меню слева → **Dashboards** → **New** → **New dashboard**
2. **Add visualization** (или «+ Add»)

## 3. Добавление панелей с запросами

### Панель 1: Request Rate (график)

1. В дашборде нажмите **Add** → **Visualization**
2. Выберите источник **Prometheus**
3. В поле **Query** вставьте:
   ```
   rate(ml_service_requests_total[5m])
   ```
4. В **Legend** (справа): `{{method}} - {{endpoint}}`
5. **Save** → **Apply**

### Панель 2: Prediction Count (число)

1. **Add** → **Visualization**
2. Выберите тип **Stat** (или **Gauge**)
3. В **Query**:
   ```
   increase(ml_service_predictions_total[1h])
   ```
4. **Apply**

### Панель 3: Request Latency p95 (график)

1. **Add** → **Visualization**
2. В **Query**:
   ```
   histogram_quantile(0.95, rate(ml_service_request_duration_seconds_bucket[5m]))
   ```
3. **Legend**: `p95`
4. **Apply**

### Панель 4: Predict Latency (график)

1. **Add** → **Visualization**
2. В **Query**:
   ```
   histogram_quantile(0.95, rate(ml_service_predict_duration_seconds_bucket[5m]))
   ```
3. **Apply**

## 4. Сохранение дашборда

Нажмите **Save dashboard** (иконка дискеты) → введите имя → **Save**.

## Запросы для копирования

| Панель | Запрос |
|--------|--------|
| Request Rate | `rate(ml_service_requests_total[5m])` |
| Prediction Count | `increase(ml_service_predictions_total[1h])` |
| Request Latency p95 | `histogram_quantile(0.95, rate(ml_service_request_duration_seconds_bucket[5m]))` |
| Predict Latency p95 | `histogram_quantile(0.95, rate(ml_service_predict_duration_seconds_bucket[5m]))` |
