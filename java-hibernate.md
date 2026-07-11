# Вопросы по Hibernate / JPA (с ответами)

## Оглавление

- [1. JPA и Hibernate — основы](#1-jpa-и-hibernate--основы)
  - [1.1. Что такое JPA и чем он отличается от Hibernate?](#11-что-такое-jpa-и-чем-он-отличается-от-hibernate)
  - [1.2. Архитектура Hibernate](#12-архитектура-hibernate)
  - [1.3. Session vs EntityManager](#13-session-vs-entitymanager)
- [2. EntityManager, EntityManagerFactory и Persistence Context](#2-entitymanager-entitymanagerfactory-и-persistence-context)
  - [2.1. Как работает EntityManagerFactory?](#21-как-работает-entitymanagerfactory)
  - [2.2. Как работает Persistence Context (L1-кэш)?](#22-как-работает-persistence-context-l1-кэш)
  - [2.3. Как @PersistenceContext внедряет EntityManager в Spring?](#23-как-persistencecontext-внедряет-entitymanager-в-spring)
  - [2.4. EntityManagerFactory vs SessionFactory](#24-entitymanagerfactory-vs-sessionfactory)
- [3. Состояния сущностей и операции](#3-состояния-сущностей-и-операции)
  - [3.1. Состояния сущностей (жизненный цикл)](#31-состояния-сущностей-жизненный-цикл)
  - [3.2. persist() vs merge() vs save() vs update()](#32-persist-vs-merge-vs-save-vs-update)
  - [3.3. flush() — как и когда?](#33-flush--как-и-когда)
  - [3.4. clear(), detach(), refresh(), contains()](#34-clear-detach-refresh-contains)
  - [3.5. find() vs getReference()](#35-find-vs-getreference)
  - [3.6. remove()](#36-remove)
- [4. Маппинг сущностей](#4-маппинг-сущностей)
  - [4.1. @Entity и @Table](#41-entity-и-table)
  - [4.2. @Id и стратегии генерации (@GeneratedValue)](#42-id-и-стратегии-генерации-generatedvalue)
  - [4.3. @Column](#43-column)
  - [4.4. @Transient, @Formula, @Enumerated, @Lob](#44-transient-formula-enumerated-lob)
- [5. Маппинг связей (@OneToOne, @ManyToOne, @OneToMany, @ManyToMany)](#5-маппинг-связей-onetoone-manytoone-onetomany-manytomany)
  - [5.1. @ManyToOne и @OneToMany](#51-manytoone-и-onetomany)
  - [5.2. @OneToOne](#52-onetoone)
  - [5.3. @ManyToMany](#53-manytomany)
  - [5.4. FetchType: LAZY vs EAGER](#54-fetchtype-lazy-vs-eager)
- [6. Cascade, orphanRemoval и владение связью](#6-cascade-orphanremoval-и-владение-связью)
  - [6.1. Cascade-типы](#61-cascade-типы)
  - [6.2. orphanRemoval = true](#62-orphanremoval--true)
  - [6.3. mappedBy и владение связью](#63-mappedby-и-владение-связью)
- [7. Fetch-стратегии и проблема N+1](#7-fetch-стратегии-и-проблема-n1)
  - [7.1. Проблема N+1](#71-проблема-n1)
  - [7.2. Решения проблемы N+1](#72-решения-проблемы-n1)
  - [7.3. JOIN FETCH vs EntityGraph](#73-join-fetch-vs-entitygraph)
  - [7.4. @NamedEntityGraph](#74-namedentitygraph)
  - [7.5. @Fetch (Hibernate) — стратегии загрузки](#75-fetch-hibernate--стратегии-загрузки)
  - [7.6. @BatchSize (Hibernate)](#76-batchsize-hibernate)
  - [7.7. @LazyToOne, @LazyCollection (Hibernate)](#77-lazytoone-lazycollection-hibernate)
- [8. Dirty Checking (отслеживание изменений)](#8-dirty-checking-отслеживание-изменений)
  - [8.1. Как работает Dirty Checking?](#81-как-работает-dirty-checking)
  - [8.2. Стратегии сравнения](#82-стратегии-сравнения)
  - [8.3. Оптимизация Dirty Checking](#83-оптимизация-dirty-checking)
- [9. Прокси и ленивая загрузка](#9-прокси-и-ленивая-загрузка)
  - [9.1. Как Hibernate создаёт прокси?](#91-как-hibernate-создаёт-прокси)
  - [9.2. HibernateProxy и Hibernate.initialize()](#92-hibernateproxy-и-hibernateinitialize)
  - [9.3. LazyInitializationException](#93-lazyinitializationexception)
  - [9.4. Проблемы с equals/hashCode и прокси](#94-проблемы-с-equalshashcode-и-прокси)
  - [9.5. Сериализация прокси](#95-сериализация-прокси)
- [10. Наследование в JPA](#10-наследование-в-jpa)
  - [10.1. Стратегии наследования](#101-стратегии-наследования)
  - [10.2. @DiscriminatorColumn и @DiscriminatorValue (SINGLE_TABLE)](#102-discriminatorcolumn-и-discriminatorvalue-single_table)
  - [10.3. @MappedSuperclass](#103-mappedsuperclass)
  - [10.4. @AttributeOverride](#104-attributeoverride)
  - [10.5. @SecondaryTable](#105-secondarytable)
- [11. Встроенные объекты и коллекции](#11-встроенные-объекты-и-коллекции)
  - [11.1. @Embeddable и @Embedded](#111-embeddable-и-embedded)
  - [11.2. @ElementCollection](#112-elementcollection)
- [12. Кэширование в Hibernate (L1, L2, Query Cache)](#12-кэширование-в-hibernate-l1-l2-query-cache)
  - [12.1. L1 Cache (Persistence Context)](#121-l1-cache-persistence-context)
  - [12.2. L2 Cache (SessionFactory-level)](#122-l2-cache-sessionfactory-level)
  - [12.3. Стратегии кэширования (@Cache)](#123-стратегии-кэширования-cache)
  - [12.4. Query Cache](#124-query-cache)
  - [12.5. @NaturalId и кэширование](#125-naturalid-и-кэширование)
- [13. Блокировки и конкурентность](#13-блокировки-и-конкурентность)
  - [13.1. Оптимистичная блокировка (@Version)](#131-оптимистичная-блокировка-version)
  - [13.2. Пессимистичные блокировки (@Lock)](#132-пессимистичные-блокировки-lock)
  - [13.3. LockModeType в JPA](#133-lockmodetype-в-jpa)
  - [13.4. Как работает lock() в Hibernate?](#134-как-работает-lock-в-hibernate)
- [14. Equals/hashCode и версионирование](#14-equalshashcode-и-версионирование)
  - [14.1. Проблема equals/hashCode в Hibernate](#141-проблема-equalshashcode-в-hibernate)
  - [14.2. @Version — детали](#142-version--детали)
- [15. Hibernate — расширенные аннотации](#15-hibernate--расширенные-аннотации)
  - [15.1. @Subselect](#151-subselect)
  - [15.2. @Immutable](#152-immutable)
  - [15.3. @NaturalId](#153-naturalid)
  - [15.4. @DynamicUpdate и @DynamicInsert](#154-dynamicupdate-и-dynamicinsert)
  - [15.5. @RowId](#155-rowid)
  - [15.6. @Check](#156-check)
  - [15.7. @NotFound](#157-notfound)
- [16. Мягкое удаление и фильтры](#16-мягкое-удаление-и-фильтры)
  - [16.1. @Where — простое мягкое удаление](#161-where--простое-мягкое-удаление)
  - [16.2. @FilterDef и @Filter — динамические фильтры](#162-filterdef-и-filter--динамические-фильтры)
  - [16.3. @FilterJoinTable](#163-filterjointable)
  - [16.4. Мягкое удаление vs реальное удаление](#164-мягкое-удаление-vs-реальное-удаление)
- [17. Производительность и пакетная обработка](#17-производительность-и-пакетная-обработка)
  - [17.1. JDBC Batching](#171-jdbc-batching)
  - [17.2. StatelessSession](#172-statelesssession)
  - [17.3. ScrollableResults](#173-scrollableresults)
  - [17.4. Read-only сущности](#174-read-only-сущности)
  - [17.5. Профилирование запросов](#175-профилирование-запросов)
- [18. JPQL, Criteria API и нативные запросы](#18-jpql-criteria-api-и-нативные-запросы)
  - [18.1. JPQL (Java Persistence Query Language)](#181-jpql-java-persistence-query-language)
  - [18.2. Criteria API](#182-criteria-api)
  - [18.3. Нативные SQL-запросы](#183-нативные-sql-запросы)
  - [18.4. Хранимые процедуры](#184-хранимые-процедуры)
  - [18.5. @NamedQuery и @NamedNativeQuery](#185-namedquery-и-namednativequery)
- [19. Callback-и и Event Listener-ы](#19-callback-и-и-event-listener-ы)
  - [19.1. JPA Entity Listeners и callback-аннотации](#191-jpa-entity-listeners-и-callback-аннотации)
  - [19.2. Два способа использования](#192-два-способа-использования)
  - [19.3. AuditingEntityListener (Spring Data)](#193-auditingentitylistener-spring-data)
  - [19.4. Hibernate Interceptor](#194-hibernate-interceptor)
  - [19.5. Порядок вызова callback-ов](#195-порядок-вызова-callback-ов)
- [20. Транзакции в Hibernate](#20-транзакции-в-hibernate)
  - [20.1. Как @Transactional работает с Hibernate](#201-как-transactional-работает-с-hibernate)
  - [20.2. propagation = REQUIRES_NEW с Hibernate](#202-propagation--requires_new-с-hibernate)
  - [20.3. propagation = NESTED с Hibernate](#203-propagation--nested-с-hibernate)
  - [20.4. @Transactional(readOnly = true) — что именно делает Hibernate](#204-transactionalreadonly--true--что-именно-делает-hibernate)
  - [20.5. SharedEntityManagerCreator — как Spring управляет EntityManager](#205-sharedentitymanagercreator--как-spring-управляет-entitymanager)
- [21. Hibernate 6 — изменения и новые возможности](#21-hibernate-6--изменения-и-новые-возможности)
  - [21.1. Основные изменения в Hibernate 6](#211-основные-изменения-в-hibernate-6)
  - [21.2. Составные ключи (@IdClass vs @EmbeddedId)](#212-составные-ключи-idclass-vs-embeddedid)

---

## 1. JPA и Hibernate — основы

### 1.1. Что такое JPA и чем он отличается от Hibernate?

Это, пожалуй, самый частый вопрос на собеседованиях, и в нём легко запутаться. **JPA (Jakarta Persistence API)** — это спецификация, то есть просто набор интерфейсов и правил: вот `EntityManager`, вот `@Entity`, вот JPQL. Это как чертёж моста. **Hibernate** — это конкретная реализация, то есть сам мост из стали и бетона. Он содержит всю тяжёлую логику: генерацию SQL, кэши, dirty checking, прокси.

Есть и другие реализации — EclipseLink, Apache OpenJPA — но Hibernate де-факто стандарт, и Spring Boot по умолчанию использует именно его. При этом Hibernate не ограничивается JPA: он добавляет кучу своих фич, которых в спецификации нет — `@Subselect`, `@Where`, `@Filter`, `@BatchSize`, многоуровневое кэширование. В повседневной работе вы пишете на JPA, но под капотом у вас почти наверняка Hibernate.

### 1.2. Архитектура Hibernate

Hibernate — это не чёрный ящик, а конвейер из нескольких ключевых компонентов. Когда вы вызываете `entityManager.persist(user)`, за кулисами происходит целая цепочка событий:

- **SessionFactory** (в терминах JPA — `EntityManagerFactory`) — это завод, который создаётся один раз при старте и живёт всё время работы приложения. Он тяжёлый, потокобезопасный, и хранит внутри себя все метаданные: маппинги таблиц, связи, конфигурацию кэшей. Создавать его на каждый запрос — самоубийство для производительности.

- **Session** (JPA: `EntityManager`) — легковесный, однопоточный объект, который вы получаете от фабрики под каждую единицу работы. Обычно одна сессия = одна транзакция. Внутри сессии живёт Persistence Context — L1-кэш, который хранит все сущности, с которыми вы работаете прямо сейчас.

- **Transaction** — граница атомарности. Внутри транзакции изменения либо все применяются, либо все откатываются. Hibernate тесно связан с транзакциями: dirty checking, flush, кэши — всё завязано на транзакционные границы.

- **Persistence Context** — сердце Hibernate. Это не просто кэш, это Identity Map, который гарантирует что для одной и той же строки БД вы всегда получите один и тот же Java-объект. Подробнее — в следующей секции.

### 1.3. Session vs EntityManager

Два интерфейса к одному и тому же. `EntityManager` — JPA-стандарт из пакета `jakarta.persistence`. `Session` — родной интерфейс Hibernate из `org.hibernate`. `Session` расширяет `EntityManager` и добавляет то, чего в JPA нет: `createCriteria()` для старого Criteria API, `createSQLQuery()` для нативных запросов, управление flush mode и cache mode напрямую.

В Spring Boot 99% времени вы работаете через `EntityManager` — это «правильный» путь, не привязывающий вас к конкретному провайдеру. Но если очень нужно достать Hibernate-специфичную функциональность:

```java
// Получить Hibernate Session из JPA EntityManager
Session session = entityManager.unwrap(Session.class);

// Примеры Hibernate-специфичных операций:
session.doWork(connection -> {
    // прямой доступ к JDBC Connection
    connection.setNetworkTimeout(null, 5000);
});

// Работа с Natural ID (JPA-стандарта для этого нет):
User user = session.byNaturalId(User.class)
    .using("email", "john@example.com")
    .load();

// Включение фильтров (Hibernate-специфично):
session.enableFilter("activeFilter").setParameter("status", "ACTIVE");

// StatelessSession для массовой вставки:
StatelessSession stateless = sessionFactory.openStatelessSession();
```

**Как Session связан с EntityManager (иерархия):**
```
EntityManager (JPA interface)
    ↑
Session (Hibernate interface — extends EntityManager)
    ↑
SessionImpl (Hibernate implementation class)
```

В Spring `SharedEntityManagerInvocationHandler` (прокси, внедряемый через `@PersistenceContext`) работает на уровне `EntityManager`, но делает `unwrap(Session.class)` при необходимости внутри транзакции.

---

## 2. EntityManager, EntityManagerFactory и Persistence Context

### 2.1. Как работает EntityManagerFactory?

EntityManagerFactory — это «завод», который владеет всей информацией о вашей модели данных. Создаётся **один раз** при старте приложения из `persistence.xml` (или, в Spring Boot, автоматически из `application.properties`). Внутри он хранит метаданные о каждой сущности: поля, типы, связи, стратегии генерации ID — всё что Hibernate нужно для превращения Java-объектов в SQL.

В Spring Boot вы редко видите его напрямую — за вас всё делает `LocalContainerEntityManagerFactoryBean`. Но понимать его роль важно: это точка входа для создания EntityManager-ов. Каждый раз когда начинается транзакция, фабрика выдаёт новый EntityManager.

### 2.2. Как работает Persistence Context (L1-кэш)?

Persistence Context — это то место, где живут ваши сущности пока вы с ними работаете. Но это не просто Map-а. У него есть чёткая структура:

**Внутренние структуры данных:**

| Структура | Тип | Что хранит |
|---|---|---|
| **Identity Map** | `Map<EntityUniqueKey, Object>` | Ключ = тип сущности + ID. Гарантирует что для одной строки БД есть ровно один Java-объект |
| **EntityEntry** | привязан к каждой managed-сущности | Статус (MANAGED/READ_ONLY/DELETED) + снимок `loadedState` — массив исходных значений полей |
| **loadedState** | `Object[]` внутри `EntityEntry` | Значения всех полей какими они были при загрузке из БД. Основа dirty checking |
| **PersistentCollection** | обёртки LAZY-коллекций | Хранят флаг `dirty` и отслеживают добавление/удаление элементов |

**Как операции ложатся на эти структуры:**

- **`persist(entity)`** — создаёт `EntityEntry` со статусом SAVING, кладёт объект в Identity Map, планирует INSERT. Сам SQL пока не выполняется.
- **`find(Class, id)`** — сначала смотрит в Identity Map. Нашёл? Вернул, никакого SQL. Не нашёл? Идёт в L2-кэш (если включён), потом в БД. Загрузил → создаёт `EntityEntry` со снимком → кладёт в Identity Map.
- **`merge(entity)`** — тут хитрее: ищет в Identity Map по ID. Если нет — грузит из БД. Затем копирует все поля из переданного объекта в managed-экземпляр. Возвращает managed-копию. Переданный объект остаётся detached.
- **`remove(entity)`** — ставит статус DELETED, планирует DELETE. Объект остаётся в Identity Map до закрытия сессии.
- **`flush()`** — самый важный момент: Hibernate проходит по **всем** EntityEntry в PC. Для каждого со статусом MANAGED сравнивает текущие значения со снимком `loadedState`. Нашёл изменения → генерирует UPDATE.

**Что это значит на практике:**

- **Повторяемое чтение по identity** — `find(User.class, 1L)` дважды в одной сессии даст один и тот же объект и один SQL-запрос. Второй раз — из Identity Map.
- **Рост памяти** — все managed-сущности + их снимки висят в памяти до `clear()` или `close()`. Обрабатываете 100 000 записей без промежуточной очистки? Готовьтесь к OutOfMemoryError. Правильный паттерн: каждые N записей делать `flush()` + `clear()`.

### 2.3. Как @PersistenceContext внедряет EntityManager в Spring?

Вот за это я люблю Spring — он превращает потенциально опасную операцию в безопасную. `@PersistenceContext` внедряет не сам EntityManager (он не потокобезопасен), а **прокси**. Этот прокси (`SharedEntityManagerInvocationHandler`) при каждом вызове метода смотрит: есть ли активная транзакция? Если да — берёт EntityManager, привязанный к текущей транзакции. Если нет — создаёт временный, выполняет операцию и сразу закрывает.

Именно это позволяет использовать `@PersistenceContext` в singleton-бинах без единой проблемы с конкурентностью. Каждый поток получает свой EntityManager, привязанный к своей транзакции.

### 2.4. EntityManagerFactory vs SessionFactory

| Характеристика | EntityManagerFactory | SessionFactory |
|---|---|---|
| Спецификация | JPA | Hibernate native |
| Метод создания | `Persistence.createEntityManagerFactory()` | `new Configuration().configure().buildSessionFactory()` |
| Создание сессии | `createEntityManager()` | `openSession()` / `getCurrentSession()` |
| В Spring Boot | `LocalContainerEntityManagerFactoryBean` | Можно достать: `emf.unwrap(SessionFactory.class)` |

---

## 3. Состояния сущностей и операции

### 3.1. Состояния сущностей (жизненный цикл)

Любая сущность в Hibernate в любой момент времени находится ровно в одном из четырёх состояний. Понимание этих состояний — ключ к тому чтобы не совершать глупых ошибок:

1. **Transient** — объект только что создан через `new User()`. Hibernate о нём ничего не знает. Никакой связи с БД нет, в Persistence Context его нет. Удаляется сборщиком мусора как обычный Java-объект.

2. **Managed** — объект находится под управлением Hibernate. Он в Persistence Context, и каждое изменение его полей **автоматически** попадёт в БД при flush. Попасть в это состояние можно через `persist()`, `merge()`, `find()`. Это самое важное состояние — именно здесь работает dirty checking.

3. **Detached** — объект когда-то был managed, но сессия закрылась (или его явно отсоединили через `detach()`/`clear()`). Изменения полей в этом состоянии в БД не попадают. Вернуть в managed можно только через `merge()`.

4. **Removed** — объект помечен на удаление через `remove()`. Физически он ещё в БД (DELETE будет при flush), но в Persistence Context он уже «покойник» — изменять его бесполезно.

**Диаграмма переходов:**
```
                  persist()
    Transient ───────────────► Managed
        ▲                        │    │
        │ new                    │    │ remove()
        │                        │    ▼
        ▼              merge()   │  Removed
    [GC] ◄─────────────────────┘│
                                 │ close() / clear() / detach()
                                 ▼
                   Detached ───────────────► Managed
                              merge()
```

**Примеры каждого перехода:**
```java
// Transient → Managed:
User user = new User("John");     // transient
em.persist(user);                  // → managed (INSERT запланирован)

// Managed → Detached:
em.detach(user);                   // → detached
// или: em.clear();
// или: сессия закрылась

// Detached → Managed:
user.setName("John Updated");      // изменение в detached-объекте
User managed = em.merge(user);     // → managed (user остаётся detached!)
managed.setName("Another change"); // это изменение отслеживается (managed)

// Managed → Removed:
em.remove(managed);                // → removed (DELETE запланирован)

// Removed → Managed (через persist — редко, но возможно):
em.persist(managed);               // → managed (отменяет удаление)

// Важно: find()/getReference() загружают объект сразу в Managed:
User loaded = em.find(User.class, 1L);  // сразу managed
User proxy  = em.getReference(User.class, 1L); // сразу managed (прокси)
```

### 3.2. persist() vs merge() vs save() vs update()

Вечная путаница, особенно у начинающих. Давайте раз и навсегда:

- **`persist(entity)`** — «сохрани новую сущность». Объект должен быть transient. После вызова он становится managed, но INSERT в БД ещё не выполнен (отложен до flush). Возвращает void. Если передать уже managed-сущность — исключение.

- **`merge(entity)`** — «верни мне управляемую копию этого объекта». Принимает detached-сущность, ищет в БД запись с таким же ID. Если находит — копирует поля из переданного объекта в managed-экземпляр. Если нет — создаёт новый. **Важно**: переданный объект так и останется detached, а метод вернёт другой, managed-объект. Типичная ошибка новичка: `user = em.merge(user)` — забыли присвоить результат.

- **`save(entity)`** — родной метод Hibernate, не JPA. Может выполнить INSERT немедленно чтобы вернуть сгенерированный ID. В JPA-мире лучше использовать `persist()`.

- **`update(entity)`** — тоже Hibernate native. Переводит detached-сущность в managed. JPA-эквивалент — `merge()`.

**Простое правило:** для новых сущностей — `persist()`, для существующих — не надо ничего (они managed и сохранятся сами), для detached — `merge()`.

### 3.3. flush() — как и когда?

`flush()` — это момент когда Hibernate превращает накопившиеся изменения в SQL и отправляет их в БД. Но сама транзакция ещё не завершена — `commit()` будет позже.

**Когда flush происходит автоматически:**
- Перед коммитом транзакции — самое очевидное
- Перед выполнением JPQL/Criteria запроса — чтобы запрос видел актуальные данные из Persistence Context
- Когда вы явно вызываете `entityManager.flush()`

**FlushMode настраивает это поведение:**
- `AUTO` (по умолчанию) — flush перед коммитом и перед запросами
- `COMMIT` — только перед коммитом. Быстрее, но запросы могут не видеть ваши незакоммиченные изменения

**Важный нюанс про `@Transactional(readOnly = true)`**: Spring устанавливает `FlushMode.MANUAL`, что запрещает автоматический flush. Dirty checking отключается, снимки не делаются. Идеально для операций чистого чтения.

### 3.4. clear(), detach(), refresh(), contains()

Четыре утилитарные операции, которые нужно знать:

- **`clear()`** — ядерная кнопка. Очищает весь Persistence Context. Все managed-сущности становятся detached. Все несохранённые изменения (недошедшие до flush) — теряются. Используйте вместе с `flush()` при пакетной обработке.
- **`detach(entity)`** — точечная версия `clear()`. Убирает конкретную сущность из PC. Её ленивые прокси после этого сломаются — обращения к LAZY-полям дадут `LazyInitializationException`.
- **`refresh(entity)`** — перечитывает сущность из БД, **отменяя** все незакоммиченные изменения. Полезно когда нужно сбросить случайные правки или получить актуальные данные после нативного запроса.
- **`contains(entity)`** — быстрая проверка O(1): в Identity Map сущность или нет. Можно использовать перед `merge()`/`persist()` чтобы избежать исключений.

### 3.5. find() vs getReference()

Два способа загрузить сущность, и разница между ними принципиальна:

- **`find(Class, id)`** — сразу идёт в БД и возвращает полноценный объект или `null`. Предсказуемо и безопасно.
- **`getReference(Class, id)`** — возвращает **прокси** без единого запроса к БД. Прокси хранит только ID. Как только вы дёрнете любой геттер (кроме `getId()`), прокси пойдёт в БД и загрузит данные. Если сущности не существует — `EntityNotFoundException` при обращении к полям.

**Где полезен `getReference()`**: когда вам нужно установить связь, а сами данные не нужны. Например: `order.setUser(em.getReference(User.class, userId))`. Это сэкономит SELECT к таблице users.

### 3.6. remove()

Удаление managed-сущности. Звучит просто, но есть тонкости:

- **Сущность должна быть managed** — передадите detached → `IllegalArgumentException`. Сначала `merge()`, потом `remove()`.
- **Статус DELETED** — сущность остаётся в Identity Map до закрытия сессии, но помечена как удалённая. При flush — DELETE.
- **Hibernate сам разбирается с порядком**: анализирует внешние ключи и удаляет дочерние записи раньше родительских. Но если FK-constraint нарушен — `ConstraintViolationException`.
- **Каскадное удаление** — по умолчанию удаляется только переданная сущность. Нужны дети? `CascadeType.REMOVE` на родителе. Нужно удалять осиротевшие? `orphanRemoval = true`.
- **JPQL bulk delete** — `DELETE FROM Entity WHERE ...` — выполняется напрямую в БД, **минуя** Persistence Context. Не каскадирует, не проверяет orphanRemoval. Managed-сущности в PC не узнают что их удалили. После bulk delete всегда делайте `clear()`.

---

## 4. Маппинг сущностей

### 4.1. @Entity и @Table

**@Entity** — помечает класс как сущность JPA. Обязательные требования:
- Класс должен быть top-level (не вложенный), не `final`, с `public` или `protected` конструктором без аргументов
- Не может быть `enum` или `interface`
- Поля, которые будут маппиться, должны иметь геттеры/сеттеры (property access) либо быть непосредственно доступны (field access — зависит от расположения `@Id`)

```java
@Entity(name = "User")  // имя сущности для JPQL (по умолчанию — простое имя класса)
public class User {
    // ...
}
```

**@Table** — настраивает маппинг на конкретную таблицу:

```java
@Entity
@Table(name = "app_users",                    // имя таблицы (по умолчанию = имя класса)
       schema = "public",                     // схема (PostgreSQL, Oracle, SQL Server)
       catalog = "my_app",                    // каталог (MySQL)
       uniqueConstraints = {
           @UniqueConstraint(name = "uk_user_email", columnNames = {"email"}),
           @UniqueConstraint(name = "uk_user_phone", columnNames = {"country_code", "phone"})
       },
       indexes = {
           @Index(name = "idx_user_status", columnList = "status"),
           @Index(name = "idx_user_created", columnList = "created_at DESC"),
           @Index(name = "idx_user_name_status", columnList = "last_name, first_name, status")
       })
public class User {
    @Id private Long id;
    private String email;
    private String status;
    // ...
}
```

**`uniqueConstraints` vs `@Column(unique = true)`**: первые генерируют именованные constraint-ы на уровне таблицы (видны в DDL), вторые — на уровне колонки. Для составных уникальных ключей только `uniqueConstraints`. Оба влияют только на генерацию DDL (`hibernate.hbm2ddl.auto`), но не на runtime-поведение Hibernate.

**`indexes`** — то же самое: только для DDL-генерации. Не влияет на запросы — индексы используются на уровне БД.

### 4.2. @Id и стратегии генерации (@GeneratedValue)

**@Id** — объявляет первичный ключ сущности. Может быть:
- Простым (одно поле): `@Id private Long id;`
- Составным: через `@IdClass` или `@EmbeddedId` (см. раздел 21.2)

**@GeneratedValue** — делегирует генерацию значения ключа. Без неё вы обязаны присваивать ID вручную до вызова `persist()`.

| Стратегия | Как работает | Что происходит в БД | Влияние на JDBC batching |
|---|---|---|---|
| `AUTO` (по умолчанию) | Hibernate выбирает сам, исходя из диалекта | Зависит от диалекта: для PostgreSQL → SEQUENCE, для MySQL → IDENTITY | Зависит от выбранной стратегии |
| `IDENTITY` | БД генерирует ID при INSERT (AUTO_INCREMENT / SERIAL / IDENTITY) | `INSERT INTO users (name) VALUES (?)` → БД возвращает сгенерированный ID | **Ломает batching**: Hibernate обязан выполнить INSERT немедленно, чтобы узнать ID. Каждый INSERT = отдельный round-trip |
| `SEQUENCE` | Использует sequence-объект БД | `SELECT nextval('users_seq')` → `INSERT INTO users (id, name) VALUES (?, ?)` | Поддерживает batching: ID известны до INSERT, Hibernate может группировать операции |
| `TABLE` | Отдельная таблица-счётчик: `SELECT next_val FROM id_table WHERE name='users' FOR UPDATE` → `UPDATE id_table SET next_val = ?` | Два запроса на каждый ID + row-level locking на таблице-счётчике | Поддерживает batching, но медленно из-за блокировок. **Не рекомендуется** |
| `UUID` | Генерирует UUID на стороне приложения | UUID генерируется в Java, вставляется как обычная строка/бинарное значение | Поддерживает batching, ID известны до INSERT |

**Детали по каждой стратегии:**

**IDENTITY — почему ломает batching:**
```java
// При IDENTITY Hibernate обязан сделать так (внутри persist()):
// INSERT INTO users (name) VALUES ('User1')  ← немедленно, чтобы получить ID
// INSERT INTO users (name) VALUES ('User2')  ← немедленно
// INSERT INTO users (name) VALUES ('User3')  ← немедленно
// Каждый INSERT — отдельный round-trip к БД, даже при batch_size=50

// При SEQUENCE:
// SELECT nextval('users_seq')  ← получаем 50 ID за раз (allocationSize)
// Затем flush отправляет batch из 50 INSERT'ов:
// INSERT INTO users (id, name) VALUES (1, 'User1'), (2, 'User2'), ...
```

**SEQUENCE — allocationSize и оптимизация:**
```java
@Id
@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "users_seq")
@SequenceGenerator(
    name = "users_seq",
    sequenceName = "users_id_seq",   // имя sequence в БД
    allocationSize = 50              // Hibernate берёт сразу 50 ID за один вызов nextval
)
private Long id;
```

`allocationSize` — ключевая оптимизация. Hibernate вызывает `nextval` не для каждой сущности, а раз в N сущностей, и держит пул ID в памяти. При падении приложения неиспользованные ID теряются — в последовательности образуются «дырки». Это нормально для surrogate key.

В Hibernate 6 появились расширенные генераторы через `@IdGeneratorType` и `@ValueGenerationType`, позволяющие создавать собственные стратегии генерации.

**UUID — детали хранения:**
```java
@Id
@GeneratedValue(strategy = GenerationType.UUID)
private UUID id;  // Hibernate 6: автоматически выберет бинарное хранение (BINARY(16))

// Для контроля над форматом хранения (Hibernate 6):
@Id
@GeneratedValue(strategy = GenerationType.UUID)
@JdbcTypeCode(SqlTypes.CHAR)     // хранить как CHAR(36) (строка)
private UUID id;

@Id
@GeneratedValue(strategy = GenerationType.UUID)
@JdbcTypeCode(SqlTypes.BINARY)   // хранить как BINARY(16) (компактнее, быстрее)
private UUID id;
```

**Что выбрать:**
- **PostgreSQL** → `SEQUENCE` с `allocationSize` под нагрузку (50-200). Самый эффективный вариант, поддерживает batching.
- **MySQL** → `IDENTITY` (единственная встроенная опция, кроме TABLE). Планируете высокую нагрузку на вставку — рассмотрите UUID или ручное присвоение ID (например, Snowflake ID / TSID).
- **Oracle** → `SEQUENCE` (нативный механизм Oracle).
- **UUID** → распределённые системы, микросервисы без общей БД, мульти-мастер репликация. Минус: больше размер индекса, фрагментация B-tree.

### 4.3. @Column

Точная настройка маппинга поля на колонку:

```java
@Column(name = "full_name",                  // имя колонки (по умолчанию = имя поля)
        nullable = false,                    // NOT NULL constraint (DDL + валидация)
        unique = true,                       // UNIQUE constraint (DDL)
        length = 100,                        // VARCHAR(100) (для строк)
        precision = 10, scale = 2,           // DECIMAL(10,2) (для BigDecimal)
        columnDefinition = "TEXT CHECK (status IN ('ACTIVE','INACTIVE'))", // сырой DDL-фрагмент
        insertable = false,                  // не включать в INSERT (вычисляемые/read-only колонки)
        updatable = false)                   // не включать в UPDATE (неизменяемые колонки)
private String name;
```

**`insertable = false, updatable = false`** — полезно для:
- Колонок, заполняемых триггером БД или `@Generated` (БД-side generation)
- Колонок из `@SecondaryTable`, которые не должны обновляться через эту сущность
- Поля `@Formula` — они и так read-only, но явное указание делает намерение понятнее

**`columnDefinition`** — передаёт SQL-фрагмент напрямую в DDL. Не влияет на runtime (Hibernate не парсит его), только на генерацию схемы. Используйте осознанно: теряется переносимость между диалектами.

**Важно**: `nullable = false` влияет **только на DDL-генерацию**, но не на runtime-валидацию. Hibernate не проверяет поля на `null` перед INSERT/UPDATE. Для реальной валидации используйте Bean Validation (`@NotNull`).

### 4.4. @Transient, @Formula, @Enumerated, @Lob

**@Transient** — исключает поле из персистентности:
```java
@Transient
private String temporaryCache;  // не маппится, не сохраняется, не загружается
```
Полезно для вычисляемых полей, кэшей, временных данных на время жизни Java-объекта. Не путать с ключевым словом `transient` (Java serialization) — они ортогональны. `@Transient` управляет JPA, `transient` — Java serialization.

**@Formula** (Hibernate-specific) — вычисляемое поле на уровне БД, только для чтения:
```java
@Entity
public class Order {
    @Id private Long id;

    @Formula("(SELECT COALESCE(SUM(oi.price * oi.quantity), 0) FROM order_items oi WHERE oi.order_id = id)")
    private BigDecimal totalAmount;  // вычисляется БД при каждом SELECT

    @Formula("(SELECT COUNT(*) FROM order_items oi WHERE oi.order_id = id)")
    private Integer itemCount;

    @Formula("created_at + INTERVAL '30 days'")  // диалект-зависимый SQL!
    private LocalDate paymentDueDate;
}
```
Генерируемый SQL: `SELECT o.id, (SELECT COALESCE(SUM(...)...)) AS totalAmount, ... FROM orders o`

**Ограничения `@Formula`**:
- Только чтение — запись в такое поле не генерирует UPDATE
- SQL внутри `@Formula` диалект-зависим (PostgreSQL vs MySQL синтаксис)
- Может замедлить запросы, если подзапрос тяжёлый (выполняется для каждой строки)
- Не работает с Criteria API (Hibernate не может разобрать SQL-выражение)

**@Enumerated** — маппинг Java `enum`:
```java
public enum Status {
    ACTIVE, INACTIVE, SUSPENDED  // порядок важен для ORDINAL!
}

@Entity
public class User {
    @Enumerated(EnumType.STRING)    // хранить как 'ACTIVE' / 'INACTIVE' — рекомендуется
    private Status status;

    @Enumerated(EnumType.ORDINAL)   // хранить как 0 / 1 / 2 — ОПАСНО!
    private Status legacyStatus;
}
```

**Почему ORDINAL опасен**: если вы добавите новое значение в середину enum (например, `TEMP` между `ACTIVE` и `INACTIVE`) или переупорядочите значения, все существующие записи в БД станут невалидными. 0 начнёт означать не `ACTIVE`, а что-то другое. STRING чуть больше места на диске (VARCHAR вместо INT), но безопасен для рефакторинга.

**Для хранения enum как INT с явным кодом** (компромисс):
```java
public enum Status {
    ACTIVE(1), INACTIVE(2), SUSPENDED(3);

    private final int code;
    // constructor, getter...
}

// Использовать AttributeConverter (см. ниже) или @Type (Hibernate 6)
```

**@Lob** — большие объекты (Large Objects):
```java
@Entity
public class Document {
    @Lob
    @Column(columnDefinition = "TEXT")  // PostgreSQL: TEXT; MySQL: LONGTEXT
    private String content;             // CLOB (Character Large Object)

    @Lob
    @Column(columnDefinition = "BYTEA")  // PostgreSQL: BYTEA; MySQL: LONGBLOB
    private byte[] attachment;           // BLOB (Binary Large Object)
}
```

**Поведение @Lob**: Hibernate может загружать LOB-поля лениво (зависит от JDBC-драйвера и диалекта). В PostgreSQL для настоящей ленивой загрузки больших полей используйте `@Basic(fetch = FetchType.LAZY)` — но это требует bytecode enhancement (см. раздел 9). Без него `FetchType.LAZY` для `@Basic` — это лишь hint, который Hibernate (и большинство провайдеров) игнорирует.

**AttributeConverter** — преобразование Java-типа в JDBC-тип и обратно (JPA 2.1+):
```java
@Converter(autoApply = true)  // автоматически применять ко всем полям этого типа
public class StatusConverter implements AttributeConverter<Status, String> {
    @Override
    public String convertToDatabaseColumn(Status status) {
        return status == null ? null : status.name().toLowerCase();
    }

    @Override
    public Status convertToEntityAttribute(String dbData) {
        return dbData == null ? null : Status.valueOf(dbData.toUpperCase());
    }
}

// Использование: просто объявите поле типа Status — конвертер применится автоматически
@Entity
public class User {
    private Status status;  // в БД — VARCHAR, в Java — enum Status
}
```

Конвертеры позволяют хранить enum как INT с явным кодом, JSON-поля как объекты, `PhoneNumber` как строку, и т.д. Один конвертер — одно поле, не работает для коллекций (для этого `@ElementCollection` или UserType).

---

## 5. Маппинг связей (@OneToOne, @ManyToOne, @OneToMany, @ManyToMany)

### 5.1. @ManyToOne и @OneToMany

Самая распространённая связь. `@ManyToOne` — сторона-владелец (внешний ключ). `@OneToMany(mappedBy = "...")` — обратная сторона.

```java
@Entity
public class Order {
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id",
                foreignKey = @ForeignKey(name = "fk_order_user"))  // имя FK-constraint в DDL
    private User user;
}

@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Order> orders = new ArrayList<>();
}
```

**Что Hibernate делает под капотом для `@ManyToOne`**:
1. При загрузке `Order` загружается значение колонки `user_id`
2. Если связь LAZY — в поле `user` помещается прокси (см. раздел 9), хранящее `userId`
3. При первом обращении к любому полю `user` (кроме `id`) — прокси выполняет `SELECT * FROM users WHERE id = ?`
4. Если связь EAGER — сразу выполняется JOIN или дополнительный SELECT (зависит от FetchMode)

**Для `@OneToMany`** — это обратная сторона. Hibernate НЕ хранит никакой информации о коллекции в таблице `users`. При обращении к `user.getOrders()`:
1. Если коллекция LAZY — `PersistentBag` (Hibernate-обёртка) проверяет, инициализирована ли коллекция
2. Если нет — `SELECT * FROM orders WHERE user_id = ?`
3. Результат кэшируется в `PersistentBag`

**`@JoinColumn` — что можно настраивать:**
```java
@ManyToOne
@JoinColumn(name = "user_id",           // имя FK-колонки
            referencedColumnName = "id", // на какую колонку родителя ссылается (по умолчанию — PK)
            nullable = false,            // NOT NULL — у каждого Order должен быть User
            foreignKey = @ForeignKey(name = "fk_order_user"))  // имя constraint в БД
private User user;
```

**Однонаправленная @OneToMany (без @ManyToOne)** — особая ситуация:
```java
@Entity
public class User {
    @OneToMany
    @JoinColumn(name = "user_id")  // FK находится в таблице orders, но в коде его нет!
    private List<Order> orders;
}
```
Hibernate генерирует дополнительный UPDATE: `UPDATE orders SET user_id = ? WHERE id = ?` после вставки Order. Менее эффективно, чем двунаправленная связь. Лучше всегда делать двунаправленную связь, даже если обратная сторона не нужна в коде (просто не добавляйте геттер для User в Order, если он не нужен публично).

### 5.2. @OneToOne

Использует `@JoinColumn` на владеющей стороне (где FK). Уникальность FK гарантирует связь 1:1.

```java
@Entity
public class User {
    @OneToOne(mappedBy = "user", cascade = CascadeType.ALL,
              fetch = FetchType.LAZY)  // ← LAZY, но может не сработать!
    private Profile profile;
}

@Entity
public class Profile {
    @OneToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id", unique = true)  // unique = true → 1:1
    private User user;
}
```

**Проблема ленивой загрузки для `@OneToOne`** — одна из самых нетривиальных в Hibernate:

Hibernate должен знать, есть ли связанная сущность или `null`, чтобы решить: поместить в поле прокси или `null`. Но FK находится в таблице `profile` (колонка `user_id`), а не в `users`. Когда Hibernate загружает `User`, он не знает, существует ли связанный `Profile`, **не заглянув в таблицу `profiles`**. Поэтому он выполняет `SELECT * FROM profiles WHERE user_id = ?` сразу при загрузке `User` — даже если указан `FetchType.LAZY`. Это сводит на нет ленивую загрузку.

**Решения:**

1. **Bytecode Enhancement + `@LazyToOne(NO_PROXY)`**:
```java
@Entity
public class User {
    @OneToOne(mappedBy = "user", fetch = FetchType.LAZY)
    @LazyToOne(LazyToOneOption.NO_PROXY)  // требует bytecode enhancement
    private Profile profile;
}
```
Требует настройки Gradle/Maven плагина для пост-компиляции байткода. Усложняет сборку, но даёт настоящую ленивую загрузку.

2. **`@MapsId`** — когда дочерняя сущность разделяет PK с родителем:
```java
@Entity
public class User {
    @Id @GeneratedValue private Long id;

    @OneToOne(mappedBy = "user", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
    private Profile profile;  // теперь LAZY работает!
}

@Entity
public class Profile {
    @Id
    private Long id;  // НЕ генерируется — берётся от User

    @OneToOne(fetch = FetchType.LAZY)
    @MapsId  // profile.id = user.id
    @JoinColumn(name = "id")
    private User user;
}

// Использование:
User user = em.find(User.class, 1L);        // SELECT * FROM users WHERE id = 1
Profile p = user.getProfile();               // LAZY работает! SELECT * FROM profiles WHERE id = 1
```
Почему это работает: FK и PK совпадают. Hibernate знает, что `Profile` имеет тот же ID что и `User`. Он может создать прокси с этим ID и не идти в БД для проверки существования.

3. **Перепроектировать связь** — если Profile не является обязательным атрибутом User, можно сделать связь через `@ManyToOne` на стороне Profile и не делать обратную `@OneToOne` на User. Или вообще разнести на разные агрегаты (DDD).

### 5.3. @ManyToMany

Использует промежуточную таблицу (`@JoinTable`):

```java
@Entity
public class Student {
    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id"),
        indexes = {
            @Index(name = "idx_sc_course", columnList = "course_id")
        },
        uniqueConstraints = {
            @UniqueConstraint(name = "uk_student_course",
                              columnNames = {"student_id", "course_id"})
        }
    )
    private Set<Course> courses = new HashSet<>();
}

@Entity
public class Course {
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();
}
```

**Использование `Set` vs `List` для @ManyToMany:**
- **`Set`** — рекомендуемый вариант. Hibernate использует `PersistentSet`, что позволяет эффективно удалять элементы без пересоздания всей коллекции.
- **`List`** — Hibernate использует `PersistentBag`, который не отслеживает удаление отдельных элементов. При изменении Bag Hibernate удаляет **все** строки из join-таблицы и вставляет заново. Это может быть катастрофично для производительности.

**Когда не стоит использовать `@ManyToMany`**: если нужны дополнительные поля в промежуточной таблице (дата записи, оценка, роль). Тогда разбиваем на `@OneToMany → JoinEntity → @ManyToOne`:

```java
@Entity
public class Student {
    @OneToMany(mappedBy = "student", cascade = CascadeType.ALL, orphanRemoval = true)
    private Set<Enrollment> enrollments = new HashSet<>();
}

@Entity
public class Course {
    @OneToMany(mappedBy = "course")
    private Set<Enrollment> enrollments = new HashSet<>();
}

@Entity
@Table(name = "student_course")
public class Enrollment {
    @EmbeddedId
    private EnrollmentId id;  // student_id + course_id

    @ManyToOne(fetch = FetchType.LAZY)
    @MapsId("studentId")
    @JoinColumn(name = "student_id")
    private Student student;

    @ManyToOne(fetch = FetchType.LAZY)
    @MapsId("courseId")
    @JoinColumn(name = "course_id")
    private Course course;

    private LocalDateTime enrolledAt;   // дополнительные поля
    private Integer grade;
    private String role;                // например, 'STUDENT' / 'TEACHING_ASSISTANT'
}

@Embeddable
public class EnrollmentId implements Serializable {
    private Long studentId;
    private Long courseId;
    // equals() + hashCode()
}
```

### 5.4. FetchType: LAZY vs EAGER

| Тип связи | По умолчанию | Рекомендация |
|---|---|---|
| `@OneToOne` | **EAGER** | Всегда переопределяйте на `LAZY` (помня об ограничениях, см. 5.2) |
| `@ManyToOne` | **EAGER** | Всегда переопределяйте на `LAZY` |
| `@OneToMany` | **LAZY** | Оставить LAZY |
| `@ManyToMany` | **LAZY** | Оставить LAZY |

**Почему EAGER по умолчанию для `@ManyToOne` и `@OneToOne` — историческая ошибка JPA.** В спецификации JPA 1.0 это казалось удобным: «загрузи сразу, чтобы не было проблем». На практике это главная причина лавины N+1 и проблем с производительностью.

**Правило**: всегда используйте `FetchType.LAZY` для **всех** связей. Когда связь реально нужна в 90%+ случаев — решайте это точечно через `JOIN FETCH`, `@EntityGraph` или `@Fetch(FetchMode.JOIN)`.

**Пример влияния EAGER на производительность:**
```java
// Безобидный запрос:
List<Order> orders = em.createQuery("SELECT o FROM Order o", Order.class)
    .getResultList();  // 1 SQL-запрос

// Но если Order.user = EAGER (по умолчанию):
// SELECT * FROM orders          — 1 запрос
// SELECT * FROM users WHERE id=? — N запросов (для каждого order!)
// Order.orderItems = LAZY — ок, не грузится
// Но User.profile = EAGER (по умолчанию):
// SELECT * FROM profiles WHERE user_id=? — ещё N запросов!
// Итого: 1 + 2N запросов для простого List<Order>
```

---

## 6. Cascade, orphanRemoval и владение связью

### 6.1. Cascade-типы

Определяют, какие операции EntityManager распространяются на связанные сущности. Каскад срабатывает **на уровне Persistence Context**, а не на уровне БД (это не `ON DELETE CASCADE` в SQL!).

| Тип | Действие EntityManager | Когда срабатывает |
|---|---|---|
| `PERSIST` | `em.persist(parent)` → `em.persist(child)` | При сохранении родителя — сохранить детей |
| `MERGE` | `em.merge(parent)` → `em.merge(child)` | При merge родителя — merge детей |
| `REMOVE` | `em.remove(parent)` → `em.remove(child)` | При удалении родителя — удалить детей |
| `REFRESH` | `em.refresh(parent)` → `em.refresh(child)` | При refresh родителя — перечитать детей из БД |
| `DETACH` | `em.detach(parent)` → `em.detach(child)` | При detach родителя — отсоединить детей от PC |
| `ALL` | = PERSIST + MERGE + REMOVE + REFRESH + DETACH | Все операции |

**Пример каскадного сохранения:**
```java
@Entity
public class Order {
    @OneToMany(mappedBy = "order", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<OrderItem> items = new ArrayList<>();

    public void addItem(OrderItem item) {
        items.add(item);
        item.setOrder(this);  // синхронизация обратной стороны
    }
}

// Использование:
Order order = new Order();
order.addItem(new OrderItem("Book", 2));
order.addItem(new OrderItem("Pen", 5));
em.persist(order);  // каскадно сохранит оба OrderItem — один вызов!
```

**Важно понимать отличие каскада от БД-каскада:**
```java
// CascadeType.REMOVE в Hibernate:
em.remove(order);  // Hibernate выполняет для каждого OrderItem:
                   // DELETE FROM order_items WHERE id = ?
                   // DELETE FROM orders WHERE id = ?
                   // Это Java-цикл, не один SQL-запрос!

// ON DELETE CASCADE в БД (добавляется через @OnDelete):
@OneToMany(mappedBy = "order", cascade = CascadeType.ALL)
@OnDelete(action = OnDeleteAction.CASCADE)  // Hibernate-специфичная аннотация
private List<OrderItem> items;
// Теперь: ALTER TABLE order_items ADD CONSTRAINT ... FOREIGN KEY ... ON DELETE CASCADE
// При удалении Order БД сама удалит все связанные OrderItem — одним DELETE.
```

### 6.2. orphanRemoval = true

Отличие от `CascadeType.REMOVE`:

- **`orphanRemoval = true`**: удалить ребёнка, если он **удалён из коллекции родителя** (но сам родитель остаётся)
- **`CascadeType.REMOVE`**: удалить ребёнка при **удалении родителя**

```java
// orphanRemoval в действии:
Order order = em.find(Order.class, 1L);
order.getItems().remove(0);  // удалили первый элемент из коллекции
// При flush: DELETE FROM order_items WHERE id = ? (этот элемент осиротел)

// CascadeType.REMOVE в действии:
em.remove(order);
// При flush: DELETE FROM order_items WHERE order_id = ? (все элементы)
//            DELETE FROM orders WHERE id = ?
```

Часто используются вместе: `cascade = CascadeType.ALL, orphanRemoval = true`. Это паттерн «родитель владеет детьми»: дети не существуют отдельно от родителя, удаление из коллекции = удаление из БД.

**Типичный пример — Заказ и Позиции заказа:**
```java
// Без orphanRemoval:
order.getItems().clear();    // удалили из коллекции, но в БД остались сироты
order.addItem(newItem);
em.merge(order);
// Результат: старые items остались в БД с order_id = NULL (или с битой ссылкой)

// С orphanRemoval = true:
order.getItems().clear();
order.addItem(newItem);
em.merge(order);
// Результат: старые items удалены из БД, новый item добавлен
```

### 6.3. mappedBy и владение связью

В двунаправленной связи одна сторона — владелец (owner), другая — обратная (inverse). `mappedBy` всегда на обратной стороне. Только изменения на стороне-владельце влияют на БД.

```java
// Владелец: Order.user (здесь FK user_id)
@ManyToOne
@JoinColumn(name = "user_id")
private User user;

// Обратная: User.orders (не влияет на БД)
@OneToMany(mappedBy = "user")
private List<Order> orders;
```

**Как Hibernate определяет владельца:**
- Сторона с `@JoinColumn` — владелец (там физически находится FK)
- Сторона с `mappedBy` — обратная (FK в другой таблице)
- Для `@ManyToMany`: сторона с `@JoinTable` — владелец

**Почему это важно:** когда вы делаете `user.getOrders().add(order)`, но забываете `order.setUser(user)`, Hibernate **не сохранит связь в БД** — колонка `user_id` в таблице `orders` останется NULL (или старым значением). FK обновляется только при изменении на стороне-владельце (Order.user).

**Синхронизация** — всегда обновляйте обе стороны связи:

```java
// Вариант 1: метод-хелпер на родителе (рекомендуется)
@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Order> orders = new ArrayList<>();

    public void addOrder(Order order) {
        orders.add(order);          // обратная сторона
        order.setUser(this);        // сторона-владелец (важно!)
    }

    public void removeOrder(Order order) {
        orders.remove(order);       // обратная сторона
        order.setUser(null);        // сторона-владелец (разрыв связи)
    }
}

// Вариант 2: метод-хелпер на дочерней сущности
@Entity
public class Order {
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;

    public void setUser(User user) {
        if (this.user != null) {
            this.user.getOrders().remove(this);  // удалить из старого родителя
        }
        this.user = user;
        if (user != null) {
            user.getOrders().add(this);           // добавить к новому родителю
        }
    }
}
```

---

## 7. Fetch-стратегии и проблема N+1

### 7.1. Проблема N+1

**Классический сценарий:**

```java
List<User> users = userRepo.findAll();  // 1 запрос: SELECT * FROM users
for (User user : users) {
    System.out.println(user.getOrders().size());  // N запросов: SELECT * FROM orders WHERE user_id = ?
}
// Итого: 1 + N запросов
```

**Почему это происходит:** `getOrders()` вызывает геттер LAZY-коллекции, обёрнутой в `PersistentCollection`. Прокси коллекции проверяет, инициализирована ли она. Если нет — выполняет отдельный `SELECT` для загрузки заказов именно этого пользователя. Каждый пользователь инициирует свой запрос независимо.

**Почему EAGER не решает проблему, а иногда ухудшает:**
- EAGER просто выполняет доп. запросы на этапе загрузки родительской сущности, а не при обращении
- Если связь не всегда нужна — EAGER делает лишнюю работу всегда
- `@ManyToOne(fetch = EAGER)` — каждый `Order` при загрузке делает доп. запрос за `User`, даже если `User` не нужен
- Картезианский продукт: несколько EAGER-коллекций → `JOIN` даёт перемножение строк

**Как обнаружить N+1:**
- `spring.jpa.show-sql=true` — увидеть лавину SQL-запросов в логах
- `hibernate.generate_statistics=true` — посмотреть `StatementCount` после операции
- Инструменты: p6spy (прокси-драйвер), Datadog APM, JProfiler
- Тест: `assertThat(jpaMetamodel.getEntities()).hasSize(expectedTableCount)` + подсчёт запросов

### 7.2. Решения проблемы N+1

| Решение | SQL | Сложность | Ограничения |
|---|---|---|---|
| **JOIN FETCH** | `SELECT u, o FROM User u JOIN FETCH u.orders` | Низкая | Несколько коллекций → `MultipleBagFetchException`; нельзя с пагинацией |
| **@EntityGraph** | Аналогично JOIN FETCH, но декларативно | Средняя | Те же ограничения что JOIN FETCH; `LOAD` vs `FETCH` типы |
| **@BatchSize** | `SELECT * FROM orders WHERE user_id IN (?,?,...?)` | Низкая | Не убирает доп. запросы полностью — заменяет N на N/batchSize |
| **SUBSELECT** | `SELECT * FROM orders WHERE user_id IN (SELECT id FROM users WHERE ...)` | Низкая | Дублирует WHERE родительского запроса; дорого при сложных условиях |
| **DTO-проекция** | `SELECT new UserDto(u.id, u.name, o.id) FROM User u JOIN u.orders o` | Средняя | Нет сущностей → нет PC, нет dirty checking, read-only |

**Когда что использовать:**
1. **Одна коллекция, всегда нужна** → `JOIN FETCH` в запросе
2. **Несколько сценариев загрузки** → `@NamedEntityGraph` + выбор графа по имени
3. **Нельзя менять запросы (legacy)** → `@BatchSize(size = 50)` на коллекцию
4. **Только чтение, нужна агрегация** → DTO-проекция (самый быстрый вариант, обходит PC)

**MultipleBagFetchException:** Hibernate не может сделать `JOIN FETCH` на две коллекции типа `List` одновременно (картезианский продукт). Решение: заменить один `List` на `Set`, или использовать `@BatchSize`, или делать отдельные запросы.

**JOIN FETCH + Пагинация:** Hibernate не может применить `LIMIT/OFFSET` в SQL с JOIN FETCH (одна родительская строка дублируется на каждую дочернюю). Hibernate загружает **все** данные в память и пагинирует там → утечка памяти. Решение: сначала загрузить ID с пагинацией, потом основные данные с JOIN FETCH по этим ID.

### 7.3. JOIN FETCH vs EntityGraph

- **JOIN FETCH**: ручное управление в каждом запросе. Гибко, но дублирование кода.
- **EntityGraph**: декларативное описание графа загрузки. Переиспользуется. Может быть ad-hoc (`attributePaths`) или именованным (`@NamedEntityGraph`).

### 7.4. @NamedEntityGraph

```java
@Entity
@NamedEntityGraph(name = "User.orders",
    attributeNodes = @NamedAttributeNode("orders"))
public class User {
    @OneToMany(mappedBy = "user")
    private List<Order> orders;
}

// Использование
@EntityGraph("User.orders")
@Query("SELECT u FROM User u WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

### 7.5. @Fetch (Hibernate) — стратегии загрузки

- `FetchMode.JOIN` — загружает связь в одном JOIN-запросе с родителем. Переопределяет LAZY (всегда загружает). Полезно когда связь нужна в 90%+ случаев.
- `FetchMode.SELECT` — отдельный SELECT для каждой связи (поведение LAZY по умолчанию). Явно указывать почти никогда не нужно — это то, что происходит по умолчанию.
- `FetchMode.SUBSELECT` — один дополнительный подзапрос: `WHERE parent_id IN (SELECT id FROM parents WHERE <original_conditions>)`. Повторяет WHERE-условие родительского запроса → может быть дорого при сложных условиях. Полезно когда обрабатываешь всю коллекцию элементов (навигация по всем детям всех загруженных родителей).

**Когда что использовать:**
- `JOIN` → единичный запрос с известным ID (`findById`), связь всегда нужна
- `SUBSELECT` → пакетная обработка: загрузили 1000 заказов и для каждого нужны items
- `SELECT` (default) → не трогать, оставить LAZY и решать проблему N+1 точечно через JOIN FETCH / EntityGraph

**Взаимодействие с HQL:** `JOIN FETCH` в запросе всегда переопределяет `@Fetch` — даже если стоит `@Fetch(FetchMode.SELECT)`, JOIN FETCH заставит загрузить через JOIN.

### 7.6. @BatchSize (Hibernate)

Определяет размер пакета для ленивых коллекций:

```java
@OneToMany(mappedBy = "user")
@BatchSize(size = 10)
private List<Order> orders;
```

Генерирует: `SELECT * FROM orders WHERE user_id IN (?, ?, ?, ...)` — вместо N запросов будет N/10 запросов.

### 7.7. @LazyToOne, @LazyCollection (Hibernate)

Точная настройка ленивой загрузки:
- `@LazyToOne(PROXY)` — стандартное проксирование (по умолчанию)
- `@LazyToOne(NO_PROXY)` — через bytecode enhancement (более лениво, требует инструментации)
- `@LazyCollection(TRUE/FALSE/EXTRA)` — для коллекций; `EXTRA` загружает только размер коллекции, элементы — при обращении

---

## 8. Dirty Checking (отслеживание изменений)

### 8.1. Как работает Dirty Checking?

**Dirty Checking** — автоматическое обнаружение изменений в управляемых сущностях. Происходит при `flush()` (и, соответственно, при коммите транзакции).

**Внутренний механизм:**

1. **Снимок при загрузке**: когда сущность загружается из БД (или после flush), Hibernate сохраняет `Object[] loadedState` в `EntityEntry` — массив значений всех persistent-полей.

2. **Сравнение при flush**: `DefaultFlushEntityEventListener` для каждой managed-сущности:
   - Извлекает текущие значения полей (через геттеры или direct field access — зависит от `@Access`)
   - Сравнивает поэлементно с `loadedState` через `Type.isEqual()`:
     ```java
     // Упрощённо:
     for (int i = 0; i < loadedState.length; i++) {
         if (!types[i].isEqual(currentState[i], loadedState[i])) {
             dirtyProperties.add(i);  // найдено изменение
         }
     }
     ```
   - `Type.isEqual()` → обычно `Objects.deepEquals()`, но для Hibernate-типов может быть кастомное сравнение

3. **Генерация UPDATE**: если `dirtyProperties` не пуст → UPDATE SQL. Если `@DynamicUpdate` — только изменённые колонки; иначе — все колонки.

4. **Обновление снимка**: после успешного flush `loadedState` обновляется → новые значения становятся базовыми для следующего сравнения.

**Отслеживание коллекций (отдельный механизм):**

Коллекции **не сравниваются через loadedState**. Hibernate оборачивает LAZY-коллекции в `PersistentCollection` (например, `PersistentBag`, `PersistentSet`), которые:
- Хранят флаг `dirty` (выставляется при `add()`/`remove()`/`clear()`)
- Хранят список добавленных/удалённых элементов
- При flush, если `dirty == true` → синхронизация коллекции с БД (INSERT/DELETE в join-таблицу или FK-колонку)

**Почему это дорого:** при flush итерируются **все** managed-сущности. При 100K сущностей в PC → 100K сравнений полей. Это основная причина ограничения размера Persistence Context.

### 8.2. Как именно Hibernate сравнивает состояние при Dirty Checking?

**Стратегии доступа к полям:**

Hibernate определяет стратегию доступа через `@Access` или тип аннотации `@Id`:
- **Property access** (по умолчанию если `@Id` на геттере): значения извлекаются через геттеры, записываются через сеттеры
- **Field access** (по умолчанию если `@Id` на поле): значения извлекаются напрямую из полей через Reflection (`Field.get()`)

**Сравнение разных типов:**

- **Примитивы и обёртки**: `equals()`
- **Строки**: `equals()`
- **Enum**: `equals()` (ORDINAL опасно — номер может измениться; STRING безопаснее)
- **Даты**: сравнение через `equals()` для `java.util.Date`; специальные компараторы для `java.time.*`
- **Embeddable**: сравнивается целиком через `equals()`, поэтому нужна корректная реализация `equals()`/`hashCode()`
- **@ManyToOne / @OneToOne**: сравнивается по ID связанной сущности (не по ссылке на объект). Изменение ссылки на другой объект с тем же ID не считается dirty.

**Влияние @DynamicUpdate на сравнение:**
- Без `@DynamicUpdate`: сравниваются все поля → UPDATE со всеми колонками (даже неизменёнными)
- С `@DynamicUpdate`: сравниваются все поля → но UPDATE включает только реально изменённые колонки
- В обоих случаях **грязная проверка одинакова** — сравниваются все поля. Разница только в генерируемом SQL.

**Кастомные UserType:**
Реализации `UserType` могут переопределить `isMutable()` и стратегию сравнения. Например, JSONB-тип может сравнивать дерево вместо строки, или использовать глубокое сравнение (deep equals).

### 8.3. Оптимизация Dirty Checking

- **@Transactional(readOnly = true)**: Hibernate пропускает dirty checking (не делает снимки)
- **@DynamicUpdate**: UPDATE только для реально изменённых полей (не для всех). Экономит трафик, но добавляет CPU на анализ.
- **@Immutable**: сущность неизменяема — Hibernate никогда не делает UPDATE, не хранит снимок.
- **StatelessSession**: вообще не использует Persistence Context и dirty checking.
- `session.setReadOnly(entity, true)`: программное отключение для конкретной сущности.

---

## 9. Прокси и ленивая загрузка

### 9.1. Как Hibernate создаёт прокси?

Для ленивой загрузки Hibernate создаёт прокси через библиотеку **ByteBuddy** (ранее Javassist/CGLIB):

1. Создаётся подкласс сущности (`User$HibernateProxy$xxx extends User`)
2. Все геттеры (кроме `@Id`) переопределяются: при первом вызове → загрузка из БД → вызов геттера суперкласса
3. При повторном вызове — данные уже загружены, вызов суперкласса напрямую
4. Идентификатор сущности (`@Id`) доступен без инициализации — прокси хранит его в себе
5. `final`-классы не могут быть проксированы (ByteBuddy не может создать подкласс) → `final` сущности всегда EAGER

**Что происходит внутри прокси (упрощённая модель):**
```java
// Примерно так выглядит сгенерированный прокси (упрощённо):
public class User$HibernateProxy$abc123 extends User implements HibernateProxy {
    private Long id;                    // ID известен без запроса
    private boolean initialized = false;
    private String entityName = "User";
    private transient Session session;  // ссылка на сессию для ленивой загрузки

    @Override
    public String getName() {
        if (!initialized) {
            // Ленивая загрузка: SELECT * FROM users WHERE id = ?
            Object target = session.implementor()
                .load(entityName, id, ...);  // загружает реальный объект
            this.name = ((User) target).name;
            this.email = ((User) target).email;
            // ... копирует все persistent-поля в поля прокси
            initialized = true;
        }
        return this.name;
    }

    @Override
    public Long getId() {
        return id;  // доступно всегда, без инициализации
    }
}
```

### 9.2. HibernateProxy и Hibernate.initialize()

Работа с прокси в runtime:

```java
// 1. Проверка, является ли объект прокси
User user = em.getReference(User.class, 1L);
boolean isProxy = user instanceof HibernateProxy;  // true
// Альтернатива (JPA-стандарт):
PersistenceUnitUtil util = emf.getPersistenceUnitUtil();
boolean isLoaded = util.isLoaded(user);  // false

// 2. Проверка инициализации
boolean initialized = Hibernate.isInitialized(user);  // false

// 3. Принудительная инициализация
Hibernate.initialize(user);  // выполняет SELECT, загружает данные
// После этого:
Hibernate.isInitialized(user);  // true
user.getName();  // не делает запрос — данные уже загружены

// 4. Инициализация прокси-коллекции
Hibernate.initialize(user.getOrders());  // выполняет SELECT * FROM orders WHERE user_id = ?

// 5. Получение класса сущности без инициализации прокси
Class<?> entityClass = HibernateProxyHelper.getClassWithoutInitializingProxy(user);
// Возвращает User.class, а не User$HibernateProxy$xxx.class
// Не вызывает ленивую загрузку!

// 6. Получение ID прокси без инициализации
Long userId = (Long) sessionFactory.getPersistenceUnitUtil().getIdentifier(user);
// Не вызывает ленивую загрузку — ID уже хранится в прокси
```

**Практический паттерн — безопасная работа с опциональной связью:**
```java
public String getUserEmail(User proxyOrEntity) {
    if (Hibernate.isInitialized(proxyOrEntity)) {
        return proxyOrEntity.getEmail();  // быстро, данные уже загружены
    }
    // Прокси не инициализирован — возможно, нам и не нужна полная сущность
    // Можно получить ID без загрузки:
    Long id = (Long) ((HibernateProxy) proxyOrEntity).getHibernateLazyInitializer()
        .getIdentifier();
    // Или загрузить только нужное поле через прямую проекцию
    return "unknown (id=" + id + ")";
}
```

### 9.3. LazyInitializationException

Самое известное исключение Hibernate. Возникает при попытке доступа к ленивому полю/связи **после** закрытия Session (EntityManager).

```java
// Ошибка:
User user = repo.findById(1L);  // транзакция завершена, Session закрылась
user.getOrders();  // LazyInitializationException!
```

**Почему это происходит технически:** прокси хранит ссылку на `Session`, через которую должен был загрузить данные. После закрытия сессии эта ссылка становится невалидной. При обращении к непроинициализированному полю прокси пытается выполнить `session.load(...)` → сессия уже закрыта → исключение.

**Решения (от лучшего к худшему):**

1. **DTO-проекции на уровне репозитория** — не возвращать сущности из сервисного слоя:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT new com.example.dto.UserDto(u.id, u.name, u.email) FROM User u WHERE u.id = :id")
    Optional<UserDto> findDtoById(@Param("id") Long id);
}
// Сущности остаются внутри @Transactional-метода, наружу уходит DTO
```

2. **JOIN FETCH / @EntityGraph** — загрузить связь внутри транзакции:
```java
@Query("SELECT u FROM User u JOIN FETCH u.orders WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

3. **`Hibernate.initialize()` внутри транзакции**:
```java
@Transactional
public User getUserWithOrders(Long id) {
    User user = em.find(User.class, id);
    Hibernate.initialize(user.getOrders());  // инициализация в пределах транзакции
    return user;  // теперь orders доступны после закрытия транзакции
}
```

4. **Open Session in View (OSIV)** — `spring.jpa.open-in-view=true` (по умолчанию). Сессия живёт весь HTTP-запрос. **Антипаттерн**: маскирует проблему, приводит к неконтролируемым запросам во время рендеринга представления, мешает масштабированию.

5. **`spring.jpa.open-in-view=false`** + явная загрузка связей в сервисном слое — **рекомендуемый подход** для production.

### 9.4. Проблемы с equals/hashCode и прокси

Прокси — это подкласс. Сравнение через `equals()`/`hashCode()` с прокси требует аккуратности. См. раздел 14.

### 9.5. Сериализация прокси

Прокси Hibernate не предназначены для сериализации (Jackson, HTTP-сессии). При попытке сериализовать неинициализированный прокси:
- **Jackson**: столкнётся с прокси-полями (ByteBuddy interceptor, session reference), которые не может сериализовать → `LazyInitializationException` или `JsonMappingException`
- **Jackson + Hibernate Module**: `jackson-datatype-hibernate5` (или hibernate6) добавляет `HibernateProxySerializer`, который пропускает неинициализированные прокси (пишет `null`) и сериализует инициализированные как обычные объекты
- **Java Serialization**: неинициализированный прокси содержит ссылку на Session → `NotSerializableException`

**Решения:**
```java
// 1. Jackson Hibernate Module (автоматически обрабатывает прокси)
// build.gradle:
// implementation 'com.fasterxml.jackson.datatype:jackson-datatype-hibernate6'

// 2. @JsonIgnore на LAZY-полях
@Entity
public class User {
    @OneToMany(mappedBy = "user")
    @JsonIgnore  // никогда не сериализовать
    private List<Order> orders;
}

// 3. DTO — правильный способ (см. выше)
// 4. Явная инициализация перед сериализацией
@Transactional
public UserDto getUser(Long id) {
    User user = em.find(User.class, id);
    Hibernate.initialize(user.getOrders());
    return mapper.map(user, UserDto.class);  // MapStruct / ModelMapper
}
```

---

## 10. Наследование в JPA

### 10.1. Стратегии наследования

**@Inheritance(strategy = ...)**:

| Стратегия | Как хранится | Плюсы | Минусы |
|---|---|---|---|
| `SINGLE_TABLE` | Все классы в одной таблице + `@DiscriminatorColumn` | Максимальная производительность, нет JOIN-ов | Много NULL-ов, нарушение нормализации, все колонки всех наследников в одной таблице |
| `TABLE_PER_CLASS` | Каждый конкретный класс — отдельная таблица со всеми полями (включая унаследованные) | Нет JOIN-ов, нет NULL-ов | Дублирование колонок, полиморфные запросы через UNION ALL, неэффективно для больших иерархий |
| `JOINED` | Каждый класс в своей таблице, общие поля в таблице родителя, JOIN по PK | Нормализация, чистые данные, нет дублирования | JOIN-ы при каждом запросе (даже для листового класса), ниже производительность |

**Сравнение SQL для одних и тех же данных:**

```java
// Модель:
@Entity
@Inheritance(strategy = ...)
public abstract class Vehicle {
    @Id @GeneratedValue private Long id;
    private String manufacturer;
    private BigDecimal price;
}

@Entity
public class Car extends Vehicle {
    private Integer seats;
    private String fuelType;
}

@Entity
public class Motorcycle extends Vehicle {
    private Boolean hasSidecar;
    private Integer engineCC;
}
```

**SINGLE_TABLE — SQL вывод:**
```sql
-- Одна таблица на всех:
CREATE TABLE vehicle (
    id BIGINT PRIMARY KEY,
    manufacturer VARCHAR(255),
    price DECIMAL(10,2),
    vehicle_type VARCHAR(31),  -- discriminator column (Car / Motorcycle)
    seats INT,                 -- NULL для Motorcycle
    fuel_type VARCHAR(255),    -- NULL для Motorcycle
    has_sidecar BOOLEAN,       -- NULL для Car
    enginecc INT               -- NULL для Car
);

-- Запрос за всеми транспортными средствами:
SELECT * FROM vehicle;  -- один запрос, без JOIN-ов

-- Запрос только за Car:
SELECT * FROM vehicle WHERE vehicle_type = 'Car';
```

**TABLE_PER_CLASS — SQL вывод:**
```sql
-- Отдельные таблицы, без общей:
CREATE TABLE car (
    id BIGINT PRIMARY KEY,
    manufacturer VARCHAR(255),
    price DECIMAL(10,2),
    seats INT,
    fuel_type VARCHAR(255)
);

CREATE TABLE motorcycle (
    id BIGINT PRIMARY KEY,
    manufacturer VARCHAR(255),
    price DECIMAL(10,2),
    has_sidecar BOOLEAN,
    enginecc INT
);

-- Запрос за всеми транспортными средствами (полиморфный):
SELECT * FROM (
    SELECT id, manufacturer, price, seats, fuel_type, NULL AS has_sidecar, NULL AS enginecc, 'Car' AS clazz
    FROM car
    UNION ALL
    SELECT id, manufacturer, price, NULL AS seats, NULL AS fuel_type, has_sidecar, enginecc, 'Motorcycle' AS clazz
    FROM motorcycle
) AS vehicle;
-- Полиморфные запросы дорогие — UNION ALL по всем таблицам иерархии

-- Запрос за конкретным Vehicle по ID:
-- Hibernate сначала должен понять тип:
SELECT ... FROM car WHERE id = ?;      -- не нашёл? пробуем следующую
SELECT ... FROM motorcycle WHERE id = ?;
-- Может потребоваться до N запросов (по одному на каждый подкласс!)
```

**JOINED — SQL вывод:**
```sql
-- Отдельные таблицы, нормализованные:
CREATE TABLE vehicle (
    id BIGINT PRIMARY KEY,
    manufacturer VARCHAR(255),
    price DECIMAL(10,2)
);

CREATE TABLE car (
    id BIGINT PRIMARY KEY,
    seats INT,
    fuel_type VARCHAR(255),
    FOREIGN KEY (id) REFERENCES vehicle(id)
);

CREATE TABLE motorcycle (
    id BIGINT PRIMARY KEY,
    has_sidecar BOOLEAN,
    enginecc INT,
    FOREIGN KEY (id) REFERENCES vehicle(id)
);

-- Запрос за всеми транспортными средствами:
SELECT v.*, c.seats, c.fuel_type, m.has_sidecar, m.enginecc,
       CASE WHEN c.id IS NOT NULL THEN 'Car'
            WHEN m.id IS NOT NULL THEN 'Motorcycle' END AS clazz
FROM vehicle v
LEFT JOIN car c ON v.id = c.id
LEFT JOIN motorcycle m ON v.id = m.id;
-- Всегда JOIN ко всем подклассам — медленно для глубоких иерархий

-- При вставке Car:
INSERT INTO vehicle (id, manufacturer, price) VALUES (?, ?, ?);
INSERT INTO car (id, seats, fuel_type) VALUES (?, ?, ?);
```

**Когда что выбирать:**

- **SINGLE_TABLE** — лучшая производительность для полиморфных запросов. Используйте когда подклассы не сильно отличаются по полям и иерархия стабильна. Минус — потенциально широкая таблица с сотнями колонок и ограничения БД на их количество.
- **JOINED** — хороший компромисс когда важна нормализация, а иерархия неглубокая (2-3 уровня). Минус — JOIN-ы при каждом запросе, ниже производительность чем SINGLE_TABLE.
- **TABLE_PER_CLASS** — избегайте для полиморфных запросов. Используйте только если вы **никогда** не делаете полиморфные запросы (`FROM Vehicle`) и всегда работаете с конкретными подклассами (`FROM Car`). ID должны быть уникальны глобально (нельзя использовать IDENTITY).

### 10.2. @DiscriminatorColumn и @DiscriminatorValue (для SINGLE_TABLE)

```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "type", discriminatorType = DiscriminatorType.STRING)
public abstract class Animal {
    @Id @GeneratedValue private Long id;
}

@Entity
@DiscriminatorValue("DOG")
public class Dog extends Animal { }

@Entity
@DiscriminatorValue("CAT")
public class Cat extends Animal { }
```

### 10.3. @MappedSuperclass

Абстрактный класс, содержащий общие поля, но **не являющийся сущностью** (нет своей таблицы). Поля наследуются в конкретных сущностях:

```java
@MappedSuperclass
public abstract class BaseEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @CreatedDate
    private LocalDateTime createdAt;
}

@Entity
@Table(name = "users")
public class User extends BaseEntity { }
```

### 10.4. @AttributeOverride

Переопределяет маппинг поля из `@MappedSuperclass`:

```java
@Entity
@AttributeOverride(name = "id", column = @Column(name = "user_id"))
public class User extends BaseEntity { }
```

### 10.5. @SecondaryTable

Маппинг одной сущности на несколько таблиц (редкий кейс):

```java
@Entity
@Table(name = "users")
@SecondaryTable(name = "user_details", pkJoinColumns = @PrimaryKeyJoinColumn(name = "user_id"))
public class User {
    @Column(table = "user_details")
    private String address;
}
```

---

## 11. Встроенные объекты и коллекции

### 11.1. @Embeddable и @Embedded

Позволяют сгруппировать поля в отдельный класс без создания сущности:

```java
@Embeddable
public class Address {
    private String street;
    private String city;
    private String zipCode;
}

@Entity
public class User {
    @Embedded
    private Address homeAddress;

    @Embedded
    @AttributeOverrides({
        @AttributeOverride(name = "street", column = @Column(name = "work_street")),
        @AttributeOverride(name = "city", column = @Column(name = "work_city"))
    })
    private Address workAddress;
}
```

### 11.2. @ElementCollection

Для хранения коллекций примитивных типов или embeddable-объектов в отдельной таблице:

```java
@Entity
public class User {
    @ElementCollection
    @CollectionTable(name = "user_phones", joinColumns = @JoinColumn(name = "user_id"))
    @Column(name = "phone")
    private Set<String> phones = new HashSet<>();

    @ElementCollection
    @CollectionTable(name = "user_addresses", joinColumns = @JoinColumn(name = "user_id"))
    private List<Address> addresses = new ArrayList<>();
}
```

**Как это работает под капотом:** для `@ElementCollection` Hibernate создаёт отдельную таблицу без собственного первичного ключа сущности. Каждая запись идентифицируется по FK на родителя + значению(ям) коллекции:

```sql
CREATE TABLE user_phones (
    user_id BIGINT NOT NULL,
    phone VARCHAR(255)
    -- Нет своего ID! Составной ключ: (user_id, phone)
);
```

**Ключевые ограничения @ElementCollection:**

1. **Нет identity (нет своего @Id)** — нельзя напрямую обновить или удалить один элемент через JPQL. Только через родительскую сущность.
2. **Всегда LAZY** — и переопределить нельзя (в отличие от @OneToMany где можно поставить EAGER).
3. **При изменении коллекции Hibernate удаляет ВСЕ строки и вставляет заново** — главная проблема производительности:
```java
User user = em.find(User.class, 1L);
user.getPhones().add("+7-999-123-45-67");  // добавили один номер

// При flush Hibernate делает:
// DELETE FROM user_phones WHERE user_id = 1;     -- удалил все 5 существующих номеров
// INSERT INTO user_phones VALUES (1, '+7-...');  -- вставил заново все 6
// INSERT INTO user_phones VALUES (1, '+7-...');
// ... (6 вставок)
```
Это происходит потому, что у элементов коллекции нет собственного ID, и Hibernate не может сопоставить «старые» элементы с «новыми». Решение: использовать `Set` (а не `List`) — тогда Hibernate может сравнить элементы по `equals()`/`hashCode()` Embeddable-объекта. Но для строк/примитивов даже с `Set` могут быть проблемы.

4. **Не поддерживает каскад** — вложенные `@ElementCollection` внутри `@ElementCollection` не поддерживаются.
5. **Не может быть лениво загружена по ID** — нельзя сделать `em.find(Phone.class, phoneId)`, потому что у `Phone` нет своего ID.

**Когда использовать @ElementCollection, а когда @OneToMany:**
- **@ElementCollection** — для простых value objects без собственного жизненного цикла: телефоны пользователя, email-ы, теги, простые настройки (ключ-значение)
- **@OneToMany** — когда элемент имеет свой жизненный цикл, может существовать независимо или запрашиваться отдельно. Или когда элементов может быть очень много (нужна пагинация).

---

## 12. Кэширование в Hibernate (L1, L2, Query Cache)

### 12.1. L1 Cache (Persistence Context)

- **Включён всегда**, не отключается
- Кэширует сущности в рамках одной Session/EntityManager через **Identity Map**
- Гарантирует: повторный `find(1L)` в той же сессии не сделает SQL-запрос

**Порядок поиска при `find()`:**
```
1. Identity Map (L1) → если найден, вернуть (даже если БД изменилась)
2. L2 Cache (если включён) → если найден, загрузить данные, создать объект, поместить в L1
3. База данных → загрузить, создать объект, поместить в L1, поместить в L2
```

**Проблема устаревания в L1:** если нативный SQL-запрос или другая транзакция меняет данные, L1 об этом не знает. JPQL/Criteria-запросы автоматически разрешают результаты через L1 (identity guarantee). Нативные запросы — нет. Решение: `session.clear()` перед нативным запросом, или `@Modifying(clearAutomatically = true)`.

**Рост памяти:** при пакетной обработке PC растёт бесконечно. Шаблон:
```java
for (int i = 0; i < entities.size(); i++) {
    em.persist(entities.get(i));
    if (i % 50 == 0) {
        em.flush();  // синхронизировать с БД
        em.clear();  // очистить PC, освободить память
    }
}
```

### 12.2. L2 Cache (SessionFactory-level)

Глобальный кэш между сессиями. Настраивается:

```properties
spring.jpa.properties.hibernate.cache.use_second_level_cache=true
spring.jpa.properties.hibernate.cache.region.factory_class=jcache  # JCache (JSR-107)
```

**Провайдеры:**
- **EhCache** — популярный in-memory/на диске, морально устарел
- **Hazelcast** — распределённый (микросервисы)
- **Infinispan** — распределённый, от JBoss/Red Hat
- **Redis** — внешний, через Redisson Hibernate L2 Cache
- **Caffeine** — высокопроизводительный in-memory (современная замена EhCache, рекомендуется для monolith)

**Пример конфигурации Caffeine как L2 Cache (Spring Boot):**

```groovy
// build.gradle
implementation 'org.hibernate.orm:hibernate-jcache:6.x.x'
implementation 'com.github.ben-manes.caffeine:jcache:3.x.x'
```

```properties
# application.properties
spring.jpa.properties.hibernate.cache.use_second_level_cache=true
spring.jpa.properties.hibernate.cache.region.factory_class=jcache
spring.jpa.properties.hibernate.javax.cache.provider=com.github.benmanes.caffeine.jcache.spi.CaffeineCachingProvider
spring.jpa.properties.hibernate.javax.cache.missing_cache_strategy=create
# Таймауты для разных регионов кэша:
spring.jpa.properties.hibernate.cache.default_cache_concurrency_strategy=READ_WRITE
```

```java
// Кэшируемая сущность:
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE, region = "users")
public class User {
    // ...
}

// Коллекция тоже может кэшироваться:
@Entity
public class User {
    @OneToMany(mappedBy = "user")
    @Cache(usage = CacheConcurrencyStrategy.READ_WRITE, region = "user-orders")
    private List<Order> orders;
}
```

**Как работает L2 Cache на практике:**

```
Запрос: em.find(User.class, 1L)

1. Смотрим в L1 (Persistence Context)
   → Нашли? Возвращаем. SQL не выполнялся.
2. Смотрим в L2 (SessionFactory-level cache)
   → Нашли? Извлекаем данные (по сути — snapshot значений полей).
   → Создаём объект User, заполняем поля.
   → Помещаем объект в L1.
   → Возвращаем. SQL не выполнялся.
3. Идём в БД:
   → SELECT * FROM users WHERE id = 1
   → Создаём объект User из ResultSet.
   → Помещаем в L1.
   → Сохраняем данные (snapshot) в L2.
   → Возвращаем.
```

**Инвалидация L2:** при UPDATE/DELETE сущности Hibernate удаляет её из L2. При следующем запросе — загрузка из БД и снова помещение в L2. Инвалидация происходит автоматически для сущностей, загруженных через Hibernate. Но если другая транзакция (или другой экземпляр приложения) меняет данные в обход Hibernate — L2 устаревает (stale cache). Для распределённых систем это главная проблема L2 — нужны распределённые провайдеры (Hazelcast, Redis) с инвалидацией.

**Кого кэшировать в L2:**
- ✅ Справочники (Category, Country, Currency) — редко меняются, часто читаются
- ✅ Lookup-таблицы (status codes, types)
- ✅ Natural ID (email → user, см. 12.5)
- ❌ Быстро меняющиеся данные (orders, transactions)
- ❌ Таблицы с высокой конкурентностью (счётчики, балансы)
- ❌ Сущности, которые всегда загружаются с JOIN-ами (L2 хранит только саму сущность, не связи)

### 12.3. Стратегии кэширования (@Cache)

```java
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class User { ... }
```

- **READ_ONLY**: только чтение, максимальная производительность
- **NONSTRICT_READ_WRITE**: чтение-запись без строгой изоляции (допустимы расхождения)
- **READ_WRITE**: полная изоляция через мягкие блокировки (soft locks)
- **TRANSACTIONAL**: транзакционное кэширование (для JTA)

### 12.4. Query Cache

Кэширует результаты JPQL/Criteria запросов. **Двухшаговый механизм:**

1. **Ключ**: SQL-запрос + значения параметров → хранится в регионе Query Cache
2. **Значение**: **список ID сущностей** (не сами объекты!)
3. **Resolve**: каждый ID разрешается через L2-кэш (или БД) → получение актуальных объектов

**Критическое следствие**: Query Cache без L2 cache **медленнее** чем без кэша! Сохраняется только компиляция SQL, но каждый ID всё равно идёт в БД.

```properties
spring.jpa.properties.hibernate.cache.use_query_cache=true
```

```java
@Query("SELECT u FROM User u WHERE u.status = :status")
@QueryHints(@QueryHint(name = HINT_CACHEABLE, value = "true"))
List<User> findActive(@Param("status") String status);
```

**Гранулярность инвалидации:** любое изменение таблицы (INSERT/UPDATE/DELETE) инвалидирует **все** закэшированные запросы для этого entity-региона. Вывод: Query Cache полезен только для read-heavy справочных таблиц, которые обновляются крайне редко. В высоконагруженных системах может принести больше вреда, чем пользы.

### 12.5. @NaturalId и кэширование

`@NaturalId` — бизнес-ключ (например, email). В отличие от `@Id`, естественные идентификаторы могут кэшироваться во L2:

```java
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class User {
    @Id private Long id;

    @NaturalId
    @Column(unique = true)
    private String email;
}

// Использование: загрузка через естественный ключ (обходит L2)
User user = session.byNaturalId(User.class).using("email", "john@example.com").load();
```

---

## 13. Блокировки и конкурентность

### 13.1. Оптимистичная блокировка (@Version)

Самый распространённый подход в JPA:

```java
@Entity
public class User {
    @Version
    private Long version;
}
```

При UPDATE генерируется: `UPDATE users SET ..., version = version + 1 WHERE id = ? AND version = ?`. Если другая транзакция уже обновила → `OptimisticLockException`.

**Плюсы**: нет блокировок БД, высокая производительность. **Минусы**: конфликты обрабатываются на уровне приложения.

### 13.2. Пессимистичные блокировки (@Lock)

Блокировка на уровне БД:

```java
@Lock(LockModeType.PESSIMISTIC_WRITE)
@Query("SELECT u FROM User u WHERE u.id = :id")
Optional<User> findByIdWithLock(@Param("id") Long id);
```

- **PESSIMISTIC_READ**: другие могут читать, не могут писать (shared lock)
- **PESSIMISTIC_WRITE**: другие не могут ни читать, ни писать (exclusive lock)
- **PESSIMISTIC_FORCE_INCREMENT**: exclusive lock + инкремент версии

**Минусы**: блокировки снижают конкурентность, риск deadlock.

### 13.3. LockModeType в JPA

| Тип | Механизм |
|---|---|
| `OPTIMISTIC` | Проверка `@Version` при коммите |
| `OPTIMISTIC_FORCE_INCREMENT` | Проверка + принудительный инкремент версии |
| `PESSIMISTIC_READ` | `SELECT ... FOR SHARE` |
| `PESSIMISTIC_WRITE` | `SELECT ... FOR UPDATE` |
| `PESSIMISTIC_FORCE_INCREMENT` | `SELECT ... FOR UPDATE` + инкремент версии |
| `NONE` | Без блокировки |

### 13.4. Как работает lock() в Hibernate?

`entityManager.lock(entity, LockModeType.PESSIMISTIC_WRITE)` — устанавливает блокировку на уровне БД.

**Что происходит на уровне SQL:**
- `PESSIMISTIC_READ` → `SELECT ... FOR SHARE` (PostgreSQL) / `SELECT ... LOCK IN SHARE MODE` (MySQL)
- `PESSIMISTIC_WRITE` → `SELECT ... FOR UPDATE` — эксклюзивная блокировка строки до конца транзакции
- `PESSIMISTIC_FORCE_INCREMENT` → `SELECT ... FOR UPDATE` + инкремент `@Version`

**Важные детали:**
- **Данные сущности НЕ перезагружаются**: `lock()` только устанавливает блокировку на уже загруженную строку. Поля сущности не обновляются из БД. Если нужно перечитать → `refresh()` отдельно.
- **Проверка версии**: для `OPTIMISTIC` / `OPTIMISTIC_FORCE_INCREMENT` проверяется актуальность `@Version` (совпадает ли с БД).
- **Влияние незакоммиченных изменений**: если сущность изменена в PC (грязная), `flush()` может быть вызван перед lock, чтобы синхронизировать состояние (зависит от `FlushMode`).
- **Deadlock**: если Транзакция А блокирует строку 1, затем строку 2; а Транзакция Б — строку 2, затем строку 1 → deadlock. БД разрешает его, убивая одну из транзакций → `LockAcquisitionException` / `PessimisticLockException`. Решение: всегда блокировать строки в одном порядке.

**Таймаут блокировки:**
```java
entityManager.lock(entity, LockModeType.PESSIMISTIC_WRITE,
    Map.of("jakarta.persistence.lock.timeout", 0));  // 0 = NOWAIT, сразу исключение если занято
```

**Диалектные различия:**
- PostgreSQL: `FOR UPDATE` / `FOR SHARE` / `FOR NO KEY UPDATE`
- MySQL: `FOR UPDATE` / `LOCK IN SHARE MODE` (InnoDB)
- Oracle: `FOR UPDATE` / `FOR UPDATE WAIT n`
- SQL Server: `WITH (UPDLOCK, ROWLOCK)`

### 13.5. @OptimisticLocking — стратегии оптимистичной блокировки

- `OptimisticLockType.VERSION` (по умолчанию): проверка по полю с `@Version`
- `OptimisticLockType.ALL`: проверка всех полей в WHERE-условии UPDATE
- `OptimisticLockType.DIRTY`: проверка только изменённых полей в WHERE
- `OptimisticLockType.NONE`: оптимистичная блокировка отключена

---

## 14. Equals/hashCode и версионирование

### 14.1. Проблема equals/hashCode в Hibernate

Главная проблема: когда сущность ещё не сохранена, её `id = null`. После `persist()` появляется id. Объект остаётся тем же, но `hashCode()` меняется → если объект был в `HashSet`/`HashMap`, он «потеряется».

**Решение — использовать бизнес-ключ:**

```java
@Entity
public class User {
    @Id @GeneratedValue private Long id;

    @NaturalId
    @Column(unique = true, nullable = false)
    private String email;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof User that)) return false;
        return Objects.equals(email, that.email);       // НЕ use id!
    }

    @Override
    public int hashCode() {
        return Objects.hash(email);                      // НЕ use id!
    }
}
```

**Правила:**
1. Не используйте `@Id` в equals/hashCode
2. Используйте бизнес-ключ (уникальное неизменяемое поле)
3. Если бизнес-ключа нет — используйте `instanceof` + сравнение по `id`, но осознавайте риски
4. Не используйте LAZY-ассоциации в equals/hashCode (они могут быть прокси)

### 14.2. @Version — детали

- Поле с `@Version` может быть: `int`, `long`, `Long`, `java.sql.Timestamp`
- Автоматически инкрементируется/обновляется при каждом UPDATE
- При `OPTIMISTIC_FORCE_INCREMENT` — инкрементируется даже при чтении
- `OptimisticLockException` оборачивается Spring в `ObjectOptimisticLockingFailureException` (подкласс `DataAccessException`)

---

## 15. Hibernate — расширенные аннотации

### 15.1. @Subselect

Маппит сущность на подзапрос (read-only по умолчанию):

```java
@Entity
@Subselect("SELECT u.id, u.name, COUNT(o.id) AS order_count " +
           "FROM users u LEFT JOIN orders o ON u.id = o.user_id " +
           "GROUP BY u.id, u.name")
@Synchronize({"users", "orders"})  // инвалидация кэша
public class UserSummary {
    @Id private Long id;
    private String name;
    private Long orderCount;
}
```

`@Synchronize` — при изменении таблиц `users` или `orders` Hibernate сбрасывает кэш.

### 15.2. @Immutable

Сущность неизменяема — Hibernate не выполняет UPDATE/DELETE, не хранит снимки для dirty checking, не проверяет изменения. Повышает производительность.

### 15.3. @NaturalId

Бизнес-ключ (альтернативный уникальный идентификатор):
- Может быть составным (`@NaturalId` на нескольких полях)
- Может быть mutable (`@NaturalId(mutable = true)`)
- Загружается быстрее через L2-кэш (без запроса к БД)

### 15.4. @DynamicUpdate и @DynamicInsert

- **@DynamicUpdate**: UPDATE содержит только изменённые поля (экономия на bandwidth, но CPU overhead на сравнение)
- **@DynamicInsert**: INSERT содержит только не-null поля (полезно при частичном создании через `@ColumnDefault`)
- **@SelectBeforeUpdate**: загружает текущее состояние перед UPDATE для сравнения (дорого, редко нужно)

### 15.5. @RowId

Включает поддержку Oracle ROWID / PostgreSQL ctid — физического идентификатора строки, который позволяет БД выполнять UPDATE/DELETE без поиска по индексу PK.

```java
@Entity
@RowId("ROWID")  // имя псевдо-колонки: ROWID для Oracle, ctid для PostgreSQL
public class SomeEntity {
    @Id private Long id;
    // ...
}
```

**Когда это даёт выигрыш:**
- Oracle: `UPDATE ... WHERE ROWID = ?` вместо `UPDATE ... WHERE id = ?` (быстрее, потому что ROWID — это физический указатель на блок данных)
- Актуально для таблиц без первичного ключа (legacy системы, логирование) или когда PK — составной/длинный
- В PostgreSQL не даёт значимого выигрыша (ctid меняется при UPDATE строки)

**Недостатки:**
- ROWID/ctid может измениться (реорганизация таблицы, VACUUM FULL) → Hibernate не узнает об этом
- Не переносимо между БД
- Редко нужно в современных приложениях с суррогатными ключами

### 15.6. @Check

Добавляет CHECK constraint на уровне БД (не на уровне Hibernate!):

```java
@Entity
@Check(constraints = "salary > 0 AND salary < 1000000")
public class Employee {
    private BigDecimal salary;
    private String department;
}

// Составные проверки:
@Entity
@Check(constraints = "start_date < end_date OR end_date IS NULL")
public class Contract {
    private LocalDate startDate;
    private LocalDate endDate;
}

// Несколько @Check:
@Entity
@Check(constraints = "price >= 0")
@Check(constraints = "quantity > 0")
public class Product {
    private BigDecimal price;
    private Integer quantity;
}
```

**Важно:** `@Check` влияет **только на генерацию DDL** (`hibernate.hbm2ddl.auto`). Hibernate не проверяет constraint перед выполнением INSERT/UPDATE — это делает БД, выбрасывая `ConstraintViolationException`. Для валидации на уровне приложения используйте Bean Validation (`@Min`, `@Max`, `@AssertTrue`).

**Типичная ошибка:** разработчики пишут `@Check(constraints = "status IN ('ACTIVE', 'INACTIVE')")` и ожидают что Hibernate это проверит, но DDL не генерируется (ddl-auto = validate/none), и constraint не применяется. На production constraint молча отсутствует.

### 15.7. @NotFound

Поведение при битой ссылке — FK ссылается на несуществующую запись:

```java
@Entity
public class Order {
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    @NotFound(action = NotFoundAction.IGNORE)  // если user не найден → поле будет null
    private User user;
}

@Entity
public class User {
    // ...
}
```

**Сценарии использования:**
- Legacy БД с отсутствующими FK-constraint-ами
- Интеграция с другой системой, где данные могут быть удалены в обход Hibernate
- Архивные таблицы с «битыми» ссылками на удалённые записи

**@NotFound(IGNORE) — как работает:**
```sql
-- Без @NotFound (по умолчанию EXCEPTION):
SELECT o.*, u.* FROM orders o LEFT JOIN users u ON o.user_id = u.id;
-- Если user не найден → EntityNotFoundException

-- С @NotFound(IGNORE):
SELECT o.* FROM orders o;  -- загружаем order
SELECT u.* FROM users u WHERE u.id = ?;  -- отдельно загружаем user
-- Если user не найден → order.user = null, исключения нет
```
Hibernate переключается на стратегию отдельных SELECT-ов вместо JOIN, потому что `LEFT JOIN` с отсутствующей строкой всё равно вернёт `null` для колонок users, и Hibernate не сможет отличить «нет user» от «user есть но все поля null».

**Минусы @NotFound(IGNORE):**
- Всегда EAGER для `@ManyToOne` (даже если указан LAZY) — Hibernate должен проверить, есть ли связанная сущность
- Отключает JOIN-ы для этой связи → N+1, если не использовать `JOIN FETCH` явно
- Маскирует проблемы целостности данных

---

## 16. Мягкое удаление и фильтры

### 16.1. @Where — простое мягкое удаление

```java
@Entity
@Where(clause = "deleted = false")
@SQLDelete(sql = "UPDATE users SET deleted = true WHERE id = ?")
public class User { ... }
```

Все запросы Hibernate к этой сущности автоматически добавляют `WHERE deleted = false`. Но НЕ работает для нативных запросов и ручных SQL.

### 16.2. @FilterDef и @Filter — динамические фильтры

Более гибкий механизм, чем `@Where`:

```java
@Entity
@FilterDef(name = "statusFilter",
    parameters = @ParamDef(name = "status", type = String.class))
@Filter(name = "statusFilter", condition = "status = :status")
public class User { ... }

// Активация:
session.enableFilter("statusFilter").setParameter("status", "ACTIVE");
```

Фильтр должен быть явно активирован в сессии. Можно активировать постоянно через AOP или Interceptor.

### 16.3. @FilterJoinTable

Применяет фильтр к join-таблице в `@ManyToMany`:

```java
@ManyToMany
@JoinTable(...)
@FilterJoinTable(name = "activeOnly", condition = "active = true")
private Set<Role> roles;
```

### 16.4. Мягкое удаление vs реальное удаление

**Мягкое удаление** (soft delete):
- `deleted = true` / `deleted_at = NOW()`
- Данные остаются, можно восстановить
- Усложняет все запросы и индексы (`WHERE deleted = false`)
- Проблемы с уникальными constraints (email должен быть уникальным среди активных)

**Реальное удаление** (hard delete):
- Данные удаляются физически
- Проще запросы и индексы
- Нужен аудит/логирование изменений отдельно

---

## 17. Производительность и пакетная обработка

### 17.1. JDBC Batching

Группировка INSERT/UPDATE/DELETE в пакеты для снижения round-trips к БД:

```properties
spring.jpa.properties.hibernate.jdbc.batch_size=50
spring.jpa.properties.hibernate.order_inserts=true
spring.jpa.properties.hibernate.order_updates=true
```

**Как это работает (детально):**

```
Без batching (batch_size не задан или = 0):
  Hibernate → JDBC Driver → БД:
    execute("INSERT INTO users ...")  → round-trip
    execute("INSERT INTO users ...")  → round-trip
    execute("INSERT INTO users ...")  → round-trip
  Итого: 3 round-trips для 3 INSERT-ов

С batching (batch_size=50):
  Hibernate → JDBC Driver:
    addBatch("INSERT INTO users ...")   // накапливаем в буфере
    addBatch("INSERT INTO users ...")
    addBatch("INSERT INTO users ...")
    executeBatch()  → round-trip (один на все 3 операции)
  Итого: 1 round-trip для 3 INSERT-ов
```

**`order_inserts` / `order_updates` критически важны:**

Без них Hibernate генерирует INSERT-ы в порядке вызова `persist()`. Если вставляются разные сущности вперемешку (User, Order, User, Order) → пакет прерывается при смене таблицы:

```
# Без order_inserts:
persist(user1)  → INSERT INTO users ...
persist(order1) → INSERT INTO orders ...  ← смена таблицы → пакет сбрасывается
persist(user2)  → INSERT INTO users ...   ← смена таблицы → пакет сбрасывается
persist(order2) → INSERT INTO orders ...
# Каждая операция — отдельный round-trip!

# С order_inserts=true:
persist(user1)  → (накапливаем)
persist(order1) → (накапливаем)
persist(user2)  → (накапливаем)
persist(order2) → (накапливаем)
flush() → executeBatch:
  INSERT INTO users (name) VALUES (?), (?)     -- user1, user2
  INSERT INTO orders (amount) VALUES (?), (?)  -- order1, order2
# 2 round-trips вместо 4
```

**IDENTITY-генерация ломает batching:**

```java
@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```

С IDENTITY Hibernate **обязан** выполнить INSERT немедленно (не при flush), чтобы получить сгенерированный ID. Каждый INSERT — отдельный round-trip:

```
# IDENTITY + JDBC Batching (batch_size=50):
persist(user1) → INSERT INTO users (name) VALUES ('User1')  ← немедленно, чтобы узнать ID
persist(user2) → INSERT INTO users (name) VALUES ('User2')  ← немедленно
# JDBC batching игнорируется! Каждая операция идёт отдельно.
```

Решение: `SEQUENCE` (PostgreSQL) или TABLE-генератор с pre-allocation.

**Оптимальная конфигурация batching:**
```properties
# application.properties (production)
spring.jpa.properties.hibernate.jdbc.batch_size=50
spring.jpa.properties.hibernate.order_inserts=true
spring.jpa.properties.hibernate.order_updates=true
spring.jpa.properties.hibernate.jdbc.batch_versioned_data=true  # batch-ить UPDATE с @Version

# Для массовой вставки — увеличить batch_size
spring.jpa.properties.hibernate.jdbc.batch_size=200

# ВАЖНО: переподключение к БД с параметром rewriteBatchedInserts (PostgreSQL)
# jdbc:postgresql://localhost:5432/db?reWriteBatchedInserts=true
# Без этого драйвер PostgreSQL не объединяет INSERT-ы в одну команду
```

**Проверка, что batching работает:**
```properties
# Включить статистику:
spring.jpa.properties.hibernate.generate_statistics=true
# После выполнения:
# Hibernate: insert into users (name) values (?) {heap size: 50}
# {heap size: 50} ← batch отправлен с 50 операциями!
```

Альтернативно можно логировать на уровне JDBC-драйвера (Datasource Proxy, p6spy).

**Обработка ошибок:** если одна из операций в пакете падает (constraint violation), поведение зависит от JDBC-драйвера:
- PostgreSQL: весь пакет откатывается (драйвер останавливает executeBatch при первой ошибке)
- Некоторые драйверы продолжают выполнение и возвращают массив с результатами по каждой операции

Конкретная строка-нарушитель может быть неочевидна. Для отладки временно уменьшите `batch_size` до 1.

### 17.2. StatelessSession

Сессия без Persistence Context: нет dirty checking, нет L1/L2-кэша, нет каскадных операций. Для массовой вставки:

```java
StatelessSession session = sessionFactory.openStatelessSession();
Transaction tx = session.beginTransaction();
for (User user : users) {
    session.insert(user);  // немедленный INSERT, без задержки до flush
}
tx.commit();
session.close();
```

### 17.3. ScrollableResults

Построчная обработка больших выборок без загрузки всего в память:

```java
try (Session session = sessionFactory.openSession()) {
    ScrollableResults<User> results = session
        .createQuery("FROM User", User.class)
        .setFetchSize(50)  // размер курсора
        .setCacheMode(CacheMode.IGNORE)  // не кэшировать
        .scroll(ScrollMode.FORWARD_ONLY);

    while (results.next()) {
        User user = results.get();
        process(user);
        session.evict(user);  // очистка из Persistence Context
    }
}
```

### 17.4. Read-only сущности

Для сущностей, которые только читаются:
- `@Immutable` на уровне класса
- `session.setDefaultReadOnly(true)` — вся сессия
- `session.setReadOnly(entity, true)` — конкретная сущность
- Отключает dirty checking, не хранит снимки

### 17.5. Профилирование запросов

```properties
# Логирование SQL
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.use_sql_comments=true

# Метрики
spring.jpa.properties.hibernate.generate_statistics=true
```

Анализ через `Statistics` MBean (JMX) или Actuator: количество запросов, попадания в кэш, время выполнения.

---

## 18. JPQL, Criteria API и нативные запросы

### 18.1. JPQL (Java Persistence Query Language)

Объектно-ориентированный язык запросов, оперирующий сущностями, а не таблицами:

```java
// Базовый
TypedQuery<User> query = em.createQuery(
    "SELECT u FROM User u WHERE u.email = :email", User.class);
query.setParameter("email", "test@example.com");

// JOIN FETCH (решение N+1)
List<User> users = em.createQuery(
    "SELECT DISTINCT u FROM User u JOIN FETCH u.orders", User.class)
    .getResultList();

// JPQL с конструктором DTO
List<UserDto> dtos = em.createQuery(
    "SELECT new com.example.UserDto(u.id, u.name) FROM User u", UserDto.class)
    .getResultList();
```

### 18.2. Criteria API

Программное построение запросов (typesafe, через `Metamodel`):

```java
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> root = cq.from(User.class);
cq.select(root)
  .where(cb.and(
      cb.equal(root.get("status"), "ACTIVE"),
      cb.like(root.get("name"), "%John%")
  ))
  .orderBy(cb.asc(root.get("createdAt")));

List<User> users = em.createQuery(cq).getResultList();
```

**Плюсы**: compile-time безопасность, динамическое построение, нет строковых JPQL. **Минусы**: многословный.

**Typesafe Criteria с Metamodel (рекомендуемый подход):**

JPA Static Metamodel генерирует классы `User_`, `Order_` и т.д., которые описывают атрибуты сущностей как типизированные поля. Это заменяет строковые литералы `"status"`, `"name"` на проверяемые компилятором ссылки:

```java
// Генерируется автоматически (Hibernate Metamodel Generator / Gradle / Maven):
@StaticMetamodel(User.class)
public abstract class User_ {
    public static volatile SingularAttribute<User, Long> id;
    public static volatile SingularAttribute<User, String> name;
    public static volatile SingularAttribute<User, String> email;
    public static volatile SingularAttribute<User, Status> status;
    public static volatile SingularAttribute<User, LocalDateTime> createdAt;
    public static volatile ListAttribute<User, Order> orders;
}

// Использование — без строковых литералов, полный type-safety:
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> root = cq.from(User.class);

cq.select(root)
  .where(cb.and(
      cb.equal(root.get(User_.status), Status.ACTIVE),  // ← тип Status, не Object!
      cb.like(root.get(User_.name), "%John%")
  ))
  .orderBy(cb.asc(root.get(User_.createdAt)));

List<User> users = em.createQuery(cq).getResultList();
```

**Настройка генерации Metamodel:**

```groovy
// build.gradle (Gradle)
dependencies {
    annotationProcessor 'org.hibernate.orm:hibernate-jpamodelgen:6.x.x'
}

// Для компиляции в IntelliJ IDEA:
// Settings → Build → Compiler → Annotation Processors → Enable annotation processing
```

**Сложный Criteria — JOIN, подзапросы, агрегация:**
```java
CriteriaBuilder cb = em.getCriteriaBuilder();

// 1. JOIN с условием:
CriteriaQuery<User> userQuery = cb.createQuery(User.class);
Root<User> userRoot = userQuery.from(User.class);
Join<User, Order> orderJoin = userRoot.join(User_.orders, JoinType.INNER);
orderJoin.on(cb.greaterThan(orderJoin.get(Order_.totalAmount), new BigDecimal("1000")));
userQuery.select(userRoot).distinct(true);

// 2. Подзапрос:
CriteriaQuery<User> subQuery = cb.createQuery(User.class);
Subquery<Long> sq = subQuery.subquery(Long.class);
Root<Order> orderRoot = sq.from(Order.class);
sq.select(cb.count(orderRoot))
  .where(cb.equal(orderRoot.get(Order_.user), userRoot));
cq.where(cb.greaterThan(sq, 3L));  // пользователи с >3 заказов

// 3. Агрегация + DTO:
CriteriaQuery<UserStatsDto> statsQuery = cb.createQuery(UserStatsDto.class);
Root<Order> orderRoot2 = statsQuery.from(Order.class);
Join<Order, User> userJoin = orderRoot2.join(Order_.user);

statsQuery.select(cb.construct(UserStatsDto.class,
    userJoin.get(User_.id),
    userJoin.get(User_.name),
    cb.count(orderRoot2),
    cb.sum(orderRoot2.get(Order_.totalAmount))
))
.groupBy(userJoin.get(User_.id), userJoin.get(User_.name));

// 4. Multi-select (без конструктора):
CriteriaQuery<Object[]> multiQuery = cb.createQuery(Object[].class);
Root<User> multiRoot = multiQuery.from(User.class);
multiQuery.multiselect(
    multiRoot.get(User_.id),
    multiRoot.get(User_.name),
    multiRoot.get(User_.email)
);
List<Object[]> results = em.createQuery(multiQuery).getResultList();
```

**CriteriaDelete / CriteriaUpdate (bulk operations):**
```java
// Аналог JPQL: UPDATE User u SET u.status = 'INACTIVE' WHERE u.lastLoginDate < :date
CriteriaUpdate<User> update = cb.createCriteriaUpdate(User.class);
Root<User> updateRoot = update.from(User.class);
update.set(User_.status, Status.INACTIVE)
      .where(cb.lessThan(updateRoot.get(User_.lastLoginDate),
                         LocalDateTime.now().minusYears(1)));

int updatedCount = em.createQuery(update).executeUpdate();
// Внимание: bulk update минует Persistence Context — см. раздел 3.6
```

**Когда использовать Criteria API:**
- ✅ Динамические фильтры (пользователь выбирает произвольный набор полей для поиска)
- ✅ Сложные условия, собираемые из нескольких частей (if-else ветвления)
- ✅ Type-safety критичен (рефакторинг сущностей)
- ❌ Простые статические запросы — избыточен, используйте JPQL или Spring Data JPA derived queries

### 18.3. Нативные SQL-запросы

```java
// С маппингом на сущность
Query query = em.createNativeQuery(
    "SELECT * FROM users WHERE status = :status", User.class);
query.setParameter("status", "ACTIVE");
List<User> users = query.getResultList();

// С SqlResultSetMapping
@SqlResultSetMapping(name = "UserDtoMapping",
    classes = @ConstructorResult(
        targetClass = UserDto.class,
        columns = {@ColumnResult(name = "id"), @ColumnResult(name = "name")}
    ))
// ...
List<UserDto> dtos = em.createNativeQuery("SELECT id, name FROM users", "UserDtoMapping")
    .getResultList();
```

### 18.4. Хранимые процедуры

```java
StoredProcedureQuery sp = em.createStoredProcedureQuery("GET_USER_COUNT");
sp.registerStoredProcedureParameter("result", Integer.class, ParameterMode.OUT);
sp.execute();
Integer count = (Integer) sp.getOutputParameterValue("result");
```

В Spring Data JPA: `@Procedure("GET_USER_COUNT") Integer getUserCount();`

### 18.5. @NamedQuery и @NamedNativeQuery

```java
@Entity
@NamedQuery(name = "User.findByEmail",
    query = "SELECT u FROM User u WHERE u.email = :email")
@NamedNativeQuery(name = "User.findActive",
    query = "SELECT * FROM users WHERE status = 'ACTIVE'",
    resultClass = User.class)
public class User { }

// Использование:
em.createNamedQuery("User.findByEmail", User.class)
  .setParameter("email", "test@example.com")
  .getSingleResult();
```

---

## 19. Callback-и и Event Listener-ы

### 19.1. JPA Entity Listeners и callback-аннотации

Выполняются на определённых событиях жизненного цикла сущности:

| Аннотация | Когда вызывается |
|---|---|
| `@PrePersist` | До INSERT |
| `@PostPersist` | После INSERT |
| `@PreUpdate` | До UPDATE |
| `@PostUpdate` | После UPDATE |
| `@PreRemove` | До DELETE |
| `@PostRemove` | После DELETE |
| `@PostLoad` | После SELECT/загрузки |

### 19.2. Два способа использования

**Внутри сущности:**

```java
@Entity
public class User {
    @PrePersist
    public void beforeSave() {
        this.createdAt = LocalDateTime.now();
    }
}
```

**Внешний слушатель (рекомендуется):**

```java
public class UserListener {
    @PrePersist
    public void beforeSave(User user) {
        user.setCreatedAt(LocalDateTime.now());
    }
}

@Entity
@EntityListeners(UserListener.class)
public class User { ... }
```

### 19.3. AuditingEntityListener (Spring Data)

Специализированный слушатель для аудита:

```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    @CreatedDate private LocalDateTime createdAt;
    @LastModifiedDate private LocalDateTime updatedAt;
    @CreatedBy private String createdBy;
    @LastModifiedBy private String updatedBy;
}
```

Требует `@EnableJpaAuditing` и `AuditorAware` бин (для `@CreatedBy` / `@LastModifiedBy`).

### 19.4. Hibernate Interceptor

Более низкоуровневый механизм, чем JPA callback-и. Позволяет перехватывать операции на уровне Session:

```java
public class AuditInterceptor extends EmptyInterceptor {
    @Override
    public boolean onSave(Object entity, ...) {
        if (entity instanceof Auditable a) {
            a.setCreatedAt(Instant.now());
        }
        return false;  // false = не изменять состояние
    }

    @Override
    public boolean onFlushDirty(Object entity, ...) { ... }
}

// Регистрация:
Session session = sessionFactory.withOptions().interceptor(new AuditInterceptor()).openSession();
```

Interceptor работает для всех сущностей, может модифицировать SQL, состояние объектов. Но сложнее в использовании, чем Entity Listeners.

### 19.5. Порядок вызова callback-ов

Для одного события (`@PrePersist`):
1. `@EntityListeners` — внешние слушатели (в порядке объявления)
2. Методы самой сущности с аннотацией
3. Методы `@MappedSuperclass` (если есть)
4. `default` методы интерфейсов (JPA 2.2+)

---

## 20. Транзакции в Hibernate

### 20.1. Как @Transactional работает с Hibernate

1. Spring AOP создаёт прокси вокруг бина
2. При вызове метода с `@Transactional`:
   - `JpaTransactionManager` получает `EntityManager` из `EntityManagerFactory`
   - Привязывает EntityManager к текущей транзакции (через `TransactionSynchronizationManager`)
   - Начинает транзакцию БД: `entityManager.getTransaction().begin()`
3. После выполнения метода:
   - Успех: `flush()` → `commit()`
   - Исключение (unchecked): `rollback()`
4. EntityManager закрывается или возвращается в пул

### 20.2. propagation = REQUIRES_NEW с Hibernate

**Механизм приостановки (suspension):**

`TransactionSynchronizationManager` хранит ресурсы (EntityManager, Connection) в `ThreadLocal<Map<Object, Object>>`. При REQUIRES_NEW:

```
1. Сохранить текущее состояние TransactionSynchronizationManager
   → suspend(): выгрузить ресурсы из ThreadLocal, сохранить в SuspendedResourcesHolder
2. Создать новый EntityManager (из EntityManagerFactory)
3. Начать новую транзакцию БД
4. Привязать новый EntityManager к TransactionSynchronizationManager
5. Выполнить внутренний метод
6. Закоммитить/откатить → закрыть новый EntityManager
7. resume(): восстановить сохранённое состояние TransactionSynchronizationManager
   → старый EntityManager снова активен
```

**Что это означает на практике:**

- **Разные Persistence Context**: внутренний метод работает со своим EntityManager (своя Identity Map). Сущности, загруженные во внешнем EM, не видны во внутреннем (и наоборот).
- **Изменения изолированы**: если внутренняя транзакция закоммитилась, данные в БД, но внешний EM об этом не знает. Его снимки (`loadedState`) устарели.
- **Риск `OptimisticLockException`**: если оба EM меняют одну строку → при коммите внешней транзакции `@Version` уже изменён внутренней → исключение.

**Self-invocation pitfall (важнейший нюанс):**

```java
@Service
public class OrderService {
    @Transactional
    public void createOrder(Order order) {
        // REQUIRED
        auditLog("Order created");  // ← self-invocation! Прокси не срабатывает!
    }

    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void auditLog(String message) {
        // Этот метод выполняется в той же транзакции, что и createOrder()
        // потому что вызов идёт через this, а не через прокси
    }
}
```

**Правильное решение:** вынести auditLog в отдельный бин:

```java
@Service
public class AuditService {
    @Transactional(propagation = Propagation.REQUIRES_NEW)
    public void log(String message) { ... }
}

@Service
public class OrderService {
    @Autowired private AuditService auditService;  // ← внедрение через Spring

    @Transactional
    public void createOrder(Order order) {
        auditService.log("Order created");  // ← вызов через прокси → REQUIRES_NEW работает
    }
}
```

**Когда использовать REQUIRES_NEW:**
- Аудит/логирование (не должен откатываться с бизнес-ошибкой)
- Отправка уведомлений (email, push)
- Идемпотентная запись в отдельную БД/таблицу
- Не использовать для бизнес-логики, связанной с текущей операцией

### 20.3. propagation = NESTED с Hibernate

**JPA + Hibernate НЕ поддерживают NESTED напрямую.** JPA не имеет savepoints. NESTED работает только через JDBC-соединение (обход JPA):

```java
// Только через нативный JDBC внутри JPA-транзакции:
Session session = entityManager.unwrap(Session.class);
session.doWork(connection -> {
    Savepoint sp = connection.setSavepoint();
    try { /* ... */ } catch (Exception e) {
        connection.rollback(sp);
    }
});
```

### 20.4. @Transactional(readOnly = true) — что именно делает Hibernate

1. **Отключает dirty checking**: `session.setDefaultReadOnly(true)` — сущности не проверяются на изменения, снимки не делаются
2. **FlushMode.MANUAL**: flush не вызывается автоматически перед запросами
3. **JDBC Connection**: может быть помечен как read-only на уровне пула соединений
4. Оптимизация для мастер-слейв маршрутизации (Spring может направить read-only транзакции на реплику)

### 20.5. SharedEntityManagerCreator — как Spring управляет EntityManager

Spring не использует реальный EntityManager напрямую в singleton-бинах. Вместо этого `@PersistenceContext` внедряет прокси (`SharedEntityManagerCreator`), который:
1. При вызове метода проверяет: есть ли активная транзакция?
2. Если да — возвращает EntityManager, привязанный к транзакции (через `TransactionSynchronizationManager`)
3. Если нет — создаёт временный EntityManager (закрывается после операции)
4. Это обеспечивает потокобезопасность и привязку к транзакциям

---

## 21. Hibernate 6 — изменения и новые возможности

### 21.1. Основные изменения в Hibernate 6

- **Jakarta EE 9+**: пакеты `javax.persistence` → `jakarta.persistence`. Это breaking change — все импорты нужно обновить. В Spring Boot 3+ используется Hibernate 6 с Jakarta.
- **SQM (Semantic Query Model)**: полностью новый внутренний движок запросов, заменяющий старый интерпретатор JPQL/Criteria. SQM сначала строит семантическое дерево запроса, потом транслирует его в SQL. Это даёт:
  - Улучшенную обработку ошибок (ошибки в JPQL точнее указывают на проблемное место)
  - Поддержку более сложных SQL-конструкций (оконные функции, CTE, LATERAL JOIN)
  - Единый путь для JPQL и Criteria API (раньше они обрабатывались разными частями кода, что приводило к расхождениям)
- **Новый Sequence Naming**: стратегия именования последовательностей изменилась. Раньше `@SequenceGenerator` генерировал имя `hibernate_sequence` по умолчанию. В Hibernate 6 используется `SEQUENCE` по умолчанию с именем `<table_name>_seq`. При миграции с Hibernate 5 → 6 проверьте имена последовательностей!
- **UUID-генерация**: `@GeneratedValue(strategy = GenerationType.UUID)` теперь автоматически выбирает бинарное хранение (BINARY(16)) вместо VARCHAR(36), что компактнее и быстрее. Поддержка UUID v7 (time-ordered) для лучшей индексации B-tree.
- **Типы дат**: улучшена работа с `java.time`, встроенная поддержка `Duration` и `Period` как базовых типов (раньше требовался `@Type` или AttributeConverter):
  ```java
  @Entity
  public class Event {
      private Duration duration;      // маппится на INTERVAL (PostgreSQL) / BIGINT (MySQL — в секундах)
      private Period recurrencePeriod; // маппится на INTERVAL или VARCHAR
  }
  ```
- **HQL расширен**: оконные функции (`ROW_NUMBER()`, `RANK()`, `LAG()`, `LEAD()`), операции над множествами (`INTERSECT`, `EXCEPT`), `LATERAL JOIN`:
  ```java
  // HQL с оконной функцией (Hibernate 6):
  List<Order> latestOrders = em.createQuery(
      "SELECT o FROM (" +
      "  SELECT o2, ROW_NUMBER() OVER (PARTITION BY o2.user.id ORDER BY o2.createdAt DESC) AS rn " +
      "  FROM Order o2" +
      ") WHERE rn = 1", Order.class)
      .getResultList();
  ```
- **Gradle/Maven Plugin**: AOT-генерация метамодели (Static Metamodel) и валидация JPQL/Criteria на этапе компиляции
- **Отказ от deprecated API**: удалены `hibernate.query.startup_check`, старые сигнатуры `Session.load()`/`Session.save()`, `Type` (заменён на `@JdbcType`/`@JdbcTypeCode`), `@TypeDef`
- **Batch-оптимизации**: автоматический ordering INSERT/UPDATE (раньше нужно было включать `hibernate.order_inserts=true` явно), улучшен JDBC batching для SEQUENCE-стратегий
- **Multi-tenancy**: улучшена поддержка tenant-per-database и tenant-per-schema, включая автоматическое разрешение tenant-а через контекст
- **High-Low генератор** (новый): альтернатива TABLE-генератору для ID, эффективнее за счёт pre-allocation без блокировки на каждую вставку

**Ключевые различия Hibernate 5 → 6 для миграции:**

| Аспект | Hibernate 5 | Hibernate 6 |
|---|---|---|
| Пакеты | `javax.persistence` | `jakarta.persistence` |
| Генерация ID | `@GenericGenerator` | `@IdGeneratorType` (новый SPI) |
| Типы | `@Type(type = "yes_no")` | `@JdbcTypeCode(SqlTypes.CHAR)` |
| Sequence naming | `hibernate_sequence` (default) | `<table>_seq` (default) |
| Duration/Period | Требуется конвертер | Встроенная поддержка |
| HQL функции | Базовые | Оконные, INTERSECT, EXCEPT, LATERAL |
| Bytecode enhancement | Отдельный плагин | Встроен в hibernate-core |
| `@Filter` | Не работает с `@OneToMany` sub-select | Починено |
| Array/Collection параметры | Не поддерживаются | `WHERE u.id IN :ids` — `ids` может быть `List<Long>` в JPQL |

### 21.2. Составные ключи (@IdClass vs @EmbeddedId)

**@IdClass** — класс-ключ с полями, дублирующими поля сущности:

```java
@IdClass(UserPK.class)
@Entity
public class User {
    @Id private String department;
    @Id private Long employeeId;
    private String name;
}

public class UserPK implements Serializable {
    private String department;
    private Long employeeId;
    // equals() + hashCode()
}
```

**@EmbeddedId** — встроенный объект-ключ:

```java
@Entity
public class User {
    @EmbeddedId
    private UserPK pk;
    private String name;
}

@Embeddable
public class UserPK implements Serializable {
    private String department;
    private Long employeeId;
    // equals() + hashCode()
}
```

| Характеристика | @IdClass | @EmbeddedId |
|---|---|---|
| Поля ключа | Дублируются в сущности и классе-ключе | Только во встроенном классе |
| JPQL-доступ | `SELECT u.department FROM User u` | `SELECT u.pk.department FROM User u` |
| Использование | Проще для ручного поиска | Инкапсуляция, чище код |
| Выбор | Когда нужен простой доступ к полям ключа | Когда ключ используется как объект (DTO, кэш) |
