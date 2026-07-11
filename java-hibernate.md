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

В Spring Boot 99% времени вы работаете через `EntityManager` — это «правильный» путь, не привязывающий вас к конкретному провайдеру. Но если очень нужно достать Hibernate-специфичную функциональность: `entityManager.unwrap(Session.class)`.

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

- **@Entity**: помечает класс как сущность JPA. Обязательно.
- **@Table(name = "...")**: имя таблицы в БД (по умолчанию = имя класса). Дополнительно: `catalog`, `schema`, `uniqueConstraints`, `indexes`.

### 4.2. @Id и стратегии генерации (@GeneratedValue)

- **@Id**: первичный ключ
- **@GeneratedValue(strategy = ...)**:

| Стратегия | Описание | Реализация |
|---|---|---|
| `AUTO` (по умолчанию) | Hibernate выбирает сам | Зависит от диалекта |
| `IDENTITY` | AUTO_INCREMENT / SERIAL | БД генерирует при INSERT |
| `SEQUENCE` | Последовательность БД | `@SequenceGenerator` |
| `TABLE` | Таблица для генерации ID | Медленная, не рекомендуется |
| `UUID` | UUID v4 / v7 | `@GenericGenerator` |

**Что выбрать:**
- PostgreSQL → `SEQUENCE` (через `@SequenceGenerator`) — эффективная пакетная вставка
- MySQL → `IDENTITY` — но ограничивает JDBC batching (нельзя batch-ить INSERT с IDENTITY)
- UUID → когда нужна распределённая генерация (микросервисы без общей БД)

### 4.3. @Column

Основные атрибуты: `name`, `nullable`, `unique`, `length`, `precision`/`scale` (для `BigDecimal`), `columnDefinition` (DDL-фрагмент), `insertable`/`updatable` (исключение из INSERT/UPDATE).

### 4.4. @Transient, @Formula, @Enumerated, @Lob

- **@Transient**: поле НЕ маппится на колонку
- **@Formula("count(*) ...")** (Hibernate): вычисляемое поле на уровне БД (только чтение)
- **@Enumerated(EnumType.STRING)**: enum → строка (рекомендуется; `ORDINAL` — порядковый номер, опасно при изменении enum)
- **@Lob**: большие объекты (CLOB — текст, BLOB — бинарные)

---

## 5. Маппинг связей (@OneToOne, @ManyToOne, @OneToMany, @ManyToMany)

### 5.1. @ManyToOne и @OneToMany

Самая распространённая связь. `@ManyToOne` — сторона-владелец (внешний ключ). `@OneToMany(mappedBy = "...")` — обратная сторона.

```java
@Entity
public class Order {
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id")
    private User user;
}

@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Order> orders = new ArrayList<>();
}
```

### 5.2. @OneToOne

Использует `@JoinColumn` на владеющей стороне (где FK). Уникальность FK гарантирует связь 1:1.

```java
@Entity
public class User {
    @OneToOne(mappedBy = "user", cascade = CascadeType.ALL)
    private Profile profile;
}

@Entity
public class Profile {
    @OneToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "user_id", unique = true)
    private User user;
}
```

Проблема ленивой загрузки для `@OneToOne`: Hibernate не знает, есть ли связанная сущность, не заглянув в БД (FK на Profile — в таблице users или наоборот?). Поэтому `@OneToOne` часто загружается EAGER даже с `FetchType.LAZY`. Обход: `@LazyToOne(LazyToOneOption.NO_PROXY)` (bytecode enhancement), либо `@OneToOne` с `@MapsId`.

### 5.3. @ManyToMany

Использует промежуточную таблицу (`@JoinTable`):

```java
@Entity
public class Student {
    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();
}

@Entity
public class Course {
    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();
}
```

**Когда не стоит использовать `@ManyToMany`**: если нужны дополнительные поля в промежуточной таблице (дата записи, оценка). Тогда разбиваем на `@OneToMany → JoinEntity → @ManyToOne`.

### 5.4. FetchType: LAZY vs EAGER

- **@ManyToOne**: по умолчанию **EAGER** (опасно — N+1!). Всегда переопределяйте на `LAZY`.
- **@OneToMany**: по умолчанию **LAZY**.
- **@OneToOne**: по умолчанию **EAGER**.
- **@ManyToMany**: по умолчанию **LAZY**.

**Правило**: всегда используйте `FetchType.LAZY` для всех связей. EAGER — только когда связь 100% всегда нужна и содержит 1-2 записи.

---

## 6. Cascade, orphanRemoval и владение связью

### 6.1. Cascade-типы

Определяют, какие операции распространяются на связанные сущности:

- **PERSIST**: при сохранении родителя — сохранить детей
- **MERGE**: при merge родителя — merge детей
- **REMOVE**: при удалении родителя — удалить детей
- **REFRESH**: при refresh родителя — refresh детей
- **DETACH**: при detach родителя — detach детей
- **ALL** = все вышеперечисленные

### 6.2. orphanRemoval = true

Отличие от `CascadeType.REMOVE`:
- `orphanRemoval = true`: удалить ребёнка, если он удалён из коллекции родителя (но сам родитель остаётся)
- `CascadeType.REMOVE`: удалить ребёнка при удалении родителя

Часто используются вместе: `cascade = CascadeType.ALL, orphanRemoval = true`.

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

**Синхронизация**: всегда обновляйте обе стороны связи:

