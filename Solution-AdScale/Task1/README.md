# Задание 1. Архитектурная диагностика и целевое видение

## О чём эта часть

AdScale уже работает на пределе монолита. Интеграция с новой DSP-площадкой добавляет трафик и более жёсткий SLA. Здесь зафиксированы диагноз, драйверы, стиль эволюции и целевая схема через год.

## Состав

| Файл | Зачем |
| --- | --- |
| [AS-IS.md](AS-IS.md) | Узкие места, точки отказа, влияние на latency |
| [drivers.md](drivers.md) | Функциональные требования, атрибуты качества, ограничения |
| [TO-BE.md](TO-BE.md) | Целевая архитектура через год и переходный контур на 3 месяца |
| [diagrams/c4-container-as-is.puml](diagrams/c4-container-as-is.puml) · [drawio](diagrams/c4-container-as-is.drawio) | C4 Container, текущее состояние |
| [diagrams/c4-container-transition-3m.puml](diagrams/c4-container-transition-3m.puml) · [drawio](diagrams/c4-container-transition-3m.drawio) | C4 Container, контур интеграции через 3 месяца |
| [diagrams/c4-container-to-be.puml](diagrams/c4-container-to-be.puml) · [drawio](diagrams/c4-container-to-be.drawio) | C4 Container, цель через 12 месяцев |
| [adr/ADR-001-evolution-strategy.md](adr/ADR-001-evolution-strategy.md) | Strangler Fig вместо «остаться монолитом» и вместо одномоментных микросервисов |
| [adr/ADR-002-bidding-service-first.md](adr/ADR-002-bidding-service-first.md) | Первым выносится сервис ставок |
| [adr/ADR-003-event-streaming.md](adr/ADR-003-event-streaming.md) | Kafka и Avro для событий показов и кликов |

Диаграммы — PlantUML со стандартной библиотекой C4-PlantUML. Локальный просмотр: [PlantUML](https://www.plantuml.com/plantuml) или плагин IDE.

## Решение в одном абзаце

Критический путь аукциона синхронно читает единственный PostgreSQL, в который одновременно пишутся события и по которому считаются тяжёлые отчёты. За три месяца новый DSP подключается к выделенному сервису ставок за Envoy: кандидаты и бюджеты читаются из памяти и Redis, события уходят в Kafka уже после ответа. Монолит в это время продолжает обслуживать текущих клиентов. За год из него по тому же шву выносятся кампании, финансы, статистика и аналитика.
