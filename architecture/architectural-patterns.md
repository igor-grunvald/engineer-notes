# Архитектурные паттерны

> **Полный каталог архитектурных паттернов проектирования** — от управления данными до деплоя.  
> Каждый паттерн: суть, проблема, решение, диаграмма, технологии, примеры кода, плюсы/минусы, комбинации.
> 
> **Архитектурный стиль** (см. [software-architectures.md](software-architectures.md)) — это фундаментальная организация системы (монолит vs микросервисы).  
> **Архитектурный паттерн** — это конкретный шаблон решения типовой проблемы *внутри* выбранного стиля.
>
> ⸻

---

## Оглавление

- [Введение: стиль vs паттерн](#введение-стиль-vs-паттерн)
- **[Часть I. Паттерны управления данными](#часть-i-паттерны-управления-данными)**
  - [1. Database per Service](#1-database-per-service)
  - [2. Shared Database](#2-shared-database)
  - [66. Database Sharding](#66-database-sharding)
  - [3. CQRS](#3-cqrs-command-query-responsibility-segregation)
  - [4. Event Sourcing](#4-event-sourcing)
  - [5. Saga](#5-saga)
  - [6. Transactional Outbox](#6-transactional-outbox)
  - [7. Change Data Capture (CDC)](#7-change-data-capture-cdc)
  - [8. Domain Event](#8-domain-event)
  - [9. API Composition](#9-api-composition)
  - [10. Materialized View / CQRS Read Model](#10-materialized-view--cqrs-read-model)
- **[Часть II. Паттерны обмена сообщениями](#часть-ii-паттерны-обмена-сообщениями)**
  - [11. Inbox Pattern (Idempotent Consumer)](#11-inbox-pattern-idempotent-consumer)
  - [67. Idempotency Key](#67-idempotency-key)
  - [12. Publish-Subscribe](#12-publish-subscribe)
  - [13. Competing Consumers](#13-competing-consumers)
  - [14. Claim Check](#14-claim-check)
  - [15. Content-Based Router](#15-content-based-router)
  - [16. Message Filter](#16-message-filter)
  - [17. Recipient List](#17-recipient-list)
  - [18. Scatter-Gather](#18-scatter-gather)
  - [19. Routing Slip](#19-routing-slip)
  - [20. Priority Queue](#20-priority-queue)
  - [21. Dead Letter Queue (DLQ)](#21-dead-letter-queue-dlq)
  - [68. Backpressure](#68-backpressure)
- **[Часть III. Паттерны Service Discovery](#часть-iii-паттерны-service-discovery)**
  - [22. Service Registry](#22-service-registry)
  - [23. Self-Registration](#23-self-registration)
  - [24. Third-Party Registration](#24-third-party-registration)
  - [25. Client-Side Discovery](#25-client-side-discovery)
  - [26. Server-Side Discovery](#26-server-side-discovery)
- **[Часть IV. Паттерны отказоустойчивости (Resilience)](#часть-iv-паттерны-отказоустойчивости-resilience)**
  - [27. Circuit Breaker](#27-circuit-breaker)
  - [28. Retry](#28-retry)
  - [29. Timeout](#29-timeout)
  - [30. Bulkhead](#30-bulkhead)
  - [31. Rate Limiting / Throttling](#31-rate-limiting--throttling)
  - [32. Fallback / Graceful Degradation](#32-fallback--graceful-degradation)
  - [33. Health Check API](#33-health-check-api)
  - [34. Cache-Aside](#34-cache-aside)
- **[Часть V. Коммуникационные паттерны](#часть-v-коммуникационные-паттерны)**
  - [35. API Gateway](#35-api-gateway)
  - [36. Backend for Frontend (BFF)](#36-backend-for-frontend-bff)
  - [69. API Versioning](#69-api-versioning)
  - [37. Sidecar](#37-sidecar)
  - [38. Ambassador](#38-ambassador)
  - [39. Anti-Corruption Layer](#39-anti-corruption-layer)
  - [40. Strangler Fig](#40-strangler-fig)
- **[Часть VI. Паттерны безопасности](#часть-vi-паттерны-безопасности)**
  - [43. API Gateway Authentication](#43-api-gateway-authentication)
  - [44. Access Token / JWT](#44-access-token--jwt)
  - [45. OAuth 2.0 / OpenID Connect](#45-oauth-20--openid-connect)
  - [46. Consumer-Driven Contracts](#46-consumer-driven-contracts)
- **[Часть VII. Паттерны наблюдаемости (Observability)](#часть-vii-паттерны-наблюдаемости-observability)**
  - [47. Log Aggregation](#47-log-aggregation)
  - [48. Distributed Tracing](#48-distributed-tracing)
  - [50. Metrics Aggregation](#50-metrics-aggregation)
  - [51. Correlation ID](#51-correlation-id)
  - [52. Audit Logging](#52-audit-logging)
- **[Часть VIII. Паттерны деплоя и поставки](#часть-viii-паттерны-деплоя-и-поставки)**
  - [53. Blue-Green Deployment](#53-blue-green-deployment)
  - [54. Canary Release](#54-canary-release)
  - [55. Feature Toggle / Feature Flag](#55-feature-toggle--feature-flag)
  - [56. Rolling Deployment](#56-rolling-deployment)
  - [57. Shadow Deployment / Dark Launch](#57-shadow-deployment--dark-launch)
  - [58. Service Template](#58-service-template)
  - [59. Externalized Configuration](#59-externalized-configuration)
  - [60. Single Service per Host / Multiple Services per Host](#60-single-service-per-host--multiple-services-per-host)
- **[Часть IX. Инфраструктурные и оркестрационные паттерны](#часть-ix-инфраструктурные-и-оркестрационные-паттерны)**
  - [61. Service Mesh](#61-service-mesh)
  - [70. Leader Election](#70-leader-election)
  - [62. Choreography vs Orchestration (глубокое сравнение)](#62-choreography-vs-orchestration-глубокое-сравнение)
  - [63. Transactional Outbox + Inbox (связка)](#63-transactional-outbox--inbox-связка)
  - [64. Event Collaboration](#64-event-collaboration)
  - [65. Process Manager](#65-process-manager)
- **[Карта совместного использования паттернов](#карта-совместного-использования-паттернов)**
- **[Заключение: как выбирать паттерны](#заключение-как-выбирать-паттерны)**

---

## Введение: стиль vs паттерн

```
Архитектурный СТИЛЬ                Архитектурный ПАТТЕРН
─────────────────────              ────────────────────────
• Фундаментальная организация      • Шаблон решения конкретной
  системы                           проблемы
• Примеры: Микросервисы, SOA,      • Примеры: CQRS, Saga, Circuit
  Монолит, Serverless               Breaker, Outbox
• "Как система устроена            • "Как решить проблему X
  в целом"                          внутри архитектуры Y"
```

Паттерны комбинируются. Типичный микросервисный проект использует **одновременно**: Database per Service, Saga, Transactional Outbox, Circuit Breaker, Service Discovery, API Gateway, Health Check, Distributed Tracing.

---

# Часть I. Паттерны управления данными

> В распределённой системе данные — самая сложная часть. ACID-транзакции работают только в пределах одной БД.  
> Как только данные распределены по сервисам — нужны новые подходы.

---

## 1. Database per Service

### Проблема

В микросервисной архитектуре несколько сервисов не могут делить одну БД — это создаёт **жёсткую связь на уровне данных**. Если Сервис A пишет в таблицу `orders`, а Сервис B напрямую читает её же — любое изменение схемы в А ломает B.

### Решение

**Каждый сервис владеет своей БД.** Никакой другой сервис не имеет прямого доступа к данным. Общение — только через API (синхронное) или события (асинхронное).

```
┌──────────┐     ┌──────────┐     ┌──────────┐
│  Orders  │     │ Payment  │     │  Catalog │
│  Service │     │ Service  │     │  Service │
│  ┌─────┐ │     │  ┌─────┐ │     │  ┌─────┐ │
│  │  PG │ │     │  │  PG │ │     │  │Mongo│ │
│  └─────┘ │     │  └─────┘ │     │  └─────┘ │
└──────────┘     └──────────┘     └──────────┘
     ✘                 ✘                 ✘
  Order Service    Payment Service    Catalog Service
  не может читать  не может читать   не может читать
  payment.payments  catalog.products   orders.orders
```

### Варианты реализации

| Подход | Описание | Когда |
|--------|----------|-------|
| **Отдельная физическая БД** | Каждый сервис → своя СУБД (PostgreSQL, MongoDB, DynamoDB) | Жёсткая изоляция, разная природа данных |
| **Отдельная логическая БД (схема)** | Одна физическая СУБД, но разные схемы/базы внутри (`orders_db`, `payment_db`) | Упрощённое администрирование, shared-nothing по данным |
| **Table per Service** | Все таблицы в одной БД, но сервис имеет доступ только к «своим» | Компромисс с риском связывания |

### Технологии

- **Реляционные:** PostgreSQL, MySQL, Oracle, MS SQL
- **Документные:** MongoDB, Couchbase
- **Key-Value:** Redis, DynamoDB, Cassandra (wide-column)
- **Графовые:** Neo4j, Amazon Neptune
- **Поисковые:** Elasticsearch
- **Time-Series:** InfluxDB, TimescaleDB

### Плюсы

- **Слабая связанность.** Изменение схемы в одном сервисе не затрагивает другие.
- **Polyglot Persistence.** Каждый сервис выбирает БД под свою задачу (каталог → Elasticsearch, заказы → PostgreSQL, аналитика → ClickHouse).
- **Независимое масштабирование.** Нагруженный сервис масштабируется вместе со своей БД.

### Минусы

- **Нет ACID-транзакций между сервисами.** Нужны саги, Event Sourcing, компенсации.
- **Распределённые запросы.** JOIN двух таблиц из разных БД невозможен → API Composition или CQRS.
- **Удорожание инфраструктуры.** Вместо 1 СУБД администрируешь N.
- **Консистентность данных.** Eventual consistency вместо strong consistency.

### Пример: Заказ в интернет-магазине

```
1. POST /orders → Order Service сохраняет заказ в orders_db
2. Order Service публикует событие OrderPlaced
3. Payment Service слушает событие → создаёт платёж в payment_db
4. Payment Service публикует PaymentProcessed
5. Notification Service слушает → отправляет email (notification_db)
```

Каждый сервис работает **только со своей БД**.

---

## 2. Shared Database

### Проблема

Несколько сервисов должны читать/писать одни и те же данные с сильной консистентностью. Database per Service не подходит — бизнес требует ACID.

### Решение

**Несколько сервисов используют одну общую БД.** Это антипаттерн в чистом микросервисном мире, но рабочий паттерн для модульных монолитов и переходных архитектур.

```
┌──────────┐  ┌──────────┐  ┌──────────┐
│  Orders  │  │ Payment  │  │  Catalog │
│  Service │  │ Service  │  │  Service │
└────┬─────┘  └────┬─────┘  └────┬─────┘
     └──────────────┼──────────────┘
                    │
            ┌───────┴───────┐
            │   ЕДИНАЯ БД   │
            │  PostgreSQL   │
            └───────────────┘
```

### Когда использовать

- **Модульный монолит на этапе миграции.** Сервисы уже выделены как модули, но БД ещё общая.
- **Строгие ACID-требования.** Финансовый учёт, бухгалтерия — консистентность важнее изоляции.
- **Небольшие системы (до 3–5 сервисов).**

### Риски и компенсации

| Риск | Компенсация |
|------|-------------|
| Изменение схемы ломает несколько сервисов | Строгая дисциплина: каждый сервис читает/пишет только «свои» таблицы через views/схемы |
| Блокировки между сервисами | Row-level locking, оптимистичные блокировки |
| Общая точка отказа | Репликация, кластеризация |

### Технологии

PostgreSQL (схемы), Oracle (pluggable databases), MS SQL (schemas).

---

## 66. Database Sharding

### Проблема

Database per Service решает проблему изоляции данных между сервисами, но не проблему **объёма данных внутри одного сервиса**. Когда одна БД перестаёт вмещать данные (сотни гигабайт/терабайты) или не справляется с нагрузкой на запись — вертикальное масштабирование упирается в потолок железа.

### Решение

**Шардирование (Sharding)** — горизонтальное партиционирование: данные распределяются по нескольким независимым БД (шардам) на основе **шард-ключа** (partition key). Каждый шард содержит подмножество данных и обслуживает свою долю нагрузки.

```
                    ┌──────────────────┐
                    │  Routing Layer   │  ← Определяет шард по ключу
                    │  (Proxy / Driver)│
                    └──┬───────┬───────┘
                       │       │
              ┌────────┘       └────────┐
              ▼                         ▼
        ┌──────────┐              ┌──────────┐
        │  Shard 0 │              │  Shard 1 │
        │customers │              │customers │
        │  A–M     │              │  N–Z     │
        └──────────┘              └──────────┘
```

### Стратегии шардирования

| Стратегия | Принцип | Плюсы | Минусы |
|-----------|---------|-------|--------|
| **Range-based** | Диапазоны ключа: A–M → Shard 0, N–Z → Shard 1 | Простота, range queries | Неравномерное распределение (hot shard) |
| **Hash-based** | `hash(key) % N` → Shard | Равномерное распределение | Теряются range queries; решардинг дорог (меняется N) |
| **Directory-based** | Отдельный routing table: `key → shard_id` | Гибкость, ручное управление | Дополнительный компонент (directory service) |
| **Geo-based** | По региону пользователя | Локализация данных, compliance | Неравномерность по регионам |

### Кросс-шард запросы

JOIN и агрегации между шардами **не работают** на уровне БД. Решения:
- **Денормализация** — дублировать нужные данные на каждом шарде.
- **Scatter-Gather** — запрос на все шарды, агрегация на клиенте/прокси.
- **Избегать кросс-шард операций** — выбирать шард-ключ так, чтобы 95%+ запросов были в пределах одного шарда.

### Технологии

| Инструмент | Тип | Особенности |
|------------|-----|-------------|
| **Vitess** | MySQL-совместимый прокси | Автоматический шардинг, миграции без downtime |
| **Citus** | Расширение PostgreSQL | Distributed tables + reference tables |
| **MongoDB Sharding** | Встроенный шардинг | Автоматическая балансировка chunk'ов |
| **Cassandra** | Wide-column | Partition key = шард-ключ из коробки |
| **YugabyteDB / CockroachDB** | NewSQL | Автоматический шардинг + ACID |

### Плюсы

- **Горизонтальное масштабирование.** Добавил шард = добавил ёмкость и throughput.
- **Изоляция нагрузки.** Один горячий пользователь не влияет на остальных.
- **Geo-distribution.** Шарды могут быть в разных регионах.

### Минусы

- **Сложность запросов.** JOIN между шардами невозможен; агрегации — scatter-gather.
- **Решардинг.** При добавлении шарда нужно перераспределить данные (Vitess/Citus упрощают).
- **Нет ACID-транзакций между шардами.**
- **Выбор шард-ключа.** Ошибка в выборе ключа = неравномерное распределение и кросс-шард запросы.

### Когда использовать

- **Объём данных > 500 GB** на одном сервисе.
- **Высокая нагрузка на запись** (>10k writes/sec на одну БД).
- **Мультитенантность** — шард на клиента (tenant).

---

## 3. CQRS (Command Query Responsibility Segregation)

### Проблема

В традиционной архитектуре одна модель данных используется и для чтения, и для записи. Но:
- **Чтение** требует денормализованных, оптимизированных под UI данных (JOIN'ы, агрегации).
- **Запись** требует нормализованных, консистентных данных (бизнес-правила, инварианты).

Одна модель компрометирует обе операции: запись становится сложной из-за учёта читательских сценариев, чтение — медленным из-за нормализации.

### Решение

**Разделить модель на две: Command (запись) и Query (чтение).** Каждая оптимизирована под свою задачу.

```
                     ┌──────────────────────┐
                     │     Command Stack      │
                     │  (Write Model)         │
    POST /orders ──→ │  • Order Aggregate     │ ──→ PostgreSQL (нормализованная)
    PUT /orders/1 ──→│  • Бизнес-правила      │
    DELETE /orders/1→│  • Инварианты          │
                     └──────────┬─────────────┘
                                │ События
                                ▼
                     ┌──────────────────────┐
                     │     Query Stack        │
                     │  (Read Model)          │
    GET /orders ────→│  • OrderProjection     │ ──→ Elasticsearch / MongoDB
    GET /orders/1 ──→│  • Денормализованные   │     (оптимизированная под чтение)
                     │  • Материализованные   │
                     └──────────────────────┘
```

### Детальная архитектура

```
┌──────────────────────────────────────────────────────────┐
│                        API Gateway                        │
└────────────┬────────────────────────────┬────────────────┘
             │                            │
    ┌────────┴────────┐          ┌────────┴────────┐
    │  Command Side   │          │   Query Side    │
    │                 │          │                 │
    │ • Command DTO   │          │ • Query DTO     │
    │ • Command       │  events  │ • QueryHandler  │
    │   Handler       │─────────→│ • Read Model    │
    │ • Aggregate     │          │ • Projection    │
    │ • Repository    │          │                 │
    └───────┬─────────┘          └───────┬─────────┘
            │                            │
    ┌───────┴─────────┐          ┌───────┴─────────┐
    │  Write DB       │          │  Read DB        │
    │  PostgreSQL     │          │  Elasticsearch  │
    │  (нормализация) │          │  MongoDB        │
    └─────────────────┘          │  (денормализ.)  │
                                 └─────────────────┘
```

### Синхронизация моделей

| Способ | Описание | Инструменты |
|--------|----------|-------------|
| **Синхронный** | После команды сразу обновить read-модель (в одной транзакции) | Простой, но связывает стеки |
| **Асинхронный (события)** | Command Stack публикует события → Projection Handler обновляет Read DB | Kafka, RabbitMQ, Debezium (CDC) |
| **CDC** | Чтение WAL (Write-Ahead Log) БД → обновление Read DB | Debezium + Kafka Connect |

### Строгая vs Eventual Consistency

- **Строгая:** команда возвращает ответ только после синхронизации Read DB. Подходит, когда клиент должен увидеть результат сразу.
- **Eventual:** команда возвращает ответ после записи в Write DB; Read DB обновляется асинхронно. Клиент может увидеть устаревшие данные несколько мс/сек.

### Технологии

| Компонент | Варианты |
|-----------|----------|
| **Write DB** | PostgreSQL, MySQL, MS SQL, Oracle |
| **Read DB** | Elasticsearch, MongoDB, Cassandra, DynamoDB, Redis |
| **Event Bus** | Kafka, RabbitMQ, AWS SNS/SQS, Azure Service Bus |
| **CDC** | Debezium, AWS DMS, Oracle GoldenGate |
| **Фреймворки** | Axon Framework (Java), NServiceBus (.NET), Eventuate |

### Пример: Заказ в CQRS (Java + Axon Framework)

```java
// === COMMAND SIDE ===
@Data
public class CreateOrderCommand {
    @TargetAggregateIdentifier
    private final String orderId;
    private final String customerId;
    private final List<OrderLine> lines;
}

@Aggregate
public class OrderAggregate {
    @AggregateIdentifier
    private String orderId;
    private OrderStatus status;
    private BigDecimal total;

    @CommandHandler
    public OrderAggregate(CreateOrderCommand cmd) {
        // Бизнес-правила валидации
        if (cmd.getLines().isEmpty()) {
            throw new IllegalArgumentException("Order must have at least one line");
        }
        // Публикуем событие
        AggregateLifecycle.apply(new OrderCreatedEvent(
            cmd.getOrderId(), cmd.getCustomerId(), cmd.getLines(), calculateTotal(cmd.getLines())
        ));
    }

    @EventSourcingHandler
    public void on(OrderCreatedEvent event) {
        this.orderId = event.getOrderId();
        this.status = OrderStatus.CREATED;
        this.total = event.getTotal();
    }
}

// === QUERY SIDE ===
@EventHandler
public class OrderProjection {
    private final ElasticsearchRepository esRepo;

    @EventHandler
    public void on(OrderCreatedEvent event) {
        OrderView view = new OrderView(
            event.getOrderId(),
            event.getCustomerId(),
            event.getLines(),
            event.getTotal(),
            "CREATED"
        );
        esRepo.save(view); // Сохраняем в Elasticsearch для быстрого поиска
    }
}

// Query endpoint
@GetMapping("/orders/{id}")
public OrderView getOrder(@PathVariable String id) {
    return esRepo.findById(id)
        .orElseThrow(() -> new OrderNotFoundException(id));
}
```

### Плюсы

- **Оптимизация чтения и записи независимо.** Read DB может быть денормализована под конкретные UI-экраны.
- **Масштабирование.** Read side масштабируется горизонтально (реплики Elasticsearch).
- **Разделение команд.** Read и Write команды могут развиваться независимо.

### Минусы

- **Сложность.** Два стека вместо одного. Две БД.
- **Eventual consistency.** Read-сторона может отставать.
- **Избыточно для простого CRUD.**

### Когда использовать

- **Сложные чтения:** отчёты, дашборды, полнотекстовый поиск, сложные фильтры.
- **Разные профили нагрузки:** много записей и много чтений с разной структурой.
- **Event Sourcing** — естественный спутник CQRS.

---

## 4. Event Sourcing

### Проблема

Традиционная модель сохраняет **текущее состояние** (`UPDATE orders SET status = 'PAID'`). При этом:
- Теряется история изменений.
- Невозможно узнать, *почему* заказ в статусе PAID (кто, когда, через какие шаги).
- Сложный аудит и временные запросы («показать состояние на 2025-01-01»).

### Решение

**Хранить не текущее состояние, а последовательность событий, которые привели к этому состоянию.** Состояние вычисляется воспроизведением событий.

```
Традиционный подход:               Event Sourcing:
┌──────────────────┐              ┌──────────────────────────────┐
│ orders            │              │ events                       │
│ id │ status│total │              │ id │ type         │ data     │
│ 1  │ PAID  │ 150  │              │ 1  │ OrderCreated │ { ... }  │
└──────────────────┘              │ 2  │ PaymentInit  │ { ... }  │
                                  │ 3  │ PaymentDone  │ { ... }  │
                                  │ 4  │ OrderPacked  │ { ... }  │
                                  └──────────────────────────────┘
                                            │
                                  Воспроизведение 1→2→3→4
                                            │
                                            ▼
                                  ┌────────────────────┐
                                  │ Текущее состояние:  │
                                  │ status = PACKED     │
                                  │ total  = 150        │
                                  └────────────────────┘
```

### Архитектура Event Store

```
┌──────────────────────────────────────────────────┐
│                  Event Store                      │
│  ┌─────────────────────────────────────────────┐ │
│  │            Append-Only Log                   │ │
│  │                                             │ │
│  │  aggregateId │ version │ eventType │ payload │ │
│  │  ─────────────────────────────────────────  │ │
│  │  order-1     │    1    │Created    │ {...}   │ │
│  │  order-1     │    2    │Paid       │ {...}   │ │
│  │  order-1     │    3    │Shipped    │ {...}   │ │
│  │  order-2     │    1    │Created    │ {...}   │ │
│  └─────────────────────────────────────────────┘ │
└──────────────────────────────────────────────────┘
```

### Снимки (Snapshots)

Воспроизводить миллион событий при каждой загрузке агрегата — дорого.  
**Snapshots** — периодические срезы состояния:

```
События: E1 → E2 → ... → E100 → [Snapshot S100] → E101 → ... → E500
Загрузка: читаем S100 + воспроизводим E101...E500 (вместо 500 событий)
```

### Технологии

| Инструмент | Тип | Описание |
|------------|-----|----------|
| **Axon Server** | Специализированный Event Store | Хранение событий + маршрутизация команд/запросов |
| **EventStoreDB** | Специализированный Event Store | Высокопроизводительное хранилище событий с подписками |
| **Kafka** | Event Log | Хранение событий с retention + compaction |
| **PostgreSQL** | Универсальная БД | Таблица events с индексом по (aggregateId, version) |
| **Marten** (.NET) | Библиотека поверх PostgreSQL | Event Sourcing + CQRS для .NET |

### Пример: Агрегат банковского счёта (Java + Axon)

```java
// === СОБЫТИЯ (факты, произошедшие в прошлом) ===
public class AccountCreatedEvent {
    private final String accountId;
    private final String owner;
}

public class MoneyDepositedEvent {
    private final String accountId;
    private final BigDecimal amount;
}

public class MoneyWithdrawnEvent {
    private final String accountId;
    private final BigDecimal amount;
}

// === АГРЕГАТ (Application State) ===
@Aggregate
public class BankAccount {
    @AggregateIdentifier
    private String accountId;
    private BigDecimal balance;
    private String owner;

    @CommandHandler
    public BankAccount(CreateAccountCommand cmd) {
        if (cmd.getInitialBalance().compareTo(BigDecimal.ZERO) < 0) {
            throw new IllegalArgumentException("Negative initial balance");
        }
        AggregateLifecycle.apply(
            new AccountCreatedEvent(cmd.getAccountId(), cmd.getOwner())
        );
    }

    @CommandHandler
    public void handle(DepositMoneyCommand cmd) {
        AggregateLifecycle.apply(
            new MoneyDepositedEvent(accountId, cmd.getAmount())
        );
    }

    @CommandHandler
    public void handle(WithdrawMoneyCommand cmd) {
        if (balance.compareTo(cmd.getAmount()) < 0) {
            throw new InsufficientFundsException(accountId, balance, cmd.getAmount());
        }
        AggregateLifecycle.apply(
            new MoneyWithdrawnEvent(accountId, cmd.getAmount())
        );
    }

    // Event Sourcing Handlers — перестраивают состояние
    @EventSourcingHandler
    public void on(AccountCreatedEvent evt) {
        this.accountId = evt.getAccountId();
        this.owner = evt.getOwner();
        this.balance = BigDecimal.ZERO;
    }

    @EventSourcingHandler
    public void on(MoneyDepositedEvent evt) {
        this.balance = this.balance.add(evt.getAmount());
    }

    @EventSourcingHandler
    public void on(MoneyWithdrawnEvent evt) {
        this.balance = this.balance.subtract(evt.getAmount());
    }
}
```

### Плюсы

- **Полный аудит.** Каждое изменение — событие. Кто, когда, откуда.
- **Временные запросы.** Восстановить состояние на любой момент времени.
- **Отладка.** Переиграть события и найти баг (time-travel debugging).
- **Проекции.** Строить read-модели заново из событий.

### Минусы

- **Сложность.** Разработчикам трудно переключиться с «сохранить состояние» на «сохранить событие».
- **Eventual consistency.** Проекции обновляются асинхронно.
- **Миграции событий.** Изменение структуры события требует upcaster'ов.
- **Объём данных.** Событий может быть на порядки больше, чем строк состояния.

### Когда использовать

- **Финансовые системы** (аудит каждой транзакции обязателен).
- **Бухгалтерия, учёт** (история — не опция, а требование).
- **Сложные бизнес-процессы** (заказ → оплата → сборка → доставка).
- **Системы с требованиями к полной прослеживаемости.**

---

## 5. Saga

### Проблема

В микросервисной архитектуре бизнес-транзакция охватывает несколько сервисов. Распределённых ACID-транзакций не существует (2PC/XA — антипаттерн для высоконагруженных систем). Как гарантировать консистентность данных?

### Решение

**Saga** — последовательность локальных транзакций, где каждая обновляет данные в одном сервисе и публикует событие/сообщение для следующего шага. Если шаг терпит неудачу — выполняются **компенсирующие транзакции**, откатывающие предыдущие шаги.

### Два типа саг

#### A. Choreography (Хореография) — децентрализованная сага

```
Order        Payment      Warehouse    Shipping
Service      Service      Service      Service
  │             │             │            │
  ├─Order─────→│             │            │
  │ Placed     │             │            │
  │            ├─Payment────→│            │
  │            │ Processed   │            │
  │            │             ├─Goods─────→│
  │            │             │ Reserved   │
  │            │             │            ├─Order────→
  │            │             │            │ Shipped
  │            │             │            │
  │            │    ОТКАЗ: GoodsReservationFailed
  │            │←────────────┤            │
  │            ├─Refund─────→│            │
  │            │ Payment     │            │
  │←Cancel─────┤             │            │
  │ Order      │             │            │
```

**Плюсы хореографии:**
- Слабая связанность — сервисы не знают друг о друге.
- Простота добавления новых шагов (просто подписаться на событие).
- Нет единой точки отказа (оркестратора).

**Минусы хореографии:**
- Сложно понять end-to-end flow (логика размазана по сервисам).
- Циклические зависимости при неосторожном проектировании.
- Сложность тестирования всей саги целиком.

#### B. Orchestration (Оркестрация) — централизованная сага

```
                    ┌──────────────────┐
                    │  Saga            │
                    │  Orchestrator    │
                    │  (OrderSaga)     │
                    └──┬───┬───┬───┬──┘
                       │   │   │   │
              ┌────────┘   │   │   └────────┐
              ▼            ▼   ▼            ▼
        ┌──────────┐ ┌──────────┐ ┌──────────┐
        │  Orders  │ │ Payment  │ │ Warehouse│
        └──────────┘ └──────────┘ └──────────┘
```

**Оркестратор** — конечный автомат, управляющий процессом:
1. Создать заказ → Orders Service
2. Принять платёж → Payment Service
3. Зарезервировать товар → Warehouse Service
4. Организовать доставку → Shipping Service

На каждом шаге — сценарии успеха и отказа (с компенсацией).

**Плюсы оркестрации:**
- Flow явный — вся логика в оркестраторе.
- Легче тестировать — оркестратор можно запустить изолированно.
- Нет циклических зависимостей.

**Минусы оркестрации:**
- Оркестратор — дополнительный компонент.
- Риск «божественного объекта», знающего слишком много.
- Дополнительная связность.

### Технологии

| Инструмент | Тип саги | Особенности |
|------------|----------|-------------|
| **Axon Framework** | Оба | Saga = @Saga класс; управляет ассоциациями по ключу |
| **Temporal** | Оркестрация | Workflow as Code; долгоиграющие процессы, retry, таймауты |
| **Camunda / Zeebe** | Оркестрация | BPMN-движок; визуальное моделирование саг |
| **AWS Step Functions** | Оркестрация | Управляемый сервис; JSON-описание flow |
| **MicroProfile LRA** | Оба | Стандарт Jakarta EE для Long-Running Actions |
| **Kafka / RabbitMQ** | Хореография | События как клей между сервисами |

### Пример: Сага заказа (Java + Axon — оркестрация)

```java
@Saga
public class OrderSaga {

    // Сага начинается, когда создан заказ
    @StartSaga
    @SagaEventHandler(associationProperty = "orderId")
    public void on(OrderCreatedEvent event) {
        // Шаг 1: отправить команду на создание платежа
        SagaLifecycle.associateWith("paymentId", event.getPaymentId());
        commandGateway.send(new ProcessPaymentCommand(
            event.getPaymentId(), event.getOrderId(), event.getAmount()
        ));
    }

    // Платёж обработан успешно
    @SagaEventHandler(associationProperty = "orderId")
    public void on(PaymentProcessedEvent event) {
        // Шаг 2: зарезервировать товар
        commandGateway.send(new ReserveGoodsCommand(
            event.getOrderId(), event.getItems()
        ));
    }

    // Ошибка резервирования → компенсация: возврат платежа
    @SagaEventHandler(associationProperty = "orderId")
    public void on(GoodsReservationFailedEvent event) {
        commandGateway.send(new RefundPaymentCommand(
            event.getPaymentId(), event.getOrderId()
        ));
    }
}
```

### Компенсирующие транзакции — ключевая концепция

| Шаг | Локальная транзакция | Компенсация при откате |
|-----|---------------------|------------------------|
| 1 | Создать заказ (Order Service) | Отменить заказ |
| 2 | Зарезервировать кредит (Payment Service) | Вернуть кредит |
| 3 | Зарезервировать товар (Warehouse Service) | Снять резерв |
| 4 | Создать доставку (Shipping Service) | Отменить доставку |

### Плюсы саг

- **Консистентность данных без распределённых транзакций.**
- **Отказоустойчивость.** Каждый шаг — локальная транзакция в своём сервисе.

### Минусы саг

- **Сложность компенсаций.** Не все операции обратимы (отправлен email — не отзовёшь).
- **Eventual consistency.** Между шагами данные могут быть несогласованны.
- **Отладка.** Ошибка на шаге 5 — нужно понять, что было на шагах 1–4.

---

## 6. Transactional Outbox

### Проблема

Сервис должен атомарно: **сохранить данные в БД + отправить сообщение в брокер.** Но БД и брокер — разные системы. Без атомарности возможны два сбоя:

1. Данные сохранены, сообщение **НЕ** отправлено → потеря события.
2. Сообщение отправлено, данные **НЕ** сохранены → неконсистентность.

Распределённые транзакции (XA/2PC) — медленно и не поддерживается многими брокерами.

### Решение

Вместо отправки сообщения напрямую — **записать его в таблицу `outbox` в той же транзакции, что и бизнес-данные.** Отдельный процесс (Outbox Publisher) читает outbox-таблицу и отправляет сообщения в брокер.

```
┌─────────────────────────────────────────────────────┐
│                  Service Transaction                 │
│                                                     │
│  ┌─────────────────┐     ┌─────────────────┐        │
│  │  Бизнес-запись   │     │  Outbox запись   │        │
│  │  INSERT INTO     │     │  INSERT INTO     │        │
│  │  orders (...)    │  +  │  outbox (id,     │        │
│  │                  │     │   aggregate_id,  │        │
│  │                  │     │   event_type,    │        │
│  │                  │     │   payload)       │        │
│  └─────────────────┘     └────────┬────────┘        │
│                         │                           │
│                   ┌─────┴─────┐                     │
│                   │   COMMIT   │                     │
│                   └─────┬─────┘                     │
└─────────────────────────┼───────────────────────────┘
                          │
               ┌──────────┴──────────┐
               │  Outbox Publisher    │  ← Отдельный процесс/поток
               │  (Polling / CDC)     │
               └──────────┬──────────┘
                          │
                    ┌─────┴─────┐
                    │   Kafka   │
                    │ RabbitMQ  │
                    └───────────┘
```

### Варианты чтения outbox

| Способ | Описание | Инструменты |
|--------|----------|-------------|
| **Polling Publisher** | Периодический `SELECT ... FOR UPDATE SKIP LOCKED` по таблице outbox | Простая реализация в коде сервиса |
| **Change Data Capture (CDC)** | Чтение WAL БД → трансляция событий в Kafka | Debezium, AWS DMS |
| **Transaction Log Tailing** | Прямое чтение журнала транзакций БД | Debezium, pgoutput (PostgreSQL) |

### Пример: Outbox в Spring (Java + PostgreSQL)

```java
// 1. Бизнес-операция + запись в outbox в одной транзакции
@Service
@Transactional
public class OrderService {

    private final OrderRepository orderRepo;
    private final OutboxRepository outboxRepo;
    private final ObjectMapper mapper;

    public Order createOrder(CreateOrderRequest request) {
        // Бизнес-логика
        Order order = new Order(request.getCustomerId(), request.getItems());
        order = orderRepo.save(order);

        // Запись в outbox — в той же транзакции
        OrderCreatedEvent event = new OrderCreatedEvent(order.getId(), order.getTotal());
        OutboxEntry outbox = new OutboxEntry(
            UUID.randomUUID().toString(),
            "Order",
            order.getId().toString(),
            "OrderCreated",
            mapper.writeValueAsString(event)
        );
        outboxRepo.save(outbox);

        return order;
    }
}

// 2. Outbox Publisher (запускается по расписанию)
@Component
public class OutboxPublisher {
    private final OutboxRepository outboxRepo;
    private final KafkaTemplate<String, String> kafka;

    @Scheduled(fixedDelay = 100) // каждые 100 мс
    @Transactional
    public void publishOutbox() {
        List<OutboxEntry> entries = outboxRepo.findUnpublished(100);
        for (OutboxEntry entry : entries) {
            try {
                kafka.send(entry.getTopic(), entry.getAggregateId(), entry.getPayload()).get();
                entry.markPublished();
                outboxRepo.save(entry);
            } catch (Exception e) {
                log.error("Failed to publish outbox entry {}", entry.getId(), e);
            }
        }
    }
}
```

### Решение через Debezium (CDC)

Без написания Polling Publisher — Debezium читает WAL PostgreSQL и отправляет изменения в Kafka:

```
PostgreSQL WAL → Debezium Connector → Kafka Topic (outbox) → Консьюмеры
```

### Плюсы

- **Гарантированная доставка.** Данные и событие — в одной транзакции.
- **Нет XA/2PC.** Просто и быстро.
- **Переиспользование существующей БД.**

### Минусы

- **Дополнительная нагрузка на БД** (polling).
- **Задержка** между коммитом и отправкой (зависит от polling interval / CDC latency).
- **Ручная очистка outbox таблицы** (published записи нужно удалять).

### Когда использовать

- **Всегда, когда нужно атомарно сохранить данные и отправить событие.**
- Базовая часть микросервисной архитектуры с событийным взаимодействием.
- Часто комбинируется с Inbox Pattern для идемпотентной обработки.

---

## 7. Change Data Capture (CDC)

### Проблема

Нужно синхронизировать данные из БД одного сервиса в другой сервис, поисковый индекс (Elasticsearch), кэш (Redis) или Data Lake — без изменения кода сервиса-источника.

### Решение

**Отслеживать изменения в БД на уровне журнала транзакций (WAL / binlog)** и публиковать их как поток событий.

```
┌──────────┐     WAL/бинлог     ┌──────────────┐     ┌──────────┐
│PostgreSQL│ ─────────────────→ │   Debezium   │ ──→ │  Kafka   │
│  MySQL   │                    │  (Kafka      │     │  Topics  │
│  MongoDB │                    │   Connect)   │     └────┬─────┘
└──────────┘                    └──────────────┘          │
                                              ┌──────────┼──────────┐
                                              │          │          │
                                        ┌─────┴────┐ ┌───┴────┐ ┌───┴────┐
                                        │  Search  │ │ Cache  │ │ Data   │
                                        │  Index   │ │ Update │ │ Lake   │
                                        │(Elastic) │ │(Redis) │ │  (S3)  │
                                        └──────────┘ └────────┘ └────────┘
```

### Инструменты

| Инструмент | Источник БД | Назначение |
|------------|-------------|------------|
| **Debezium** | PostgreSQL, MySQL, MongoDB, MS SQL, Oracle, Db2 | Самый популярный open-source CDC |
| **AWS DMS** | Oracle, MySQL, PostgreSQL, MS SQL, SAP ASE | Миграция + ongoing replication |
| **Oracle GoldenGate** | Oracle (и другие) | Enterprise CDC |
| **Google Cloud Datastream** | MySQL, PostgreSQL, Oracle | CDC в BigQuery, Cloud Storage |
| **pgoutput** (встроенный в PG) | PostgreSQL | Логическая репликация |

### Сценарии

1. **Синхронизация Read DB в CQRS:** CDC → Kafka → обновление Elasticsearch.
2. **Data pipeline:** CDC → Kafka → Stream Processing (Flink) → Data Lake.
3. **Межсервисная синхронизация:** CDC → Kafka → консьюмер в другом сервисе.
4. **Invalidation кэша:** CDC → обновление/сброс Redis.

---

## 8. Domain Event

### Описание

**Domain Event** — событие, которое означает нечто важное, произошедшее в домене. В отличие от системных событий (запись создана), доменное событие отражает бизнес-факт.

```
Системное событие:              Доменное событие:
┌──────────────────────┐        ┌──────────────────────┐
│ RowInsertedEvent     │        │ OrderPlacedEvent     │
│ table=orders         │        │ orderId=123          │
│ id=123               │        │ customerId=456       │
└──────────────────────┘        │ total=150.00 USD     │
                                │ timestamp=...        │
                                └──────────────────────┘
```

### Характеристики

- **Иммутабельно** — событие произошло, его нельзя изменить.
- **Именуется в прошедшем времени** — `OrderPlaced`, `PaymentProcessed`, `ShipmentDelayed`.
- **Содержит всё необходимое** для реакции (или ссылку на агрегат).
- **Часть Ubiquitous Language (DDD)** — термин, понятный бизнесу.

### Связь с другими паттернами

Domain Events — фундамент для: Event Sourcing, Saga (хореография), CQRS (синхронизация), Outbox (публикация).

---

## 9. API Composition

### Проблема

В микросервисной архитектуре данные разбросаны по сервисам. UI нужно показать экран с данными из Orders, Payment, Shipping. JOIN невозможен, потому что данные в разных БД.

### Решение

**API Composer** собирает данные из нескольких сервисов и агрегирует их в один ответ.

```
    GET /order-details/123
            │
    ┌───────┴────────┐
    │  API Composer  │
    └───┬───┬───┬────┘
        │   │   │
   ┌────┘   │   └────┐
   ▼        ▼        ▼
┌──────┐ ┌──────┐ ┌──────┐
│Orders│ │Payment│ │Ship  │
│Svc   │ │Svc   │ │Svc   │
└──────┘ └──────┘ └──────┘

Ответ: {
  "order":    { ... },
  "payment":  { ... },
  "shipping": { ... }
}
```

### Инструменты

| Инструмент | Особенность |
|------------|-------------|
| **GraphQL Federation** | Декларативная композиция типами |
| **Spring Cloud Gateway** + кастомный фильтр | Императивная композиция |
| **Netflix Falcor** | JSON Graph для эффективных запросов |
| **Apache Camel** | Интеграционный фреймворк с композицией |

### Минусы

- Снижение доступности (если один из сервисов упал).
- Увеличение латентности (N последовательных или параллельных вызовов).
- Over-fetching (композер тянет всё, даже если UI нужны не все поля).

---

## 10. Materialized View / CQRS Read Model

### Описание

**Материализованное представление** — денормализованная, оптимизированная под конкретные запросы копия данных. Обновляется асинхронно через события или CDC.

```
События (OrderCreated, PaymentProcessed, Shipped)
        │
        ▼
┌───────────────────────┐
│   Projection Handler   │
│   (Kafka Consumer)     │
└───────────┬───────────┘
            │
            ▼
┌───────────────────────────────────────┐
│          Materialized View             │
│  ┌───────────────────────────────────┐│
│  │ orders_view                       ││
│  │ id │ customer│status│total│pymt   ││  ← все данные из разных
│  │ 1  │ Ivan    │PAID  │ 150 │card   ││     сервисов в одной строке
│  │ 2  │ Maria   │NEW   │ 300 │ NULL  ││
│  └───────────────────────────────────┘│
│         (MongoDB / Elasticsearch)      │
└───────────────────────────────────────┘
```

### Технологии

- **MongoDB** — гибкая схема для денормализованных документов.
- **Elasticsearch** — полнотекстовый поиск + агрегации.
- **Redis** — сверхбыстрые материализованные кэши.
- **ClickHouse** — аналитические материализованные представления.
- **PostgreSQL** — Materialized Views (обновляемые по расписанию).

---

# Часть II. Паттерны обмена сообщениями

---

## 11. Inbox Pattern (Idempotent Consumer)

### Проблема

Брокеры сообщений гарантируют **at-least-once** доставку (Kafka после rebalance, RabbitMQ при ack-таймауте). Консьюмер может получить одно и то же сообщение дважды. Повторная обработка должна быть безопасной.

### Решение

**Консьюмер хранит ID обработанных сообщений** в таблице `inbox`. Перед обработкой проверяет — если ID уже есть, пропускает.

```
Сообщение приходит
        │
        ▼
┌──────────────────┐
│ SELECT FROM inbox │
│ WHERE msg_id = ?  │
└───────┬──────────┘
        │
   ┌────┴────┐
   │ Найдено? │
   └────┬────┘
    Да  │  Нет
    │   │
    ▼   ▼
  SKIP  INSERT INTO inbox (msg_id, processed_at)
        │
        ▼
  Бизнес-обработка
        │
        ▼
  COMMIT (inbox + бизнес-данные)
```

### Пример: Idempotent Consumer (Java + Kafka + PostgreSQL)

```java
@KafkaListener(topics = "orders")
@Transactional
public void onOrderEvent(ConsumerRecord<String, OrderPlacedEvent> record) {
    String messageId = record.key(); // или header с UUID

    // Идемпотентность через inbox-таблицу
    boolean alreadyProcessed = inboxRepo.existsById(messageId);
    if (alreadyProcessed) {
        log.info("Duplicate message {}, skipping", messageId);
        return;
    }

    // Обработка + запись в inbox в одной транзакции
    inboxRepo.save(new InboxEntry(messageId, Instant.now()));
    // бизнес-логика...
}
```

### Альтернативы

- **Дедупликация на уровне БД:** уникальный индекс `(messageId)`. При вставке — `ON CONFLICT DO NOTHING`.
- **Идемпотентная бизнес-логика:** операция, которую можно выполнить повторно без побочных эффектов. Но это сложно («отправить email» — не идемпотентно).
- **Kafka Exactly-Once Semantics:** через транзакции Kafka Streams. Требует использования Kafka Streams API.

### Связка Outbox + Inbox

```
Service A                    Service B
┌──────────┐                ┌──────────┐
│ Outbox   │───→ Kafka ──→  │  Inbox   │
│ (гарант. │                │ (идемпот.│
│  отправка)│                │  приём)  │
└──────────┘                └──────────┘
```

Это даёт **exactly-once** семантику на уровне бизнес-операций: гарантированная отправка + идемпотентная обработка.

---

## 67. Idempotency Key

### Проблема

Сетевые сбои и retry-логика приводят к дублированию запросов. Клиент отправил `POST /payments`, не дождался ответа (таймаут) и повторил. Сервер обработал оба — **двойное списание**. Inbox Pattern решает проблему на уровне сообщений брокера, но как быть с HTTP/gRPC вызовами?

### Решение

**Idempotency Key** — клиент генерирует уникальный ключ (UUID) и передаёт его в заголовке запроса. Сервер сохраняет ключ вместе с результатом обработки. При повторном запросе с тем же ключом — возвращает сохранённый результат без повторной бизнес-обработки.

```
Client                              Server
  │                                     │
  │──1. POST /payments ────────────────→│
  │   Idempotency-Key: abc-123          │
  │                                     │ 2. Проверить: ключ abc-123 уже есть?
  │                                     │    → Нет
  │                                     │ 3. Обработать платёж
  │                                     │ 4. Сохранить (ключ + результат) в БД
  │←──5. 201 Created + результат ───────│
  │                                     │
  │   ... сетевой таймаут, клиент       │
  │   не получил ответ и повторяет ...  │
  │                                     │
  │──6. POST /payments ────────────────→│
  │   Idempotency-Key: abc-123          │
  │                                     │ 7. Проверить: ключ abc-123 уже есть?
  │                                     │    → Да!
  │←──8. 200 OK + сохранённый результат─│  Возвращаем кэшированный ответ
```

### Реализация

```java
@PostMapping("/payments")
public ResponseEntity<PaymentResponse> createPayment(
        @RequestHeader("Idempotency-Key") String idempotencyKey,
        @RequestBody PaymentRequest request) {

    // Проверяем, не обрабатывали ли уже этот ключ
    Optional<IdempotencyRecord> existing = idempotencyRepo.findById(idempotencyKey);
    if (existing.isPresent()) {
        return ResponseEntity.ok(existing.get().getResponse());
    }

    // Бизнес-обработка
    PaymentResponse response = paymentService.process(request);

    // Сохраняем ключ + результат (в одной транзакции с бизнес-данными)
    idempotencyRepo.save(new IdempotencyRecord(
        idempotencyKey, response, Instant.now()
    ));

    return ResponseEntity.status(201).body(response);
}
```

### Хранение ключей и TTL

- **Таблица `idempotency_keys`** в той же БД, что и бизнес-данные (атомарность транзакции).
- **Redis** — для высоконагруженных систем, но требует компенсации при потере ключа.
- **TTL** — 24–48 часов. После истечения ключ можно удалять (повторный запрос через 2 дня — допустимый риск).

### Связь с другими паттернами

- **Inbox Pattern (#11):** решает ту же проблему для сообщений брокера. Idempotency Key — для синхронных запросов.
- **Retry (#28):** Retry БЕЗ Idempotency Key опасен для неидемпотентных операций.

---

## 12. Publish-Subscribe

### Описание

Продюсер публикует сообщение в **топик/канал**, все подписанные консьюмеры получают копию. Продюсер не знает, кто потребит сообщение.

```
              ┌─────────────────┐
Producer ───→ │  Topic: orders   │ ─┬─→ Consumer A (Payment Service)
              └─────────────────┘  │
                                   ├─→ Consumer B (Notification Service)
                                   └─→ Consumer C (Analytics Service)
```

### Инструменты

| Брокер | Модель | Семантика |
|--------|--------|-----------|
| **Kafka** | Распределённый лог | Каждый консьюмер со своим offset; replay возможен |
| **RabbitMQ** | Очереди с fanout exchange | Сообщение — копия в каждую подписанную очередь |
| **Google Pub/Sub** | Управляемый сервис | Push + pull подписки |
| **AWS SNS + SQS** | SNS — pub, SQS — sub (с durability) | SNS → SQS для гарантированной обработки |

### Когда использовать

- **Оповещение нескольких сервисов об одном событии.**
- **Слабая связь между сервисами.**
- **Event-Driven Architecture.**

---

## 13. Competing Consumers

### Описание

Несколько экземпляров консьюмера читают из одной очереди. Сообщение доставляется только одному консьюмеру. Это позволяет горизонтально масштабировать обработку.

```
             ┌──────────────┐
Producer ──→ │  Queue/Topic  │ ─┬─→ Consumer Instance 1
             │  (partition)  │  ├─→ Consumer Instance 2
             └──────────────┘  └─→ Consumer Instance 3
```

### Реализация

- **RabbitMQ:** несколько консьюмеров на одной очереди (round-robin).
- **Kafka:** несколько консьюмеров в одной consumer group — каждый получает свои партиции.

---

## 14. Claim Check

### Проблема

Сообщение содержит большой payload (файл, изображение, массив данных). Передавать его через брокер дорого — брокер не рассчитан на гигабайтные сообщения.

### Решение

**Сохранить большой payload во внешнее хранилище, в сообщении передать только ссылку (claim check).** Консьюмер загружает payload по ссылке.

```
Producer → [Сохранить файл в S3] → Сообщение { claimCheck: "s3://bucket/file-123" } → Consumer → [Загрузить из S3]
```

### Хранилища

AWS S3, GCP Cloud Storage, Azure Blob Storage, MinIO (on-premise).

---

## 15. Content-Based Router

### Описание

Сообщение направляется в разные очереди/обработчики в зависимости от его содержимого.

```
                    ┌─────────────────┐
                    │ Content-Based   │
Сообщение {      ──→│    Router       │──→ type=ORDER → Order Queue
  type: "ORDER",    │                 │──→ type=PAYMENT → Payment Queue
  data: {...}       └─────────────────┘──→ type=REFUND → Refund Queue
}
```

### Инструменты

- **Apache Camel** — встроенные Content-Based Router.
- **Kafka Streams** — `branch()` метод для маршрутизации.
- **Spring Integration** — `<router/>` в DSL.

---

## 16. Message Filter

### Описание

Пропускать только сообщения, удовлетворяющие условию. Остальные отбрасываются (или направляются в discard channel).

```
Сообщения ──→ [Message Filter] ──→ Только подходящие ──→ Обработчик
                   │
                   └──→ Discard (неподходящие) → DLQ / игнор
```

---

## 17. Recipient List

### Описание

Сообщение направляется списку получателей — каждый получает копию. В отличие от Pub-Sub, список получателей определяется динамически (например, из заголовков сообщения).

```
Сообщение { recipients: ["A", "B"] } ──→ [Recipient List Router] ─┬─→ Service A
                                                                  └─→ Service B
```

---

## 18. Scatter-Gather

### Описание

Запрос рассылается нескольким обработчикам (scatter), их ответы агрегируются (gather). Полезно для параллельных запросов к нескольким сервисам.

```
                  ┌──────────┐
Запрос ──→ Scatter│→ Service A │──→ Ответ A
                  │→ Service B │──→ Ответ B  ──→ Gather ──→ Агрегированный
                  │→ Service C │──→ Ответ C               ответ
                  └──────────┘
```

### Инструменты

Spring Integration, Apache Camel, Netflix Conductor.

---

## 19. Routing Slip

### Описание

Маршрут обработки закодирован в самом сообщении. Каждый обработчик выполняет свой шаг и передаёт сообщение следующему по списку.

```
Сообщение { routingSlip: ["Validate", "Enrich", "Store"] }
    │
    ▼
Validate ──→ Enrich ──→ Store
```

### Отличие от Routing Table

- **Routing Slip:** маршрут в сообщении (гибкость на уровне сообщения).
- **Routing Table:** маршрут в конфигурации брокера (централизованное управление).

---

## 20. Priority Queue

### Описание

Сообщения обрабатываются в порядке приоритета. Высокоприоритетные сообщения обслуживаются раньше.

### Реализация

- **RabbitMQ:** `x-max-priority` аргумент очереди + `priority` в свойствах сообщения.
- **Kafka:** несколько топиков с разным приоритетом; consumer сначала читает high-priority, потом low-priority.
- **AWS SQS:** нет нативной поддержки приоритетов; обходной путь — несколько очередей.

### Когда использовать

- **Платежи vs уведомления** — платёж важнее, должно обрабатываться первым.
- **SLA с разными уровнями обслуживания.**

---

## 21. Dead Letter Queue (DLQ)

### Описание

Сообщения, которые не удалось обработать (после N попыток), перемещаются в отдельную очередь — Dead Letter Queue. Оттуда их можно изучить, исправить причину и переотправить.

```
Основная очередь          Dead Letter Queue
┌──────────────┐          ┌──────────────┐
│ Сообщения    │          │ Failed Msgs  │
│              │  после   │              │
│   ✘ ✘ ✘     │  N retry │   ✘ ✘ ✘     │
│              │ ───────→ │              │
└──────────────┘          └──────┬───────┘
                                 │
                          ┌──────┴───────┐
                          │  Аналитика    │
                          │  / Ручное     │
                          │  переигрывание│
                          └──────────────┘
```

### Реализация

- **RabbitMQ:** `x-dead-letter-exchange` на очереди.
- **Kafka:** отдельный топик для failed messages.
- **AWS SQS:** Redrive Policy + DLQ.

---

## 68. Backpressure

### Проблема

Быстрый продюсер генерирует данные быстрее, чем консьюмер успевает обрабатывать. Без механизма обратной связи консьюмер накапливает сообщения в памяти → **OutOfMemoryError** → падение. Это каскадный отказ: упавший консьюмер перестаёт ack-ать → брокер ребалансирует → другие консьюмеры получают ещё больше нагрузки.

### Решение

**Backpressure** — механизм, при котором консьюмер сигнализирует продюсеру замедлиться. Продюсер адаптирует скорость отправки под возможности самого медленного консьюмера.

```
Без Backpressure:                  С Backpressure:
Producer →→→→→→→→ Consumer         Producer →→→ Consumer
                  (падает)                        ← request(5)
                                                  → 5 элементов
                                                  ← request(2)
                                                  → 2 элемента
                                           Producer ждёт, пока
                                           Consumer не запросит ещё
```

### Варианты реализации

| Уровень | Механизм | Инструменты |
|--------|----------|-------------|
| **Прикладной (Reactive Streams)** | Спецификация Reactive Streams: `Publisher.subscribe(Subscriber)`; Subscriber запрашивает N элементов через `request(n)` | Project Reactor, RxJava, Akka Streams, Kotlin Flow, WebFlux |
| **Сетевой (TCP)** | TCP flow control: receive window; если буфер получателя заполнен → окно = 0 → отправитель останавливается | Встроено в TCP |
| **Брокер (Kafka)** | `pause()` / `resume()` consumer; poll только когда есть capacity | Kafka Consumer API |
| **RPC (gRPC)** | HTTP/2 flow control на уровне stream | Встроено в gRPC |
| **RSocket** | Нативный backpressure на уровне протокола | RSocket (Java, Kotlin, Go) |

### Пример: Reactive Backpressure (Project Reactor)

```java
Flux.range(1, 1_000_000)              // Продюсер: миллион элементов
    .onBackpressureBuffer(1000)        // Буфер на 1000; при переполнении — ошибка
    .flatMap(i -> reactiveDb.save(i)) // Консьюмер: медленная запись в БД
    .subscribe();
```

### Связь с другими паттернами

- **Bulkhead (#30):** изолирует ресурсы консьюмера, но не решает проблему переполнения. Backpressure + Bulkhead вместе — надёжная защита.
- **Rate Limiting (#31):** ограничивает продюсера, но статически. Backpressure — динамически, под возможности консьюмера.
- **Circuit Breaker (#27):** разрывает цепь при накоплении ошибок, но не предотвращает OOM. Backpressure предотвращает.

### Когда использовать

- **Потоковая обработка** (Kafka Streams, Flink).
- **Реактивные системы** на WebFlux / Project Reactor.
- **Ingestion pipeline** (продюсеров много, консьюмер один).

---

# Часть III. Паттерны Service Discovery

> В микросервисной архитектуре инстансы сервисов динамичны: появляются, умирают, масштабируются.  
> Service Discovery отвечает на вопрос: «Как сервису A узнать, где находится экземпляр сервиса B *прямо сейчас*?»

---

## 22. Service Registry

### Описание

**Service Registry** — база данных всех доступных экземпляров сервисов и их сетевых адресов. Сервисы регистрируются при старте и удаляются при остановке.

```
┌──────────────────────────────┐
│       Service Registry        │
│  ┌──────────────────────────┐ │
│  │ Service  │ Hosts         │ │
│  │ Orders   │ 10.0.1.5:8080 │ │
│  │          │ 10.0.1.6:8080 │ │
│  │ Payment  │ 10.0.2.1:8081 │ │
│  │ Catalog  │ 10.0.3.1:8082 │ │
│  │          │ 10.0.3.2:8082 │ │
│  └──────────────────────────┘ │
└──────────────────────────────┘
```

### Инструменты

| Инструмент | Тип | CAP | Особенности |
|------------|-----|-----|-------------|
| **Consul** | Service Mesh + Registry | CP | Health checks, KV store, multi-DC |
| **Eureka** (Netflix) | Registry | AP | Клиентский discovery, самозащита |
| **ZooKeeper** | Coordination | CP | Строгий порядок, старый, тяжеловесный |
| **etcd** | Coordination | CP | Используется в Kubernetes |
| **Kubernetes DNS (CoreDNS)** | Встроенный в K8s | — | Service + DNS-based discovery |
| **AWS Cloud Map** | Управляемый сервис | — | Интеграция с ECS, EKS |

---

## 23. Self-Registration

### Описание

Сервис сам регистрируется в Service Registry при старте и сам удаляется при остановке.

```
Старт: Service Instance ──→ POST /register { name: "orders", host: "10.0.1.5:8080" } ──→ Service Registry
Стоп:  Service Instance ──→ DELETE /deregister { name: "orders", host: "10.0.1.5:8080" } ──→ Service Registry
Health: Service Instance ──→ PUT /heartbeat (периодически) ──→ Service Registry
```

### Инструменты

Spring Cloud Netflix Eureka Client, Consul Agent, Netflix OSS.

---

## 24. Third-Party Registration

### Описание

Регистрацию выполняет не сам сервис, а сторонний компонент — оркестратор, sidecar или service mesh control plane.

```
Kubernetes:
  Pod запускается → Kubelet → регистрирует в CoreDNS (через Service)

Consul Connect / Istio:
  Sidecar прокси регистрирует сервис в реестре
```

---

## 25. Client-Side Discovery

### Описание

**Клиент сам опрашивает Service Registry**, выбирает экземпляр (часто с балансировкой) и делает запрос.

```
┌──────────┐   1. Где Payment?   ┌──────────────┐
│  Client  │ ──────────────────→ │   Service     │
│ (Orders) │ ←────────────────── │   Registry    │
└────┬─────┘   2. 10.0.2.1:8081  └──────────────┘
     │
     │ 3. HTTP GET /payments
     ▼
┌──────────┐
│ Payment  │
│ 10.0.2.1 │
└──────────┘
```

### Инструменты

Netflix Eureka + Ribbon (устарел, заменён на Spring Cloud LoadBalancer).

### Плюсы

- Простота — клиент сам решает.
- Меньше движущихся частей (нет промежуточного балансировщика).

### Минусы

- Клиент должен знать о Service Registry.
- Логика выбора реализуется в каждом клиенте (или библиотеке).

---

## 26. Server-Side Discovery

### Описание

Клиент делает запрос через **балансировщик (Load Balancer)**, который сам опрашивает Service Registry и направляет запрос к доступному экземпляру.

```
┌──────────┐  1. GET /payments   ┌──────────────┐
│  Client  │ ───────────────────→│     Load      │
│ (Orders) │ ←───────────────────│   Balancer    │
└──────────┘  4. response         └──────┬───────┘
                                   2. Query│
                                 ┌─────────┴───────┐
                                 │ Service Registry │
                                 └─────────┬───────┘
                                     3. 10.0.2.1│
                                          ┌─────┴──────┐
                                          │  Payment    │
                                          └────────────┘
```

### Инструменты

AWS ELB/ALB/NLB, Kubernetes Service + kube-proxy, Traefik, Envoy.

### Плюсы

- Клиенту не нужно знать о Service Registry (просто вызывает LB).
- Балансировка централизована — конфигурация в одном месте.

### Минусы

- LB — дополнительный hop и потенциальная точка отказа.
- Немного больше задержки.

---

# Часть IV. Паттерны отказоустойчивости (Resilience)

> Распределённые системы ломаются. Не «если», а «когда».  
> Сеть откажет, сервис перегрузится, БД уйдёт в таймаут.  
> Resilience-паттерны — это стратегии выживания в таком мире.

---

## 27. Circuit Breaker

### Проблема

Сервис A вызывает Сервис B. Если B начинает тормозить, A ждёт. Потоки A зависают. Новые запросы приходят, создаются новые потоки — и A тоже падает. **Каскадный отказ.**

### Решение

**Circuit Breaker** отслеживает успешность вызовов. При превышении порога ошибок — **разрывает цепь**: последующие вызовы немедленно возвращают ошибку, не дожидаясь таймаута. Через время — **half-open**: пробный запрос для проверки восстановления.

```
Состояния Circuit Breaker:

  ┌──────────┐    errors > threshold    ┌──────────┐
  │  CLOSED  │ ────────────────────────→│   OPEN   │
  │ (норма)  │                          │ (блок)   │
  └──────────┘                          └────┬─────┘
       ▲                                     │
       │                               timeout (sleepWindow)
       │                                     │
       │          ┌──────────┐               │
       └──────────┤ HALF-OPEN │←─────────────┘
                  │ (пробный) │
                  └────┬─────┘
                       │
                  success│ failure
                       │     │
                       │     └──→ обратно в OPEN
                       │
                       └──→ CLOSED (восстановлен)
```

### Параметры

| Параметр | Описание | Типичное значение |
|----------|----------|:-----------------:|
| **Failure threshold** | Сколько ошибок до разрыва | 50% за 5 сек |
| **Sleep window** | Сколько ждать до half-open | 10–30 сек |
| **Sliding window** | Окно подсчёта ошибок | 10–100 вызовов |
| **Half-open calls** | Сколько пробных запросов | 1–3 |

### Пример: Resilience4j (Java)

```java
// Конфигурация
CircuitBreakerConfig config = CircuitBreakerConfig.custom()
    .failureRateThreshold(50)                         // 50% ошибок → OPEN
    .slidingWindowSize(10)                            // окно в 10 вызовов
    .waitDurationInOpenState(Duration.ofSeconds(10))  // ждать 10 сек до HALF-OPEN
    .permittedNumberOfCallsInHalfOpenState(3)         // 3 пробных запроса
    .recordExceptions(IOException.class, TimeoutException.class)
    .build();

CircuitBreaker circuitBreaker = CircuitBreaker.of("paymentService", config);

// Использование
Supplier<PaymentResponse> decorated = CircuitBreaker
    .decorateSupplier(circuitBreaker, () -> paymentClient.process(paymentRequest));

try {
    PaymentResponse response = decorated.get();
} catch (CallNotPermittedException e) {
    // Circuit is OPEN — сразу возвращаем fallback
    return fallbackResponse();
}
```

### Инструменты

| Инструмент | Платформа | Особенности |
|------------|-----------|-------------|
| **Resilience4j** | Java | Circuit Breaker, Retry, Bulkhead, RateLimiter, Timeout |
| **Polly** | .NET | Circuit Breaker, Retry, Timeout, Bulkhead, Cache |
| **Hystrix** (deprecated) | Java | Перешёл в maintenance mode |
| **Istio** | Service Mesh | Circuit Breaking через DestinationRule |
| **Envoy** | Proxy | Circuit Breaking через cluster config |
| **Sentinel** (Alibaba) | Java | Flow control, Circuit Breaking, адаптивен |

---

## 28. Retry

### Проблема

Временный сбой (блоб сетевого соединения, мерцание БД) не должен ронять операцию.

### Решение

Повторять операцию при transient-ошибках (`IOException`, `SocketTimeoutException`, HTTP 503).

### Стратегии

| Стратегия | Описание | Пример |
|-----------|----------|--------|
| **Fixed** | Повтор через фиксированный интервал | 1 сек × 3 |
| **Exponential Backoff** | Интервал растёт экспоненциально | 1 сек, 2 сек, 4 сек, 8 сек |
| **Exponential + Jitter** | Backoff + случайный разброс (избегает thundering herd) | 1.2 сек, 2.7 сек, 5.1 сек |
| **Fibonacci** | Интервал как числа Фибоначчи | 1, 1, 2, 3, 5, 8 сек |

### Пример: Exponential Backoff + Jitter

```java
RetryConfig config = RetryConfig.custom()
    .maxAttempts(3)
    .intervalFunction(IntervalFunction.ofExponentialRandomBackoff(
        Duration.ofSeconds(1),  // начальный интервал
        2.0,                     // множитель
        Duration.ofSeconds(10)   // максимальный интервал
    ))
    .retryOnException(e -> e instanceof TransientException)
    .build();

Retry retry = Retry.of("paymentRetry", config);

Supplier<PaymentResponse> decorated = Retry
    .decorateSupplier(retry, () -> paymentClient.process(paymentRequest));

PaymentResponse response = decorated.get();
```

### Что НЕ надо ретраить

- **400 Bad Request** — проблема не на сервере, а в запросе.
- **Долгоиграющие операции без идемпотентности** — повтор создаст дубликат.
- **Критические операции без компенсации.**

### Ретраи и Dual-Writes

Повтор неидемпотентной операции опасен. Если `POST /payments` создаёт новый платёж без ключа идемпотентности, retry создаст дубликат. Решение: **Idempotency Key** в заголовке.

```
POST /payments
Idempotency-Key: 6f9a3b2e-...
```

---

## 29. Timeout

### Проблема

Бесконечное ожидание ответа от удалённого сервиса — убийца потоков и ресурсов. Если Сервис B завис, Сервис A тоже зависнет (поток заблокирован навсегда).

### Решение

**Каждый удалённый вызов должен иметь таймаут.** При превышении — исключение + retry/fallback.

### Типы таймаутов

| Тип | Где настраивается | Пример |
|-----|-------------------|--------|
| **Connection timeout** | HTTP Client | 1–5 сек |
| **Read/Socket timeout** | HTTP Client | 5–30 сек |
| **Request timeout** | Прикладной уровень | Общий лимит на операцию |

### Рекомендации

- Таймаут должен быть **меньше, чем готов ждать пользователь**.
- **Connection timeout < Read timeout < Request timeout.**
- Использовать **Deadlines** в gRPC (передаётся от клиента к серверу).

### Инструменты

| Инструмент | Подход |
|------------|--------|
| **RestTemplate** (Spring) | `setConnectTimeout()`, `setReadTimeout()` |
| **WebClient** (Spring WebFlux) | `.timeout(Duration.ofSeconds(5))` |
| **HttpClient** (Java 11+) | `HttpClient.newBuilder().connectTimeout(Duration.ofSeconds(3))` |
| **gRPC** | `withDeadline(Deadline.after(5, SECONDS))` |

---

## 30. Bulkhead

### Проблема

Пул потоков общий для всех вызовов. Медленный downstream-сервис съедает все потоки — и остальные запросы не могут быть обработаны.

### Решение

**Разделить ресурсы на изолированные пулы.** Как отсеки на корабле (bulkheads): пробоина в одном не топит весь корабль.

```
Без Bulkhead:                     С Bulkhead:
┌──────────────────────┐          ┌──────────┐ ┌──────────┐ ┌──────────┐
│  Thread Pool (200)   │          │ Payment  │ │ Catalog  │ │ Notify   │
│  • Payment calls     │          │ Pool (50)│ │ Pool (50)│ │ Pool(50)│
│  • Catalog calls     │          └──────────┘ └──────────┘ └──────────┘
│  • Notification calls│          Даже если Payment забьёт свои 50 потоков,
└──────────────────────┘          Catalog и Notification продолжают работать.
```

### Два типа Bulkhead

| Тип | Что изолирует | Инструменты |
|-----|---------------|-------------|
| **Thread Pool** | Потоки | Resilience4j, Hystrix (deprecated) |
| **Semaphore** | Количество одновременных вызовов (накладные расходы меньше) | Resilience4j |

### Пример: Resilience4j Bulkhead

```java
ThreadPoolBulkheadConfig config = ThreadPoolBulkheadConfig.custom()
    .maxThreadPoolSize(20)    // максимум потоков для этого пула
    .coreThreadPoolSize(5)    // минимум
    .queueCapacity(50)        // максимум в очереди
    .build();

ThreadPoolBulkhead bulkhead = ThreadPoolBulkhead.of("paymentPool", config);

Supplier<PaymentResponse> decorated = ThreadPoolBulkhead
    .decorateSupplier(bulkhead, () -> paymentClient.process(paymentRequest));

try {
    PaymentResponse response = decorated.get();
} catch (BulkheadFullException e) {
    // Пул переполнен — возвращаем 429 Too Many Requests
}
```

---

## 31. Rate Limiting / Throttling

### Проблема

Downstream-сервис не должен быть перегружен слишком большим количеством запросов. Клиент должен ограничивать частоту вызовов.

### Решение

Ограничить количество запросов в единицу времени (rate limit) или количество одновременных запросов (concurrency limit).

### Алгоритмы

| Алгоритм | Принцип | Инструменты |
|----------|---------|-------------|
| **Token Bucket** | Выдаются токены с фиксированной скоростью; запрос без токена отклоняется | Resilience4j, Guava RateLimiter |
| **Leaky Bucket** | Запросы кладутся в очередь; обрабатываются с фиксированной скоростью | Traffic Shaping в Nginx |
| **Fixed Window** | Счётчик в пределах временного окна (1 мин) | Простейшая реализация |
| **Sliding Window Log** | Список временных меток; точный, но memory-heavy | Redis Sorted Set |
| **Sliding Window Counter** | Гибрид: окно + счётчик (приближённо) | Kong, Envoy |

### Где применять

- **API Gateway:** глобальный rate limiting (Kong, APISIX, Ambassador).
- **Клиент сервиса:** защита downstream (Resilience4j RateLimiter).
- **Kubernetes Ingress:** ограничение на уровне Ingress Controller (Nginx, Traefik).

### Пример: Token Bucket (Resilience4j)

```java
RateLimiterConfig config = RateLimiterConfig.custom()
    .limitRefreshPeriod(Duration.ofSeconds(1))   // обновление раз в секунду
    .limitForPeriod(10)                           // 10 токенов за период = 10 RPS
    .timeoutDuration(Duration.ofMillis(100))      // ждать до 100 мс
    .build();

RateLimiter rateLimiter = RateLimiter.of("paymentRateLimiter", config);

Supplier<PaymentResponse> decorated = RateLimiter
    .decorateSupplier(rateLimiter, () -> paymentClient.process(paymentRequest));

try {
    PaymentResponse response = decorated.get();
} catch (RequestNotPermitted e) {
    throw new TooManyRequestsException("Rate limit exceeded");
}
```

---

## 32. Fallback / Graceful Degradation

### Проблема

Сервис недоступен, но пользователь должен получить хоть какой-то ответ (пусть и урезанный).

### Решение

При ошибке вернуть **заранее заготовленный ответ** — кэшированные данные, дефолтные значения, заглушку.

### Типы fallback

| Тип | Описание | Пример |
|-----|----------|--------|
| **Статический fallback** | Фиксированный ответ | Рекомендации = пустой список |
| **Кэшированный fallback** | Последние успешные данные из кэша | Каталог из Redis при падении Catalog Service |
| **Деградированный ответ** | Частичные данные | Заказ без данных о доставке (Shipping Service упал) |
| **Stubbed ответ** | Технический ответ для non-critical функциональности | Реклама = пустой баннер |

### Пример: Cache Fallback + Circuit Breaker

```java
Supplier<ProductPage> productPageSupplier = () -> catalogClient.getProductPage(productId);

Supplier<ProductPage> decorated = Decorators.ofSupplier(productPageSupplier)
    .withCircuitBreaker(circuitBreaker)
    .withFallback(asList(
        TimeoutException.class, CallNotPermittedException.class
    ), throwable -> cacheRepository.getProductPage(productId)) // fallback to cache
    .decorate();

ProductPage page = decorated.get();
```

---

## 33. Health Check API

### Проблема

Балансировщику или оркестратору нужно знать, жив ли сервис, чтобы не отправлять трафик на мёртвый экземпляр.

### Решение

Сервис предоставляет `/health` endpoint, возвращающий статус. Различают:

- **Liveness** (`/health/liveness`) — «жив ли процесс?» (если нет → перезапуск).
- **Readiness** (`/health/readiness`) — «готов ли принимать запросы?» (если нет → исключить из балансировки).
- **Health** (`/health`) — общий статус = liveness + readiness.

### Пример: Spring Boot Actuator

```yaml
# application.yml
management:
  endpoints:
    web:
      exposure:
        include: health,info,metrics,prometheus
  health:
    livenessState:
      enabled: true
    readinessState:
      enabled: true
  endpoint:
    health:
      probes:
        enabled: true
```

```json
// GET /actuator/health
{
  "status": "UP",
  "components": {
    "livenessState": { "status": "UP" },
    "readinessState": { "status": "ACCEPTING_TRAFFIC" },
    "db": { "status": "UP", "details": { "database": "PostgreSQL", "validationQuery": "isValid()" } },
    "redis": { "status": "UP" },
    "kafka": { "status": "UP" }
  }
}
```

### Уровни эндпоинтов

```
/health           → общий статус (Liveness AND Readiness = UP)
/health/liveness  → процесс жив? крэш → k8s перезапустит под
/health/readiness → готов принимать трафик? нет → k8s исключит из сервиса
/health/{component} → статус конкретной зависимости (db, redis, kafka)
```

### Интеграции

- **Kubernetes:** liveness/readiness probes → Spring Boot Actuator.
- **AWS ELB:** target group health checks → `/health`.
- **Consul:** health check → `/health`.

---

## 34. Cache-Aside

### Описание

Приложение управляет кэшем само: при запросе сначала проверяется кэш, при промахе — загрузка из БД и сохранение в кэш.

```
         ┌──────────────────────┐
Запрос ──→│ 1. Проверить кэш     │
         │ 2. Промах? Загрузить │
         │    из БД              │
         │ 3. Сохранить в кэш    │
         │ 4. Вернуть результат  │
         └──────────────────────┘
```

### Инструменты

Redis, Memcached, Hazelcast, Caffeine (in-process).

### Паттерны инвалидации

| Паттерн | Стратегия | Когда |
|---------|-----------|------|
| **TTL** | Данные живут N секунд | Простая стратегия, eventual consistency |
| **Write-through** | При записи в БД сразу обновить кэш | Сильная консистентность, но медленная запись |
| **Write-behind** | При записи в БД асинхронно обновить кэш | Быстрая запись, eventual consistency |
| **Active Invalidation** | Сервис явно сбрасывает кэш при изменении данных | Точечная инвалидация через CDC/события |

---

# Часть V. Коммуникационные паттерны

---

## 35. API Gateway

### Проблема

В микросервисной архитектуре клиент сталкивается с N сервисов. Разные протоколы, авторизация, rate limiting, трансформация форматов. Клиент не должен знать топологию системы.

### Решение

**API Gateway** — единая точка входа для внешних клиентов. Маршрутизирует запросы к сервисам, выполняет кросс-каттинг задачи (аутентификация, rate limiting, логирование, SSL termination).

```
                    ┌─────────────────────────────────┐
                    │           API Gateway             │
                    │  ┌─────────────────────────────┐ │
Mobile App ────────→│  │ Auth │ Rate Limit │ Router  │ │──→ Order Service
Web SPA ───────────→│  │ Log  │ Transform  │ Cache   │ │──→ Payment Service
Partner API ───────→│  │ CORS │ Circuit Brk│Metrics │ │──→ Catalog Service
                    │  └─────────────────────────────┘ │
                    └─────────────────────────────────┘
```

### Инструменты

| Инструмент | Тип | Особенности |
|------------|-----|-------------|
| **Kong** | Open Source | Плагины (Lua), высокая производительность, декларативная конфигурация |
| **APISIX** | Open Source | Плагины (Lua/Go/Wasm), динамическое управление, etcd |
| **Spring Cloud Gateway** | Java/Spring | Интеграция со Spring-эосистемой, программируемые фильтры |
| **Traefik** | Open Source | Автообнаружение в Docker/K8s, Let's Encrypt |
| **AWS API Gateway** | Управляемый | Полная интеграция с AWS-эосистемой |
| **Azure API Management** | Управляемый | XML-политики, Developer Portal |
| **Apigee** (Google) | Управляемый | Enterprise, аналитика |
| **Envoy** | Proxy/Data Plane | Service Mesh, API Gateway через Gateway API |

### Плюсы

- **Единая точка** аутентификации, rate limiting, мониторинга.
- **Скрытие внутренней топологии** от клиентов.
- **Protocol translation** (REST → gRPC, внешний REST → внутренний gRPC).

### Минусы

- **Единая точка отказа** (решается кластеризацией).
- **Узкое горло** при неправильной настройке.
- **Риск «божественного шлюза»** — слишком много логики в Gateway.

---

## 36. Backend for Frontend (BFF)

### Проблема

Разные клиенты (мобильное приложение, веб-SPA, партнёрский API) имеют разные потребности: разный набор данных, разная форма ответа, разная granularity запросов. Один API Gateway не может эффективно обслуживать всех.

### Решение

**Отдельный бэкенд для каждого типа клиента.** Каждый BFF агрегирует данные из микросервисов и адаптирует ответ под конкретный UI.

```
                         ┌──────────────────┐
                         │   API Gateway     │
                         └───┬──────┬──────┬─┘
                             │      │      │
                    ┌────────┘      │      └────────┐
                    ▼               ▼               ▼
            ┌────────────┐ ┌────────────┐ ┌────────────┐
            │  Mobile BFF│ │  Web BFF   │ │Partner BFF │
            │  (Node.js) │ │  (Kotlin)  │ │  (Go)      │
            └──┬──┬──┬───┘ └──┬──┬──┬───┘ └──┬──┬──┬───┘
               │  │  │        │  │  │        │  │  │
               ▼  ▼  ▼        ▼  ▼  ▼        ▼  ▼  ▼
            ┌──────┐ ┌──────┐ ┌──────┐ ┌──────────┐
            │Orders│ │Paymt │ │Catalog│ │Recommend │
            └──────┘ └──────┘ └──────┘ └──────────┘
```

### Отличие от API Gateway

| API Gateway | BFF |
|-------------|-----|
| Единая точка входа для всех | Отдельная точка для каждого клиента |
| Routing + кросс-каттинг | Агрегация + адаптация данных под UI |
| Конфигурация (декларативная/скриптовая) | Код (императивный) |
| Не содержит бизнес-логики | Может содержать логику, специфичную для UI |

### Когда использовать

- **Разные потребности клиентов** (mobile — минимум данных, web — полные).
- **Разные протоколы** (mobile — GraphQL, web — REST, partner — gRPC).
- **Разные команды** для разных клиентов.

### Инструменты

- **GraphQL Federation** — BFF как шлюз GraphQL с резолвингом по типам.
- **Node.js + Express/Fastify** — лёгкий BFF.
- **Spring Boot** — если вся команда на Java/Kotlin.

---

## 69. API Versioning

### Проблема

API меняется: добавляются/удаляются поля, меняется структура ответа, меняется семантика эндпоинтов. Клиенты обновляются не мгновенно (мобильные приложения — недели, партнёрские интеграции — месяцы). Изменение API без версионирования ломает клиенты.

### Решение

**Явное версионирование API** — каждая версия API имеет свой идентификатор. Старые версии поддерживаются в течение периода устаревания (deprecation window), давая клиентам время на миграцию.

### Стратегии версионирования

| Стратегия | Пример | Плюсы | Минусы |
|-----------|--------|-------|--------|
| **URI Path** | `/api/v1/orders`, `/api/v2/orders` | Явно, кэшируется, видно в логах | Раздувание URL, нарушает HATEOAS |
| **HTTP Header** | `Accept: application/vnd.company.orders.v2+json` | Чистые URL, контент-негосиация | Сложнее тестировать (curl), менее заметно |
| **Query Parameter** | `/api/orders?version=2` | Простота | Путаница с бизнес-параметрами, слабое кэширование |
| **Domain** | `v2.api.company.com/orders` | Разные кластеры под версии | DNS-усложнение, не масштабируется на много версий |

### Рекомендация

**URI Path** — самый популярный и практичный выбор для REST API. Прост в реализации, виден в логах и метриках, легко тестировать. gRPC использует Protobuf-версионирование (field numbers). GraphQL — избегает версионирования (клиент запрашивает только нужные поля).

### Deprecation Policy

```
1. Релиз v2 → v1 помечается как deprecated
2. HTTP заголовок: Sunset: Sat, 01 Jan 2027 00:00:00 GMT
   + Warning: 299 - "v1 is deprecated, migrate to v2"
3. Период поддержки: 3–6 месяцев для внутренних API, 6–12 для публичных
4. Мониторинг: кто ещё ходит на v1 → точечная коммуникация → отключение
```

### Связь с другими паттернами

- **API Gateway (#35):** маршрутизирует `/v1/*` и `/v2/*` на разные сервисы/версии.
- **Consumer-Driven Contracts (#46):** контракты пишутся под конкретную версию API.
- **Backend for Frontend (#36):** BFF адаптирует версию API под UI, скрывая версионирование от фронтенда.
- **Strangler Fig (#40):** версионирование — ключевой механизм постепенной миграции.

### Когда использовать

- **Всегда** для публичных и партнёрских API.
- **Для внутренних микросервисов** — по необходимости (частые изменения контракта).

---

## 37. Sidecar

### Проблема

Кросс-каттинг функциональность (логирование, мониторинг, service discovery, TLS) должна быть реализована в каждом сервисе. Дублирование кода на разных языках, разная реализация, сложность обновления.

### Решение

**Sidecar** — процесс/контейнер, развёрнутый вместе с сервисом (в одном Pod/хосте). Sidecar перехватывает входящий/исходящий трафик и выполняет кросс-каттинг задачи. Сервис не знает о sidecar.

```
┌─────────────────────────────────────┐
│              Pod (K8s)              │
│  ┌──────────┐      ┌──────────────┐ │
│  │  Service │ ←──→ │   Sidecar    │←┼──→ Сеть
│  │(Business)│      │ (Envoy Proxy)│ │
│  └──────────┘      └──────────────┘ │
└─────────────────────────────────────┘
```

### Что делает Sidecar

- **TLS termination / mTLS** — шифрование трафика.
- **Service Discovery** — поиск других сервисов.
- **Retry / Circuit Breaking / Timeout** — resilience на уровне прокси.
- **Metrics / Tracing** — сбор телеметрии.
- **Logging** — перехват логов.

### Инструменты

- **Envoy** — sidecar в Istio.
- **Linkerd-proxy** — легковесный Rust-прокси.
- **Consul Connect** — sidecar с Consul.
- **Dapr** — более высокоуровневый sidecar (state management, pub/sub, bindings).

---

## 38. Ambassador

### Проблема

Сервис должен вызывать внешнюю систему, но внешняя система имеет сложный API, меняется, требует ретраев и аутентификации. Хочется изолировать эту сложность от бизнес-логики.

### Решение

**Ambassador** — sidecar/прокси, специализирующийся на взаимодействии с конкретной внешней системой. Сервис вызывает Ambassador локально (localhost), Ambassador берёт на себя всю сложность.

```
┌────────────────────────────────────────────┐
│                   Host                      │
│  ┌──────────┐    ┌──────────────────────┐   │
│  │ Service  │───→│  Ambassador (proxy)  │───┼──→ Внешняя система
│  │ localhost│    │  • Retry             │   │   (Cloud SQL,
│  │          │    │  • Auth              │   │    Redis,
│  │          │    │  • Connection Pool   │   │    LDAP, etc.)
│  └──────────┘    └──────────────────────┘   │
└────────────────────────────────────────────┘
```

### Примеры

- **Cloud SQL Proxy** (GCP) — Ambassador для Cloud SQL; service обращается через него локально.
- **Envoy** как Ambassador для внешних API.

### Отличие от Sidecar

| Sidecar | Ambassador |
|---------|------------|
| Управляет трафиком **между своими сервисами** (east-west) | Управляет трафиком **к внешним системам** (north-south) |
| Работает с входящим и исходящим трафиком | Чаще только исходящий трафик |
| Общий прокси | Специализированный прокси под конкретную внешнюю систему |

---

## 39. Anti-Corruption Layer

### Проблема

Интеграция с legacy-системой или внешним сервисом, чья модель данных уродлива, не соответствует вашему домену, и будет «заражать» вашу систему.

### Решение

**Anti-Corruption Layer (ACL)** — слой между вашим доменом и внешней системой, который **транслирует** модель внешней системы в вашу модель и обратно.

```
┌─────────────────────────────────────────────────┐
│                Ваша система                       │
│  ┌──────────┐     ┌──────────┐     ┌──────────┐  │
│  │  Domain  │ ←──→│   ACL    │ ←──→│  Legacy  │  │
│  │  Model   │     │          │     │  System  │  │
│  │(чистая)  │     │Translator│     │(грязная) │  │
│  └──────────┘     └──────────┘     └──────────┘  │
└─────────────────────────────────────────────────┘
```

### Функции ACL

1. **Трансляция модели** — внешний `T_CST_MSTR_013` → внутренний `Customer`.
2. **Адаптация протокола** — SOAP → REST, gRPC → AMQP.
3. **Изоляция ошибок** — Circuit Breaker, Retry только в ACL.
4. **Фасад** — предоставление удобного API для домена.

### Пример: ACL для Legacy SOAP-сервиса

```java
// Чистый домен
public interface CustomerRepository {
    Customer findById(CustomerId id);
}

// ACL — реализация, изолирующая грязь
@Repository
public class LegacyCustomerRepository implements CustomerRepository {

    private final LegacySoapClient soapClient;

    @Override
    public Customer findById(CustomerId id) {
        // 1. Адаптация запроса (наш ID → их формат)
        LegacyCustomerRequest request = LegacyMapper.toLegacyRequest(id);

        // 2. Вызов внешней системы (с ретраями)
        LegacyCustomerResponse response = callWithRetry(() ->
            soapClient.getCustomer(request)
        );

        // 3. Трансляция ответа (их модель → наша)
        return LegacyMapper.toDomain(response);
    }
}
```

---

## 40. Strangler Fig

### Проблема

Переписывание монолита на микросервисы целиком — рискованно, долго и дорого.

### Решение

**Постепенное «удушение» монолита.** Новая функциональность пишется в микросервисах. Старая — постепенно переносится. Монолит «усыхает» до полного исчезновения.

```
         Время ────────────────────────────────→

Фаза 1:  [████████████████████████████]  Монолит (100%)
         ┌──────────────────────────┐
         │       API Gateway         │ → всё в монолит
         └──────────────────────────┘

Фаза 2:  [███████████████████░░░░░░░]  Монолит (70%), Микросервисы (30%)
         ┌──────────────────────────┐
         │       API Gateway         │ → маршрутизация по URL
         └────┬──────────────┬──────┘
              │              │
         ┌────┴────┐    ┌────┴────┐
         │ Монолит │    │  Новый   │
         └─────────┘    │ Сервис   │
                        └─────────┘

Фаза 3:  [██████░░░░░░░░░░░░░░░░░░]  Монолит (20%), Микросервисы (80%)

Фаза 4:  [░░░░░░░░░░░░░░░░░░░░░░░░]  Монолит (0%)  — выключен
```

### Стратегии миграции

| Стратегия | Описание | Пример |
|-----------|----------|--------|
| **По URL** | `/api/v1/catalog` → старый, `/api/v2/catalog` → новый | Новый API для каталога |
| **По функциям** | Каждая бизнес-возможность выносится отдельно | Модуль «Склад» → Warehouse Service |
| **По таблицам БД** | Вынос таблиц в отдельную БД с синхронизацией | Таблица `customers` → Customers Service |

### Инструменты

API Gateway (Kong, Spring Cloud Gateway) для маршрутизации; CDC для синхронизации данных при переходном периоде.

---


# Часть VI. Паттерны безопасности

---

## 43. API Gateway Authentication

### Проблема

В микросервисной архитектуре каждый сервис имеет свой API. Если каждый сервис самостоятельно аутентифицирует запросы — дублирование логики, риск несогласованной политики безопасности, сложность аудита.

### Решение

**Аутентификация выносится на API Gateway** — единую точку входа. Gateway проверяет учётные данные, выпускает внутренний токен (JWT) или прокидывает заголовки с идентификатором пользователя. Сервисы внутри периметра **доверяют Gateway** и не аутентифицируют запросы повторно.

### Модель доверенного периметра

```
                        ┌──────────────────────────────┐
                        │      Trusted Perimeter        │
                        │                              │
Client ──→ [Creds] ──→ │  ┌──────────┐    ┌────────┐  │
                        │  │  API GW  │───→│Service │  │
                        │  │ AuthN+Z  │    │  (no   │  │
                        │  └──────────┘    │  auth) │  │
                        │                  └────────┘  │
                        └──────────────────────────────┘
```

За пределами Gateway — непроверенный мир. Внутри — все сервисы доверяют друг другу (или используют mTLS для взаимной аутентификации).

### Flow

1. **Client → Gateway:** credentials (Basic, OAuth2 token, API Key, cookie).
2. **Gateway:** валидирует credentials → извлекает identity (userId, roles).
3. **Gateway → Service:** проксирует запрос с заголовком `X-User-ID`, `X-User-Roles` или внутренним JWT.
4. **Service:** доверяет заголовкам (не проверяет credentials повторно).

### Когда использовать

- Все микросервисные системы — это стандартный паттерн.
- **Не подходит**, если сервисы вызываются напрямую (без Gateway) — тогда нужна аутентификация на каждом сервисе + Service-to-Service токены (см. OAuth 2.0 Client Credentials).

### Связь с другими паттернами

- **OAuth 2.0 / OIDC (#45):** Gateway выступает как Resource Server — валидирует токены.
- **JWT (#44):** Gateway выпускает или прокидывает JWT сервисам.
- **Rate Limiting (#31):** Gateway применяет rate limiting на основе identity.

## 44. Access Token / JWT

### Описание

После аутентификации клиент получает **токен доступа** (чаще JWT). Токен содержит claims (userId, roles, permissions) и подписан сервером авторизации. Сервисы проверяют подпись без запроса к серверу авторизации (stateless).

```json
// JWT Payload
{
  "sub": "user-123",
  "iss": "auth.mycompany.com",
  "iat": 1680000000,
  "exp": 1680003600,
  "roles": ["customer"],
  "permissions": ["order:create", "order:read"]
}
```

### Access Token + Refresh Token

**Access Token** — короткоживущий (5–15 минут). Если украден — окно атаки ограничено.  
**Refresh Token** — долгоживущий (дни/недели). Используется только для получения нового access token без повторного ввода логина/пароля.

```
Client                Auth Server              Resource Server
  │                       │                        │
  │──1. Login + Pass───→│                        │
  │←──2. Access (15min)  │                        │
  │    + Refresh (7d) ──┤                        │
  │                       │                        │
  │──3. GET /orders + Access Token ──────────────→│
  │←──4. 200 OK ──────────────────────────────────│
  │                       │                        │
  │  ... 20 минут спустя ...                      │
  │                       │                        │
  │──5. GET /orders + Access Token ──────────────→│
  │←──6. 401 Expired ─────────────────────────────│
  │                       │                        │
  │──7. Refresh Token ──→│                        │
  │←──8. New Access (15min)                       │
  │    + New Refresh (7d)┤                        │
  │                       │                        │
  │──9. GET /orders + New Access Token ───────────→│
  │←──10. 200 OK ─────────────────────────────────│
```

### Ротация Refresh Token

При каждом обновлении access token **выдаётся новый refresh token**, а старый инвалидируется. Это защищает от replay-атак: если старый refresh token украден и использован злоумышленником — легитимный пользователь при следующем обновлении получит ошибку (его refresh token уже аннулирован) и поймёт, что произошла утечка.

### Token Revocation

Сервер авторизации должен предоставлять `/oauth2/revoke` endpoint для инвалидации токенов (выход из системы, смена пароля, компрометация). Рекомендация: хранить revoked token IDs в быстром хранилище (Redis) с TTL = expiry токена.

### Где хранить токены

| Клиент | Access Token | Refresh Token |
|--------|:-----------:|:------------:|
| **SPA (браузер)** | Память (замыкание) | HttpOnly, Secure, SameSite cookie (BFF) |
| **Мобильное приложение** | Память / Keychain (iOS) / Keystore (Android) | Защищённое хранилище ОС |
| **BFF (сервер)** | Память сессии (Redis) | Память сессии (Redis) |
| **Service-to-Service** | Память + кэш до expiry | Не используется (Client Credentials без refresh) |

### Инструменты

- **Keycloak**, **Auth0**, **Okta**, **AWS Cognito**, **Azure AD**.
- **Nimbus JOSE + JWT**, **jjwt**, **Microsoft.IdentityModel.Tokens** (для валидации).
- **Redis** — хранение revoked tokens / refresh token family.

## 45. OAuth 2.0 / OpenID Connect

### Описание

OAuth 2.0 — протокол **авторизации** (делегирования доступа). OpenID Connect (OIDC) — надстройка над OAuth 2.0 для **аутентификации**.

### Потоки (Grant Types)

| Flow | Когда | Пример |
|------|-------|--------|
| **Authorization Code + PKCE** | SPA, мобильные приложения | React-приложение с Keycloak |
| **Client Credentials** | Service-to-service, нет пользователя | Order Service → Payment Service |
| **Resource Owner Password** | Устарел, не рекомендуется | — |
| **Device Code** | Устройства без браузера | Smart TV, IoT |

### Service-to-Service

```
┌──────────┐  1. Client Credentials   ┌──────────┐
│  Orders  │ ────────────────────────→│   Auth    │
│  Service │ ←────────────────────────│  Server   │
└────┬─────┘  2. Access Token (JWT)   │(Keycloak) │
     │                                └──────────┘
     │ 3. GET /payments + JWT
     ▼
┌──────────┐  4. Validate JWT (public key, local)
│ Payment  │     ← без запроса к Auth Server!
│ Service  │
└──────────┘
```

---

## 46. Consumer-Driven Contracts

### Проблема

При изменении API провайдера ломаются консьюмеры. Тесты провайдера не знают, как именно консьюмеры используют API.

### Решение

**Консьюмеры описывают свои ожидания от API в виде контракта** (спецификации запросов/ответов). Провайдер тестирует свой API на соответствие всем контрактам.

```
┌──────────┐     Контракт       ┌──────────────┐
│ Consumer │ ─────────────────→ │   Pact File   │
│  (Order) │   ожидаю от API... │  (JSON)       │
└──────────┘                    └──────┬───────┘
                                      │
                                      ▼
                               ┌──────────────┐
                               │   Provider    │
                               │   (Payment)   │
                               │               │
                               │ Проверяет API  │
                               │ против Pact   │
                               └──────────────┘
```

### Инструменты

- **Pact** — самый популярный CDC-фреймворк (Java, .NET, JS, Go, Python).
- **Spring Cloud Contract** — контракты на стороне провайдера, stubs генерируются для консьюмеров.

### Пример: Spring Cloud Contract (Groovy)

```groovy
// contract.groovy — на стороне провайдера (Payment Service)
Contract.make {
    description "Should return payment by order ID"
    request {
        method GET()
        url "/api/payments" {
            queryParameters {
                parameter("orderId", "123")
            }
        }
        headers {
            header("Authorization", "Bearer valid_token")
        }
    }
    response {
        status OK()
        headers {
            contentType applicationJson()
        }
        body([
            orderId: "123",
            status: "COMPLETED",
            amount: 150.00
        ])
    }
}
```

---

# Часть VII. Паттерны наблюдаемости (Observability)

---

## 47. Log Aggregation

### Проблема

В распределённой системе логи разбросаны по десяткам/сотням контейнеров. SSH на каждый сервер и `tail -f` не масштабируется.

### Решение

Все логи отправляются в централизованное хранилище. Единый UI для поиска и анализа.

```
Service A ──→ Fluentd/Filebeat ──→ ┌─────────────────┐
Service B ──→ Fluentd/Filebeat ──→│ Elasticsearch    │ ← единое хранилище
Service C ──→ Fluentd/Filebeat ──→│                  │
...                                 │                  │
Service N ──→ Fluentd/Filebeat ──→│      Kibana      │ ← UI для поиска
                                   └─────────────────┘
```

### Стек (ELK / EFK)

| Компонент | Альтернативы |
|-----------|-------------|
| **Collector** | Fluentd, Fluent Bit, Filebeat, Logstash |
| **Storage** | Elasticsearch, OpenSearch, Loki |
| **UI** | Kibana, Grafana (с Loki) |
| **Pipeline** | Kafka (буферизация перед Elasticsearch) |

### Structured Logging

Логи должны быть структурированными (JSON), чтобы их можно было эффективно индексировать и искать.

```json
{
  "timestamp": "2026-07-12T10:30:00.000Z",
  "level": "INFO",
  "service": "order-service",
  "instance": "order-service-7d4f9b8c-x2k5",
  "traceId": "a1b2c3d4e5f6...",
  "spanId": "12345",
  "message": "Order created",
  "orderId": "ord-456",
  "customerId": "cust-789",
  "total": 150.00
}
```

---

## 48. Distributed Tracing

### Проблема

Запрос проходит через 5–10 сервисов. По каждому есть лог, но как связать их в единую картину? Где именно произошла задержка?

### Решение

Каждый входящий запрос получает **Trace ID** (сквозной идентификатор) и генерирует **Span ID** для своих операций. Заголовки передаются между сервисами.

```
Trace: a1b2c3... (весь путь запроса)
  │
  ├── Span: OrderService.createOrder  (50ms)
  │     │
  │     ├── Span: OrderRepo.save       (15ms)
  │     └── Span: PaymentClient.pay    (85ms)
  │           │
  │           └── Span: PaymentService.process (80ms)
  │
  └── Span: NotificationService.send   (95ms)
```

### Стандарты и протоколы

| Стандарт | Описание |
|----------|----------|
| **W3C Trace Context** | HTTP-заголовки `traceparent`, `tracestate` — стандарт W3C |
| **B3** (Zipkin) | Заголовки `X-B3-TraceId`, `X-B3-SpanId` — исторически от Zipkin, де-факто стандарт |
| **Jaeger** (uber-trace-id) | Собственный формат Jaeger |

### Инструменты

| Инструмент | Тип | Хранилище |
|------------|-----|-----------|
| **Jaeger** | Сборщик + UI | Elasticsearch, Cassandra, Badger |
| **Zipkin** | Сборщик + UI | Elasticsearch, MySQL, Cassandra |
| **OpenTelemetry** | Стандарт сбора (SDK + Collector) | Jaeger, Zipkin, Prometheus, любой backend |
| **AWS X-Ray** | Управляемый сервис | Собственное хранилище |
| **Google Cloud Trace** | Управляемый сервис | Собственное хранилище |
| **Grafana Tempo** | Хранилище трейсов | Grafana UI |

### Пример: OpenTelemetry auto-instrumentation (Java)

```bash
# Автоматический трейсинг без изменения кода
java -javaagent:opentelemetry-javaagent.jar \
     -Dotel.service.name=order-service \
     -Dotel.traces.exporter=jaeger \
     -Dotel.metrics.exporter=prometheus \
     -jar order-service.jar
```

---


## 50. Metrics Aggregation

### Проблема

Нужно знать: сколько запросов в секунду, какая латентность (p50, p95, p99), сколько ошибок, utilisation CPU/памяти, размер очередей.

### Решение

Сервисы **экспортируют** метрики; **сборщик** (Prometheus) опрашивает их; **база** (Prometheus TSDB, VictoriaMetrics) хранит; **дашборды** (Grafana) визуализируют.

```
Сервисы → /metrics (Prometheus формат) → Prometheus (scrape) → Grafana (визуализация)
                                                                    │
                                                              ┌─────┴─────┐
                                                              │ AlertManager│ → PagerDuty/Slack
                                                              └────────────┘
```

### Метрики: The Four Golden Signals

| Сигнал | Что измеряет | Пример метрики |
|--------|-------------|---------------|
| **Latency** | Время обработки запроса | `http_request_duration_seconds{p50,p95,p99}` |
| **Traffic** | Объём запросов | `http_requests_total{rate}` |
| **Errors** | Частота ошибок | `http_requests_total{status=~"5.."}` |
| **Saturation** | Насколько система загружена | `jvm_threads_current`, `queue_size`, `cpu_usage` |

### Инструменты

| Компонент | Варианты |
|-----------|----------|
| **Сборщик** | Prometheus, VictoriaMetrics, Datadog Agent |
| **Хранилище** | Prometheus TSDB, VictoriaMetrics, Thanos, Cortex |
| **Визуализация** | Grafana, Datadog, New Relic |
| **Alerting** | AlertManager, Grafana Alerting, PagerDuty |

---

## 51. Correlation ID

### Проблема

Как связать логи от одного клиентского запроса через 10 сервисов?

### Решение

Генерировать **Correlation ID** на входе (API Gateway) и передавать во всех последующих вызовах (HTTP Header `X-Correlation-ID`, gRPC metadata, Kafka header).

```
Client → [X-Correlation-ID: abc-123]
    │
    ▼
API Gateway → генерирует / прокидывает ID
    │
    ▼
Order Service → X-Correlation-ID: abc-123 (логи, исходящие вызовы)
    │
    ▼
Payment Service → X-Correlation-ID: abc-123 (логи)
```

### Реализация (Spring Boot + MDC)

```java
@Component
public class CorrelationIdFilter implements Filter {

    @Override
    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) {
        HttpServletRequest httpReq = (HttpServletRequest) req;
        String correlationId = httpReq.getHeader("X-Correlation-ID");
        if (correlationId == null) {
            correlationId = UUID.randomUUID().toString();
        }
        MDC.put("correlationId", correlationId);
        try {
            chain.doFilter(req, resp);
        } finally {
            MDC.remove("correlationId");
        }
    }
}
```

```xml
<!-- logback.xml — прокинули в логи -->
<pattern>%d %-5level [%thread] %X{correlationId} %logger{36} - %msg%n</pattern>
```

### Отличие от Trace ID

| Correlation ID | Trace ID |
|----------------|----------|
| Идентифицирует запрос на бизнес-уровне | Идентифицирует распределённый трейс |
| Один для всего жизненного цикла (даже через message broker) | Может быть разным для разных частей flow |
| Логи, аудит | Трейсинг, задержки |

---

## 52. Audit Logging

### Проблема

Кто, когда и что изменил? (Комплаенс, безопасность, расследование инцидентов.)

### Решение

Писать audit log — неизменяемый журнал действий пользователей/сервисов. В отличие от обычных логов, audit log фокусируется на «кто сделал что».

```
┌──────────────────────────────────────────────────────┐
│                     Audit Log                         │
│ ┌────────────────────────────────────────────────────┐│
│ │ user   │ action         │ resource  │ timestamp    ││
│ │────────┼────────────────┼───────────┼──────────────││
│ │ivanov  │ ORDER.CREATE   │ ord-123   │ 2026-07-12.. ││
│ │petrov  │ ORDER.APPROVE  │ ord-123   │ 2026-07-12.. ││
│ │sidorov │ PAYMENT.REFUND │ paym-456  │ 2026-07-12.. ││
│ └────────────────────────────────────────────────────┘│
└──────────────────────────────────────────────────────┘
```

### Технологии

- **Event Sourcing** — естественная модель аудита (каждое изменение — событие).
- **Audit-таблицы в БД** — для монолитов и небольших систем.
- **Kafka + Elasticsearch** — масштабируемый аудит для микросервисов.
- **AWS CloudTrail** — аудит API-вызовов AWS.

---

# Часть VIII. Паттерны деплоя и поставки

---

## 53. Blue-Green Deployment

### Проблема

Деплой новой версии с остановкой старой вызывает downtime. Если новая версия багованная — откат долгий и мучительный.

### Решение

Два идентичных окружения: **Blue** (текущее) и **Green** (новое). Трафик переключается с Blue на Green мгновенно. Если проблемы — переключение обратно.

```
Шаг 1:                     Шаг 2:                    Шаг 3 (откат):
┌──────┐                  ┌──────┐                  ┌──────┐
│ Blue │← 100% трафика    │ Blue │ (idle)           │ Blue │← 100% трафика
│ v1.0 │                  │ v1.0 │                  │ v1.0 │
└──────┘                  └──────┘                  └──────┘
┌──────┐                  ┌──────┐                  ┌──────┐
│ Green│ (deploying)      │ Green│← 100% трафика    │ Green│ (idle)
│ v2.0 │                  │ v2.0 │                  │ v2.0 │
└──────┘                  └──────┘                  └──────┘
   Deploy                    Switch                  Rollback
```

### Требования

- Два набора ресурсов (вдвое больше инфраструктуры на время деплоя).
- БД должна поддерживать одновременную работу двух версий (миграции — backward compatible).

### Инструменты

- **Kubernetes:** два Deployment + один Service → переключение selector'а.
- **AWS Elastic Beanstalk:** встроенная Blue/Green.
- **Traefik / Nginx:** переключение upstream.
- **Cloud Foundry:** `cf map-route`.

### Плюсы

- **Нулевой downtime.**
- **Мгновенный откат** (просто переключить трафик обратно).
- **Возможность тестирования Green до переключения** (smoke tests).

### Минусы

- **Дороже** (двойная инфраструктура).
- **Сложные миграции БД** (совместимость старой и новой версии).

---

## 54. Canary Release

### Проблема

Обновить все экземпляры сразу — риск. Если баг, затронет всех пользователей.

### Решение

Новая версия деплоится на небольшой процент экземпляров, получает малую долю трафика. Если метрики в норме — доля увеличивается поэтапно.

```
Шаг 1:  v2.0 = 5%  [▓▓░░░░░░░░░░░░░░░░░░]  v1.0 = 95%
Шаг 2:  v2.0 = 25% [▓▓▓▓▓▓▓░░░░░░░░░░░░░]  v1.0 = 75%
Шаг 3:  v2.0 = 50% [▓▓▓▓▓▓▓▓▓▓▓▓▓░░░░░░░]  v1.0 = 50%
Шаг 4:  v2.0 = 100%[▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓]  v1.0 = 0%

Если на любом шаге ошибка → откат к v1.0 = 100%.
```

### Инструменты

| Инструмент | Механизм |
|------------|----------|
| **Kubernetes + Service Mesh (Istio/Linkerd)** | Weighted routing (VirtualService) |
| **AWS App Mesh** | Weighted routing |
| **Nginx Ingress** | Canary annotations |
| **Argo Rollouts** | Kubernetes-native Canary |
| **Flagger** | Автоматизированный Canary (Prometheus + Istio) |
| **Spinnaker** | Canary pipeline с Kayenta для анализа метрик |

### Пример: Istio VirtualService (Canary)

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: order-service
spec:
  hosts:
    - order-service
  http:
    - route:
        - destination:
            host: order-service
            subset: v1
          weight: 90      # 90% трафика на старую версию
        - destination:
            host: order-service
            subset: v2
          weight: 10      # 10% на новую
```

---

## 55. Feature Toggle / Feature Flag

### Проблема

Новая фича готова, но релизить целиком страшно. Хочется включить её для 1% пользователей или для внутреннего тестирования.

### Решение

**Feature Toggle** — флаг, управляющий видимостью функциональности. Может включаться для конкретных пользователей, групп, процента трафика.

```java
// Пример с LaunchDarkly
if (featureFlagService.isEnabled("new-checkout-flow", user)) {
    return newCheckoutService.process(order);  // Новый flow
} else {
    return legacyCheckoutService.process(order);  // Старый flow
}
```

### Типы Feature Toggles

| Тип | Жизненный цикл | Пример |
|-----|---------------|--------|
| **Release Toggle** | Короткий (до полного rollout) | Новый UI, бета-версия функциональности |
| **Experiment Toggle** | Средний (A/B тест) | Сравнение конверсии старого и нового flow |
| **Ops Toggle** | Длинный (инфраструктурный) | Переключение между БД/брокерами на лету |
| **Permission Toggle** | Постоянный | Premium-функции для платящих пользователей |

### Инструменты

| Инструмент | Хостинг | Особенности |
|------------|---------|-------------|
| **LaunchDarkly** | SaaS | Real-time стриминг, эксперименты, segment-based |
| **Flagsmith** | SaaS / Open Source | Self-hosted опция |
| **Unleash** | Open Source | Self-hosted, активационные стратегии |
| **CloudBees Feature Management** | SaaS | Enterprise |
| **Config file / DB** | Self-hosted | Просто, но без стриминга изменений |

### Плюсы

- **Деплой ≠ Релиз.** Код в проде, но выключен — безопасно.
- **A/B тесты.**
- **Kill switch.** Мгновенно отключить проблемную фичу.
- **Trunk-based development** — все в main, фичи за флагами.

### Минусы

- **Сложность тестирования** — N² комбинаций флагов.
- **Технический долг** — забытые флаги.
- **Зависимость от внешнего сервиса** (LaunchDarkly, Unleash).

---

## 56. Rolling Deployment

### Описание

Экземпляры обновляются последовательно: один за другим или группами. В каждый момент времени часть экземпляров обслуживает трафик.

```
Экземпляры: [A, B, C, D]

Шаг 1: A=новый, B=старый, C=старый, D=старый
Шаг 2: A=новый, B=новый,  C=старый, D=старый
Шаг 3: A=новый, B=новый,  C=новый,  D=старый
Шаг 4: A=новый, B=новый,  C=новый,  D=новый
```

### Инструменты

- **Kubernetes:** `spec.strategy.type: RollingUpdate` (стандартный деплой).
- **Docker Swarm:** rolling update.

### Плюсы

- **Без downtime.**
- **Постепенная нагрузка** на новую версию.

### Минусы

- **Медленнее, чем Blue-Green.**
- **Версии смешаны** — backward compatibility обязательна.

---

## 57. Shadow Deployment / Dark Launch

### Описание

Новая версия получает **копию реального трафика** (теневой трафик). Ответы новой версии не возвращаются пользователю — только анализируются для сравнения.

```
              ┌──────────────┐
Traffic ─────→│   Router     │──→ v1.0 (production) ──→ пользователю
              │              │──→ v2.0 (shadow)      ──→ аналитика / сравнение
              └──────────────┘
```

### Инструменты

- **Istio:** `mirror` в VirtualService.
- **Envoy:** Request Mirroring.
- **GoReplay:** перехват и повтор HTTP-трафика.

### Когда использовать

- **Миграция на новый стек** (старый = production, новый = shadow, сравниваем результаты).
- **Нагрузочное тестирование** в production-условиях без влияния на пользователей.

---

## 58. Service Template

### Проблема

Создание нового микросервиса с нуля требует много boilerplate: CI/CD pipeline, мониторинг, логирование, health checks, конфигурация Docker, Kubernetes манифесты.

### Решение

**Service Template** (архетип, cookiecutter) — шаблон проекта, из которого команда генерирует новый сервис за минуты. Включает пред настроенные: build tool, Dockerfile, Helm chart, Actuator, Resilience4j, OpenTelemetry, тесты.

### Инструменты

- **JHipster** — генератор Spring Boot + Microservices.
- **Maven Archetypes** — шаблоны проектов Maven.
- **Cookiecutter** (Python) — универсальный шаблонизатор.
- **Backstage** (Spotify) — Software Catalog + Software Templates.
- **Yeoman** — генератор проектов (JS-экосистема).

---

## 59. Externalized Configuration

### Проблема

Конфигурация, вшитая в jar/образ, требует пересборки при изменении. В микросервисах конфигурация должна меняться на лету.

### Решение

Конфигурация хранится вне сервиса — в Config Server, Git, Vault, Consul KV. Сервис загружает её при старте и может обновлять без рестарта (через `/actuator/refresh` или Spring Cloud Bus).

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│  Git Repo    │────→│ Config Server│────→│ Order Service│
│ (config.yml) │     │  (Spring     │     │              │
│              │     │   Cloud      │     │              │
│              │     │   Config)    │     │              │
└──────────────┘     └──────────────┘     └──────────────┘
```

### Инструменты

| Инструмент | Тип | Особенности |
|------------|-----|-------------|
| **Spring Cloud Config** | Config Server | Git/Vault/JDBC backend |
| **HashiCorp Consul** | KV Store + Service Discovery | Плюс health checks |
| **HashiCorp Vault** | Secrets Management | Шифрование, динамические секреты |
| **Kubernetes ConfigMap/Secret** | Встроенный в K8s | Монтирование как volumes/env vars |
| **AWS Systems Manager Parameter Store** | Управляемый | Простые параметры |
| **AWS AppConfig** | Управляемый | Feature flags + валидация |

---

## 60. Single Service per Host / Multiple Services per Host

### Описание

**Single Service per Host** — один экземпляр сервиса на физической машине/виртуалке. Типично для Kubernetes (один контейнер — один Pod).
**Multiple Services per Host** — несколько сервисов на одной машине. Типично для pre-K8s эпохи.

| Модель | Плюсы | Минусы |
|--------|-------|--------|
| **Single per Host** | Изоляция, независимое масштабирование, безопасность | Дороже (больше ресурсов на overhead) |
| **Multiple per Host** | Экономия ресурсов | Конфликты портов/зависимостей, сложность изоляции |

---

# Часть IX. Инфраструктурные и оркестрационные паттерны

---

## 61. Service Mesh

### Проблема

С ростом числа микросервисов растёт сложность сетевого взаимодействия. Каждый сервис должен реализовывать: retry, circuit breaking, mTLS, traffic splitting, observability. Дублирование в каждом языке/фреймворке — дорого.

### Решение

**Service Mesh** — инфраструктурный слой, управляющий сетевым взаимодействием. Выносит network-логику из кода сервиса во внешний прокси (sidecar).

```
┌──────────────────────────────────────────────────┐
│                   Control Plane                    │
│               (Istiod / Consul Server)             │
│         Конфигурация, политики, сертификаты        │
└──────┬───────────────────────┬──────────────────┬─┘
       │                       │                  │
┌──────┴───────────────────────┴──────────────────┴─────┐
│                      Data Plane                         │
│                                                        │
│  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐   │
│  │ Service │  │ Service │  │ Service │  │ Service │   │
│  │   A     │  │   B     │  │   C     │  │   D     │   │
│  ├─────────┤  ├─────────┤  ├─────────┤  ├─────────┤   │
│  │  Proxy  │←→│  Proxy  │←→│  Proxy  │←→│  Proxy  │   │
│  │ (Envoy) │  │ (Envoy) │  │ (Envoy) │  │ (Envoy) │   │
│  └─────────┘  └─────────┘  └─────────┘  └─────────┘   │
└───────────────────────────────────────────────────────┘
```

### Инструменты

| Service Mesh | Control Plane | Data Plane | Особенности |
|--------------|--------------|------------|-------------|
| **Istio** | Istiod | Envoy | Самый функциональный; сложный |
| **Linkerd** | Linkerd Controller | linkerd2-proxy (Rust) | Легковесный; проще Istio |
| **Consul Connect** | Consul Server | Envoy / built-in proxy | Интеграция с Consul Service Discovery |
| **AWS App Mesh** | Управляемый | Envoy | Управляемый сервис AWS |
| **Kuma** | Kuma Control Plane | Envoy | CNCF; multi-mesh |
| **Cilium** | Cilium Agent | eBPF (без sidecar!) | Kernel-level; производительность |

### Возможности Service Mesh

- **mTLS** — автоматическое взаимное TLS между сервисами.
- **Traffic Routing** — weight-based routing, canary deployments.
- **Resilience** — timeout, retry, circuit breaking на уровне прокси.
- **Observability** — метрики, трейсы, логи трафика.
- **Fault Injection** — тестирование отказоустойчивости (искусственные задержки/ошибки).

### Sidecar-less (eBPF / ambient mesh)

Новое поколение: Cilium (eBPF), Istio Ambient Mesh (ztunnel + waypoint proxy). Не требуют sidecar на каждый под — меньше overhead.

---

## 70. Leader Election

### Проблема

В распределённой системе часто нужно, чтобы **только один экземпляр** выполнял задачу: singleton scheduler (ночной отчёт), обработка партиции Kafka (ровно один consumer на партицию), запись в общий ресурс без конфликтов. Без лидера — либо дублирование работы, либо задача не выполняется вообще.

### Решение

**Leader Election** — алгоритм, выбирающий один экземпляр-лидер из группы равноправных узлов. Если лидер падает — автоматически избирается новый. Остальные узлы ждут (standby).

```
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Instance │  │ Instance │  │ Instance │
│    A     │  │    B     │  │    C     │
│ (Leader) │  │(Standby) │  │(Standby) │
│   ★      │  │          │  │          │
└────┬─────┘  └──────────┘  └──────────┘
     │
     │  Выполняет задачу
     ▼
  ┌──────────┐
  │ Scheduled │
  │   Task    │
  └──────────┘

Если A падает:
┌──────────┐  ┌──────────┐  ┌──────────┐
│ Instance │  │ Instance │  │ Instance │
│    A     │  │    B     │  │    C     │
│ (упал)   │  │ (Leader) │  │(Standby) │
└──────────┘  └────┬─────┘  └──────────┘
                   │ ★
                   ▼
              ┌──────────┐
              │ Scheduled │
              │   Task    │
              └──────────┘
```

### Механизмы выбора

| Механизм | Принцип | Инструменты |
|----------|---------|-------------|
| **Lease** | Узлы борются за lease (аренду) с TTL; лидер продлевает lease периодически. Если не продлил → lease истекает → другой узел захватывает | Kubernetes Lease, etcd, Consul Session |
| **Consensus (Raft/Paxos)** | Кластер выбирает лидера через консенсус | etcd (Raft), Consul (Raft) |
| **ZooKeeper Ephemeral Node** | Узлы создают эфемерный znode; узел с наименьшим sequential номером = лидер | Apache ZooKeeper |
| **Database Lock** | `SELECT ... FOR UPDATE` на таблице `leader_lock` | PostgreSQL Advisory Lock |

### Пример: Kubernetes Lease (Java)

```java
// Spring Boot + Kubernetes Client — Leader Election через Lease
@Service
public class ScheduledTaskLeaderElection {
    private final LeaderElector elector;

    public ScheduledTaskLeaderElection(KubernetesClient client) {
        this.elector = client.leaderElector()
            .withConfig(new LeaderElectionConfig(
                "tasks-lease",           // имя Lease
                "30s",                    // Lease Duration
                "10s",                    // Renew Deadline
                "2s",                     // Retry Period
                () -> log.info("I am the leader now"),
                () -> log.info("I am no longer the leader"),
                () -> "instance-" + hostname
            ))
            .build();
    }

    @Scheduled(fixedDelay = 60_000)
    public void doScheduledWork() {
        if (elector.isLeader()) {
            // Только лидер выполняет задачу
            generateNightlyReport();
        }
    }
}
```

### Инструменты

| Инструмент | Тип | Особенности |
|------------|-----|-------------|
| **Kubernetes Lease** | Встроенный в K8s | Не требует внешних зависимостей |
| **etcd** | Распределённое KV-хранилище | Raft-консенсус, высокая надёжность |
| **HashiCorp Consul** | Service Discovery + KV | Session + Lock |
| **Apache ZooKeeper** | Координационный сервис | Ephemeral Sequential znodes |
| **Apache Curator** | Библиотека поверх ZK | `LeaderLatch`, `LeaderSelector` |
| **ShedLock** (Spring) | Таблица в БД | Простейший вариант: `shedlock` table + `@SchedulerLock` |

### Плюсы

- **Исключение дублирования.** Задача выполняется ровно один раз.
- **Автоматическое восстановление.** Падение лидера → избрание нового.
- **Стандартный механизм** в Kubernetes (Lease) — не нужно ставить ZK/etcd.

### Минусы

- **Задержка при смене лидера** — lease TTL определяет, как быстро обнаружат падение.
- **Split-brain** при некорректной настройке lease timeout.
- **Дополнительная сложность** (нужен доступ к K8s API / etcd / ZK).

### Когда использовать

- **Singleton scheduler в микросервисах.**
- **Обработка партиции Kafka** (решено Consumer Group, но Leader Election для координации).
- **Запись в общий ресурс без конфликтов.**
- **Активный/пассивный failover для stateful сервисов.**

---

## 62. Choreography vs Orchestration (глубокое сравнение)

Подробно расписано в разделе Saga. Дополнительное сравнение:

| Характеристика | Хореография | Оркестрация |
|----------------|:-----------:|:-----------:|
| **Где логика** | Распределена по сервисам | Централизована в оркестраторе |
| **Видимость flow** | Сложно отследить | Явная (в оркестраторе) |
| **Связанность** | Очень низкая | Средняя (сервисы знают оркестратора) |
| **Single point of failure** | Нет | Оркестратор (решается HA) |
| **Добавление шагов** | Подписаться на событие | Изменить оркестратор |
| **Тестирование** | Сложное (много сервисов) | Среднее (оркестратор изолирован) |
| **Инструменты** | Kafka, RabbitMQ | Camunda, Temporal, Axon |

### Когда что выбирать

- **Хореография:** простые линейные процессы (Order → Payment → Notification), высокие требования к автономии команд.
- **Оркестрация:** сложные branching процессы (заявка на кредит: проверка → scoring → андеррайтинг → одобрение/отказ), требования к видимости flow для бизнеса.

---

## 63. Transactional Outbox + Inbox (связка)

### Описание

Комбинация Outbox и Inbox даёт **гарантированную exactly-once доставку** на бизнес-уровне:

1. **Outbox** гарантирует, что событие БУДЕТ отправлено (атомарно с бизнес-данными).
2. **Inbox** гарантирует, что событие НЕ обработается дважды.

```
Service A                              Service B
┌───────────────────┐                 ┌───────────────────┐
│ 1. BEGIN TX       │                 │ 3. Receive event  │
│ 2. INSERT order   │                 │ 4. SELECT inbox   │
│ 3. INSERT outbox  │  ──→ Kafka ──→  │    (is duplicate?)│
│ 4. COMMIT         │                 │ 5. INSERT inbox   │
│                   │                 │ 6. Process event  │
│ OutboxPublisher:  │                 │ 7. COMMIT         │
│ Poll outbox →     │                 │                   │
│   Send to Kafka → │                 │                   │
└───────────────────┘                 └───────────────────┘
```

### Реализация в Spring

Используется **Debezium** для Outbox (без кода) + **уникальный индекс на message_id** для Inbox (без таблицы inbox — просто `ON CONFLICT DO NOTHING`).

---

## 64. Event Collaboration

### Описание

Сервисы обмениваются событиями для поддержания копий данных друг друга в локальных БД. Каждый сервис хранит денормализованные копии нужных ему данных из других сервисов.

```
┌──────────┐  OrderCreated  ┌──────────┐
│  Orders  │ ──────────────→│ Payment  │
│  Service │                │ Service  │
│  ┌─────┐ │                │  ┌─────┐ │
│  │orders│ │                │  │pymts │ │
│  └─────┘ │                │  │ +    │ │
│          │                │  │copy  │ │
│          │                │  │orders│ │ ← локальная копия данных заказа
│          │                │  └─────┘ │
└──────────┘                └──────────┘
```

Это позволяет Payment Service обрабатывать платежи без синхронного вызова Order Service.

---

## 65. Process Manager

### Описание

**Process Manager** — более сложная версия Saga Orchestrator. В отличие от Saga (которая управляет компенсациями), Process Manager может:
- **Ждать несколько событий** перед переходом.
- **Принимать решения** на основе состояния.
- **Длиться дни/недели** (долгоиграющие процессы).

### Пример: Процесс одобрения кредита

```java
// Temporal Workflow (Java SDK)
@WorkflowInterface
public interface LoanApprovalWorkflow {

    @WorkflowMethod
    LoanDecision processLoan(LoanApplication app);
}

public class LoanApprovalWorkflowImpl implements LoanApprovalWorkflow {

    private final ActivityStub activities = Workflow.newActivityStub(Activities.class);
    private LoanDecision decision = new LoanDecision();

    @Override
    public LoanDecision processLoan(LoanApplication app) {
        // Шаг 1: Проверка заявителя (может занять часы)
        BackgroundCheckResult check = activities.checkBackground(app);

        // Шаг 2: Скоринг
        int score = activities.calculateScore(app, check);

        // Шаг 3: Если требуется, ручное одобрение (ждёт дни)
        if (score < 700 && score > 500) {
            boolean approved = activities.manualApproval(app);
            decision.setManualReview(true);
        }

        // Шаг 4: Финальное решение
        decision.setApproved(score >= 700);
        return decision;
    }
}
```

### Инструменты

- **Temporal** — Workflow as Code (Go, Java, TypeScript, Python).
- **Camunda / Zeebe** — BPMN-движок.
- **AWS Step Functions** — управляемый.
- **Netflix Conductor** — микросервисная оркестрация.

---

## Карта совместного использования паттернов

Типичные комбинации в реальных проектах:

```
Микросервисы + Event-Driven Архитектура
├── Database per Service                    (изоляция данных)
├── Transactional Outbox + Inbox            (гарантированная доставка)
├── Saga (Choreography или Orchestration)   (распределённые транзакции)
├── CQRS + Materialized View                (разделение read/write)
│   └── CDC (Debezium)                      (синхронизация моделей)
├── API Gateway + BFF                       (входная точка)
├── Service Discovery (Client/Server-Side)  (динамическое обнаружение)
├── Circuit Breaker + Retry + Timeout       (resilience)
│   └── Bulkhead                            (изоляция ресурсов)
├── Sidecar (Service Mesh: Istio/Linkerd)   (сетевой слой)
├── Health Check + Metrics + Tracing        (observability)
│   ├── Correlation ID                     (связывание логов)
│   └── Audit Logging                      (комплаенс)
├── Feature Toggle                          (безопасные релизы)
├── Canary/Blue-Green/Rolling               (стратегии деплоя)
├── Externalized Configuration              (Config Server / Vault)
├── Consumer-Driven Contracts               (Pact / Spring Cloud Contract)
└── Service Template                        (стандартизация сервисов)
```

---

## Заключение: как выбирать паттерны

### Дерево решений (упрощённое)

```
1. Какая архитектура?
   ├── Монолит → Shared Database, Cache-Aside, Health Check, Feature Toggle
   │
   └── Микросервисы →
       │
       2. Как сервисы общаются?
          ├── Синхронно → API Gateway, BFF, Service Discovery,
          │               Circuit Breaker, Retry, Timeout, Bulkhead
          │
          └── Асинхронно → Pub-Sub, Outbox + Inbox, Domain Events,
                           Choreography Saga, CDC, Claim Check
          │
          3. Как управлять данными?
             ├── Один сервис — одна БД → Database per Service
             ├── Сложные чтения → CQRS + Materialized View
             ├── Нужен полный аудит → Event Sourcing
             └── Межсервисная консистентность → Saga
             │
             4. Как деплоить?
                ├── Нулевой downtime → Blue-Green
                ├── Постепенное обновление → Rolling
                ├── Минимизация риска → Canary
                └── Безопасность фич → Feature Toggle

5. Как наблюдать?
   └── Log Aggregation + Distributed Tracing + Metrics + Health Checks
       + Correlation ID
```

### Эволюция сложности

```
Стартап → Монолит + Shared DB + Cache-Aside
        → Модульный монолит + Outbox
        → Микросервисы + Database per Service + API Gateway + Saga
        → CQRS + Event Sourcing (только для hot paths)
        → Service Mesh (когда сервисов > 20–30)
```

Большинство проектов останавливается на уровне микросервисов с Outbox + Saga + API Gateway — и это достаточно для 90% случаев.