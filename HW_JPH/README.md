# HW_JPH — JupyterHub в Docker

## Структура

- `Dockerfile` — образ на базе python:3.14-slim с JupyterHub и configurable-http-proxy
- `docker-compose.yaml` — сборка и запуск JupyterHub
- `.env` — секреты (токены, пути)
- `jupyterhub_config.py` — конфигурация JupyterHub

## Запуск

```bash
# Сборка и запуск
docker compose build
docker compose up -d

# Просмотр логов
docker compose logs -f jupyterhub
```

## Вход под admin

1. Откройте http://localhost:8000
2. На странице входа введите **admin** в поле Username
3. Поле Password можно оставить пустым (DummyAuthenticator)
4. Нажмите Sign in

## Остановка

```bash
docker compose down
```
