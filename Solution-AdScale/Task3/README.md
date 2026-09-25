# Задание 3. Данные, масштабирование и отказоустойчивость

## О чём эта часть

Хранилища разведены по сервисам так, чтобы аукцион больше не делил диск с отчётами и журналом денег. Все оценки RPO и RTO относятся к целевой схеме года, если явно не сказано, что шаг делается уже в первые три месяца.

## Состав

| Файл | Зачем |
| --- | --- |
| [database-strategy.md](database-strategy.md) | Тип базы у каждого сервиса |
| [scaling.md](scaling.md) | Реплики, шардирование, CQRS |
| [caching.md](caching.md) | Redis, TTL, инвалидация, прогрев |
| [event-streaming.md](event-streaming.md) | Топики, схемы, группы, хранение |
| [failover.md](failover.md) | RPO, RTO, копии, 12-factor |
| [diagrams/data-architecture.puml](diagrams/data-architecture.puml) · [drawio](diagrams/data-architecture.drawio) | Сервисы и их хранилища |
| [diagrams/kafka-topology.puml](diagrams/kafka-topology.puml) · [drawio](diagrams/kafka-topology.drawio) | Потоки и потребители |
| [diagrams/cache-and-cqrs.puml](diagrams/cache-and-cqrs.puml) · [drawio](diagrams/cache-and-cqrs.drawio) | Проекция ставок и витрины отчётов |

Сервис ставок сознательно без собственной базы учёта. Это записано в стратегии, а не забыто.
