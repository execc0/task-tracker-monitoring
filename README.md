# Monitoring Stack

Docker Compose стек для мониторинга сервера: Prometheus + Grafana + Node Exporter.

Используется для мониторинга двух проектов на одном сервере — **Task Tracker API** и **Telegram-бота для Task Tracker**.

## Связанные проекты

- [Task Tracker](https://github.com/execc0/task-tracker) — трекер задач
- [Telegram Bot](https://github.com/execc0/task-tracker-TGBot) — телеграм-бот

## Состав

- **Prometheus** — сбор и хранение метрик (retention: 3 дня)
- **Grafana** — визуализация метрик и дашборды
- **Node Exporter** — метрики хоста (CPU, RAM, диск, сеть)

## Требования

- Docker, Docker Compose
- Внешняя сеть `shared-network` (должна быть создана заранее):
  ```bash
  docker network create shared-network
  ```

## Запуск

```bash
docker compose up -d
```

## Доступ

Все порты проброшены только на `127.0.0.1` — доступ извне закрыт, наружу можно отдать через reverse proxy (nginx и т.п.).

| Сервис        | Адрес                    |
|---------------|---------------------------|
| Prometheus    | http://127.0.0.1:9095     |
| Grafana       | http://127.0.0.1:3000     |
| Node Exporter | http://127.0.0.1:9100     |

Логин/пароль Grafana по умолчанию: `admin` / `admin` (сменить при первом входе).

## Скриншоты

Пример дашбордов Grafana:

Метрики Spring boot приложения:
<img width="1566" height="944" alt="image" src="https://github.com/user-attachments/assets/f20b0c4a-cfb8-4e13-a149-9acf379878ab" />

Метрики node-exporter: 
<img width="1536" height="874" alt="image" src="https://github.com/user-attachments/assets/5c436733-dc45-40b6-94f0-9569987d0481" />

## Данные

Метрики Prometheus и настройки Grafana хранятся в именованных volume'ах (`prometheus_data`, `grafana_data`) и переживают перезапуск контейнеров.