```java
public void addOrder(Order order) {
    orders.add(order);          // обратная сторона
    order.setUser(this);        // сторона-владелец (важно!)
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
2. Все геттеры переопределяются: при первом вызове → загрузка из БД → вызов геттера суперкласса
3. При повторном вызове — данные уже загружены
4. Идентификатор сущности (`@Id`) доступен без инициализации

### 9.2. HibernateProxy и Hibernate.initialize()

- `HibernateProxy` — интерфейс, реализуемый всеми прокси
- `Hibernate.initialize(proxy)` — принудительная инициализация прокси
- `Hibernate.isInitialized(proxy)` — проверка, загружены ли данные
- `entity instanceof HibernateProxy` — проверка, является ли объект прокси

### 9.3. LazyInitializationException

Самое известное исключение Hibernate. Возникает при попытке доступа к ленивому полю/связи **после** закрытия Session.

```java
// Ошибка:
User user = repo.findById(1L); // Session закрылась
user.getOrders(); // LazyInitializationException!
```

**Решения:**
1. Загрузить связь внутри транзакции: `JOIN FETCH`, `@EntityGraph`, `Hibernate.initialize()`
2. Использовать Open Session in View (OSIV) — антипаттерн; оставляет сессию открытой до конца HTTP-запроса
3. DTO-проекции: не возвращать сущности из сервисного слоя
4. `spring.jpa.open-in-view=false` + явная загрузка связей

### 9.4. Проблемы с equals/hashCode и прокси

Прокси — это подкласс. Сравнение через `equals()`/`hashCode()` с прокси требует аккуратности. См. раздел 14.

### 9.5. Сериализация прокси

Прокси Hibernate не предназначены для сериализации (Jackson, HTTP-сессии). При попытке сериализовать неинициализированный прокси:
- Jackson: невозможно сериализовать (нет данных) → `LazyInitializationException` или исключение Jackson
- Решение: использовать DTO, `@JsonIgnore` на LAZY-полях, либо загружать данные явно

---

## 10. Наследование в JPA

### 10.1. Стратегии наследования

**@Inheritance(strategy = ...)**:

| Стратегия | Как хранится | Плюсы | Минусы |
|---|---|---|---|
| `SINGLE_TABLE` | Все классы в одной таблице + `@DiscriminatorColumn` | Максимальная производительность | Много NULL-ов, нарушение нормализации |
| `TABLE_PER_CLASS` | Каждый конкретный класс — отдельная таблица со всеми полями | Нет JOIN-ов | Дублирование, полиморфные запросы через UNION |
| `JOINED` | Каждый класс в своей таблице, JOIN по PK | Нормализация, чистые данные | JOIN-ы, ниже производительность |

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

`@ElementCollection` всегда LAZY и не может быть запрошена отдельно как сущность. Не поддерживает identity (id). Для сложных коллекций лучше создавать отдельную сущность.

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
- **Caffeine** — высокопроизводительный in-memory (современная замена EhCache)

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

Включает поддержку Oracle ROWID / PostgreSQL ctid для более быстрых UPDATE/DELETE. Актуально только для таблиц без первичного ключа.

### 15.6. @Check

Добавляет CHECK constraint на уровне БД:

```java
@Entity
@Check(constraints = "salary > 0 AND department IS NOT NULL")
public class Employee { ... }
```

### 15.7. @NotFound

Поведение при битой ссылке (FK ссылается на несуществующую запись):
- `NotFoundAction.IGNORE` — проигнорировать (поле будет null)
- `NotFoundAction.EXCEPTION` — исключение (по умолчанию)

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

**Как это работает:**
1. Hibernate накапливает PreparedStatement-ы в пакете
2. Когда накоплено `batch_size` операций для одной таблицы → отправляет batch-execute в БД
3. Пакет также отправляется при: смене таблицы, SELECT между DML, коммите

**`order_inserts` / `order_updates` критически важны:** без них Hibernate генерирует INSERT-ы в порядке вызова `persist()`. Если вставляются разные сущности вперемешку (User, Order, User, Order) → пакет не формируется. `order_inserts=true` группирует INSERT-ы по таблицам → все User, потом все Order.

**IDENTITY-генерация ломает batching:**
```java
@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```
С IDENTITY Hibernate **обязан** выполнить INSERT немедленно (не при flush), чтобы получить сгенерированный ID. Каждый INSERT — отдельный round-trip. Batching невозможен. Решение: `SEQUENCE` (PostgreSQL) или `TABLE`-генератор с pre-allocation.

**Проверка, что batching работает:**
- Включить `hibernate.generate_statistics=true`
- Проверить лог: `Hibernate: insert into ... values (?, ?) {heap size: 50}` — batch отправлен
- Альтернатива: `p6spy` или логирование на уровне JDBC-драйвера

**Обработка ошибок:** если одна из операций в пакете падает (constraint violation), весь пакет откатывается. Конкретная строка-нарушитель может быть неочевидна (зависит от драйвера).

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

- **Jakarta EE 9+**: пакеты `javax.persistence` → `jakarta.persistence`
- **Новый Sequence Naming**: стратегия именования последовательностей изменилась (может сломать миграцию)
- **UUID-генерация**: переработана, `@GeneratedValue` с UUID даёт оптимизированное хранение в БД
- **Типы дат**: улучшена работа с `java.time`, встроенная поддержка `Duration` и `Period`
- **SQM (Semantic Query Model)**: новый внутренний движок запросов, заменяющий старый Criteria API runtime
- **HQL расширен**: оконные функции, `INTERSECT`/`EXCEPT`, `LATERAL JOIN`
- **Gradle/Maven Plugin**: AOT-генерация метамодели (Static Metamodel)
- **Отказ от deprecated API**: удалены `hibernate.query.startup_check`, старые `Session.load()`/`Session.save()` со старыми сигнатурами
- **Batch-оптимизации**: автоматический ordering INSERT/UPDATE, улучшен JDBC batching
- **Multi-tenancy**: улучшена поддержка tenant-per-database и tenant-per-schema

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
