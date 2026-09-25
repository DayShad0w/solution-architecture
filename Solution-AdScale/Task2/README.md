# Задание 2. RTB и интеграция с DSP

## О чём эта часть

Спроектирован контур, которым AdScale отвечает новой DSP: границы сервиса ставок, протоколы, шлюз и поведение при отказах. Контур встраивается в переход на три месяца из [задания 1](../Task1/TO-BE.md) и остаётся тем же горячим путём в целевой схеме года.

## Состав

| Файл | Зачем |
| --- | --- |
| [bidding-service.md](bidding-service.md) | Границы, API, зависимости, модель данных |
| [interaction.md](interaction.md) | Протоколы и почему они разные на разных границах |
| [api-gateway.md](api-gateway.md) | Вход DSP: маршрут, лимит, аутентификация, размыкатель, метрики |
| [reliability.md](reliability.md) | Таймауты, повтор, идемпотентность, запасные стратегии |
| [diagrams/component-bidding.puml](diagrams/component-bidding.puml) · [drawio](diagrams/component-bidding.drawio) | Компоненты сервиса ставок |
| [diagrams/sequence-bid.puml](diagrams/sequence-bid.puml) · [drawio](diagrams/sequence-bid.drawio) | Последовательность bid request |
| [diagrams/sequence-tracking.puml](diagrams/sequence-tracking.puml) · [drawio](diagrams/sequence-tracking.drawio) | Показ и клик мимо горячего пути |

## Инвариант

От момента приёма bid request до HTTP-ответа сервис ставок обращается только к своей памяти и, при промахе локального кэша, к Redis. Campaign, Finance, PostgreSQL и Kafka в этот интервал не вызываются.
