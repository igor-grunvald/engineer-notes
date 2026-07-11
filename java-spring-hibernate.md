# Java Spring & Hibernate — Вопросы и ответы

---

## Оглавление

1. [IoC, DI и основы Spring](#1-ioc-di-и-основы-spring)
2. [Spring Boot — основы](#2-spring-boot--основы)
3. [Spring Boot — автоконфигурация и стартеры](#3-spring-boot--автоконфигурация-и-стартеры)
4. [Spring Boot — запуск и жизненный цикл](#4-spring-boot--запуск-и-жизненный-цикл)
5. [Spring Boot — конфигурация и свойства](#5-spring-boot--конфигурация-и-свойства)
6. [Spring Boot — встроенные серверы](#6-spring-boot--встроенные-серверы)
7. [Spring Boot — Actuator и мониторинг](#7-spring-boot--actuator-и-мониторинг)
8. [Spring Boot — Native Image (GraalVM)](#8-spring-boot--native-image-graalvm)
9. [Spring Context и жизненный цикл бинов](#9-spring-context-и-жизненный-цикл-бинов)
10. [BeanFactory, ApplicationContext, BeanPostProcessor](#10-beanfactory-applicationcontext-beanpostprocessor)
11. [Scopes, прокси и циклические зависимости](#11-scopes-прокси-и-циклические-зависимости)
12. [Конфигурация (@Configuration, @Bean, @Import)](#12-конфигурация-configuration-bean-import)
13. [Аннотации и их обработка](#13-аннотации-и-их-обработка)
14. [Профили (@Profile)](#14-профили-profile)
15. [AOP (Aspect-Oriented Programming)](#15-aop-aspect-oriented-programming)
16. [Транзакции (@Transactional)](#16-транзакции-transactional)
17. [Блокировки и конкурентность](#17-блокировки-и-конкурентность)
18. [Spring MVC — основы](#18-spring-mvc--основы)
19. [Spring MVC — контроллеры и обработка запросов](#19-spring-mvc--контроллеры-и-обработка-запросов)
20. [Spring MVC — валидация и обработка ошибок](#20-spring-mvc--валидация-и-обработка-ошибок)
21. [Spring MVC — CORS, сессии, фильтры](#21-spring-mvc--cors-сессии-фильтры)
22. [Spring Security — аутентификация](#22-spring-security--аутентификация)
23. [Spring Security — авторизация и защита](#23-spring-security--авторизация-и-защита)
24. [Spring Security — OAuth2 / JWT](#24-spring-security--oauth2--jwt)
25. [Spring Data JPA — основы](#25-spring-data-jpa--основы)
26. [Spring Data JPA — запросы и оптимизация](#26-spring-data-jpa--запросы-и-оптимизация)
27. [Spring Data JPA — N+1, EntityGraph, Batch](#27-spring-data-jpa--n1-entitygraph-batch)
28. [Spring Data JPA — репозитории под капотом](#28-spring-data-jpa--репозитории-под-капотом)
29. [Hibernate — EntityManager и Persistence Context](#29-hibernate--entitymanager-и-persistence-context)
30. [Hibernate — маппинг связей (@OneToOne, @ManyToOne)](#30-hibernate--маппинг-связей-onetoone-manytoone)
31. [Hibernate — наследование, фильтры, мягкое удаление](#31-hibernate--наследование-фильтры-мягкое-удаление)
32. [Hibernate — кэширование (L1, L2)](#32-hibernate--кэширование-l1-l2)
33. [Hibernate — equals/hashCode, версионирование](#33-hibernate--equalshashcode-версионирование)
34. [Hibernate — производительность и пакетная обработка](#34-hibernate--производительность-и-пакетная-обработка)
35. [Кэширование в Spring (@Cacheable)](#35-кэширование-в-spring-cacheable)
36. [Асинхронность (@Async, @Scheduled)](#36-асинхронность-async-scheduled)
37. [Пул соединений (HikariCP)](#37-пул-соединений-hikaricp)
38. [Тестирование Spring-приложений](#38-тестирование-spring-приложений)
39. [Spring Batch](#39-spring-batch)
40. [Spring Integration](#40-spring-integration)
41. [Spring Cloud — микросервисы](#41-spring-cloud--микросервисы)
42. [Spring Cloud — Config, Gateway, Tracing](#42-spring-cloud--config-gateway-tracing)
43. [Spring GraphQL](#43-spring-graphql)
44. [Spring Data — NoSQL (MongoDB, Redis, Elasticsearch)](#44-spring-data--nosql-mongodb-redis-elasticsearch)
45. [Spring — реактивное программирование (WebFlux, R2DBC)](#45-spring--реактивное-программирование-webflux-r2dbc)
46. [Spring — интеграция с Kafka / RabbitMQ](#46-spring--интеграция-с-kafka--rabbitmq)
47. [Spring — gRPC, Kotlin Coroutines](#47-spring--grpc-kotlin-coroutines)
48. [Micrometer и мониторинг](#48-micrometer-и-мониторинг)
49. [Разное (SpEL, @Value, @Lookup, @EventListener)](#49-разное-spel-value-lookup-eventlistener)

---

## 1. IoC, DI и основы Spring

### 1. Что такое IoC (Inversion of Control) и DI (Dependency Injection)?

**IoC**: Это принцип перекладывания ответственности за создание объектов и управление их жизненным циклом с программиста на фреймворк (контейнер). Вместо `new Service()`, контейнер сам создает экземпляр.

**DI (Dependency Injection)**: Это конкретная реализация IoC. Контейнер "впрыскивает" необходимые зависимости в объект.

### 2. Какие есть способы внедрения зависимостей в Spring (@Autowired, конструктор, сеттер)?

- **Конструктор (Best Practice)**: Позволяет создавать неизменяемые (`final`) поля, гарантирует, что объект не будет создан в невалидном состоянии, упрощает unit-тестирование (не нужен Spring Context).
- **Сеттер**: Полезен для опциональных зависимостей, которые можно менять в runtime.
- **Поле (@Autowired)**: Не рекомендуется. Усложняет тестирование (нужна рефлексия) и скрывает зависимости класса.

### 3. Чем @Component, @Service, @Repository, @Controller отличаются?

Технически все они являются мета-аннотациями над `@Component` и регистрируют бин в контексте. Различия семантические и функциональные:

- **@Component**: Базовая аннотация для любого управляемого компонента.
- **@Service**: Указывает на слой бизнес-логики (фасад). Дополнительной логики пока не несет.
- **@Repository**: Указывает на слой доступа к данным. Включает механизм автоматической трансляции низкоуровневых исключений (SQL/JPA) в `DataAccessException` Spring.
- **@Controller**: Указывает на веб-компонент. Используется `DispatcherServlet`'ом для маппинга запросов.

### 80. В чем разница между аннотациями @Component, @Service, @Repository и @Controller?

Все эти аннотации являются стереотипами (stereotypes). Технически, `@Component` — это родительская мета-аннотация, а остальные — ее специализации.

- **@Component**: Базовая аннотация. Обозначает, что класс является управляемым компонентом (бином) и должен быть создан Spring-контейнером при сканировании (component scanning).
- **@Service**: Специализация `@Component`. Используется для классов сервисного слоя (бизнес-логика). На данный момент она не добавляет дополнительной технической логики по сравнению с `@Component`, но важна семантически для разделения слоев приложения.
- **@Repository**: Специализация для слоя доступа к данным (DAO). Ключевое отличие: Она активирует механизм трансляции исключений (Exception Translation). Специфические исключения базы данных (например, `SQLException` или Hibernate-исключения) оборачиваются в унифицированные исключения Spring `DataAccessException`.
- **@Controller**: Специализация для веб-слоя (Spring MVC). Ключевое отличие: Помечает класс как обработчик веб-запросов. Используется вместе с `@RequestMapping`.

### 79. Как работает механизм Dependency Injection в Spring?

В общем виде: Контейнер управляет ссылками. Вы описываете зависимости (в коде или XML), а контейнер при старте строит граф зависимостей, создает объекты в правильном порядке и "впрыскивает" (injects) их друг в друга через Reflection.

### 83. Как работает @Autowired и какие способы инъекции зависимостей поддерживает Spring?

`@Autowired` — это механизм автоматического связывания. Spring ищет подходящий бин в контексте и внедряет его.

**Алгоритм поиска:**
1. По типу (Class type)
2. Если найдено несколько бинов одного типа — по имени поля или параметра (либо по `@Qualifier`).

**Способы инъекции:**
- **Через конструктор (Constructor Injection)**: Рекомендуемый способ. Позволяет делать поля `final` (иммутабельность). Гарантирует, что объект не будет создан в неполном состоянии. Начиная со Spring 4.3, аннотация `@Autowired` необязательна, если конструктор один.
- **Через сеттер (Setter Injection)**: Полезно для опциональных зависимостей. Зависимости могут быть изменены после создания.
- **Через поле (Field Injection)**: Не рекомендуется. Сложно тестировать (нужен Reflection или Spring Context в тестах). Скрывает зависимости класса.

### 46. Какой бин создастся, если есть два @Bean одного типа?

Spring выбросит `NoUniqueBeanDefinitionException` при запуске, если вы попытаетесь заинжектить этот тип. Чтобы исправить: используйте `@Primary` на одном из них или `@Qualifier` при инжекте. Если имена методов `@Bean` разные, создадутся оба, но внедрение упадет без уточнения.

### 121. Как Spring обрабатывает @Order, @Priority и Ordered при создании бинов и внедрении коллекций?

Используются при внедрении коллекций бинов (`List<MyInterface>`).
- **@Order (Spring)**: задает порядок в списке. Чем меньше значение, тем выше приоритет.
- **@Priority (JSR-250)**: аналогично, но учитывается также при разрешении зависимостей между несколькими кандидатами.

### 122. Как работает @Lookup и в каких случаях он полезен?

Используется, когда синглтон-бин должен обращаться к прототип-бину (prototype). Так как синглтон создается один раз, обычное `@Autowired` внедрит один и тот же экземпляр прототипа. `@Lookup` заставляет Spring каждый раз динамически запрашивать новый экземпляр из контекста.

### 123. Как можно динамически регистрировать бины в runtime (например, через BeanDefinitionRegistry)?

Это можно сделать в `BeanFactoryPostProcessor` или через реализацию `ImportBeanDefinitionRegistrar`. Вы получаете доступ к `BeanDefinitionRegistry` и вызываете `registerBeanDefinition(name, definition)`.

### 157. Как работает @Lazy и когда его использование оправдано?

Аннотация говорит Spring не создавать бин при старте, а создать его (и его прокси) только при первом обращении.

**Оправдано**: Для разруливания редких циклических зависимостей или для тяжелых бинов, которые нужны только в специфических сценариях (например, генерация тяжелых отчетов).

### 158. Как можно оптимизировать старт Spring Boot приложения (например, через spring.main.lazy-initialization)?

1. `spring.main.lazy-initialization=true`: Все бины становятся ленивыми. Ускоряет старт в разы, но ошибки конфигурации вылезут только в рантайме.
2. Использование Spring AOT (Ahead-of-Time) для компиляции в Native Image (GraalVM).
3. Отключение ненужных автоконфигураций через `exclude`.

### 191. Почему @Value не работает в static полях и как это можно обойти?

Spring внедряет зависимости в экземпляры бинов через сеттеры или поля. Статические поля принадлежат классу, а не объекту, и жизненный цикл Spring их не касается.

**Как обойти:**
- Через сеттер: Сделайте нестатический сеттер и повесьте `@Value` на него.
- Инициализация в `@PostConstruct`: Записать значение из обычного поля в статическое после создания бина.

### 192. Как работает @AliasFor в аннотациях Spring и где это применяется?

Эта аннотация позволяет создавать "синонимы" для атрибутов.
- **Внутри одной аннотации**: Чтобы `value` и `name` делали одно и то же.
- **Мета-аннотации**: Когда вы создаете свою аннотацию (например, `@MyService`) и хотите "пробросить" значение атрибута в `@Service`.

**Пример**: В `@SpringBootApplication` используется `@AliasFor`, чтобы передать параметры в `@ComponentScan` и `@EnableAutoConfiguration`.

### 193. Как реализовать кастомный PropertySource для нестандартных источников конфигурации?

1. Создайте класс, наследующий `PropertySource<T>`.
2. Реализуйте метод `getProperty(String name)`.
3. Добавьте его в окружение: `environment.getPropertySources().addLast(new MySource(...))`.

Часто используется для чтения конфигов из БД, Redis или внешних API.

---

## 2. Spring Boot — основы

### 6. В чем отличие Spring от Spring Boot?

- **Spring Framework**: Набор библиотек и инструментов для построения приложений (IoC, MVC, Security и т.д.). Требует ручной настройки (XML или Java Config) и управления версиями зависимостей.
- **Spring Boot**: Надстройка над Spring. Предоставляет "convention over configuration" (соглашение вместо конфигурации), управление зависимостями через Starters, встроенный веб-сервер (Tomcat/Jetty) и автоконфигурацию.

### 8. Что такое Starter POM и как они упрощают настройку?

Это наборы транзитивных зависимостей. Например, `spring-boot-starter-web` подтягивает Spring MVC, Jackson, Tomcat и валидатор. Это избавляет от конфликтов версий (Dependency Hell), так как версии согласованы в родительском POM (BOM).

### 73. Как работают кастомные Starter-модули?

Стартер — это способ упаковать зависимость и её автоконфигурацию в одну библиотеку. Обычно состоит из двух модулей (хотя можно и в одном):
- `library-autoconfigure`: Содержит код логики и классы `@Configuration`.
- `library-starter`: Пустой проект, который в pom.xml подтягивает `library-autoconfigure` и необходимые внешние библиотеки. Пользователь подключает именно его.

### 74. Как создать свой spring-boot-starter?

1. Создать модуль `my-library-autoconfigure`.
2. Написать `@Configuration` класс с бинами.
3. Использовать `@ConditionalOn...` для гибкости.
4. Зарегистрировать конфиг в imports файле (или `spring.factories`).
5. Создать модуль `my-library-starter`, который просто подтягивает `autoconfigure` и нужные зависимости (pom.xml).

### 75. Как избежать конфликтов автоконфигурации?

Всегда используйте `@ConditionalOnMissingBean` в автоконфигурациях. Это дает приоритет пользовательским бинам: если разработчик объявил бин сам, автоконфигурация отступает.

### 291. Как создать свой Spring Boot Starter?

Создание собственного стартера позволяет инкапсулировать конфигурацию и зависимости для повторного использования в разных проектах.

Обычно создаются два модуля: `my-library-spring-boot-starter` (пустой модуль, объединяющий зависимости) и `my-library-spring-boot-autoconfigure` (содержит код автоконфигурации).

1. Создайте класс с аннотацией `@AutoConfiguration` (или `@Configuration` для старых версий).
2. Используйте аннотации `@ConditionalOnClass`, `@ConditionalOnProperty` или `@ConditionalOnMissingBean`, чтобы бины создавались только при необходимости.
3. В файле `src/main/resources/META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` укажите полное имя вашего класса конфигурации.

### 293. Как переопределить стандартные бины Spring Boot (например, Jackson ObjectMapper)?

Spring Boot активно использует аннотацию `@ConditionalOnMissingBean`. Это означает, что если вы объявите свой бин такого же типа, Spring Boot не будет создавать дефолтный.

**Способы переопределения:**
1. Просто объявить `@Bean` того же типа в своей конфигурации.
2. Использовать `Jackson2ObjectMapperBuilder` для тонкой настройки ObjectMapper.
3. Использовать `@Primary`, если нужно переопределить бин, но оставить другие бины того же типа.

---

## 3. Spring Boot — автоконфигурация и стартеры

### 64. Как Spring Boot автоматически настраивает приложение?

Через `@EnableAutoConfiguration`.

### 65. Как работают @EnableAutoConfiguration и spring.factories?

1. Аннотация импортирует `AutoConfigurationImportSelector`.
2. Селектор сканирует файлы `META-INF/spring.factories` (в старых версиях) или `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (в новых версиях) во всех jar-файлах.
3. Находит классы конфигураций и пытается их загрузить.

### 66. Как Conditional-аннотации (@ConditionalOnClass, @ConditionalOnMissingBean) влияют на автоконфигурацию?

- **@ConditionalOnClass**: Конфигурация сработает, только если нужный класс есть в classpath (например, драйвер БД).
- **@ConditionalOnMissingBean**: Сработает, только если пользователь не создал свой бин такого типа.

### 92. Что такое Spring Boot Auto-Configuration и как оно работает?

**Spring Boot Auto-Configuration** — это механизм, который автоматически настраивает Spring-приложение на основе зависимостей, добавленных в classpath.

**Как работает:**
1. Аннотация `@EnableAutoConfiguration` (включена в `@SpringBootApplication`) импортирует `AutoConfigurationImportSelector`.
2. `AutoConfigurationImportSelector` сканирует файл `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` во всех JAR-файлах на classpath.
3. В этом файле перечислены классы автоконфигураций (например, `DataSourceAutoConfiguration`, `WebMvcAutoConfiguration`).
4. Каждый класс автоконфигурации содержит `@Conditional`-аннотации, которые определяют, должна ли эта конфигурация примениться (например, есть ли нужный класс в classpath, не создал ли пользователь свой бин).
5. Если все условия выполнены, Spring создает необходимые бины с разумными значениями по умолчанию.

### 93. Как можно переопределить настройки Auto-Configuration в Spring Boot?

**Способы переопределения:**
1. **Свойства в `application.properties`**: Самый простой способ. Spring Boot использует `@ConfigurationProperties` с префиксами (например, `spring.datasource.*`).
2. **Свой `@Bean`**: Если вы объявите бин того же типа, `@ConditionalOnMissingBean` в автоконфигурации не создаст дефолтный бин.
3. **`@SpringBootApplication(exclude = ...)`**: Полное отключение конкретной автоконфигурации.
4. **`spring.autoconfigure.exclude`**: Отключение через properties.
5. **Свой `@Configuration` класс**: Создание своей конфигурации, которая будет иметь приоритет.

### 94. Как работает @Conditional и какие его варианты существуют?

`@Conditional` — это базовая аннотация, которая позволяет включать или исключать бины/конфигурации на основе условия.

**Варианты `@Conditional` в Spring Boot:**
- **`@ConditionalOnClass`**: Бин создается, если указанный класс есть в classpath.
- **`@ConditionalOnMissingClass`**: Бин создается, если указанного класса нет в classpath.
- **`@ConditionalOnBean`**: Бин создается, если указанный бин уже существует в контексте.
- **`@ConditionalOnMissingBean`**: Бин создается, если указанного бина нет в контексте.
- **`@ConditionalOnProperty`**: Бин создается, если свойство имеет определенное значение.
- **`@ConditionalOnResource`**: Бин создается, если ресурс доступен.
- **`@ConditionalOnWebApplication`**: Бин создается, если приложение веб-приложение.
- **`@ConditionalOnNotWebApplication`**: Бин создается, если приложение НЕ веб-приложение.
- **`@ConditionalOnExpression`**: Бин создается, если SpEL-выражение истинно.
- **`@ConditionalOnJava`**: Бин создается, если версия Java соответствует.
- **`@ConditionalOnJndi`**: Бин создается, если доступен JNDI-ресурс.

### 135. Как работает @ConditionalOnMissingBean и почему он важен в Auto-Configuration?

Этот механизм позволяет пользователю "переопределить" стандартное поведение. Spring создаст свой бин (например, `ObjectMapper`) только в том случае, если разработчик не объявил свой собственный бин этого типа. Это основа гибкости Spring Boot.

### 136. Как можно отключить Auto-Configuration для определенного класса?

- Через аннотацию: `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})`.
- Через свойства: `spring.autoconfigure.exclude=org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration`.

### 137. Как Spring Boot обрабатывает spring.factories и можно ли переопределить порядок загрузки Auto-Configuration?

Spring Boot ищет файлы `META-INF/spring.factories` (в старых версиях) или `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (в новых версиях).

Порядок можно настроить через `@AutoConfigureAfter`, `@AutoConfigureBefore` или `@AutoConfigureOrder`. Это важно, чтобы, например, настроить БД до того, как начнет инициализироваться слой JPA.

### 195. Как Spring Boot обрабатывает spring-autoconfigure-metadata.json при AutoConfiguration?

Это оптимизация. Чтобы Spring Boot не загружал все классы автоконфигураций для проверки условий (`@ConditionalOnClass`), он читает этот JSON. В нем заранее прописано: "Конфигурация А нужна, только если в classpath есть класс Б". Это ускоряет старт приложения.

### 98. Как можно кастомизировать Spring Boot Starter?

**Способы кастомизации:**
1. **Свойства**: Добавить `@ConfigurationProperties` с уникальным префиксом.
2. **Условия**: Использовать `@ConditionalOnProperty`, `@ConditionalOnMissingBean` для гибкости.
3. **Порядок**: Использовать `@AutoConfigureAfter`, `@AutoConfigureBefore`, `@AutoConfigureOrder`.
4. **Документация**: Создать файл `META-INF/spring-configuration-metadata.json` для подсказок в IDE.

---

## 4. Spring Boot — запуск и жизненный цикл

### 7. Как работает SpringApplication.run()?

1. Создает `ApplicationContext`.
2. Регистрирует `CommandLinePropertySource` (аргументы запуска).
3. Загружает и применяет `application.properties`.
4. Сканирует пакеты на наличие компонентов (`@ComponentScan`).
5. Запускает автоконфигурацию (`@EnableAutoConfiguration`).
6. Поднимает встроенный веб-сервер (если это веб-приложение).

### 67. Как работает SpringApplication.run()? (детально)

1. Создается экземпляр `SpringApplication`.
2. Загружаются `SpringApplicationRunListener` (события старта).
3. Подготавливается `Environment` (свойства).
4. Создается `ApplicationContext`.
5. Загружаются источники бинов.
6. Вызывается `context.refresh()` — самое "мясо": создание бинов, запуск Tomcat.
7. Вызываются `CommandLineRunner` / `ApplicationRunner`.

### 68. Какие этапы запуска приложения (SpringApplicationRunListener, ApplicationContextInitializer)?

**SpringApplicationRunListener**: Интерфейс для прослушивания событий жизненного цикла самого старта.
- `starting()`: Самое начало.
- `environmentPrepared()`: Загружены properties/yml.
- `contextPrepared()`: Контекст создан, но еще пуст.
- `started()`: Контекст поднят, бины созданы.

**ApplicationContextInitializer**: Интерфейс, который вызывается до обновления (refresh) контекста. Позволяет программно зарегистрировать свойства или бины в контексте до начала основной работы.

### 69. Как выбирается тип ApplicationContext (AnnotationConfigServletWebServerApplicationContext vs ReactiveWebServerApplicationContext)?

Spring Boot использует `WebApplicationType.deduceFromClasspath()`:
1. Если есть классы `DispatcherHandler` и `Flux` (WebFlux) — выбирается `ReactiveWebServerApplicationContext`.
2. Если нет WebFlux, но есть Servlet и `ConfigurableWebApplicationContext` — выбирается `AnnotationConfigServletWebServerApplicationContext`.
3. Иначе — обычный `AnnotationConfigApplicationContext` (не веб).

### 96. Как работает @SpringBootApplication под капотом?

`@SpringBootApplication` — это композитная аннотация, которая объединяет три аннотации:

1. **`@SpringBootConfiguration`**: Помечает класс как конфигурацию Spring Boot (специализация `@Configuration`).
2. **`@EnableAutoConfiguration`**: Включает механизм автоконфигурации (сканирует `AutoConfiguration.imports`).
3. **`@ComponentScan`**: Включает сканирование компонентов в пакете и подпакетах класса, на котором стоит аннотация.

Также `@SpringBootApplication` использует `@AliasFor` для проброса параметров в `@ComponentScan` и `@EnableAutoConfiguration`.

### 99. Как работает @Enable семейство аннотаций (например, @EnableCaching, @EnableAsync)?

Аннотации семейства `@Enable*` работают по одному принципу — они импортируют конфигурацию через `@Import`:

1. **`@EnableCaching`**: Импортирует `CachingConfigurationSelector`, который регистрирует `BeanPostProcessor` для обработки `@Cacheable`, `@CacheEvict` и т.д., а также создает `CacheInterceptor`.
2. **`@EnableAsync`**: Импортирует `AsyncConfigurationSelector`, который регистрирует `AsyncAnnotationBeanPostProcessor` для обработки `@Async`.
3. **`@EnableScheduling`**: Импортирует `SchedulingConfiguration`, который регистрирует `ScheduledAnnotationBeanPostProcessor` для обработки `@Scheduled`.
4. **`@EnableTransactionManagement`**: Импортирует `TransactionManagementConfigurationSelector`, который регистрирует `TransactionInterceptor` для обработки `@Transactional`.
5. **`@EnableWebMvc`**: Импортирует `DelegatingWebMvcConfiguration`, который настраивает Spring MVC.
6. **`@EnableAspectJAutoProxy`**: Включает поддержку AOP через AspectJ.

Все эти аннотации работают через `@Import(SomeImportSelector.class)`, который динамически регистрирует нужные бины и BeanPostProcessor'ы.

---

## 5. Spring Boot — конфигурация и свойства

### 9. Как переопределить настройки application.properties?

Порядок приоритета (от высшего к низшему):
1. Аргументы командной строки.
2. JNDI атрибуты / System Properties (`-Dkey=value`).
3. Переменные окружения ОС.
4. Профильные конфиги (`application-dev.properties`).
5. Основной `application.properties`.

### 76. Как Spring Boot обрабатывает application.properties?

Spring Boot использует `PropertySourceLoader` для загрузки файлов `application.properties` и `application.yml`.

**Процесс:**
1. При старте `SpringApplication` создает `Environment` через `StandardEnvironment`.
2. `Environment` содержит цепочку `PropertySource` объектов.
3. Spring Boot ищет файлы `application.properties` и `application.yml` в стандартных locations:
   - `file:./config/`
   - `file:./`
   - `classpath:config/`
   - `classpath:`
4. Файлы загружаются через `PropertiesPropertySourceLoader` (для `.properties`) и `YamlPropertySourceLoader` (для `.yml`).
5. Все PropertySource добавляются в `MutablePropertySources` в порядке приоритета.
6. Значения доступны через `@Value("${property}")`, `@ConfigurationProperties` или `Environment.getProperty()`.

### 77. Как PropertySourcesPlaceholderConfigurer заменяет ${...}?

Это `BeanFactoryPostProcessor` (BFPP). Он запускается после чтения всех `BeanDefinition`, но до создания бинов. Он проходит по определениям бинов, находит строки `${property}` и заменяет их на значения из `Environment`.

### 78. Как @ConfigurationProperties биндит свойства в объекты?

`ConfigurationPropertiesBindingPostProcessor` связывает свойства из `Environment` с полями Java-бина (через сеттеры или конструктор), используя расслабленное связывание (kebab-case -> camelCase).

### 134. Как Spring Boot загружает application.properties и в каком порядке переопределяются значения?

Spring Boot загружает свойства в строгом порядке (снизу вверх — более приоритетные):
1. Дефолтные свойства (`SpringApplication.setDefaultProperties`).
2. Файлы `application.properties` / yml внутри jar.
3. Внешние файлы конфигурации (в той же папке, что и jar).
4. Переменные окружения (OS Environment Variables).
5. Системные свойства Java (`-D`).
6. Аргументы командной строки (`--server.port=8081`).

### 90. Какие есть стратегии загрузки конфигурации в Spring?

- **XML-based configuration**: Старый подход (`ClassPathXmlApplicationContext`). Все бины описываются в `.xml`.
- **Java-based configuration**: Использование `@Configuration` и `@Bean`. Современный стандарт.
- **Annotation-based configuration**: Использование `@Component`, `@Service` и т.д. в сочетании с `@ComponentScan`.
- **Groovy configuration**: Конфигурация на языке Groovy (используется редко).

В Spring Boot обычно используется гибрид: `@SpringBootApplication` включает сканирование компонентов и авто-конфигурацию.

### 91. Как работает @Profile и для чего он используется?

`@Profile` позволяет регистрировать бины только при активации определенного профиля окружения (например, dev, test, prod).

- Можно ставить над `@Configuration` или над отдельным `@Bean`.
- **Как работает**: При старте контекста Spring проверяет список активных профилей. Если профиль бина не совпадает с активным (и не является default), бин пропускается и не создается.
- **Активация через**: `application.properties` (`spring.profiles.active=dev`), аргументы JVM (`-Dspring.profiles.active=prod`) или переменные окружения.

### 194. Как @Import и @ImportResource работают на уровне загрузки контекста?

- **@Import**: Регистрирует `@Configuration` классы или обычные компоненты напрямую в `BeanDefinitionRegistry`. Работает на этапе `ConfigurationClassPostProcessor`.
- **@ImportResource**: Позволяет загружать старые добрые XML-конфиги. Spring использует `BeanDefinitionReader`, соответствующий расширению файла.

---

## 6. Spring Boot — встроенные серверы

### 70. Как Spring Boot встраивает Tomcat/Jetty?

Встроенный сервер — это не отдельный процесс, а обычный Бин внутри Spring Context.
1. Автоконфигурация (`ServletWebServerFactoryAutoConfiguration`) ищет классы Tomcat/Jetty в classpath.
2. Она создает бин типа `ServletWebServerFactory` (например, `TomcatServletWebServerFactory`).

### 71. Как ServletWebServerFactory создаёт сервер?

1. В методе `onRefresh()` веб-контекста вызывается метод фабрики `getWebServer()`.
2. Фабрика программно создает объект Tomcat (`new Tomcat()`), настраивает порты, коннекторы и base directory.
3. Запускает метод `tomcat.start()`.

### 72. Как DispatcherServlet регистрируется автоматически?

1. Создается бин `DispatcherServlet` (через `DispatcherServletAutoConfiguration`).
2. Создается специальный бин `DispatcherServletRegistrationBean`.
3. Этот регистратор берет существующий `DispatcherServlet` и добавляет его в контекст сервлетов (`ServletContext`) Tomcat'а, маппя его на путь `/` (по умолчанию). Это программный аналог записи в `web.xml`.

### 97. Как Spring Boot интегрируется со встроенными серверами (Tomcat, Jetty, Undertow)?

Spring Boot использует абстракцию `ServletWebServerFactory`:

1. **Tomcat**: `TomcatServletWebServerFactory` — создает встроенный Tomcat. Используется по умолчанию.
2. **Jetty**: `JettyServletWebServerFactory` — для замены Tomcat на Jetty (нужно исключить `spring-boot-starter-tomcat` и добавить `spring-boot-starter-jetty`).
3. **Undertow**: `UndertowServletWebServerFactory` — для замены на Undertow (нужно исключить Tomcat и добавить `spring-boot-starter-undertow`).

Все фабрики реализуют интерфейс `ServletWebServerFactory` и вызываются в методе `onRefresh()` веб-контекста.

---

## 7. Spring Boot — Actuator и мониторинг

### 95. Что такое Spring Boot Actuator и какие endpoints он предоставляет?

Actuator — это библиотека (`spring-boot-starter-actuator`), предоставляющая готовые endpoints для мониторинга и управления приложением в продакшене.

**Популярные endpoints:**
- `/actuator/health`: Состояние здоровья приложения (UP/DOWN) и его компонентов (БД, диск).
- `/actuator/info`: Произвольная информация о приложении (версия, git commit).
- `/actuator/metrics`: Различные метрики (CPU, RAM, HTTP запросы) для Prometheus/Grafana.
- `/actuator/env`: Просмотр свойств окружения.
- `/actuator/loggers`: Просмотр и изменение уровня логирования в рантайме.
- `/actuator/threaddump`: Дамп потоков.

### 307. Как Micrometer собирает метрики HTTP-запросов?

Micrometer интегрируется с Spring Boot Actuator через `WebMvcMetricsFilter` (для Spring MVC) или `WebFluxMetricsFilter` (для WebFlux).

**Как работает:**
1. Фильтр перехватывает каждый HTTP-запрос.
2. Собирает метрики: время выполнения, статус ответа, URI, метод.
3. Сохраняет их в `MeterRegistry` под именем `http.server.requests`.
4. Метрики доступны через `/actuator/metrics/http.server.requests`.

**Доступные теги:** `method`, `status`, `uri`, `exception`.

### 308. Как Flight Recorder (JFR) интегрируется с Spring Boot?

JFR (Java Flight Recorder) — это встроенный в JVM инструмент для профилирования.

**Интеграция с Spring Boot:**
1. Начиная с Spring Boot 3.x, есть поддержка JFR через `spring-boot-starter-actuator`.
2. Endpoint `/actuator/health` может показывать JFR-данные.
3. Можно запустить JFR запись через `jcmd` или через JMX.
4. Spring Boot также поддерживает `AsyncProfiler` для более детального профилирования.

---

## 8. Spring Boot — Native Image (GraalVM)

### 286. Как Spring Native компилирует приложение в нативный образ?

Процесс превращения Spring-приложения в бинарный файл (Native Image) проходит через два ключевых этапа:

1. **Spring AOT Processing (Ahead-of-Time)**: На этапе сборки (Maven/Gradle) плагин Spring анализирует ваш код, конфигурации (`@Configuration`) и зависимости. Он генерирует оптимизированный исходный код Java и байт-код, который заменяет динамическую логику Spring (например, поиск бинов через рефлексию) на прямые программные вызовы.
2. **GraalVM Native Image Builder**: Полученный байт-код подается на вход `native-image` билдеру. Он выполняет статический анализ кода, начиная от `main` метода, и ищет все достижимые пути исполнения. Всё, что не будет вызвано (мертвый код), удаляется. В итоге создается исполняемый файл, включающий в себя только нужные классы, зависимости и Substrate VM (мини-рантайм вместо полноценной JVM).

### 287. Какие ограничения есть при использовании GraalVM с Spring?

Главное ограничение — необходимость полной предсказуемости.

- **Динамические возможности**: Рефлексия, динамические прокси, сериализация и доступ к ресурсам (classpath) не работают «из коробки», если GraalVM не знает о них заранее.
- **G1 Garbage Collector**: В бесплатной версии GraalVM Community Edition доступен только Serial GC. Более эффективный G1 доступен только в Oracle GraalVM (ранее Enterprise).
- **Профилирование и мониторинг**: Привычные инструменты вроде JVisualVM или JProfiler не работают напрямую; нужно использовать специфичные для GraalVM решения.
- **Bytecode Enhancement**: Некоторые библиотеки, которые модифицируют байт-код в рантайме (например, старые версии CGLIB), могут вызывать проблемы.

### 288. Как настроить Reflection Hints для работы с JPA в Spring Native?

JPA и Hibernate активно используют рефлексию и проксирование для сущностей. Если Spring AOT не распознал вашу сущность автоматически, вам нужно подсказать компилятору через `RuntimeHints`.

Вы реализуете интерфейс `RuntimeHintsRegistrar`:

```java
public class MyHints implements RuntimeHintsRegistrar {
    @Override
    public void registerHints(RuntimeHints hints, ClassLoader classLoader) {
        hints.reflection().registerType(
            UserEntity.class,
            MemberCategory.INVOKE_PUBLIC_CONSTRUCTORS,
            MemberCategory.INVOKE_PUBLIC_METHODS
        );
    }
}
```

Затем подключаете его над любой конфигурацией или основным классом:
```java
@ImportRuntimeHints(MyHints.class)
```

Для JPA также критично, чтобы все маппинги были известны на этапе сборки, поэтому использование `persistence.xml` может потребовать дополнительных усилий по сравнению с автоконфигурацией Spring Boot.

### 289. Как Spring AOT (Ahead-of-Time) влияет на стартап приложения?

Влияние колоссальное и положительное для времени запуска:

- **Отсутствие интерпретации**: Приложению не нужно ждать JIT-компилятора, чтобы «разогреть» код. Всё уже скомпилировано в машинный код.
- **Готовый граф бинов**: Spring AOT заранее генерирует код для создания бинов. При старте приложению не нужно сканировать classpath, искать аннотации `@Service` или `@Component` и вычислять зависимости — оно просто выполняет готовый Java-код по инициализации контекста.
- **Memory Footprint**: Потребление памяти при старте снижается в 3–5 раз, так как не нужно хранить метаданные классов для всей JVM и инфраструктуру для динамической компиляции.

Время старта типичного микросервиса сокращается с 5–10 секунд до 50–100 миллисекунд.

### 290. Как дебажить нативное Spring-приложение?

Дебаг нативного образа сложнее, чем обычного .jar, так как у вас больше нет JVM-инструментария.

1. **Дебаг в JVM-режиме**: 99% ошибок в Spring Native связаны с отсутствием Hints (рефлексия, ресурсы). Сначала убедитесь, что приложение работает на обычной JVM, но с включенным AOT-режимом: `mvn spring-boot:run -Pnative`.
2. **Debug Symbols**: При сборке образа нужно добавить флаг, чтобы сохранить отладочные символы: `native-image -g ...`
3. **GDB (GNU Debugger)**: После сборки с флагом `-g` вы можете использовать стандартный отладчик C++ — `gdb`. Современные IDE (IntelliJ IDEA Ultimate, VS Code) поддерживают Native Image Debugging, позволяя ставить брейкпоинты прямо в Java-коде, когда запущен нативный бинарник.
4. **Логирование**: Поскольку традиционные дампы потоков (thread dumps) выглядят иначе, часто приходится полагаться на расширенное логирование (`-Dlogging.level.root=DEBUG`) для понимания того, где «упал» бинарник.

---

## 9. Spring Context и жизненный цикл бинов

### 4. Что такое Spring Context и как его создать?

Это контейнер (`ApplicationContext`), который управляет жизненным циклом бинов. Он расширяет `BeanFactory`, добавляя поддержку AOP, обработки сообщений, событий и контекста веб-приложения.

**Создать можно через:**
- `AnnotationConfigApplicationContext(AppConfig.class)` — для Java-конфигурации.
- `ClassPathXmlApplicationContext("beans.xml")` — для XML.
- `SpringApplication.run(...)` — в Spring Boot поднимает соответствующий контекст автоматически.

### 84. Что такое Spring Context и как он инициализируется?

Spring Context (`ApplicationContext`) — это главный интерфейс IoC-контейнера. Он отвечает за инстанцирование, настройку и сборку бинов. Он расширяет `BeanFactory`, добавляя функционал (события, i18n, AOP).

**Процесс инициализации:**
1. **Чтение конфигурации**: Загрузка определений бинов (BeanDefinitions) из XML, Java-классов или аннотаций.
2. **Парсинг и регистрация**: Создание `BeanDefinition` для каждого класса. На этом этапе объекты еще не создаются.
3. **Обработка BeanFactoryPostProcessor**: Возможность изменить определения бинов (например, подстановка property-placeholder'ов).
4. **Инстанцирование синглтонов**: Создание и связывание всех бинов со скоупом Singleton (не ленивых).

### 50. Как Spring создаёт и управляет бинами?

1. Парсинг конфигурации (BeanDefinition).
2. Создание экземпляра (Constructor).
3. Заполнение свойств (Setters).
4. Вызов Aware интерфейсов (BeanNameAware и т.д.).
5. `BeanPostProcessor.postProcessBeforeInitialization`.
6. `@PostConstruct` / init-method.
7. `BeanPostProcessor.postProcessAfterInitialization` (здесь создаются прокси для AOP/Transactional).
8. Бин готов к использованию.
9. При закрытии контекста: `@PreDestroy` / destroy-method.

### 53. Какие этапы проходит бин от создания до уничтожения?

1. **Instantiate**: Создание экземпляра (конструктор).
2. **Populate Properties**: Внедрение зависимостей (сеттеры, поля).
3. **Aware Interfaces**: Вызов `BeanNameAware`, `BeanFactoryAware` и т.д.
4. **BeanPostProcessor (Before)**: Метод `postProcessBeforeInitialization`.
5. **Initialization**: `@PostConstruct`, `InitializingBean.afterPropertiesSet()`, Custom init-method.
6. **BeanPostProcessor (After)**: Метод `postProcessAfterInitialization` (здесь создаются прокси AOP).
7. **Destruction**: `@PreDestroy` → `DisposableBean` → destroy-method.

### 81. Как Spring управляет жизненным циклом бина?

Жизненный цикл бина в Spring — это сложный процесс, который можно разделить на этапы создания и уничтожения.

**Основные шаги:**
1. **Инстанцирование (Instantiation)**: Spring создает экземпляр класса (вызывает конструктор).
2. **Заполнение свойств (Populate Properties)**: Внедрение зависимостей (DI).
3. **Вызов Aware-интерфейсов**: Если бин реализует интерфейсы типа `BeanNameAware`, `BeanFactoryAware`, Spring передает ему соответствующие данные.
4. **BeanPostProcessor (BeforeInitialization)**: Метод `postProcessBeforeInitialization()`. Здесь можно модифицировать бин до его инициализации.
5. **Инициализация (Initialization)**:
   - Методы с аннотацией `@PostConstruct`.
   - Метод `afterPropertiesSet()` (если реализован интерфейс `InitializingBean`).
   - Метод, указанный в `init-method` (в XML или `@Bean`).
6. **BeanPostProcessor (AfterInitialization)**: Метод `postProcessAfterInitialization()`. Здесь часто создаются прокси (AOP).
7. **Использование**: Бин готов к работе.
8. **Уничтожение (Destruction)**: При закрытии контекста:
   - Методы с аннотацией `@PreDestroy`.
   - Метод `destroy()` (интерфейс `DisposableBean`).
   - Метод, указанный в `destroy-method`.

### 54. Как работают BeanPostProcessor, InitializingBean, @PostConstruct, @PreDestroy?

- **BPP**: Интерфейс для кастомизации всех бинов в контексте. Работает до и после init-методов самого бина.
- **InitializingBean**: Интерфейс, который бин реализует сам, чтобы выполнить логику после настройки свойств.
- **@PostConstruct**: Стандартная аннотация (JSR-250).

### 55. Почему @PostConstruct вызывается после инъекции зависимостей, но до InitializingBean.afterPropertiesSet()?

`@PostConstruct` обрабатывается специальным BPP (`CommonAnnotationBeanPostProcessor`). Согласно жизненному циклу, BPP (BeforeInitialization) запускаются до вызова собственного метода инициализации бина (`afterPropertiesSet`).

### 178. Почему @PostConstruct метод не может быть @Transactional, и как обойти это ограничение?

`@PostConstruct` вызывается в процессе инициализации бина, когда AOP-прокси еще не полностью сформирован.

**Как обойти:**
- Использовать `EventListener` на событие `ContextRefreshedEvent`.
- Использовать `CommandLineRunner`.

---

## 10. BeanFactory, ApplicationContext, BeanPostProcessor

### 51. Расскажите про BeanFactory, ApplicationContext, их различия и иерархию.

- **BeanFactory**: Корневой интерфейс IoC-контейнера. Обеспечивает базовый механизм DI (ленивая инициализация).
- **ApplicationContext**: Расширяет `BeanFactory`. Это "полный" контейнер, который добавляет:
  1. Обработку AOP.
  2. Обработку сообщений (i18n).
  3. Публикацию событий (EventPublisher).
  4. Специфичные для Web контексты.
  5. Инициализирует все синглтоны (не ленивые) при старте.

**Иерархия**: `ApplicationContext extends ListableBeanFactory extends BeanFactory`.

### 52. Как работает DefaultListableBeanFactory?

Это ключевая реализация `BeanFactory`. Она хранит определения бинов (`BeanDefinition`) в `Map<String, BeanDefinition>` и уже созданные синглтоны. Она умеет перечислять бины (listable) и выступает как реестр (registry).

### 120. Как работает BeanPostProcessor и BeanFactoryPostProcessor? Приведи примеры их использования в Spring.

- **BeanFactoryPostProcessor**: Работает с определениями бинов (BeanDefinition) до создания самих объектов. Пример: `PropertySourcesPlaceholderConfigurer` (замена `${property}`).
- **BeanPostProcessor**: Работает с экземплярами объектов. Имеет два метода: `postProcessBeforeInitialization` и `postProcessAfterInitialization`. Пример: обработка аннотаций `@Autowired` или создание прокси для `@Transactional`.

### 188. Как работает BeanDefinitionRegistryPostProcessor и чем отличается от BeanFactoryPostProcessor?

Это "старший брат" `BeanFactoryPostProcessor`. Он позволяет добавлять новые определения бинов в runtime еще до того, как фабрика начнет их обрабатывать. Используется во внутренних механизмах Spring Boot для сканирования компонентов.

### 189. Как можно создать кастомный Scope в Spring и в каких сценариях это полезно?

Полезен в специфических средах (например, scope "Batch" или "Tenant"). Реализуется через интерфейс `Scope` и регистрацию в `ConfigurableBeanFactory`. Это позволяет управлять временем жизни бина по своим правилам.

### 292. Как добавить кастомную аннотацию с обработкой через BeanPostProcessor?

`BeanPostProcessor` (BPP) позволяет вмешиваться в процесс жизненного цикла бина на этапе его инициализации.

1. **Создание аннотации**: Установите `@Retention(RetentionPolicy.RUNTIME)` и `@Target(ElementType.FIELD)` или `ElementType.TYPE`.
2. **Реализация BPP**: В методах `postProcessBeforeInitialization` или `postProcessAfterInitialization` ищите аннотацию над полями или классом.
3. Используйте Reflection API для внедрения данных или создания прокси-объекта.

---

## 11. Scopes, прокси и циклические зависимости

### 82. Какие есть scope-ы бинов в Spring и как они работают?

Scope (область видимости) определяет, сколько экземпляров бина будет создано и как долго они живут.

- **singleton** (по умолчанию): Один экземпляр на весь Spring Context. Кэшируется контейнером.
- **prototype**: Новый экземпляр создается при каждом запросе (getBean или инъекция). Spring не управляет полным жизненным циклом (не вызывает методы уничтожения).
- **Web-aware scopes** (доступны только в веб-контексте):
  - **request**: Один экземпляр на один HTTP-запрос.
  - **session**: Один экземпляр на одну HTTP-сессию.
  - **application**: Один экземпляр на жизненный цикл ServletContext (похож на singleton, но уровень видимости другой в случае нескольких контекстов).
  - **websocket**: Жизненный цикл привязан к WebSocket-сессии.

### 56. Почему конструкторная инъекция не поддерживает циклические зависимости, а @Autowired на полях — да?

При инъекции через конструктор объект не может быть создан, пока не получены все аргументы. Если A ждет B в конструкторе, а B ждет A, ни один объект не может быть инстанцирован физически (StackOverflowError).

### 57. Как работает DefaultSingletonBeanRegistry и его early singleton objects? (как решает циклические зависимости)

Spring решает проблему циклических зависимостей (А ссылается на Б, Б на А) через механизм трехуровневого кэша. Это работает только для синглтонов и только при инъекции через поля/сеттеры (не через конструктор).

- **singletonObjects (Level 1)**: Кэш полностью готовых бинов.
- **earlySingletonObjects (Level 2)**: Кэш "сырых" объектов. Объект уже инстанцирован (вызван конструктор), но поля еще не заполнены. Сюда объект попадает, если на него есть циклическая ссылка.
- **singletonFactories (Level 3)**: Кэш фабрик (ObjectFactory). При создании бина Spring сразу кладет сюда лямбду, которая может создать ссылку на бин или его прокси.

**Алгоритм разрешения (А зависит от Б):**
1. Создается А. Его фабрика кладется в Level 3.
2. А начинает заполнять поля и видит зависимость от Б.
3. Создается Б. Он видит зависимость от А.
4. Б ищет А в кэшах. Находит фабрику в Level 3, вызывает ее, получает ссылку на "сырой" А (возможно, прокси) и кладет в Level 2.
5. Б достраивается и попадает в Level 1.
6. А получает готовый Б, достраивается и переходит из Level 2 в Level 1.

### 119. Как Spring разрешает циклические зависимости между бинами? Какие есть ограничения и как их обойти?

Spring (начиная с версии 2.6) по умолчанию запрещает циклические зависимости в Boot.

**Как разрешает**: Если это разрешено, Spring использует трехуровневый кэш (singletonFactories), чтобы отдать "сырой" (еще не полностью инициализированный) объект.

**Как обойти:**
- Использовать `@Lazy` на одном из полей внедрения.
- Внедрять через Setter вместо конструктора.
- Рефакторинг (вынос общей логики в третий бин).

### 58. Когда Spring использует JDK Dynamic Proxy, а когда CGLIB?

- **JDK Proxy**: Стандарт Java. Создает прокси только если класс реализует интерфейс.
- **CGLIB**: Сторонняя библиотека (встроена в Spring). Создает прокси через наследование от целевого класса и переопределение методов. Используется, если интерфейсов нет или принудительно (например, в `@Configuration`).

### 59. Почему final-методы нельзя проксировать через CGLIB?

CGLIB работает через наследование (`extends MyClass`). `final` методы нельзя переопределить в наследнике, поэтому прокси-логика в них не попадет.

### 86. Что такое Proxy в Spring и как он используется в AOP?

Proxy (Заместитель) — это объект, который оборачивает реальный бин ("target") и перехватывает вызовы методов к нему.

- В AOP (Aspect Oriented Programming) прокси нужны для того, чтобы добавить дополнительную логику (cross-cutting concerns) до, после или вокруг вызова метода, не меняя код самого метода.
- Когда вы внедряете зависимость, Spring на самом деле внедряет прокси-объект.
- При вызове метода на прокси, сначала выполняется логика аспектов (advice), а затем (если нужно) вызывается метод реального объекта.

### 88. В чем разница между JDK Dynamic Proxy и CGLIB в Spring?

Spring автоматически выбирает механизм проксирования:

- **JDK Dynamic Proxy**: Встроен в Java (пакет `java.lang.reflect`). Работает только если класс реализует интерфейсы. Прокси реализует интерфейсы целевого объекта.
- **CGLIB (Code Generation Library)**: Сторонняя библиотека (включена в Spring Core). Работает через наследование. Создает подкласс целевого класса и переопределяет методы. Используется, если класс не реализует интерфейсы. **Ограничение**: Не может проксировать `final` классы и `final` методы.

В Spring Boot 2.x+ по умолчанию часто используется CGLIB (свойство `spring.aop.proxy-target-class=true`), чтобы избежать проблем с инъекцией по конкретному классу, а не интерфейсу.

### 125. Как Spring выбирает между JDK Dynamic Proxy и CGLIB? Можно ли заставить Spring всегда использовать CGLIB?

- **JDK Proxy**: Используется, если класс реализует хотя бы один интерфейс.
- **CGLIB**: Используется, если интерфейсов нет (создается наследник).
- **Всегда CGLIB**: Можно форсировать через `spring.main.proxy-bean-methods=true` или в настройках AOP: `@EnableAspectJAutoProxy(proxyTargetClass = true)`.

### 126. Как работает @EnableAspectJAutoProxy(proxyTargetClass = true) и какие последствия это имеет?

Принудительно включает использование CGLIB.

**Последствия:**
- Проксируются все методы (включая те, что не в интерфейсах).
- Невозможно проксировать `final` классы или `final` методы, так как CGLIB создает подкласс.

---

## 12. Конфигурация (@Configuration, @Bean, @Import)

### 5. Как работает @Bean в @Configuration классе?

Методы с аннотацией `@Bean` производят бины. Ключевая особенность: классы с `@Configuration` проксируются библиотекой CGLIB. Это гарантирует, что при вызове метода `@Bean` внутри другого метода `@Bean`, Spring не будет выполнять код метода заново, а вернет уже существующий экземпляр из контейнера (соблюдение Singleton scope).

### 60. Как работает @Configuration и почему он требует CGLIB?

Классы с `@Configuration` оборачиваются в CGLIB-прокси. Это нужно для сохранения семантики синглтона. Если метод `beanA()` вызывает `beanB()`, прокси перехватывает вызов, проверяет контекст, и если `beanB` уже есть, возвращает его, а не создает новый через вызов метода. Без CGLIB это был бы просто вызов Java-метода (создание нового объекта).

### 85. Как работает @Configuration и чем отличается от @Component?

`@Configuration` — это тоже компонент, но с особой семантикой для Java-конфигурации. Главное отличие — в режиме работы проксирования методов (Full mode vs Lite mode).

- **@Component (Lite mode)**: Если вы определите бины через методы с `@Bean` внутри обычного компонента, вызовы этих методов будут обычными вызовами Java. Если метод `beanA()` вызывает метод `beanB()`, то `beanB` будет создаваться заново при каждом вызове.
- **@Configuration (Full mode)**: Spring использует библиотеку CGLIB для создания прокси-класса этой конфигурации. При вызове метода `@Bean` прокси перехватывает вызов и проверяет, есть ли уже такой бин в контексте. Если есть — возвращает существующий. Если нет — создает. Это гарантирует семантику Singleton.

---

## 13. Аннотации и их обработка

### 61. Как Spring обрабатывает аннотации (@Component, @Autowired)?

- **@Autowired**: Обрабатывается классом `AutowiredAnnotationBeanPostProcessor`. Это BPP, который на этапе `postProcessProperties` (или при инстанцировании конструктора) использует Reflection API, чтобы найти поля/методы/конструкторы и внедрить туда зависимости из контекста.

### 62. Как ClassPathBeanDefinitionScanner находит бины?

Он сканирует байт-код в указанных пакетах (не загружая классы в JVM полностью, используя ASM), ищет аннотации `@Component` (и производные), создает `BeanDefinition` и регистрирует их в `BeanFactory`.

### 63. Как AutowiredAnnotationBeanPostProcessor внедряет зависимости?

Это реализация интерфейса `BeanPostProcessor` (а точнее `InstantiationAwareBeanPostProcessor`).

1. На этапе `postProcessProperties` (после вызова конструктора, но до init-методов) он сканирует класс бина через Reflection API.
2. Ищет поля и методы, помеченные `@Autowired` или `@Inject`.
3. Для каждого найденного элемента определяет тип зависимости и ищет подходящий бин в `BeanFactory`.
4. Если бин найден, внедряет его (через `Field.set()` или `Method.invoke()`).
5. Если бин не найден и `required = true` (по умолчанию), выбрасывает исключение.

---

## 14. Профили (@Profile)

### 91. Как работает @Profile и для чего он используется?

`@Profile` позволяет регистрировать бины только при активации определенного профиля окружения (например, dev, test, prod).

- Можно ставить над `@Configuration` или над отдельным `@Bean`.
- **Как работает**: При старте контекста Spring проверяет список активных профилей. Если профиль бина не совпадает с активным (и не является default), бин пропускается и не создается.
- **Активация через**: `application.properties` (`spring.profiles.active=dev`), аргументы JVM (`-Dspring.profiles.active=prod`) или переменные окружения.

---

## 15. AOP (Aspect-Oriented Programming)

### 10. Что такое AOP и как он реализован в Spring?

AOP (Aspect-Oriented Programming) — это парадигма, позволяющая вынести сквозную функциональность (логирование, безопасность, транзакции) в отдельные модули — аспекты.

**Реализация в Spring:**
- Spring AOP использует прокси (JDK Dynamic Proxy или CGLIB).
- Аспект — это класс с аннотацией `@Aspect`.
- Advice — это действие (метод), которое выполняется в точке соединения (Join Point).
- Pointcut — это выражение, описывающее, когда advice должен сработать.

### 11. Какие типы Advice существуют в Spring AOP?

- **@Before**: Выполняется до метода.
- **@AfterReturning**: После успешного возврата.
- **@AfterThrowing**: После исключения.
- **@After (Finally)**: В любом случае (finally).
- **@Around**: Самый мощный. Оборачивает метод, может контролировать выполнение (ProceedingJoinPoint).

### 12. В чем разница между Spring AOP и AspectJ?

- **Spring AOP**: Работает на уровне прокси (только для публичных методов бинов). Проще, но ограничен.
- **AspectJ**: Полноценный AOP-фреймворк. Работает на уровне байт-кода (через weaving на этапе компиляции или загрузки класса). Может перехватывать приватные методы, конструкторы, поля.

### 87. Как Spring AOP создает прокси для бинов?

1. После создания бина (после `postProcessAfterInitialization`) Spring проверяет, есть ли для него подходящие аспекты.
2. Если есть, Spring создает прокси-объект (через JDK Proxy или CGLIB).
3. Прокси оборачивает оригинальный бин.
4. В контекст возвращается прокси вместо оригинального бина.

### 89. Как работает @Around Advice и чем он отличается от @Before/@After?

`@Around` — это самый мощный тип Advice. Он полностью оборачивает метод.

- **@Before**: Просто выполняет код до вызова метода. Не может предотвратить вызов или изменить результат.
- **@After**: Выполняет код после вызова метода (вне зависимости от результата).
- **@Around**: Получает `ProceedingJoinPoint`, может:
  - Выполнить код до вызова метода.
  - Решить, вызывать ли метод вообще (`proceed()`).
  - Изменить аргументы.
  - Изменить возвращаемое значение.
  - Выполнить код после вызова.

### 124. Как работает @DeclareParents в Spring AOP?

Позволяет динамически добавить новую реализацию интерфейса к существующему бину. Например, вы можете "заставить" все бины, реализующие `UserService`, также реализовывать `Auditable`, без изменения кода `UserService`.

---

## 16. Транзакции (@Transactional)

### 13. Как работает @Transactional?

1. Spring создает прокси вокруг бина.
2. При вызове метода с `@Transactional` прокси перехватывает вызов.
3. Перед выполнением метода открывается транзакция (через `TransactionManager`).
4. После выполнения метода (или при исключении) транзакция коммитится или откатывается.

### 14. Какие propagation-уровни существуют?

- **REQUIRED** (по умолчанию): Использует существующую транзакцию или создает новую.
- **REQUIRES_NEW**: Всегда создает новую транзакцию, приостанавливая текущую.
- **SUPPORTS**: Если есть транзакция — использует, если нет — работает без нее.
- **NOT_SUPPORTED**: Всегда работает без транзакции, приостанавливая текущую.
- **MANDATORY**: Требует существующей транзакции, иначе исключение.
- **NEVER**: Требует отсутствия транзакции, иначе исключение.
- **NESTED**: Создает вложенную точку сохранения (savepoint) внутри существующей транзакции.

### 15. Почему @Transactional не работает при вызове метода внутри того же класса?

Из-за механизма прокси. Когда вы вызываете `this.innerMethod()`, вы вызываете метод на реальном объекте, а не на прокси. Прокси-логика (открытие транзакции) не срабатывает.

**Решение**: Self-injection (внедрить сам себя через `@Autowired`).

### 16. Какие isolation-уровни существуют?

- **READ_UNCOMMITTED**: Грязное чтение, неповторяющееся чтение, фантомы.
- **READ_COMMITTED** (по умолчанию в PostgreSQL): Неповторяющееся чтение, фантомы.
- **REPEATABLE_READ**: Фантомы (в MySQL — нет).
- **SERIALIZABLE**: Полная изоляция.

### 17. Как работает rollback в @Transactional?

По умолчанию откат происходит только при `RuntimeException` (unchecked). Проверяемые исключения (`Exception`) не вызывают откат. Можно настроить через `rollbackFor` / `noRollbackFor`.

### 18. Как работает TransactionManager?

Это центральный интерфейс для управления транзакциями. Он знает, как открыть, закоммитить или откатить транзакцию для конкретного ресурса (БД, JMS).

- `PlatformTransactionManager` — основной интерфейс.
- `DataSourceTransactionManager` — для JDBC.
- `JpaTransactionManager` — для JPA/Hibernate.
- `JtaTransactionManager` — для распределенных транзакций (JTA).

### 19. Как работает @Transactional(readOnly = true)?

Устанавливает флаг "только чтение". Hibernate может отключить dirty checking (проверку изменений) для оптимизации. На уровне БД может быть установлен режим read-only (например, в PostgreSQL).

### 20. Как работает @Transactional(rollbackFor = Exception.class)?

Переопределяет поведение по умолчанию. Теперь любое исключение (включая checked) вызовет откат транзакции.

### 21. Как работает @Transactional(timeout = 10)?

Устанавливает таймаут в секундах. Если транзакция выполняется дольше, она будет автоматически откачена.

### 22. Как работает @Transactional(noRollbackFor = SomeException.class)?

Указывает, что при определенном исключении откат не производится.

### 23. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW)?

Приостанавливает текущую транзакцию (если есть) и создает новую. Вложенные вызовы не влияют друг на друга.

### 24. Как работает @Transactional(propagation = Propagation.NESTED)?

Создает точку сохранения (savepoint) внутри текущей транзакции. Внутренняя транзакция может откатиться независимо, не затрагивая внешнюю.

### 25. Как работает @Transactional(propagation = Propagation.MANDATORY)?

Требует, чтобы вызывающий код уже был в транзакции. Если транзакции нет — выбрасывается исключение.

### 26. Как работает @Transactional(propagation = Propagation.NEVER)?

Требует, чтобы не было активной транзакции. Если транзакция есть — выбрасывается исключение.

### 27. Как работает @Transactional(propagation = Propagation.SUPPORTS)?

Если есть транзакция — присоединяется. Если нет — работает без транзакции.

### 28. Как работает @Transactional(propagation = Propagation.NOT_SUPPORTED)?

Приостанавливает текущую транзакцию (если есть) и выполняет метод без транзакции.

### 29. Как работает @Transactional(propagation = Propagation.REQUIRED)?

Это значение по умолчанию. Если есть транзакция — присоединяется. Если нет — создает новую.

### 30. Как работает @Transactional(isolation = Isolation.SERIALIZABLE)?

Устанавливает самый строгий уровень изоляции. Гарантирует полную изоляцию транзакций, но сильно снижает производительность.

### 31. Как работает @Transactional(isolation = Isolation.REPEATABLE_READ)?

Гарантирует, что повторное чтение тех же строк в одной транзакции даст тот же результат. Защищает от неповторяющегося чтения.

### 32. Как работает @Transactional(isolation = Isolation.READ_COMMITTED)?

Гарантирует, что транзакция видит только закоммиченные данные. Защищает от грязного чтения.

### 33. Как работает @Transactional(isolation = Isolation.READ_UNCOMMITTED)?

Самый низкий уровень изоляции. Транзакция может видеть незакоммиченные изменения других транзакций (грязное чтение).

### 34. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с JPA?

Приостанавливает текущий EntityManager и создает новый. Изменения в первом EntityManager не видны во втором до коммита.

### 35. Как работает @Transactional(propagation = Propagation.NESTED) с JDBC?

Использует savepoints JDBC. Внутренняя транзакция может откатиться до savepoint, не затрагивая внешнюю.

### 36. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с JTA?

Приостанавливает текущую транзакцию JTA и создает новую. После завершения новой транзакции возобновляет старую.

### 37. Как работает @Transactional(propagation = Propagation.NESTED) с JPA?

JPA не поддерживает savepoints напрямую. NESTED с JPA может работать только через JDBC-соединение.

### 38. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Hibernate?

Приостанавливает текущую Session и создает новую. Изменения в первой Session не видны во второй.

### 39. Как работает @Transactional(propagation = Propagation.NESTED) с Hibernate?

Hibernate не поддерживает savepoints напрямую. NESTED с Hibernate может работать только через JDBC-соединение.

### 40. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Spring Data JPA?

Приостанавливает текущий EntityManager и создает новый. Изменения в первом EntityManager не видны во втором до коммита.

### 41. Как работает @Transactional(propagation = Propagation.NESTED) с Spring Data JPA?

Spring Data JPA не поддерживает savepoints напрямую. NESTED с Spring Data JPA может работать только через JDBC-соединение.

### 42. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Spring Data JDBC?

Приостанавливает текущую транзакцию и создает новую. Изменения в первой транзакции не видны во второй.

### 43. Как работает @Transactional(propagation = Propagation.NESTED) с Spring Data JDBC?

Spring Data JDBC не поддерживает savepoints напрямую. NESTED с Spring Data JDBC может работать только через JDBC-соединение.

### 44. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Spring Data MongoDB?

MongoDB не поддерживает транзакции в классическом понимании. REQUIRES_NEW с MongoDB может работать только через JTA.

### 45. Как работает @Transactional(propagation = Propagation.NESTED) с Spring Data MongoDB?

MongoDB не поддерживает savepoints. NESTED с MongoDB может работать только через JTA.

### 47. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Spring Data Redis?

Redis не поддерживает транзакции в классическом понимании. REQUIRES_NEW с Redis может работать только через JTA.

### 48. Как работает @Transactional(propagation = Propagation.NESTED) с Spring Data Redis?

Redis не поддерживает savepoints. NESTED с Redis может работать только через JTA.

### 49. Как работает @Transactional(propagation = Propagation.REQUIRES_NEW) с Spring Data Elasticsearch?

Elasticsearch не поддерживает транзакции. REQUIRES_NEW с Elasticsearch может работать только через JTA.

### 100. Как работает @Transactional с несколькими DataSource?

Если в приложении несколько DataSource, нужно явно указать, какой TransactionManager использовать. Используется `@Transactional("transactionManagerName")`.

### 101. Как работает @Transactional с JPA и Hibernate?

1. Spring создает прокси вокруг бина.
2. При вызове метода с `@Transactional` прокси перехватывает вызов.
3. Прокси получает `EntityManager` из `EntityManagerFactory`.
4. Вызывается `entityManager.getTransaction().begin()`.
5. Выполняется метод.
6. Если успешно — `entityManager.getTransaction().commit()`.
7. Если исключение — `entityManager.getTransaction().rollback()`.

### 102. Как работает @Transactional с JDBC?

1. Spring создает прокси вокруг бина.
2. При вызове метода с `@Transactional` прокси перехватывает вызов.
3. Прокси получает `Connection` из `DataSource`.
4. Вызывается `connection.setAutoCommit(false)`.
5. Выполняется метод.
6. Если успешно — `connection.commit()`.
7. Если исключение — `connection.rollback()`.

### 103. Как работает @Transactional с JTA?

1. Spring создает прокси вокруг бина.
2. При вызове метода с `@Transactional` прокси перехватывает вызов.
3. Прокси получает `UserTransaction` из JNDI.
4. Вызывается `userTransaction.begin()`.
5. Выполняется метод.
6. Если успешно — `userTransaction.commit()`.
7. Если исключение — `userTransaction.rollback()`.

### 104. Как работает @Transactional с Spring Data JPA?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 105. Как работает @Transactional с Spring Data JDBC?

Spring Data JDBC использует `DataSourceTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 106. Как работает @Transactional с Spring Data MongoDB?

Spring Data MongoDB использует `MongoTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 107. Как работает @Transactional с Spring Data Redis?

Spring Data Redis использует `RedisTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 108. Как работает @Transactional с Spring Data Elasticsearch?

Spring Data Elasticsearch не поддерживает транзакции. @Transactional с Elasticsearch может работать только через JTA.

### 109. Как работает @Transactional с Spring Data Cassandra?

Spring Data Cassandra использует `CassandraTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 110. Как работает @Transactional с Spring Data Neo4j?

Spring Data Neo4j использует `Neo4jTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 111. Как работает @Transactional с Spring Data Couchbase?

Spring Data Couchbase использует `CouchbaseTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 112. Как работает @Transactional с Spring Data R2DBC?

Spring Data R2DBC использует `R2dbcTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 113. Как работает @Transactional с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 114. Как работает @Transactional с Spring Data JDBC и Hibernate?

Spring Data JDBC использует `DataSourceTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 115. Как работает @Transactional с Spring Data MongoDB и Hibernate?

Spring Data MongoDB использует `MongoTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 116. Как работает @Transactional с Spring Data Redis и Hibernate?

Spring Data Redis использует `RedisTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 117. Как работает @Transactional с Spring Data Elasticsearch и Hibernate?

Spring Data Elasticsearch не поддерживает транзакции. @Transactional с Elasticsearch может работать только через JTA.

### 118. Как работает @Transactional с Spring Data Cassandra и Hibernate?

Spring Data Cassandra использует `CassandraTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 127. Как работает @Transactional с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 128. Как работает @Transactional с Spring Data JDBC и Hibernate?

Spring Data JDBC использует `DataSourceTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 129. Как работает @Transactional с Spring Data MongoDB и Hibernate?

Spring Data MongoDB использует `MongoTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 130. Как работает @Transactional с Spring Data Redis и Hibernate?

Spring Data Redis использует `RedisTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 131. Как работает @Transactional с Spring Data Elasticsearch и Hibernate?

Spring Data Elasticsearch не поддерживает транзакции. @Transactional с Elasticsearch может работать только через JTA.

### 132. Как работает @Transactional с Spring Data Cassandra и Hibernate?

Spring Data Cassandra использует `CassandraTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 133. Как работает @Transactional с Spring Data Neo4j и Hibernate?

Spring Data Neo4j использует `Neo4jTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 138. Как работает @Transactional с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 139. Как работает @Transactional с Spring Data JDBC и Hibernate?

Spring Data JDBC использует `DataSourceTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 140. Как работает @Transactional с Spring Data MongoDB и Hibernate?

Spring Data MongoDB использует `MongoTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 141. Как работает @Transactional с Spring Data Redis и Hibernate?

Spring Data Redis использует `RedisTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 142. Как работает @Transactional с Spring Data Elasticsearch и Hibernate?

Spring Data Elasticsearch не поддерживает транзакции. @Transactional с Elasticsearch может работать только через JTA.

### 143. Как работает @Transactional с Spring Data Cassandra и Hibernate?

Spring Data Cassandra использует `CassandraTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 144. Как работает @Transactional с Spring Data Neo4j и Hibernate?

Spring Data Neo4j использует `Neo4jTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 145. Как работает @Transactional с Spring Data Couchbase и Hibernate?

Spring Data Couchbase использует `CouchbaseTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 146. Как работает @Transactional с Spring Data R2DBC и Hibernate?

Spring Data R2DBC использует `R2dbcTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 147. Как работает @Transactional с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 148. Как работает @Transactional с Spring Data JDBC и Hibernate?

Spring Data JDBC использует `DataSourceTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 149. Как работает @Transactional с Spring Data MongoDB и Hibernate?

Spring Data MongoDB использует `MongoTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 150. Как работает @Transactional с Spring Data Redis и Hibernate?

Spring Data Redis использует `RedisTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 151. Как работает @Transactional с Spring Data Elasticsearch и Hibernate?

Spring Data Elasticsearch не поддерживает транзакции. @Transactional с Elasticsearch может работать только через JTA.

### 152. Как работает @Transactional с Spring Data Cassandra и Hibernate?

Spring Data Cassandra использует `CassandraTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 153. Как работает @Transactional с Spring Data Neo4j и Hibernate?

Spring Data Neo4j использует `Neo4jTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 154. Как работает @Transactional с Spring Data Couchbase и Hibernate?

Spring Data Couchbase использует `CouchbaseTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 155. Как работает @Transactional с Spring Data R2DBC и Hibernate?

Spring Data R2DBC использует `R2dbcTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 156. Как работает @Transactional с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

---

## 17. Блокировки и конкурентность

### 159. Как работает @Lock в Spring Data JPA?

Аннотация `@Lock` используется в Spring Data JPA для указания типа блокировки при выполнении запроса.

**Типы блокировок:**
- `LockModeType.OPTIMISTIC`: Оптимистичная блокировка. Проверяет версию сущности при коммите.
- `LockModeType.OPTIMISTIC_FORCE_INCREMENT`: Оптимистичная блокировка с принудительным увеличением версии.
- `LockModeType.PESSIMISTIC_READ`: Пессимистичная блокировка на чтение.
- `LockModeType.PESSIMISTIC_WRITE`: Пессимистичная блокировка на запись.
- `LockModeType.PESSIMISTIC_FORCE_INCREMENT`: Пессимистичная блокировка с принудительным увеличением версии.

### 160. Как работает @Version в JPA?

`@Version` используется для реализации оптимистичной блокировки. Поле с этой аннотацией автоматически увеличивается при каждом обновлении сущности. При попытке обновить устаревшие данные выбрасывается `OptimisticLockException`.

### 161. Как работает @Lock(LockModeType.PESSIMISTIC_WRITE)?

Устанавливает пессимистичную блокировку на запись. Другие транзакции не могут читать или изменять заблокированные строки до завершения текущей транзакции.

### 162. Как работает @Lock(LockModeType.PESSIMISTIC_READ)?

Устанавливает пессимистичную блокировку на чтение. Другие транзакции могут читать, но не могут изменять заблокированные строки.

### 163. Как работает @Lock(LockModeType.OPTIMISTIC)?

Устанавливает оптимистичную блокировку. Проверяет версию сущности при коммите. Если версия изменилась — выбрасывается `OptimisticLockException`.

### 164. Как работает @Lock(LockModeType.OPTIMISTIC_FORCE_INCREMENT)?

Устанавливает оптимистичную блокировку с принудительным увеличением версии. Версия увеличивается даже при чтении.

### 165. Как работает @Lock(LockModeType.PESSIMISTIC_FORCE_INCREMENT)?

Устанавливает пессимистичную блокировку с принудительным увеличением версии. Версия увеличивается даже при чтении.

### 166. Как работает @Lock с Spring Data JPA?

`@Lock` применяется к методам репозитория. При выполнении запроса Spring Data JPA устанавливает указанный тип блокировки.

### 167. Как работает @Lock с Spring Data JDBC?

Spring Data JDBC не поддерживает `@Lock`. Для блокировок нужно использовать нативный SQL.

### 168. Как работает @Lock с Spring Data MongoDB?

Spring Data MongoDB не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы MongoDB.

### 169. Как работает @Lock с Spring Data Redis?

Spring Data Redis не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Redis.

### 170. Как работает @Lock с Spring Data Elasticsearch?

Spring Data Elasticsearch не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Elasticsearch.

### 171. Как работает @Lock с Spring Data Cassandra?

Spring Data Cassandra не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Cassandra.

### 172. Как работает @Lock с Spring Data Neo4j?

Spring Data Neo4j не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Neo4j.

### 173. Как работает @Lock с Spring Data Couchbase?

Spring Data Couchbase не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Couchbase.

### 174. Как работает @Lock с Spring Data R2DBC?

Spring Data R2DBC не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы R2DBC.

### 175. Как работает @Lock с Spring Data JPA и Hibernate?

`@Lock` применяется к методам репозитория. При выполнении запроса Spring Data JPA устанавливает указанный тип блокировки.

### 176. Как работает @Lock с Spring Data JDBC и Hibernate?

Spring Data JDBC не поддерживает `@Lock`. Для блокировок нужно использовать нативный SQL.

### 177. Как работает @Lock с Spring Data MongoDB и Hibernate?

Spring Data MongoDB не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы MongoDB.

### 179. Как работает @Lock с Spring Data Redis и Hibernate?

Spring Data Redis не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Redis.

### 180. Как работает @Lock с Spring Data Elasticsearch и Hibernate?

Spring Data Elasticsearch не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Elasticsearch.

### 181. Как работает @Lock с Spring Data Cassandra и Hibernate?

Spring Data Cassandra не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Cassandra.

### 182. Как работает @Lock с Spring Data Neo4j и Hibernate?

Spring Data Neo4j не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Neo4j.

### 183. Как работает @Lock с Spring Data Couchbase и Hibernate?

Spring Data Couchbase не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы Couchbase.

### 184. Как работает @Lock с Spring Data R2DBC и Hibernate?

Spring Data R2DBC не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы R2DBC.

### 185. Как работает @Lock с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

### 186. Как работает @Lock с Spring Data JDBC и Hibernate?

Spring Data JDBC не поддерживает `@Lock`. Для блокировок нужно использовать нативный SQL.

### 187. Как работает @Lock с Spring Data MongoDB и Hibernate?

Spring Data MongoDB не поддерживает `@Lock`. Для блокировок нужно использовать нативные механизмы MongoDB.

### 190. Как работает @Lock с Spring Data JPA и Hibernate?

Spring Data JPA использует `JpaTransactionManager`. При вызове метода репозитория, если нет активной транзакции, создается новая. Если есть — присоединяется к существующей.

---

## 18. Spring MVC — основы

### 196. Как работает DispatcherServlet в Spring MVC?

`DispatcherServlet` — это фронт-контроллер (Front Controller) в Spring MVC. Он является точкой входа для всех HTTP-запросов.

**Процесс обработки запроса:**
1. `DispatcherServlet` получает HTTP-запрос.
2. Он обращается к `HandlerMapping`, чтобы найти подходящий контроллер (метод с `@RequestMapping`).
3. Вызывается `HandlerAdapter`, который выполняет метод контроллера.
4. Контроллер возвращает `ModelAndView` (или `@ResponseBody`).
5. `ViewResolver` преобразует имя представления в реальный View (JSP, Thymeleaf).
6. View рендерится и отправляется клиенту.

### 197. Как работает HandlerMapping в Spring MVC?

`HandlerMapping` — это интерфейс, который определяет, какой контроллер должен обработать запрос.

**Реализации:**
- `RequestMappingHandlerMapping`: Использует аннотации `@RequestMapping`.
- `BeanNameUrlHandlerMapping`: Использует имена бинов как URL.
- `SimpleUrlHandlerMapping`: Использует явное маппинг URL на бины.

### 198. Как работает HandlerAdapter в Spring MVC?

`HandlerAdapter` — это интерфейс, который адаптирует контроллер к DispatcherServlet.

**Реализации:**
- `RequestMappingHandlerAdapter`: Для контроллеров с `@RequestMapping`.
- `HttpRequestHandlerAdapter`: Для `HttpRequestHandler`.
- `SimpleControllerHandlerAdapter`: Для `Controller` (старый стиль).

### 199. Как работает ViewResolver в Spring MVC?

`ViewResolver` — это интерфейс, который преобразует имя представления в реальный View.

**Реализации:**
- `InternalResourceViewResolver`: Для JSP.
- `ThymeleafViewResolver`: Для Thymeleaf.
- `FreeMarkerViewResolver`: Для FreeMarker.
- `BeanNameViewResolver`: Использует имена бинов как View.

### 200. Как работает ModelAndView в Spring MVC?

`ModelAndView` — это объект, который содержит модель (данные) и представление (View). Контроллер возвращает `ModelAndView`, и DispatcherServlet использует ViewResolver для рендеринга.

### 201. Как работает @ControllerAdvice?

`@ControllerAdvice` — это глобальный обработчик для всех контроллеров.

**Использование:**
- `@ExceptionHandler`: Глобальная обработка исключений.
- `@InitBinder`: Глобальная настройка биндеров.
- `@ModelAttribute`: Глобальное добавление атрибутов в модель.

### 202. Как работает @ExceptionHandler?

`@ExceptionHandler` — это аннотация для обработки исключений в контроллере или `@ControllerAdvice`.

**Как работает:**
1. При возникновении исключения в контроллере, DispatcherServlet ищет метод с `@ExceptionHandler`, который может обработать это исключение.
2. Если метод найден, он выполняется и возвращает ответ.
3. Если не найден, исключение пробрасывается дальше.

### 203. Как работает @InitBinder?

`@InitBinder` — это аннотация для настройки биндера данных.

**Использование:**
- Регистрация кастомных редакторов свойств.
- Настройка форматирования дат.
- Указание разрешенных/запрещенных полей.

### 204. Как работает @ModelAttribute?

`@ModelAttribute` — это аннотация для добавления атрибутов в модель.

**Использование:**
- Над методом: Добавляет атрибут в модель перед вызовом любого метода контроллера.
- Над параметром: Связывает параметр запроса с атрибутом модели.

### 205. Как работает @SessionAttributes?

`@SessionAttributes` — это аннотация для хранения атрибутов модели в HTTP-сессии.

**Использование:**
- Указывается над контроллером.
- Атрибуты модели с указанными именами сохраняются в сессии.
- Позволяет сохранять состояние между запросами.

### 206. Как работает @RequestParam?

`@RequestParam` — это аннотация для извлечения параметров запроса.

**Параметры:**
- `value`: Имя параметра.
- `required`: Обязателен ли параметр (по умолчанию true).
- `defaultValue`: Значение по умолчанию.

### 207. Как работает @PathVariable?

`@PathVariable` — это аннотация для извлечения переменных из URL.

**Пример:**
```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userService.findById(id);
}
```

### 208. Как работает @RequestBody?

`@RequestBody` — это аннотация для связывания тела HTTP-запроса с параметром метода.

**Как работает:**
1. `HttpMessageConverter` преобразует тело запроса (JSON, XML) в Java-объект.
2. Jackson (или другой конвертер) десериализует JSON в объект.

### 209. Как работает @ResponseBody?

`@ResponseBody` — это аннотация для указания, что возвращаемое значение метода должно быть записано в тело HTTP-ответа.

**Как работает:**
1. `HttpMessageConverter` преобразует Java-объект в тело ответа (JSON, XML).
2. Jackson (или другой конвертер) сериализует объект в JSON.

### 210. Как работает @RestController?

`@RestController` — это комбинация `@Controller` и `@ResponseBody`. Все методы контроллера автоматически возвращают JSON/XML.

### 211. Как работает @RequestMapping?

`@RequestMapping` — это аннотация для маппинга HTTP-запросов на методы контроллера.

**Параметры:**
- `value`: URL.
- `method`: HTTP метод (GET, POST, PUT, DELETE).
- `params`: Фильтр по параметрам.
- `headers`: Фильтр по заголовкам.
- `consumes`: Тип контента запроса.
- `produces`: Тип контента ответа.

### 212. Как работает @GetMapping?

`@GetMapping` — это специализация `@RequestMapping(method = RequestMethod.GET)`.

### 213. Как работает @PostMapping?

`@PostMapping` — это специализация `@RequestMapping(method = RequestMethod.POST)`.

### 214. Как работает @PutMapping?

`@PutMapping` — это специализация `@RequestMapping(method = RequestMethod.PUT)`.

### 215. Как работает @DeleteMapping?

`@DeleteMapping` — это специализация `@RequestMapping(method = RequestMethod.DELETE)`.

### 216. Как работает @PatchMapping?

`@PatchMapping` — это специализация `@RequestMapping(method = RequestMethod.PATCH)`.

### 217. Как работает @CrossOrigin?

`@CrossOrigin` — это аннотация для включения CORS (Cross-Origin Resource Sharing).

**Параметры:**
- `origins`: Разрешенные источники.
- `methods`: Разрешенные HTTP методы.
- `allowedHeaders`: Разрешенные заголовки.
- `allowCredentials`: Разрешить куки.

### 218. Как работает @MatrixVariable?

`@MatrixVariable` — это аннотация для извлечения матричных переменных из URL.

**Пример:**
```java
@GetMapping("/cars/{path}")
public String getCars(@MatrixVariable Map<String, String> matrixVars) {
    // matrixVars содержит матричные переменные
}
```

### 219. Как работает @RequestHeader?

`@RequestHeader` — это аннотация для извлечения заголовков HTTP-запроса.

**Пример:**
```java
@GetMapping("/api/data")
public String getData(@RequestHeader("User-Agent") String userAgent) {
    return userAgent;
}
```

---

## 19. Spring MVC — контроллеры и обработка запросов

### 220. Как работает @ResponseStatus?

`@ResponseStatus` — это аннотация для указания HTTP-статуса ответа.

**Использование:**
- Над методом контроллера: Устанавливает статус ответа.
- Над классом исключения: Устанавливает статус при выбрасывании исключения.

### 221. Как работает @ControllerAdvice с @ExceptionHandler?

`@ControllerAdvice` — это глобальный обработчик для всех контроллеров. `@ExceptionHandler` внутри него обрабатывает исключения из всех контроллеров.

**Пример:**
```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ResponseEntity<String> handleNotFound(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

### 222. Как работает @RestControllerAdvice?

`@RestControllerAdvice` — это комбинация `@ControllerAdvice` и `@ResponseBody`. Все методы обработки исключений автоматически возвращают JSON/XML.

### 223. Как работает @InitBinder в @ControllerAdvice?

`@InitBinder` в `@ControllerAdvice` применяется глобально ко всем контроллерам.

**Пример:**
```java
@ControllerAdvice
public class GlobalBinder {
    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.registerCustomEditor(Date.class, new CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd"), false));
    }
}
```

### 224. Как работает @ModelAttribute в @ControllerAdvice?

`@ModelAttribute` в `@ControllerAdvice` добавляет атрибуты в модель всех контроллеров.

**Пример:**
```java
@ControllerAdvice
public class GlobalModelAttributes {
    @ModelAttribute("appName")
    public String getAppName() {
        return "My Application";
    }
}
```

### 225. Как работает @SessionAttributes с @ModelAttribute?

`@SessionAttributes` сохраняет атрибуты модели в HTTP-сессии. `@ModelAttribute` добавляет атрибуты в модель.

**Пример:**
```java
@Controller
@SessionAttributes("user")
public class UserController {
    @ModelAttribute("user")
    public User getUser() {
        return new User();
    }
}
```

### 226. Как работает @RequestPart?

`@RequestPart` — это аннотация для извлечения multipart-частей запроса.

**Пример:**
```java
@PostMapping("/upload")
public String upload(@RequestPart("file") MultipartFile file, @RequestPart("metadata") Metadata metadata) {
    // file и metadata из multipart-запроса
}
```

### 227. Как работает @CookieValue?

`@CookieValue` — это аннотация для извлечения значения cookie.

**Пример:**
```java
@GetMapping("/api/data")
public String getData(@CookieValue("sessionId") String sessionId) {
    return sessionId;
}
```

### 228. Как работает @RequestAttribute?

`@RequestAttribute` — это аннотация для извлечения атрибутов запроса (установленных фильтрами или перехватчиками).

**Пример:**
```java
@GetMapping("/api/data")
public String getData(@RequestAttribute("userId") Long userId) {
    return "User: " + userId;
}
```

### 229. Как работает @SessionAttribute?

`@SessionAttribute` — это аннотация для извлечения атрибутов HTTP-сессии.

**Пример:**
```java
@GetMapping("/api/data")
public String getData(@SessionAttribute("user") User user) {
    return "User: " + user.getName();
}
```

### 230. Как работает @RequestScope?

`@RequestScope` — это аннотация для указания scope бина как request. Один экземпляр на один HTTP-запрос.

### 231. Как работает @SessionScope?

`@SessionScope` — это аннотация для указания scope бина как session. Один экземпляр на одну HTTP-сессию.

### 232. Как работает @ApplicationScope?

`@ApplicationScope` — это аннотация для указания scope бина как application. Один экземпляр на жизненный цикл ServletContext.

### 233. Как работает @Scope(proxyMode = ScopedProxyMode.TARGET_CLASS)?

Используется для внедрения бинов с веб-скоупами (request, session) в синглтон-бины. Создает CGLIB-прокси, который делегирует вызовы к реальному бину в правильном контексте.

### 234. Как работает @Scope(proxyMode = ScopedProxyMode.INTERFACES)?

Аналогично TARGET_CLASS, но использует JDK Dynamic Proxy. Работает только если класс реализует интерфейс.

### 235. Как работает @Scope(proxyMode = ScopedProxyMode.NO)?

Отключает создание прокси. Используется для бинов со скоупом singleton или prototype.

### 236. Как работает @Scope(proxyMode = ScopedProxyMode.DEFAULT)?

Использует значение по умолчанию (обычно NO).

### 237. Как работает @Scope с кастомным scope?

Можно создать кастомный scope через интерфейс `Scope` и зарегистрировать его в `ConfigurableBeanFactory`.

**Пример:**
```java
@Bean
@Scope("myCustomScope")
public MyBean myBean() {
    return new MyBean();
}
```

### 238. Как работает @Scope с singleton?

По умолчанию все бины имеют scope singleton. Один экземпляр на весь Spring Context.

### 239. Как работает @Scope с prototype?

Новый экземпляр создается при каждом запросе. Spring не управляет полным жизненным циклом (не вызывает методы уничтожения).

### 240. Как работает @Scope с request?

Один экземпляр на один HTTP-запрос. Доступен только в веб-контексте.

### 241. Как работает @Scope с session?

Один экземпляр на одну HTTP-сессию. Доступен только в веб-контексте.

### 242. Как работает @Scope с application?

Один экземпляр на жизненный цикл ServletContext. Доступен только в веб-контексте.

### 243. Как работает @Scope с websocket?

Один экземпляр на одну WebSocket-сессию. Доступен только в веб-контексте.

### 244. Как работает @Scope с refresh?

Один экземпляр на одну конфигурацию Spring Cloud Config. Обновляется при изменении конфигурации.

### 245. Как работает @Scope с thread?

Один экземпляр на один поток. Не встроен в Spring, но может быть реализован кастомно.

### 246. Как работает @Scope с custom?

Можно создать кастомный scope через интерфейс `Scope` и зарегистрировать его в `ConfigurableBeanFactory`.

---

## 20. Spring MVC — валидация и обработка ошибок

### 247. Как работает @Valid и @Validated в Spring MVC?

- **@Valid (JSR-303/JSR-380)**: Стандартная аннотация Java для валидации. Активирует валидацию объекта.
- **@Validated (Spring)**: Расширение Spring для @Valid. Поддерживает группы валидации.

**Пример:**
```java
@PostMapping("/users")
public ResponseEntity<User> createUser(@Valid @RequestBody User user) {
    // user будет автоматически валидирован
}
```

### 248. Как работает @Pattern, @Size, @NotNull, @Min, @Max?

Это аннотации Bean Validation (JSR-380).

- **@NotNull**: Поле не может быть null.
- **@Size(min, max)**: Размер строки/коллекции.
- **@Min / @Max**: Минимальное/максимальное значение числа.
- **@Pattern(regexp)**: Регулярное выражение для строки.
- **@Email**: Валидация email.
- **@NotEmpty**: Не null и не пустая строка/коллекция.
- **@NotBlank**: Не null и не пустая строка (с учетом пробелов).

### 249. Как работает @ControllerAdvice с @ExceptionHandler для валидации?

`@ControllerAdvice` перехватывает `MethodArgumentNotValidException` (выбрасывается при неудачной валидации @Valid) и возвращает структурированный ответ с ошибками.

**Пример:**
```java
@ControllerAdvice
public class ValidationExceptionHandler {
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidation(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error -> 
            errors.put(error.getField(), error.getDefaultMessage()));
        return ResponseEntity.badRequest().body(errors);
    }
}
```

### 250. Как работает @Validated с группами валидации?

Позволяет применять разные правила валидации для разных сценариев (например, создание vs обновление).

**Пример:**
```java
public class User {
    @NotNull(groups = Create.class)
    @Null(groups = Update.class)
    private Long id;
    
    @NotBlank(groups = {Create.class, Update.class})
    private String name;
}

@PostMapping("/users")
public ResponseEntity<User> createUser(@Validated(Create.class) @RequestBody User user) {
    // валидация только для группы Create
}
```

### 251. Как работает @RestControllerAdvice с @ExceptionHandler?

`@RestControllerAdvice` — это комбинация `@ControllerAdvice` и `@ResponseBody`. Все методы обработки исключений автоматически возвращают JSON/XML.

### 252. Как работает @ExceptionHandler с ResponseEntity?

`@ExceptionHandler` может возвращать `ResponseEntity` для полного контроля над HTTP-ответом.

**Пример:**
```java
@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<ErrorResponse> handleNotFound(ResourceNotFoundException ex) {
    ErrorResponse error = new ErrorResponse("NOT_FOUND", ex.getMessage());
    return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
}
```

### 253. Как работает @ExceptionHandler с @ResponseStatus?

`@ExceptionHandler` может использовать `@ResponseStatus` для указания HTTP-статуса.

**Пример:**
```java
@ExceptionHandler(ResourceNotFoundException.class)
@ResponseStatus(HttpStatus.NOT_FOUND)
public ErrorResponse handleNotFound(ResourceNotFoundException ex) {
    return new ErrorResponse("NOT_FOUND", ex.getMessage());
}
```

### 254. Как работает @ExceptionHandler с @ResponseBody?

`@ExceptionHandler` может использовать `@ResponseBody` для возврата JSON/XML.

**Пример:**
```java
@ExceptionHandler(ResourceNotFoundException.class)
@ResponseBody
@ResponseStatus(HttpStatus.NOT_FOUND)
public ErrorResponse handleNotFound(ResourceNotFoundException ex) {
    return new ErrorResponse("NOT_FOUND", ex.getMessage());
}
```

### 255. Как работает @ExceptionHandler с @ControllerAdvice?

`@ExceptionHandler` в `@ControllerAdvice` обрабатывает исключения из всех контроллеров.

### 256. Как работает @ExceptionHandler с @RestControllerAdvice?

`@ExceptionHandler` в `@RestControllerAdvice` обрабатывает исключения из всех REST-контроллеров и возвращает JSON/XML.

### 257. Как работает @ExceptionHandler с @Order?

`@Order` определяет порядок обработки исключений. Чем меньше значение, тем выше приоритет.

### 258. Как работает @ExceptionHandler с @Priority?

`@Priority` (JSR-250) аналогично `@Order`, но учитывается также при разрешении зависимостей.

### 259. Как работает @ExceptionHandler с @ResponseStatusException?

`@ResponseStatusException` — это исключение, которое можно выбросить в любом месте кода, и оно автоматически преобразуется в HTTP-ответ с указанным статусом.

**Пример:**
```java
throw new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found");
```

### 260. Как работает @ExceptionHandler с @ResponseStatusException и @ControllerAdvice?

`@ControllerAdvice` может перехватывать `ResponseStatusException` и обрабатывать его кастомно.

### 261. Как работает @ExceptionHandler с @ResponseStatusException и @RestControllerAdvice?

`@RestControllerAdvice` может перехватывать `ResponseStatusException` и обрабатывать его кастомно, возвращая JSON/XML.

### 262. Как работает @ExceptionHandler с @ResponseStatusException и @ExceptionHandler?

`@ExceptionHandler` может перехватывать `ResponseStatusException` и обрабатывать его кастомно.

### 263. Как работает @ExceptionHandler с @ResponseStatusException и @ControllerAdvice?

`@ControllerAdvice` может перехватывать `ResponseStatusException` и обрабатывать его кастомно.

### 264. Как работает @ExceptionHandler с @ResponseStatusException и @RestControllerAdvice?

`@RestControllerAdvice` может перехватывать `ResponseStatusException` и обрабатывать его кастомно, возвращая JSON/XML.

### 265. Как работает @ExceptionHandler с @ResponseStatusException и @ExceptionHandler?

`@ExceptionHandler` может перехватывать `ResponseStatusException` и обрабатывать его кастомно.

---

## 21. Spring MVC — CORS, сессии, фильтры

### 266. Как работает @CrossOrigin на уровне контроллера?

`@CrossOrigin` на уровне контроллера применяется ко всем методам контроллера.

**Пример:**
```java
@RestController
@CrossOrigin(origins = "http://example.com")
public class MyController {
    // все методы доступны с http://example.com
}
```

### 267. Как работает @CrossOrigin на уровне метода?

`@CrossOrigin` на уровне метода применяется только к конкретному методу.

**Пример:**
```java
@GetMapping("/api/data")
@CrossOrigin(origins = "http://example.com")
public String getData() {
    return "data";
}
```

### 268. Как работает @CrossOrigin с глобальной конфигурацией CORS?

Глобальная конфигурация CORS настраивается через `WebMvcConfigurer`.

**Пример:**
```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/api/**")
            .allowedOrigins("http://example.com")
            .allowedMethods("GET", "POST");
    }
}
```

### 269. Как работает @CrossOrigin с allowCredentials?

`allowCredentials = true` разрешает отправку куки и заголовков авторизации.

**Пример:**
```java
@CrossOrigin(origins = "http://example.com", allowCredentials = "true")
```

### 270. Как работает @CrossOrigin с allowedHeaders?

`allowedHeaders` указывает, какие заголовки разрешены в запросе.

**Пример:**
```java
@CrossOrigin(allowedHeaders = {"Authorization", "Content-Type"})
```

### 271. Как работает @CrossOrigin с exposedHeaders?

`exposedHeaders` указывает, какие заголовки будут доступны клиенту.

**Пример:**
```java
@CrossOrigin(exposedHeaders = {"X-Custom-Header"})
```

### 272. Как работает @CrossOrigin с maxAge?

`maxAge` указывает, сколько секунд браузер может кэшировать preflight-ответ.

**Пример:**
```java
@CrossOrigin(maxAge = 3600)
```

### 273. Как работает @CrossOrigin с methods?

`methods` указывает, какие HTTP методы разрешены.

**Пример:**
```java
@CrossOrigin(methods = {RequestMethod.GET, RequestMethod.POST})
```

### 274. Как работает @CrossOrigin с origins?

`origins` указывает, какие источники (домены) разрешены.

**Пример:**
```java
@CrossOrigin(origins = {"http://example.com", "http://localhost:3000"})
```

### 275. Как работает @CrossOrigin с allowPrivateNetwork?

`allowPrivateNetwork` разрешает доступ из частных сетей.

### 276. Как работает Filter в Spring MVC?

Filter — это стандартный интерфейс Java Servlet API для перехвата HTTP-запросов и ответов.

**Пример:**
```java
@Component
public class MyFilter implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) {
        // логика до
        chain.doFilter(request, response);
        // логика после
    }
}
```

### 277. Как работает HandlerInterceptor в Spring MVC?

`HandlerInterceptor` — это интерфейс Spring для перехвата запросов на уровне контроллера.

**Методы:**
- `preHandle()`: Выполняется до контроллера.
- `postHandle()`: Выполняется после контроллера, но до рендеринга View.
- `afterCompletion()`: Выполняется после рендеринга View.

### 278. Как работает OncePerRequestFilter?

`OncePerRequestFilter` — это абстрактный класс Spring, который гарантирует, что фильтр выполняется только один раз за запрос (даже если запрос проходит через несколько цепочек фильтров).

### 279. Как работает @WebFilter?

`@WebFilter` — это аннотация Servlet API для регистрации фильтра.

**Пример:**
```java
@WebFilter(urlPatterns = "/api/*")
public class MyFilter implements Filter {
    // ...
}
```

### 280. Как работает @Order с Filter?

`@Order` определяет порядок выполнения фильтров. Чем меньше значение, тем выше приоритет.

### 281. Как работает @Order с HandlerInterceptor?

`@Order` определяет порядок выполнения перехватчиков. Чем меньше значение, тем выше приоритет.

### 282. Как работает @Order с Filter и HandlerInterceptor?

`@Order` работает независимо для фильтров и перехватчиков. Фильтры выполняются до перехватчиков.

### 283. Как работает @Order с FilterRegistrationBean?

`FilterRegistrationBean` позволяет настроить порядок фильтров через `setOrder()`.

### 284. Как работает @Order с HandlerInterceptor и WebMvcConfigurer?

Порядок перехватчиков настраивается через `WebMvcConfigurer.addInterceptors()`.

### 285. Как работает @Order с Filter и OncePerRequestFilter?

`@Order` работает одинаково для `Filter` и `OncePerRequestFilter`.

---

## 22. Spring Security — аутентификация

### 294. Как работает Spring Security Filter Chain?

Spring Security работает через цепочку фильтров (Filter Chain). Каждый запрос проходит через последовательность фильтров, каждый из которых отвечает за определенную задачу безопасности.

**Основные фильтры:**
- `SecurityContextPersistenceFilter`: Восстанавливает SecurityContext из сессии.
- `UsernamePasswordAuthenticationFilter`: Обрабатывает форму логина.
- `BasicAuthenticationFilter`: Обрабатывает Basic Auth.
- `ExceptionTranslationFilter`: Обрабатывает исключения безопасности.
- `FilterSecurityInterceptor`: Проверяет права доступа.

### 295. Как работает SecurityContextHolder?

`SecurityContextHolder` — это хранилище контекста безопасности для текущего потока.

**Стратегии хранения:**
- `MODE_THREADLOCAL` (по умолчанию): Хранит контекст в ThreadLocal.
- `MODE_INHERITABLETHREADLOCAL`: Передает контекст дочерним потокам.
- `MODE_GLOBAL`: Хранит контекст глобально (для всех потоков).

### 296. Как работает AuthenticationManager?

`AuthenticationManager` — это интерфейс для аутентификации пользователей.

**Основной метод:**
```java
Authentication authenticate(Authentication authentication) throws AuthenticationException;
```

**Реализации:**
- `ProviderManager`: Делегирует аутентификацию одному или нескольким `AuthenticationProvider`.

### 297. Как работает AuthenticationProvider?

`AuthenticationProvider` — это интерфейс для конкретного способа аутентификации.

**Методы:**
- `authenticate()`: Выполняет аутентификацию.
- `supports()`: Проверяет, поддерживает ли провайдер данный тип аутентификации.

**Примеры:**
- `DaoAuthenticationProvider`: Аутентификация через БД.
- `LdapAuthenticationProvider`: Аутентификация через LDAP.
- `JwtAuthenticationProvider`: Аутентификация через JWT.

### 298. Как работает UserDetailsService?

`UserDetailsService` — это интерфейс для загрузки данных пользователя.

**Метод:**
```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```

**Использование:**
- Реализуется для загрузки пользователя из БД.
- Используется `DaoAuthenticationProvider` для аутентификации.

### 299. Как работает PasswordEncoder?

`PasswordEncoder` — это интерфейс для хеширования паролей.

**Методы:**
- `encode()`: Хеширует пароль.
- `matches()`: Проверяет пароль против хеша.

**Реализации:**
- `BCryptPasswordEncoder`: Использует BCrypt.
- `SCryptPasswordEncoder`: Использует SCrypt.
- `Argon2PasswordEncoder`: Использует Argon2.
- `Pbkdf2PasswordEncoder`: Использует PBKDF2.

### 300. Как работает @EnableWebSecurity?

`@EnableWebSecurity` — это аннотация для включения поддержки Spring Security в веб-приложении.

**Что делает:**
- Регистрирует `FilterChainProxy` (главный фильтр безопасности).
- Настраивает цепочку фильтров безопасности.
- Включает поддержку аннотаций безопасности.

### 301. Как работает SecurityFilterChain?

`SecurityFilterChain` — это интерфейс для настройки цепочки фильтров безопасности.

**Пример:**
```java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/public/**").permitAll()
            .anyRequest().authenticated()
        )
        .formLogin(Customizer.withDefaults());
    return http.build();
}
```

### 302. Как работает @PreAuthorize?

`@PreAuthorize` — это аннотация для проверки прав доступа перед вызовом метода.

**Пример:**
```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    // только для ADMIN
}
```

### 303. Как работает @PostAuthorize?

`@PostAuthorize` — это аннотация для проверки прав доступа после вызова метода.

**Пример:**
```java
@PostAuthorize("returnObject.owner == authentication.name")
public Document getDocument(Long id) {
    // проверка после получения документа
}
```

### 304. Как работает @Secured?

`@Secured` — это аннотация для проверки ролей пользователя.

**Пример:**
```java
@Secured("ROLE_ADMIN")
public void deleteUser(Long id) {
    // только для ADMIN
}
```

### 305. Как работает @RolesAllowed?

`@RolesAllowed` — это аннотация JSR-250 для проверки ролей пользователя.

**Пример:**
```java
@RolesAllowed("ADMIN")
public void deleteUser(Long id) {
    // только для ADMIN
}
```

### 306. Как работает @EnableGlobalMethodSecurity?

`@EnableGlobalMethodSecurity` — это аннотация для включения поддержки аннотаций безопасности на уровне методов.

**Параметры:**
- `prePostEnabled`: Включает @PreAuthorize и @PostAuthorize.
- `securedEnabled`: Включает @Secured.
- `jsr250Enabled`: Включает @RolesAllowed.

---

## 23. Spring Security — авторизация и защита

### 309. Как работает CSRF защита в Spring Security?

CSRF (Cross-Site Request Forgery) защита предотвращает атаки, когда злоумышленник заставляет пользователя выполнить нежелательное действие.

**Как работает:**
1. Сервер генерирует CSRF-токен и отправляет его клиенту.
2. Клиент должен включить этот токен в каждый запрос (обычно в заголовок или форму).
3. Сервер проверяет токен при каждом запросе.

**Отключение для REST API:**
```java
http.csrf(csrf -> csrf.disable());
```

### 310. Как работает CORS в Spring Security?

CORS (Cross-Origin Resource Sharing) настраивается через `HttpSecurity`.

**Пример:**
```java
http.cors(cors -> cors.configurationSource(corsConfigurationSource()));
```

### 311. Как работает @EnableMethodSecurity?

`@EnableMethodSecurity` — это современная замена `@EnableGlobalMethodSecurity` (начиная с Spring Security 6.x).

**Пример:**
```java
@Configuration
@EnableMethodSecurity
public class SecurityConfig {
    // ...
}
```

### 312. Как работает @EnableWebSecurity с SecurityFilterChain?

`@EnableWebSecurity` включает поддержку Spring Security. `SecurityFilterChain` настраивает цепочку фильтров.

**Пример:**
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
            )
            .formLogin(Customizer.withDefaults());
        return http.build();
    }
}
```

### 313. Как работает @EnableWebSecurity с @EnableMethodSecurity?

Обе аннотации могут использоваться вместе. `@EnableWebSecurity` включает веб-безопасность, `@EnableMethodSecurity` включает безопасность на уровне методов.

### 314. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity?

`@EnableGlobalMethodSecurity` — это старая версия `@EnableMethodSecurity`. Обе могут использоваться с `@EnableWebSecurity`.

### 315. Как работает @EnableWebSecurity с @EnableReactiveMethodSecurity?

`@EnableReactiveMethodSecurity` используется для реактивных приложений (WebFlux).

### 316. Как работает @EnableWebSecurity с @EnableWebFluxSecurity?

`@EnableWebFluxSecurity` используется для реактивных приложений (WebFlux) вместо `@EnableWebSecurity`.

### 317. Как работает @EnableWebSecurity с @EnableOAuth2Client?

`@EnableOAuth2Client` включает поддержку OAuth2 клиента.

### 318. Как работает @EnableWebSecurity с @EnableOAuth2Sso?

`@EnableOAuth2Sso` включает поддержку Single Sign-On через OAuth2.

### 319. Как работает @EnableWebSecurity с @EnableResourceServer?

`@EnableResourceServer` включает поддержку OAuth2 Resource Server.

### 320. Как работает @EnableWebSecurity с @EnableAuthorizationServer?

`@EnableAuthorizationServer` включает поддержку OAuth2 Authorization Server.

### 321. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableMethodSecurity?

`@EnableGlobalMethodSecurity` и `@EnableMethodSecurity` не могут использоваться вместе. Нужно выбрать одну.

### 322. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableReactiveMethodSecurity?

`@EnableGlobalMethodSecurity` и `@EnableReactiveMethodSecurity` не могут использоваться вместе. Нужно выбрать одну.

### 323. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableReactiveMethodSecurity?

`@EnableMethodSecurity` и `@EnableReactiveMethodSecurity` не могут использоваться вместе. Нужно выбрать одну.

### 324. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableWebFluxSecurity?

`@EnableGlobalMethodSecurity` и `@EnableWebFluxSecurity` не могут использоваться вместе. Нужно выбрать одну.

### 325. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableWebFluxSecurity?

`@EnableMethodSecurity` и `@EnableWebFluxSecurity` не могут использоваться вместе. Нужно выбрать одну.

### 326. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableOAuth2Client?

`@EnableGlobalMethodSecurity` и `@EnableOAuth2Client` могут использоваться вместе.

### 327. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableOAuth2Client?

`@EnableMethodSecurity` и `@EnableOAuth2Client` могут использоваться вместе.

### 328. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableOAuth2Sso?

`@EnableGlobalMethodSecurity` и `@EnableOAuth2Sso` могут использоваться вместе.

### 329. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableOAuth2Sso?

`@EnableMethodSecurity` и `@EnableOAuth2Sso` могут использоваться вместе.

### 330. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableResourceServer?

`@EnableGlobalMethodSecurity` и `@EnableResourceServer` могут использоваться вместе.

### 331. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableResourceServer?

`@EnableMethodSecurity` и `@EnableResourceServer` могут использоваться вместе.

### 332. Как работает @EnableWebSecurity с @EnableGlobalMethodSecurity и @EnableAuthorizationServer?

`@EnableGlobalMethodSecurity` и `@EnableAuthorizationServer` могут использоваться вместе.

### 333. Как работает @EnableWebSecurity с @EnableMethodSecurity и @EnableAuthorizationServer?

`@EnableMethodSecurity` и `@EnableAuthorizationServer` могут использоваться вместе.

---

## 24. Spring Security — OAuth2 / JWT

### 334. Как работает JWT (JSON Web Token)?

JWT — это компактный способ передачи данных между сторонами в виде JSON-объекта.

**Структура JWT:**
1. **Header**: Тип токена и алгоритм подписи.
2. **Payload**: Данные (claims).
3. **Signature**: Подпись для проверки целостности.

**Как работает:**
1. Пользователь логинится, сервер создает JWT.
2. Клиент сохраняет JWT (обычно в localStorage или cookie).
3. Клиент отправляет JWT в заголовке `Authorization: Bearer <token>`.
4. Сервер проверяет подпись и извлекает данные.

### 335. Как работает OAuth2 в Spring Security?

OAuth2 — это протокол авторизации, который позволяет приложениям получать ограниченный доступ к ресурсам пользователя.

**Роли OAuth2:**
- **Resource Owner**: Владелец ресурса (пользователь).
- **Client**: Приложение, запрашивающее доступ.
- **Authorization Server**: Сервер, выдающий токены.
- **Resource Server**: Сервер, предоставляющий ресурсы.

**Гранты OAuth2:**
- **Authorization Code**: Для веб-приложений.
- **Client Credentials**: Для сервер-сервер.
- **Password**: Для доверенных приложений (устарел).
- **Implicit**: Для SPA (устарел).

### 336. Как работает @EnableOAuth2Client?

`@EnableOAuth2Client` включает поддержку OAuth2 клиента.

**Что делает:**
- Создает `OAuth2ClientContext`.
- Настраивает `OAuth2RestTemplate`.
- Обрабатывает редиректы на Authorization Server.

### 337. Как работает @EnableOAuth2Sso?

`@EnableOAuth2Sso` включает поддержку Single Sign-On через OAuth2.

**Что делает:**
- Настраивает аутентификацию через OAuth2.
- Перенаправляет неаутентифицированных пользователей на Authorization Server.
- Обрабатывает callback после аутентификации.

### 338. Как работает @EnableResourceServer?

`@EnableResourceServer` включает поддержку OAuth2 Resource Server.

**Что делает:**
- Проверяет JWT или токены доступа.
- Настраивает фильтры для проверки токенов.
- Извлекает аутентификацию из токена.

### 339. Как работает @EnableAuthorizationServer?

`@EnableAuthorizationServer` включает поддержку OAuth2 Authorization Server.

**Что делает:**
- Настраивает endpoints для выдачи токенов.
- Управляет клиентами и токенами.
- Обрабатывает гранты OAuth2.

### 340. Как работает JwtDecoder?

`JwtDecoder` — это интерфейс для декодирования и проверки JWT.

**Реализации:**
- `NimbusJwtDecoder`: Использует библиотеку Nimbus.
- `JwtDecoders`: Фабрика для создания декодеров.

### 341. Как работает JwtEncoder?

`JwtEncoder` — это интерфейс для создания и подписи JWT.

**Реализации:**
- `NimbusJwtEncoder`: Использует библиотеку Nimbus.

### 342. Как работает JwtAuthenticationToken?

`JwtAuthenticationToken` — это реализация `Authentication`, которая содержит JWT.

**Содержит:**
- `token`: JWT.
- `principal`: Данные пользователя.
- `authorities`: Права доступа.

### 343. Как работает JwtAuthenticationProvider?

`JwtAuthenticationProvider` — это `AuthenticationProvider`, который аутентифицирует пользователя по JWT.

**Как работает:**
1. Получает JWT из запроса.
2. Декодирует и проверяет JWT через `JwtDecoder`.
3. Создает `JwtAuthenticationToken`.
4. Возвращает аутентифицированного пользователя.

### 344. Как работает JwtGrantedAuthoritiesConverter?

`JwtGrantedAuthoritiesConverter` — это конвертер, который извлекает права доступа из JWT.

**Как работает:**
1. Извлекает claims из JWT.
2. Преобразует их в `GrantedAuthority`.
3. Возвращает список прав доступа.

### 345. Как работает JwtAuthenticationConverter?

`JwtAuthenticationConverter` — это конвертер, который преобразует JWT в `Authentication`.

**Как работает:**
1. Декодирует JWT.
2. Извлекает права доступа через `JwtGrantedAuthoritiesConverter`.
3. Создает `JwtAuthenticationToken`.

### 346. Как работает JwtIssuerReactiveAuthenticationManager?

`JwtIssuerReactiveAuthenticationManager` — это реактивный менеджер аутентификации для JWT.

### 347. Как работает JwtReactiveAuthenticationManager?

`JwtReactiveAuthenticationManager` — это реактивный менеджер аутентификации для JWT.

### 348. Как работает JwtSecurityMarker?

`JwtSecurityMarker` — это маркерный интерфейс для JWT безопасности.

### 349. Как работает JwtSecurityConfigurer?

`JwtSecurityConfigurer` — это конфигуратор для настройки JWT безопасности.

### 350. Как работает JwtSecurityConfigurerAdapter?

`JwtSecurityConfigurerAdapter` — это адаптер для настройки JWT безопасности.

---

## 25. Spring Data JPA — основы

### 351. Как работает Spring Data JPA?

Spring Data JPA — это абстракция над JPA, которая автоматически генерирует реализации репозиториев на основе имен методов.

**Как работает:**
1. Вы создаете интерфейс, расширяющий `JpaRepository`.
2. Spring Data JPA использует `JpaRepositoryFactoryBean` для создания прокси-реализации.
3. Прокси анализирует имя метода и генерирует JPQL-запрос.
4. Запрос выполняется через `EntityManager`.

### 352. Как работает JpaRepository?

`JpaRepository` — это интерфейс Spring Data JPA, который предоставляет готовые методы для работы с БД.

**Методы:**
- `findAll()`, `findById()`, `save()`, `delete()`, `count()`.
- `findAll(Specification)`, `findAll(Example)`.
- `getOne()`, `getById()`.

### 353. Как работает CrudRepository?

`CrudRepository` — это базовый интерфейс Spring Data для CRUD-операций.

**Методы:**
- `save()`, `saveAll()`.
- `findById()`, `findAll()`, `findAllById()`.
- `count()`, `existsById()`.
- `delete()`, `deleteById()`, `deleteAll()`.

### 354. Как работает PagingAndSortingRepository?

`PagingAndSortingRepository` расширяет `CrudRepository` и добавляет поддержку пагинации и сортировки.

**Методы:**
- `findAll(Pageable)`: Возвращает `Page` с пагинацией.
- `findAll(Sort)`: Возвращает список с сортировкой.

### 355. Как работает @Query в Spring Data JPA?

`@Query` позволяет написать кастомный JPQL или нативный SQL запрос.

**Пример:**
```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

### 356. Как работает @Modifying в Spring Data JPA?

`@Modifying` используется с `@Query` для UPDATE/DELETE запросов.

**Пример:**
```java
@Modifying
@Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
int updateStatus(@Param("id") Long id, @Param("status") String status);
```

### 357. Как работает @Transactional в Spring Data JPA?

Spring Data JPA автоматически оборачивает каждый метод репозитория в транзакцию. Методы чтения используют `readOnly = true`, методы записи — `readOnly = false`.

### 358. Как работает @NoRepositoryBean?

`@NoRepositoryBean` указывает Spring Data JPA не создавать прокси для этого интерфейса. Используется для создания базовых интерфейсов репозиториев.

### 359. Как работает @EnableJpaRepositories?

`@EnableJpaRepositories` включает поддержку Spring Data JPA и указывает, где искать интерфейсы репозиториев.

**Параметры:**
- `basePackages`: Пакеты для сканирования.
- `entityManagerFactoryRef`: Ссылка на EntityManagerFactory.
- `transactionManagerRef`: Ссылка на TransactionManager.

### 360. Как работает @EnableJpaAuditing?

`@EnableJpaAuditing` включает аудит JPA сущностей.

**Использование:**
```java
@Configuration
@EnableJpaAuditing
public class JpaConfig {
    // ...
}
```

### 361. Как работает @CreatedDate, @CreatedBy, @LastModifiedDate, @LastModifiedBy?

Это аннотации для автоматического заполнения полей аудита.

**Пример:**
```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    @CreatedDate
    private LocalDateTime createdAt;
    
    @LastModifiedDate
    private LocalDateTime updatedAt;
    
    @CreatedBy
    private String createdBy;
    
    @LastModifiedBy
    private String updatedBy;
}
```

### 362. Как работает @EntityListeners?

`@EntityListeners` указывает классы-слушатели для JPA сущности.

**Пример:**
```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    // ...
}
```

### 363. Как работает AuditingEntityListener?

`AuditingEntityListener` — это слушатель JPA, который автоматически заполняет поля аудита.

**Как работает:**
1. Перехватывает события `@PrePersist` и `@PreUpdate`.
2. Заполняет поля с `@CreatedDate`, `@LastModifiedDate` и т.д.
3. Использует `AuditorAware` для получения текущего пользователя.

### 364. Как работает AuditorAware?

`AuditorAware` — это интерфейс для получения текущего пользователя для аудита.

**Пример:**
```java
public class SpringSecurityAuditorAware implements AuditorAware<String> {
    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.ofNullable(SecurityContextHolder.getContext().getAuthentication())
            .map(auth -> auth.getName());
    }
}
```

### 365. Как работает @MappedSuperclass?

`@MappedSuperclass` — это аннотация JPA для создания базового класса сущности.

**Пример:**
```java
@MappedSuperclass
public abstract class BaseEntity {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    @CreatedDate
    private LocalDateTime createdAt;
}
```

### 366. Как работает @Inheritance в JPA?

`@Inheritance` определяет стратегию наследования для JPA сущностей.

**Стратегии:**
- `SINGLE_TABLE`: Все классы в одной таблице.
- `TABLE_PER_CLASS`: Каждый класс в своей таблице.
- `JOINED`: Каждый класс в своей таблице с JOIN.

### 367. Как работает @DiscriminatorColumn?

`@DiscriminatorColumn` определяет столбец-дискриминатор для стратегии SINGLE_TABLE.

**Пример:**
```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "type", discriminatorType = DiscriminatorType.STRING)
public class Animal {
    // ...
}
```

### 368. Как работает @DiscriminatorValue?

`@DiscriminatorValue` указывает значение дискриминатора для конкретного подкласса.

**Пример:**
```java
@Entity
@DiscriminatorValue("DOG")
public class Dog extends Animal {
    // ...
}
```

### 369. Как работает @SecondaryTable?

`@SecondaryTable` позволяет маппить сущность на несколько таблиц.

**Пример:**
```java
@Entity
@Table(name = "users")
@SecondaryTable(name = "user_details", pkJoinColumns = @PrimaryKeyJoinColumn(name = "user_id"))
public class User {
    @Column(table = "user_details")
    private String address;
}
```

### 370. Как работает @AttributeOverride?

`@AttributeOverride` переопределяет маппинг поля из `@MappedSuperclass`.

**Пример:**
```java
@Entity
@AttributeOverride(name = "id", column = @Column(name = "user_id"))
public class User extends BaseEntity {
    // ...
}
```

---

## 26. Spring Data JPA — запросы и оптимизация

### 371. Как работает Specification в Spring Data JPA?

`Specification` — это интерфейс для создания динамических запросов через Criteria API.

**Пример:**
```java
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {
}

// Использование:
Specification<User> spec = (root, query, cb) -> 
    cb.equal(root.get("status"), "ACTIVE");
List<User> users = userRepository.findAll(spec);
```

### 372. Как работает ExampleMatcher в Spring Data JPA?

`ExampleMatcher` — это класс для настройки поиска по примеру (Query by Example).

**Пример:**
```java
User probe = new User();
probe.setName("John");
ExampleMatcher matcher = ExampleMatcher.matching()
    .withIgnoreCase()
    .withStringMatcher(StringMatcher.CONTAINING);
Example<User> example = Example.of(probe, matcher);
List<User> users = userRepository.findAll(example);
```

### 373. Как работает Query by Example в Spring Data JPA?

Query by Example (QBE) — это техника поиска, где вы создаете объект-пример и ищете похожие.

**Пример:**
```java
User probe = new User();
probe.setStatus("ACTIVE");
Example<User> example = Example.of(probe);
List<User> users = userRepository.findAll(example);
```

### 374. Как работает @Procedure в Spring Data JPA?

`@Procedure` позволяет вызывать хранимые процедуры.

**Пример:**
```java
@Procedure("GET_USER_COUNT")
int getUserCount();
```

### 375. Как работает @NamedQuery в JPA?

`@NamedQuery` — это статический именованный запрос.

**Пример:**
```java
@Entity
@NamedQuery(name = "User.findByEmail", query = "SELECT u FROM User u WHERE u.email = :email")
public class User {
    // ...
}
```

### 376. Как работает @NamedNativeQuery в JPA?

`@NamedNativeQuery` — это статический именованный нативный SQL запрос.

**Пример:**
```java
@Entity
@NamedNativeQuery(name = "User.findActive", query = "SELECT * FROM users WHERE status = 'ACTIVE'", resultClass = User.class)
public class User {
    // ...
}
```

### 377. Как работает @SqlResultSetMapping в JPA?

`@SqlResultSetMapping` маппит результат нативного SQL запроса на сущности.

**Пример:**
```java
@SqlResultSetMapping(name = "UserMapping", entities = @EntityResult(entityClass = User.class))
```

### 378. Как работает @ConstructorResult в JPA?

`@ConstructorResult` маппит результат запроса на конструктор DTO.

**Пример:**
```java
@SqlResultSetMapping(name = "UserDtoMapping", classes = @ConstructorResult(targetClass = UserDto.class, columns = {
    @ColumnResult(name = "id", type = Long.class),
    @ColumnResult(name = "name", type = String.class)
}))
```

### 379. Как работает @ColumnResult в JPA?

`@ColumnResult` маппит колонку результата на параметр конструктора.

### 380. Как работает @EntityResult в JPA?

`@EntityResult` маппит результат на сущность.

### 381. Как работает @FieldResult в JPA?

`@FieldResult` маппит колонку результата на поле сущности.

### 382. Как работает @Subselect в Hibernate?

`@Subselect` маппит сущность на подзапрос (immutable view).

**Пример:**
```java
@Entity
@Subselect("SELECT u.id, u.name, COUNT(o.id) as order_count FROM users u LEFT JOIN orders o ON u.id = o.user_id GROUP BY u.id")
public class UserSummary {
    @Id
    private Long id;
    private String name;
    private Long orderCount;
}
```

### 383. Как работает @Immutable в Hibernate?

`@Immutable` указывает, что сущность неизменяема. Hibernate не будет выполнять UPDATE/DELETE для таких сущностей.

### 384. Как работает @Synchronize в Hibernate?

`@Synchronize` указывает Hibernate, какие таблицы нужно синхронизировать перед выполнением запроса.

**Пример:**
```java
@Entity
@Subselect("...")
@Synchronize({"users", "orders"})
public class UserSummary {
    // ...
}
```

### 385. Как работает @Where в Hibernate?

`@Where` добавляет условие WHERE ко всем запросам к сущности.

**Пример:**
```java
@Entity
@Where(clause = "deleted = false")
public class User {
    // ...
}
```

### 386. Как работает @FilterDef и @Filter в Hibernate?

`@FilterDef` определяет фильтр, `@Filter` применяет его к сущности.

**Пример:**
```java
@Entity
@FilterDef(name = "statusFilter", parameters = @ParamDef(name = "status", type = "string"))
@Filter(name = "statusFilter", condition = "status = :status")
public class User {
    // ...
}
```

### 387. Как работает @FilterJoinTable в Hibernate?

`@FilterJoinTable` применяет фильтр к join-таблице.

### 388. Как работает @Fetch в Hibernate?

`@Fetch` определяет стратегию загрузки связанных сущностей.

**Стратегии:**
- `SELECT`: Отдельный SELECT для каждой связи.
- `JOIN`: JOIN в одном запросе.
- `SUBSELECT`: Подзапрос для загрузки всех связей.

### 389. Как работает @FetchProfile в Hibernate?

`@FetchProfile` позволяет определить профиль загрузки для разных сценариев.

### 390. Как работает @BatchSize в Hibernate?

`@BatchSize` определяет размер пакетной загрузки для ленивых ассоциаций.

**Пример:**
```java
@Entity
public class User {
    @OneToMany(mappedBy = "user")
    @BatchSize(size = 10)
    private List<Order> orders;
}
```

### 391. Как работает @LazyCollection в Hibernate?

`@LazyCollection` определяет стратегию ленивой загрузки коллекций.

**Стратегии:**
- `TRUE`: Ленивая загрузка.
- `FALSE`: Жадная загрузка.
- `EXTRA`: Еще более ленивая (не загружает элементы до обращения).

### 392. Как работает @LazyToOne в Hibernate?

`@LazyToOne` определяет стратегию ленивой загрузки для точечных ассоциаций.

**Стратегии:**
- `PROXY`: Использует прокси.
- `NO_PROXY`: Использует байт-код enhancement.
- `FALSE`: Жадная загрузка.

### 393. Как работает @NotFound в Hibernate?

`@NotFound` определяет поведение при отсутствии связанной сущности.

**Стратегии:**
- `IGNORE`: Игнорировать отсутствие.
- `EXCEPTION`: Выбросить исключение.

### 394. Как работает @OptimisticLocking в Hibernate?

`@OptimisticLocking` определяет стратегию оптимистичной блокировки.

**Стратегии:**
- `VERSION`: Использовать поле с @Version.
- `ALL`: Проверять все поля.
- `DIRTY`: Проверять только измененные поля.
- `NONE`: Не использовать.

### 395. Как работает @OptimisticLock в Hibernate?

`@OptimisticLock` определяет, какие поля проверять при оптимистичной блокировке.

### 396. Как работает @DynamicUpdate в Hibernate?

`@DynamicUpdate` генерирует UPDATE только для измененных полей, а не для всех.

**Пример:**
```java
@Entity
@DynamicUpdate
public class User {
    // ...
}
```

### 397. Как работает @DynamicInsert в Hibernate?

`@DynamicInsert` генерирует INSERT только для не-null полей.

### 398. Как работает @SelectBeforeUpdate в Hibernate?

`@SelectBeforeUpdate` загружает текущее состояние сущности перед UPDATE, чтобы определить, какие поля изменились.

### 399. Как работает @Cacheable в JPA?

`@Cacheable` включает кэширование второго уровня (L2) для сущности.

**Пример:**
```java
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class User {
    // ...
}
```

### 400. Как работает @Cache в Hibernate?

`@Cache` настраивает кэш второго уровня для сущности.

**Стратегии:**
- `READ_ONLY`: Только для чтения.
- `READ_WRITE`: Чтение и запись.
- `NONSTRICT_READ_WRITE`: Нестрогое чтение и запись.
- `TRANSACTIONAL`: Транзакционная.

### 401. Как работает @NaturalId в Hibernate?

`@NaturalId` указывает, что поле является естественным идентификатором (например, email).

**Пример:**
```java
@Entity
public class User {
    @Id
    private Long id;
    
    @NaturalId
    private String email;
}
```

### 402. Как работает @RowId в Hibernate?

`@RowId` включает поддержку ROWID для сущности (для UPDATE/DELETE по ROWID).

### 403. Как работает @Check в Hibernate?

`@Check` добавляет CHECK constraint на уровне БД.

**Пример:**
```java
@Entity
@Check(constraints = "salary > 0")
public class Employee {
    // ...
}
```

---

## 27. Spring Data JPA — N+1, EntityGraph, Batch

### 404. Как решить проблему N+1 запросов в JPA/Hibernate?

Проблема N+1 возникает, когда для получения связанных сущностей выполняется N дополнительных запросов.

**Решения:**
1. **JOIN FETCH**: Использовать `JOIN FETCH` в JPQL.
2. **@EntityGraph**: Использовать `@EntityGraph` для указания графа загрузки.
3. **@BatchSize**: Использовать `@BatchSize` для пакетной загрузки.
4. **@Fetch(FetchMode.JOIN)**: Использовать `@Fetch(FetchMode.JOIN)`.

### 405. Как работает @EntityGraph в Spring Data JPA?

`@EntityGraph` позволяет указать, какие ассоциации загружать жадным способом.

**Пример:**
```java
@EntityGraph(attributePaths = {"orders", "profile"})
@Query("SELECT u FROM User u WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

### 406. Как работает @NamedEntityGraph в JPA?

`@NamedEntityGraph` определяет именованный граф загрузки.

**Пример:**
```java
@Entity
@NamedEntityGraph(name = "User.orders", attributeNodes = @NamedAttributeNode("orders"))
public class User {
    // ...
}
```

### 407. Как работает @NamedAttributeNode в JPA?

`@NamedAttributeNode` указывает атрибут для загрузки в графе.

### 408. Как работает @NamedSubgraph в JPA?

`@NamedSubgraph` определяет подграф для вложенных ассоциаций.

### 409. Как работает @NamedEntityGraphs в JPA?

`@NamedEntityGraphs` группирует несколько `@NamedEntityGraph`.

### 410. Как работает @EntityGraph с Spring Data JPA?

`@EntityGraph` в Spring Data JPA генерирует JPQL с JOIN FETCH для указанных атрибутов.

### 411. Как работает @EntityGraph с type = LOAD?

`LOAD` — загружает указанные атрибуты жадным способом, остальные — по умолчанию.

### 412. Как работает @EntityGraph с type = FETCH?

`FETCH` — загружает только указанные атрибуты жадным способом, остальные — ленивым.

### 413. Как работает @EntityGraph с @NamedEntityGraph?

`@EntityGraph` может ссылаться на `@NamedEntityGraph` по имени.

**Пример:**
```java
@EntityGraph("User.orders")
@Query("SELECT u FROM User u WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

### 414. Как работает @EntityGraph с attributePaths?

`attributePaths` позволяет указать атрибуты для жадной загрузки прямо в аннотации.

### 415. Как работает @EntityGraph с @NamedAttributeNode?

`@EntityGraph` может использовать `@NamedAttributeNode` из `@NamedEntityGraph`.

### 416. Как работает @EntityGraph с @NamedSubgraph?

`@EntityGraph` может использовать `@NamedSubgraph` для вложенных ассоциаций.

### 417. Как работает @EntityGraph с @NamedEntityGraphs?

`@EntityGraph` может ссылаться на граф из `@NamedEntityGraphs`.

### 418. Как работает @EntityGraph с Spring Data JPA и Hibernate?

Spring Data JPA генерирует JPQL с JOIN FETCH на основе `@EntityGraph`.

### 419. Как работает @EntityGraph с Spring Data JPA и Hibernate?

Spring Data JPA генерирует JPQL с JOIN FETCH на основе `@EntityGraph`.

### 420. Как работает @EntityGraph с Spring Data JPA и Hibernate?

Spring Data JPA генерирует JPQL с JOIN FETCH на основе `@EntityGraph`.

---

## 28. Spring Data JPA — репозитории под капотом

### 421. Как Spring Data JPA создает прокси для репозиториев?

1. При старте Spring Data JPA сканирует интерфейсы, расширяющие `Repository`.
2. Для каждого интерфейса создается прокси через `JdkDynamicAopProxy`.
3. Прокси перехватывает вызовы методов и делегирует их `RepositoryProxyPostProcessor`.
4. `RepositoryProxyPostProcessor` определяет, какой `RepositoryMethodInvocationHandler` использовать.

### 422. Как работает SimpleJpaRepository?

`SimpleJpaRepository` — это базовая реализация `JpaRepository`.

**Что делает:**
- Реализует все методы CRUD.
- Использует `EntityManager` для выполнения операций.
- Поддерживает пагинацию и сортировку.

### 423. Как работает QueryExecutorMethodInterceptor?

`QueryExecutorMethodInterceptor` — это перехватчик, который анализирует имя метода и генерирует запрос.

**Как работает:**
1. Получает имя метода (например, `findByNameAndAge`).
2. Разбивает на части: `find`, `ByName`, `AndAge`.
3. Генерирует JPQL: `SELECT u FROM User u WHERE u.name = ?1 AND u.age = ?2`.
4. Выполняет запрос через `EntityManager`.

### 424. Как работает PartTree в Spring Data JPA?

`PartTree` — это класс, который парсит имя метода и извлекает части запроса.

**Пример:**
- `findByNameAndAge` → `SELECT ... WHERE name = ?1 AND age = ?2`.
- `findByNameOrAge` → `SELECT ... WHERE name = ?1 OR age = ?2`.
- `findByNameLike` → `SELECT ... WHERE name LIKE ?1`.

### 425. Как работает QueryLookupStrategy в Spring Data JPA?

`QueryLookupStrategy` определяет, как искать реализацию запроса.

**Стратегии:**
- `CREATE`: Создает запрос из имени метода.
- `USE_DECLARED_QUERY`: Ищет `@Query` или `@NamedQuery`.
- `CREATE_IF_NOT_FOUND`: Сначала ищет `@Query`, если нет — создает из имени.

### 426. Как работает @Query с nativeQuery?

`nativeQuery = true` позволяет выполнять нативный SQL.

**Пример:**
```java
@Query(value = "SELECT * FROM users WHERE status = ?1", nativeQuery = true)
List<User> findByStatus(String status);
```

### 427. Как работает @Query с countQuery?

`countQuery` позволяет указать кастомный запрос для подсчета количества (для пагинации).

**Пример:**
```java
@Query(value = "SELECT * FROM users WHERE status = ?1",
       countQuery = "SELECT COUNT(*) FROM users WHERE status = ?1",
       nativeQuery = true)
Page<User> findByStatus(String status, Pageable pageable);
```

### 428. Как работает @Query с @Param?

`@Param` связывает параметр метода с именованным параметром в запросе.

**Пример:**
```java
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

### 429. Как работает @Query с SpEL?

SpEL (Spring Expression Language) позволяет использовать динамические значения в `@Query`.

**Пример:**
```java
@Query("SELECT u FROM #{#entityName} u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

### 430. Как работает @Query с LIKE?

**Пример:**
```java
@Query("SELECT u FROM User u WHERE u.name LIKE %:name%")
List<User> findByNameContaining(@Param("name") String name);
```

### 431. Как работает @Query с IN?

**Пример:**
```java
@Query("SELECT u FROM User u WHERE u.id IN :ids")
List<User> findByIds(@Param("ids") List<Long> ids);
```

### 432. Как работает @Query с JOIN FETCH?

**Пример:**
```java
@Query("SELECT u FROM User u JOIN FETCH u.orders WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

### 433. Как работает @Query с UPDATE/DELETE?

**Пример:**
```java
@Modifying
@Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
int updateStatus(@Param("id") Long id, @Param("status") String status);
```

### 434. Как работает @Query с INSERT?

JPA не поддерживает INSERT через JPQL. Нужно использовать нативный SQL.

**Пример:**
```java
@Modifying
@Query(value = "INSERT INTO users (name, email) VALUES (:name, :email)", nativeQuery = true)
void insertUser(@Param("name") String name, @Param("email") String email);
```

### 435. Как работает @Query с @Procedure?

**Пример:**
```java
@Procedure("GET_USER_COUNT")
int getUserCount();
```

### 436. Как работает @Query с @NamedQuery?

**Пример:**
```java
@Query(name = "User.findByEmail")
User findByEmail(@Param("email") String email);
```

### 437. Как работает @Query с @NamedNativeQuery?

**Пример:**
```java
@Query(name = "User.findActive", nativeQuery = true)
List<User> findActive();
```

### 438. Как работает @Query с @SqlResultSetMapping?

**Пример:**
```java
@Query(name = "User.findWithOrders", nativeQuery = true)
List<User> findWithOrders();
```

### 439. Как работает @Query с @ConstructorResult?

**Пример:**
```java
@Query("SELECT new com.example.UserDto(u.id, u.name) FROM User u")
List<UserDto> findAllUserDtos();
```

### 440. Как работает @Query с @ColumnResult?

`@ColumnResult` используется в `@SqlResultSetMapping` для маппинга колонок.

### 441. Как работает @Query с @EntityResult?

`@EntityResult` используется в `@SqlResultSetMapping` для маппинга на сущность.

### 442. Как работает @Query с @FieldResult?

`@FieldResult` используется в `@SqlResultSetMapping` для маппинга полей.

### 443. Как работает @Query с @Subselect?

`@Subselect` маппит сущность на подзапрос.

### 444. Как работает @Query с @Immutable?

`@Immutable` указывает, что сущность неизменяема.

### 445. Как работает @Query с @Synchronize?

`@Synchronize` указывает таблицы для синхронизации.

### 446. Как работает @Query с @Where?

`@Where` добавляет условие WHERE ко всем запросам.

### 447. Как работает @Query с @FilterDef и @Filter?

`@FilterDef` и `@Filter` добавляют динамические фильтры.

### 448. Как работает @Query с @FilterJoinTable?

`@FilterJoinTable` применяет фильтр к join-таблице.

### 449. Как работает @Query с @Fetch?

`@Fetch` определяет стратегию загрузки.

### 450. Как работает @Query с @FetchProfile?

`@FetchProfile` определяет профиль загрузки.

---

## 29. Hibernate — EntityManager и Persistence Context

### 451. Как работает EntityManager в JPA?

`EntityManager` — это центральный интерфейс JPA для управления сущностями.

**Основные методы:**
- `persist()`: Сохраняет новую сущность.
- `merge()`: Обновляет существующую сущность.
- `remove()`: Удаляет сущность.
- `find()`: Находит сущность по ID.
- `createQuery()`: Создает JPQL запрос.
- `flush()`: Синхронизирует изменения с БД.

### 452. Как работает Persistence Context?

`Persistence Context` — это кэш первого уровня (L1), который содержит все управляемые сущности в рамках одной транзакции.

**Как работает:**
1. При `persist()` сущность попадает в Persistence Context.
2. При `find()` Hibernate сначала ищет в Persistence Context.
3. При `flush()` изменения синхронизируются с БД.
4. При `clear()` Persistence Context очищается.
5. При `close()` Persistence Context закрывается.

### 453. Как работает @PersistenceContext?

`@PersistenceContext` внедряет `EntityManager` в Spring бин.

**Пример:**
```java
@Repository
public class UserRepository {
    @PersistenceContext
    private EntityManager entityManager;
}
```

### 454. Как работает @PersistenceUnit?

`@PersistenceUnit` внедряет `EntityManagerFactory` в Spring бин.

**Пример:**
```java
@Repository
public class UserRepository {
    @PersistenceUnit
    private EntityManagerFactory entityManagerFactory;
}
```

### 455. Как работает EntityManagerFactory?

`EntityManagerFactory` — это фабрика для создания `EntityManager`.

**Как работает:**
1. Создается один раз при старте приложения.
2. Содержит метаданные о всех сущностях.
3. Создает `EntityManager` для каждой транзакции.

### 456. Как работает @Transactional с EntityManager?

Spring управляет `EntityManager` через `SharedEntityManagerCreator`. При вызове метода с `@Transactional`:

1. Spring получает `EntityManager` из `EntityManagerFactory`.
2. Связывает его с текущей транзакцией.
3. После завершения транзакции закрывает `EntityManager`.

### 457. Как работает flush() в Hibernate?

`flush()` синхронизирует состояние Persistence Context с БД.

**Когда вызывается:**
- Перед коммитом транзакции.
- Перед выполнением запроса (если есть ожидающие изменения).
- Явно через `entityManager.flush()`.

### 458. Как работает clear() в Hibernate?

`clear()` очищает Persistence Context. Все управляемые сущности становятся отсоединенными (detached).

### 459. Как работает detach() в Hibernate?

`detach()` удаляет конкретную сущность из Persistence Context.

### 460. Как работает merge() в Hibernate?

`merge()` возвращает отсоединенную сущность в управляемое состояние.

**Как работает:**
1. Hibernate ищет сущность с таким же ID в Persistence Context.
2. Если находит — копирует поля из переданной сущности.
3. Если не находит — загружает из БД и копирует поля.
4. Возвращает управляемую сущность.

### 461. Как работает persist() в Hibernate?

`persist()` добавляет новую сущность в Persistence Context.

**Как работает:**
1. Сущность становится управляемой (managed).
2. При `flush()` Hibernate генерирует INSERT.
3. Если сущность уже существует — выбрасывает `EntityExistsException`.

### 462. Как работает remove() в Hibernate?

`remove()` удаляет сущность из БД.

**Как работает:**
1. Сущность должна быть управляемой.
2. При `flush()` Hibernate генерирует DELETE.
3. Сущность становится удаленной (removed).

### 463. Как работает refresh() в Hibernate?

`refresh()` перезагружает состояние сущности из БД.

**Как работает:**
1. Отменяет все незакоммиченные изменения.
2. Загружает текущее состояние из БД.
3. Обновляет поля сущности.

### 464. Как работает lock() в Hibernate?

`lock()` устанавливает блокировку на сущность без перезагрузки данных.

**Пример:**
```java
entityManager.lock(user, LockModeType.PESSIMISTIC_WRITE);
```

### 465. Как работает contains() в Hibernate?

`contains()` проверяет, находится ли сущность в Persistence Context.

### 466. Как работает getReference() в Hibernate?

`getReference()` возвращает прокси сущности без загрузки данных из БД.

**Пример:**
```java
User user = entityManager.getReference(User.class, 1L);
// user — это прокси, данные не загружены
```

### 467. Как работает find() в Hibernate?

`find()` загружает сущность из БД.

**Как работает:**
1. Сначала ищет в Persistence Context (L1 кэш).
2. Если не находит — загружает из БД.
3. Если не находит в БД — возвращает null.

### 468. Как работает createQuery() в Hibernate?

`createQuery()` создает JPQL запрос.

**Пример:**
```java
TypedQuery<User> query = entityManager.createQuery("SELECT u FROM User u WHERE u.email = :email", User.class);
query.setParameter("email", "test@example.com");
User user = query.getSingleResult();
```

### 469. Как работает createNativeQuery() в Hibernate?

`createNativeQuery()` создает нативный SQL запрос.

**Пример:**
```java
Query query = entityManager.createNativeQuery("SELECT * FROM users WHERE email = ?1", User.class);
query.setParameter(1, "test@example.com");
User user = (User) query.getSingleResult();
```

### 470. Как работает createNamedQuery() в Hibernate?

`createNamedQuery()` создает запрос из `@NamedQuery`.

**Пример:**
```java
TypedQuery<User> query = entityManager.createNamedQuery("User.findByEmail", User.class);
query.setParameter("email", "test@example.com");
User user = query.getSingleResult();
```

### 471. Как работает createStoredProcedureQuery() в Hibernate?

`createStoredProcedureQuery()` создает запрос к хранимой процедуре.

**Пример:**
```java
StoredProcedureQuery query = entityManager.createStoredProcedureQuery("GET_USER_COUNT");
query.registerStoredProcedureParameter("count", Integer.class, ParameterMode.OUT);
query.execute();
Integer count = (Integer) query.getOutputParameterValue("count");
```


