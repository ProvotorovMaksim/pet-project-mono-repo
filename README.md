# Pet Project Monorepo — стенд VPN-сервисов

## Назначение проекта

Собирает точку входа, авторизацию, кабинет VPN и уведомления для локальной демонстрации межсервисных интеграций.

## Функциональность

Корневой Compose включает четыре приложения. В закреплённых версиях реализованы маршрутизация шлюза, JWT-авторизация, операции личного кабинета и HTTP-уведомления. Prometheus и Grafana включены в конфигурацию шлюза.

## Архитектура

`docker-compose.yml` подключает файлы из `services/`. Шлюз проксирует HTTP, auth и VPN используют отдельные PostgreSQL. VPN обращается к auth, биллингу и VPN-провайдеру по HTTP. Уведомления используют Telegram и содержат модуль Kafka-consumer. Биллинг, VPN-провайдер и Kafka требуют отдельной инфраструктуры.

### С чего начать чтение кода

- [`docker-compose.yml`](docker-compose.yml)
- [`services/API-Gateway-service/main.py`](services/API-Gateway-service/main.py)
- [`services/E-commerce-vpn/routers/api.py`](services/E-commerce-vpn/routers/api.py)

[Граф связей Graphify](graphify-out/graph.html) · [Отчёт Graphify](graphify-out/GRAPH_REPORT.md)

Для поиска по графу из корня репозитория выполните `graphify god-nodes --top 5` или `graphify query "имя функции или модуля"`.

## Технологический стек

Python, FastAPI, HTTPX, PostgreSQL, SQLAlchemy, asyncpg, Alembic, JWT, Kafka-клиенты, Prometheus, Grafana, Docker Compose.

## Технические решения

Сервисы используют общую сеть и отдельные хранилища. Alembic применяется при старте auth и VPN. Обзор и граф опираются на закреплённые коммиты вложенных проектов.

## Запуск проекта

Требуется Docker Compose с поддержкой include. В рабочей копии нужны все четыре папки `services/` с исходниками. Git хранит их как ссылки на вложенные репозитории, но `.gitmodules` отсутствует. TODO — восстановить отображение вложенных репозиториев, устранить конфликт хост-порта 8000 и проверить чистый клон. Настройте значения по именам из `.env.example`, включая `JWT_SECRET_KEY`, `SERVICES_URLS`, `VPN_DATABASE_URL`, `REGISTRY_DATABASE_URL`, `POSTGRES_*` и настройки внешних сервисов. Сначала выполните `docker compose config --quiet`, затем `docker compose up --build` после устранения ошибок конфигурации.

## Примеры API

Шлюз предоставляет `GET /health` и прокси `/api/{path}`. Во вложенных сервисах есть `POST /register`, `POST /login`, `GET /me` и `GET /api/tariffs`. Пример обращается к шлюзу.

```bash
curl -i http://localhost:8000/health
```

## Тестирование

В локальной рабочей копии auth есть TestClient-тесты в `services/Registration-backend-service/tests.py`. Запуск из каталога auth — `python -m pytest tests.py` с тестовыми PostgreSQL и Kafka. Корневой сквозной набор отсутствует.

## Ограничения и дальнейшее развитие

Нужно восстановить воспроизводимое получение исходников, проверить итоговый Compose и зафиксировать контракты для внешних зависимостей.

## Мой вклад

TODO — описать свою роль, реализованные компоненты и принятые технические решения.

[Технический обзор проекта](PROJECT_REVIEW.md)
