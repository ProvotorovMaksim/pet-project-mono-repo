# Graph Report - pet-project-mono-repo  (2026-11-12)

## Corpus Check
- В структурный анализ включено файлов исходного кода: 30. Сторонние зависимости, документация и файлы окружения исключены.

## Summary
- 218 nodes · 365 edges · 12 communities (8 shown, 4 thin omitted)
- Extraction: 93% EXTRACTED · 7% INFERRED · 0% AMBIGUOUS · INFERRED: 25 edges (avg confidence: 0.93)
- Token cost: 0 input · 0 output

## Community Hubs (Navigation)
- Registration-backend-service/main.py
- api.py
- E-commerce-vpn/alembic_migrations/env.py
- kafka_consumer.py
- logging
- API-Gateway-service/main.py
- sqlalchemy
- httpx
- verify_token_optional

## God Nodes (most connected - your core abstractions)
1. `Client` - 7 edges
2. `login_user()` - 7 edges
3. `create_device()` - 7 edges
4. `UserSchema` - 6 edges
5. `register_user()` - 6 edges
6. `login()` - 6 edges
7. `register()` - 6 edges
8. `LoginRequest` - 5 edges
9. `Device` - 5 edges
10. `add_user_to_db()` - 5 edges

## Surprising Connections (you probably didn't know these)
- `notify()` --calls--> `start_consuming()`  [INFERRED]
  services/notification-service/main.py → services/notification-service/kafka_consumer.py
- `login_user()` --uses--> `LoginRequest`  [INFERRED]
  services/Registration-backend-service/main.py → services/Registration-backend-service/Schemas.py
- `login_user()` --uses--> `LoginResponse`  [INFERRED]
  services/Registration-backend-service/main.py → services/Registration-backend-service/Schemas.py
- `add_user_to_db()` --uses--> `UserSchema`  [INFERRED]
  services/Registration-backend-service/db_provider.py → services/Registration-backend-service/Schemas.py
- `register_user()` --uses--> `UserSchema`  [INFERRED]
  services/Registration-backend-service/main.py → services/Registration-backend-service/Schemas.py

## Import Cycles
- None detected.

## Communities (12 total, 4 thin omitted)

### Community 0 - "Registration-backend-service/main.py"
Cohesion: 0.10
Nodes (15): add_user_to_db(), get_db(), produce_message(), producer_callback(), get_current_user(), login_user(), read_root(), register_user() (+7 more)

### Community 1 - "api.py"
Cohesion: 0.12
Nodes (22): Base, Client, Device, create_device(), create_payment(), delete_device(), get_device_config(), get_devices() (+14 more)

### Community 2 - "E-commerce-vpn/alembic_migrations/env.py"
Cohesion: 0.09
Nodes (8): do_run_migrations(), run_async_migrations(), run_migrations_online(), do_run_migrations(), run_async_migrations(), run_migrations_online(), Base, User

### Community 3 - "kafka_consumer.py"
Cohesion: 0.10
Nodes (13): Settings, Config, Settings, Config, process_message(), safe_deserializer(), send_alert(), start_consuming() (+5 more)

### Community 4 - "logging"
Cohesion: 0.09
Nodes (5): healthcheck(), serve_frontend(), send_email(), notify(), send_alert()

### Community 5 - "API-Gateway-service/main.py"
Cohesion: 0.13
Nodes (7): health_check(), proxy_grafana_websocket(), proxy_to_grafana_final(), proxy_to_service(), serve_frontend(), shutdown_event(), verify_token_optional()

### Community 6 - "sqlalchemy"
Cohesion: 0.23
Nodes (6): upgrade(), downgrade(), upgrade(), downgrade(), upgrade(), upgrade()

### Community 7 - "httpx"
Cohesion: 0.13
Nodes (3): AuthServiceClient, BillingServiceClient, VpnServiceClient

## Knowledge Gaps
- **4 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Are the 5 inferred relationships involving `Client` (e.g. with `create_device()` and `get_devices()`) actually correct?**
  _`Client` has 5 INFERRED edges - model-reasoned connections that need verification._
- **Should `Registration-backend-service/main.py` be split into smaller, more focused modules?**
  _Cohesion score 0.09759759759759759 - nodes in this community are weakly interconnected._
- **Are the 2 inferred relationships involving `login_user()` (e.g. with `LoginRequest` and `LoginResponse`) actually correct?**
  _`login_user()` has 2 INFERRED edges - model-reasoned connections that need verification._
- **Should `api.py` be split into smaller, more focused modules?**
  _Cohesion score 0.11746031746031746 - nodes in this community are weakly interconnected._
- **Should `E-commerce-vpn/alembic_migrations/env.py` be split into smaller, more focused modules?**
  _Cohesion score 0.0896551724137931 - nodes in this community are weakly interconnected._
- **Should `kafka_consumer.py` be split into smaller, more focused modules?**
  _Cohesion score 0.10052910052910052 - nodes in this community are weakly interconnected._
- **Should `logging` be split into smaller, more focused modules?**
  _Cohesion score 0.09333333333333334 - nodes in this community are weakly interconnected._