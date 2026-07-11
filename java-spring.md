# Вопросы по Spring (с ответами)

## Оглавление

- [1. IoC, DI и основы Spring](#1-ioc-di-и-основы-spring)
  - [1.1. Что такое IoC (Inversion of Control) и DI (Dependency Injection)?](#11-что-такое-ioc-inversion-of-control-и-di-dependency-injection)
  - [1.2. Какие есть способы внедрения зависимостей в Spring? Как работает @Autowired?](#12-какие-есть-способы-внедрения-зависимостей-в-spring-как-работает-autowired)
  - [1.3. Чем отличаются @Component, @Service, @Repository, @Controller?](#13-чем-отличаются-component-service-repository-controller)
  - [1.4. Какой бин создастся, если есть два @Bean одного типа?](#14-какой-бин-создастся-если-есть-два-bean-одного-типа)
  - [1.5. Как Spring обрабатывает @Order, @Priority и Ordered?](#15-как-spring-обрабатывает-order-priority-и-ordered)
  - [1.6. Как работает @Lookup и когда он полезен?](#16-как-работает-lookup-и-когда-он-полезен)
  - [1.7. Как можно динамически регистрировать бины в runtime?](#17-как-можно-динамически-регистрировать-бины-в-runtime)
- [2. Spring Context и жизненный цикл бинов](#2-spring-context-и-жизненный-цикл-бинов)
  - [2.1. Что такое Spring Context (ApplicationContext) и как его создать?](#21-что-такое-spring-context-applicationcontext-и-как-его-создать)
  - [2.2. Как Spring создаёт и управляет бинами? (Полный жизненный цикл)](#22-как-spring-создаёт-и-управляет-бинами-полный-жизненный-цикл)
  - [2.3. Почему @PostConstruct вызывается после инъекции зависимостей, но до InitializingBean.afterPropertiesSet()?](#23-почему-postconstruct-вызывается-после-инъекции-зависимостей-но-до-initializingbeanafterpropertiesset)
  - [2.4. Почему @PostConstruct метод не может быть @Transactional и как обойти?](#24-почему-postconstruct-метод-не-может-быть-transactional-и-как-обойти)
- [3. BeanFactory, ApplicationContext, BeanPostProcessor](#3-beanfactory-applicationcontext-beanpostprocessor)
  - [3.1. Расскажите про BeanFactory, ApplicationContext, их различия и иерархию](#31-расскажите-про-beanfactory-applicationcontext-их-различия-и-иерархию)
  - [3.2. Как работает DefaultListableBeanFactory?](#32-как-работает-defaultlistablebeanfactory)
  - [3.3. Как работает BeanPostProcessor и BeanFactoryPostProcessor?](#33-как-работает-beanpostprocessor-и-beanfactorypostprocessor)
  - [3.4. Как работает BeanDefinitionRegistryPostProcessor и чем отличается от BFPP?](#34-как-работает-beandefinitionregistrypostprocessor-и-чем-отличается-от-bfpp)
  - [3.5. Как добавить кастомную аннотацию с обработкой через BeanPostProcessor?](#35-как-добавить-кастомную-аннотацию-с-обработкой-через-beanpostprocessor)
  - [3.6. Как можно создать кастомный Scope?](#36-как-можно-создать-кастомный-scope)
- [4. Scopes, прокси и циклические зависимости](#4-scopes-прокси-и-циклические-зависимости)
  - [4.1. Какие есть scope-ы бинов в Spring?](#41-какие-есть-scope-ы-бинов-в-spring)
  - [4.2. Как Spring разрешает циклические зависимости? (Трёхуровневый кэш)](#42-как-spring-разрешает-циклические-зависимости-трёхуровневый-кэш)
  - [4.3. Почему конструкторная инъекция не поддерживает циклические зависимости?](#43-почему-конструкторная-инъекция-не-поддерживает-циклические-зависимости)
  - [4.4. JDK Dynamic Proxy vs CGLIB: когда что используется?](#44-jdk-dynamic-proxy-vs-cglib-когда-что-используется)
  - [4.5. Почему final-методы нельзя проксировать через CGLIB?](#45-почему-final-методы-нельзя-проксировать-через-cglib)
  - [4.6. Как работает Scope-прокси для request/session бинов в синглтонах?](#46-как-работает-scope-прокси-для-requestsession-бинов-в-синглтонах)
- [5. Конфигурация (@Configuration, @Bean, @Import)](#5-конфигурация-configuration-bean-import)
  - [5.1. Как работает @Bean в @Configuration классе?](#51-как-работает-bean-в-configuration-классе)
  - [5.2. Как работает @Configuration и чем отличается от @Component? (Full mode vs Lite mode)](#52-как-работает-configuration-и-чем-отличается-от-component-full-mode-vs-lite-mode)
  - [5.3. Как @Import и @ImportResource работают на уровне загрузки контекста?](#53-как-import-и-importresource-работают-на-уровне-загрузки-контекста)
- [6. Аннотации и их обработка](#6-аннотации-и-их-обработка)
  - [6.1. Как Spring обрабатывает аннотации (@Component, @Autowired)?](#61-как-spring-обрабатывает-аннотации-component-autowired)
  - [6.2. Как работает @AliasFor?](#62-как-работает-aliasfor)
  - [6.3. Как работает @Enable* семейство аннотаций?](#63-как-работает-enable-семейство-аннотаций)
- [7. Профили (@Profile) и @Lazy](#7-профили-profile-и-lazy)
  - [7.1. Как работает @Profile?](#71-как-работает-profile)
  - [7.2. Как работает @Lazy?](#72-как-работает-lazy)
  - [7.3. Почему @Value не работает в static полях и как обойти?](#73-почему-value-не-работает-в-static-полях-и-как-обойти)
- [8. AOP (Aspect-Oriented Programming)](#8-aop-aspect-oriented-programming)
  - [8.1. Что такое AOP и как он реализован в Spring?](#81-что-такое-aop-и-как-он-реализован-в-spring)
  - [8.2. Типы Advice в Spring AOP](#82-типы-advice-в-spring-aop)
  - [8.3. Spring AOP vs AspectJ](#83-spring-aop-vs-aspectj)
  - [8.4. Как Spring AOP создаёт прокси для бинов?](#84-как-spring-aop-создаёт-прокси-для-бинов)
  - [8.5. Как работает @DeclareParents?](#85-как-работает-declareparents)
- [9. Транзакции (@Transactional)](#9-транзакции-transactional)
  - [9.1. Как работает @Transactional?](#91-как-работает-transactional)
  - [9.2. Почему @Transactional не работает при вызове метода внутри того же класса?](#92-почему-transactional-не-работает-при-вызове-метода-внутри-того-же-класса)
  - [9.3. Propagation-уровни](#93-propagation-уровни)
  - [9.4. Isolation-уровни](#94-isolation-уровни)
  - [9.5. Как работает rollback?](#95-как-работает-rollback)
  - [9.6. Как работает @Transactional(readOnly = true)?](#96-как-работает-transactionalreadonly--true)
  - [9.7. Как работает @Transactional с несколькими DataSource?](#97-как-работает-transactional-с-несколькими-datasource)
  - [9.8. Как работает @Transactional(timeout = N)?](#98-как-работает-transactionaltimeout--n)
- [10. Spring Boot — основы](#10-spring-boot--основы)
  - [10.1. В чём отличие Spring от Spring Boot?](#101-в-чём-отличие-spring-от-spring-boot)
  - [10.2. Что такое Starter POM?](#102-что-такое-starter-pom)
  - [10.3. Как работает @SpringBootApplication?](#103-как-работает-springbootapplication)
  - [10.4. Как создать свой Spring Boot Starter?](#104-как-создать-свой-spring-boot-starter)
  - [10.5. Как переопределить стандартные бины Spring Boot (например, ObjectMapper)?](#105-как-переопределить-стандартные-бины-spring-boot-например-objectmapper)
- [11. Spring Boot — автоконфигурация и стартеры](#11-spring-boot--автоконфигурация-и-стартеры)
  - [11.1. Как работает @EnableAutoConfiguration?](#111-как-работает-enableautoconfiguration)
  - [11.2. Какие @Conditional аннотации существуют?](#112-какие-conditional-аннотации-существуют)
  - [11.3. Как отключить автоконфигурацию?](#113-как-отключить-автоконфигурацию)
  - [11.4. Как управлять порядком автоконфигураций?](#114-как-управлять-порядком-автоконфигураций)
- [12. Spring Boot — запуск и жизненный цикл](#12-spring-boot--запуск-и-жизненный-цикл)
  - [12.1. Как работает SpringApplication.run()?](#121-как-работает-springapplicationrun)
  - [12.2. Что такое ApplicationContextInitializer?](#122-что-такое-applicationcontextinitializer)
  - [12.3. Что такое SpringApplicationRunListener?](#123-что-такое-springapplicationrunlistener)
- [13. Spring Boot — конфигурация и свойства](#13-spring-boot--конфигурация-и-свойства)
  - [13.1. Как Spring Boot обрабатывает application.properties/yml?](#131-как-spring-boot-обрабатывает-applicationpropertiesyml)
  - [13.2. Как @ConfigurationProperties биндит свойства в объекты?](#132-как-configurationproperties-биндит-свойства-в-объекты)
  - [13.3. @ConfigurationProperties vs @Value — что выбрать?](#133-configurationproperties-vs-value--что-выбрать)
  - [13.4. Как валидировать @ConfigurationProperties?](#134-как-валидировать-configurationproperties)
  - [13.5. Приоритет свойств (от высшего к низшему)](#135-приоритет-свойств-от-высшего-к-низшему)
  - [13.6. Как реализовать кастомный PropertySource?](#136-как-реализовать-кастомный-propertysource)
- [14. Spring Boot — встроенные серверы и сервлеты](#14-spring-boot--встроенные-серверы-и-сервлеты)
  - [14.1. Как Spring Boot встраивает Tomcat/Jetty/Undertow?](#141-как-spring-boot-встраивает-tomcatjettyundertow)
  - [14.2. Как DispatcherServlet регистрируется автоматически?](#142-как-dispatcherservlet-регистрируется-автоматически)
  - [14.3. Как заменить встроенный сервер?](#143-как-заменить-встроенный-сервер)
- [15. Spring Boot — Actuator и мониторинг](#15-spring-boot--actuator-и-мониторинг)
  - [15.1. Что такое Spring Boot Actuator?](#151-что-такое-spring-boot-actuator)
  - [15.2. Как Micrometer собирает метрики HTTP-запросов?](#152-как-micrometer-собирает-метрики-http-запросов)
- [16. Spring Boot — Native Image (GraalVM)](#16-spring-boot--native-image-graalvm)
  - [16.1. Как Spring AOT компилирует приложение в Native Image?](#161-как-spring-aot-компилирует-приложение-в-native-image)
  - [16.2. Ограничения GraalVM](#162-ограничения-graalvm)
  - [16.3. Как настроить Reflection Hints для JPA?](#163-как-настроить-reflection-hints-для-jpa)
  - [16.4. Влияние AOT на стартап](#164-влияние-aot-на-стартап)
- [17. Spring Boot — DevTools](#17-spring-boot--devtools)
  - [17.1. Что такое Spring Boot DevTools?](#171-что-такое-spring-boot-devtools)
  - [17.2. Как работает Automatic Restart?](#172-как-работает-automatic-restart)
- [18. Сервлеты (Servlet API)](#18-сервлеты-servlet-api)
  - [18.1. Что такое сервлет и как он работает?](#181-что-такое-сервлет-и-как-он-работает)
  - [18.2. Что такое ServletContext и ServletConfig?](#182-что-такое-servletcontext-и-servletconfig)
  - [18.3. Как работает FilterChain?](#183-как-работает-filterchain)
  - [18.4. Что такое асинхронные сервлеты и зачем они нужны?](#184-что-такое-асинхронные-сервлеты-и-зачем-они-нужны)
  - [18.5. Сервлеты vs Реактивный стек (WebFlux)](#185-сервлеты-vs-реактивный-стек-webflux)
- [19. Spring MVC — DispatcherServlet и обработка запросов](#19-spring-mvc--dispatcherservlet-и-обработка-запросов)
  - [19.1. Как работает DispatcherServlet?](#191-как-работает-dispatcherservlet)
  - [19.2. Как работает HandlerMapping?](#192-как-работает-handlermapping)
  - [19.3. Как работает HandlerAdapter?](#193-как-работает-handleradapter)
  - [19.4. Как работает ViewResolver?](#194-как-работает-viewresolver)
  - [19.5. Что такое ModelAndView?](#195-что-такое-modelandview)
- [20. Spring MVC — контроллеры и аннотации](#20-spring-mvc--контроллеры-и-аннотации)
  - [20.1. @RequestMapping, @GetMapping, @PostMapping и др.](#201-requestmapping-getmapping-postmapping-и-др)
  - [20.2. @RequestParam, @PathVariable, @RequestBody, @ResponseBody](#202-requestparam-pathvariable-requestbody-responsebody)
  - [20.3. @RequestHeader, @CookieValue, @RequestAttribute, @SessionAttribute](#203-requestheader-cookievalue-requestattribute-sessionattribute)
  - [20.4. @MatrixVariable](#204-matrixvariable)
  - [20.5. @CrossOrigin](#205-crossorigin)
  - [20.6. Как работает HttpMessageConverter?](#206-как-работает-httpmessageconverter)
- [21. Spring MVC — валидация и обработка ошибок](#21-spring-mvc--валидация-и-обработка-ошибок)
  - [21.1. Как работает @Valid и @Validated?](#211-как-работает-valid-и-validated)
  - [21.2. Как работают группы валидации?](#212-как-работают-группы-валидации)
  - [21.3. Основные аннотации Bean Validation](#213-основные-аннотации-bean-validation)
  - [21.4. Как работает @ControllerAdvice / @RestControllerAdvice?](#214-как-работает-controlleradvice--restcontrolleradvice)
  - [21.5. Как работает @ResponseStatusException?](#215-как-работает-responsestatusexception)
  - [21.6. Как работает ProblemDetail (RFC 7807)?](#216-как-работает-problemdetail-rfc-7807)
- [22. Spring MVC — CORS, сессии, фильтры, перехватчики](#22-spring-mvc--cors-сессии-фильтры-перехватчики)
  - [22.1. Filter vs HandlerInterceptor vs OncePerRequestFilter](#221-filter-vs-handlerinterceptor-vs-onceperrequestfilter)
  - [22.2. @SessionAttributes vs @SessionAttribute](#222-sessionattributes-vs-sessionattribute)
  - [22.3. Глобальная конфигурация CORS](#223-глобальная-конфигурация-cors)
  - [22.4. @Order для фильтров и перехватчиков](#224-order-для-фильтров-и-перехватчиков)
- [23. Spring Security — аутентификация](#23-spring-security--аутентификация)
  - [23.1. Как работает Security Filter Chain?](#231-как-работает-security-filter-chain)
  - [23.2. Как работает SecurityContextHolder?](#232-как-работает-securitycontextholder)
  - [23.3. Как работает AuthenticationManager и AuthenticationProvider?](#233-как-работает-authenticationmanager-и-authenticationprovider)
  - [23.4. Как работает UserDetailsService?](#234-как-работает-userdetailsservice)
  - [23.5. Что такое PasswordEncoder?](#235-что-такое-passwordencoder)
  - [23.6. Как работает @EnableWebSecurity и SecurityFilterChain?](#236-как-работает-enablewebsecurity-и-securityfilterchain)
- [24. Spring Security — авторизация и защита](#24-spring-security--авторизация-и-защита)
  - [24.1. @PreAuthorize, @PostAuthorize, @Secured, @RolesAllowed](#241-preauthorize-postauthorize-secured-rolesallowed)
  - [24.2. @EnableMethodSecurity vs @EnableGlobalMethodSecurity](#242-enablemethodsecurity-vs-enableglobalmethodsecurity)
  - [24.3. Как работает CSRF-защита?](#243-как-работает-csrf-защита)
  - [24.4. CORS в Spring Security](#244-cors-в-spring-security)
- [25. Spring Security — OAuth2 / JWT](#25-spring-security--oauth2--jwt)
  - [25.1. Как работает JWT (JSON Web Token)?](#251-как-работает-jwt-json-web-token)
  - [25.2. Как работает OAuth2?](#252-как-работает-oauth2)
  - [25.3. Как работает Resource Server (Bearer Token)?](#253-как-работает-resource-server-bearer-token)
  - [25.4. JwtDecoder и JwtEncoder](#254-jwtdecoder-и-jwtencoder)
- [26. Spring Data JPA — репозитории](#26-spring-data-jpa--репозитории)
  - [26.1. Как Spring Data JPA создаёт прокси для репозиториев?](#261-как-spring-data-jpa-создаёт-прокси-для-репозиториев)
  - [26.2. Как работает PartTree (парсинг имени метода)?](#262-как-работает-parttree-парсинг-имени-метода)
  - [26.3. QueryLookupStrategy](#263-querylookupstrategy)
  - [26.4. Иерархия репозиториев](#264-иерархия-репозиториев)
  - [26.5. @Query — JPQL и нативный SQL](#265-query--jpql-и-нативный-sql)
  - [26.6. @NoRepositoryBean и @EnableJpaRepositories](#266-norepositorybean-и-enablejparepositories)
  - [26.7. Как работает аудит (@CreatedDate, @LastModifiedDate)?](#267-как-работает-аудит-createddate-lastmodifieddate)
- [27. Spring Data JPA — запросы и оптимизация](#27-spring-data-jpa--запросы-и-оптимизация)
  - [27.1. Как работает Specification (Criteria API)?](#271-как-работает-specification-criteria-api)
  - [27.2. Как работает ExampleMatcher (Query by Example)?](#272-как-работает-examplematcher-query-by-example)
  - [27.3. @EntityGraph — решение N+1 в Spring Data JPA](#273-entitygraph--решение-n1-в-spring-data-jpa)
  - [27.4. Другие стратегии решения N+1](#274-другие-стратегии-решения-n1)
  - [27.5. @Procedure — вызов хранимых процедур](#275-procedure--вызов-хранимых-процедур)
- [28. Spring Data — NoSQL](#28-spring-data--nosql)
  - [28.1. Spring Data MongoDB](#281-spring-data-mongodb)
  - [28.2. Spring Data Redis](#282-spring-data-redis)
  - [28.3. Spring Data Elasticsearch](#283-spring-data-elasticsearch)
  - [28.4. Spring Data Cassandra](#284-spring-data-cassandra)
  - [28.5. Spring Data R2DBC](#285-spring-data-r2dbc)
- [29. Кэширование в Spring (@Cacheable)](#29-кэширование-в-spring-cacheable)
  - [29.1. Как работает @Cacheable, @CacheEvict, @CachePut?](#291-как-работает-cacheable-cacheevict-cacheput)
  - [29.2. CacheManager и провайдеры](#292-cachemanager-и-провайдеры)
  - [29.3. Как работает кэширование на уровне аннотаций?](#293-как-работает-кэширование-на-уровне-аннотаций)
- [30. Асинхронность (@Async, @Scheduled)](#30-асинхронность-async-scheduled)
  - [30.1. Как работает @Async?](#301-как-работает-async)
  - [30.2. TaskExecutor — конфигурация](#302-taskexecutor--конфигурация)
  - [30.3. Как работает @Scheduled?](#303-как-работает-scheduled)
  - [30.4. Как передать SecurityContext в @Async?](#304-как-передать-securitycontext-в-async)
  - [30.5. Как работает @Retryable (Spring Retry)?](#305-как-работает-retryable-spring-retry)
- [31. Spring Events](#31-spring-events)
  - [31.1. Как работает механизм событий в Spring?](#311-как-работает-механизм-событий-в-spring)
  - [31.2. @TransactionalEventListener](#312-transactionaleventlistener)
  - [31.3. Асинхронная обработка событий](#313-асинхронная-обработка-событий)
- [32. Пул соединений (HikariCP)](#32-пул-соединений-hikaricp)
  - [32.1. Почему HikariCP и как он работает?](#321-почему-hikaricp-и-как-он-работает)
  - [32.2. Основные параметры конфигурации](#322-основные-параметры-конфигурации)
  - [32.3. Как мониторить пул?](#323-как-мониторить-пул)
- [33. Тестирование Spring-приложений](#33-тестирование-spring-приложений)
  - [33.1. @SpringBootTest](#331-springboottest)
  - [33.2. Срезанные тесты (Slice Tests)](#332-срезанные-тесты-slice-tests)
  - [33.3. MockMvc](#333-mockmvc)
  - [33.4. TestContainers](#334-testcontainers)
  - [33.5. @MockBean vs @SpyBean](#335-mockbean-vs-spybean)
- [34. Spring Batch](#34-spring-batch)
  - [34.1. Архитектура Spring Batch](#341-архитектура-spring-batch)
  - [34.2. Chunk-oriented processing](#342-chunk-oriented-processing)
  - [34.3. Повторный запуск и восстановление](#343-повторный-запуск-и-восстановление)
- [35. Spring Integration](#35-spring-integration)
  - [35.1. Что такое Spring Integration?](#351-что-такое-spring-integration)
  - [35.2. Как Spring Integration связан с Spring Boot?](#352-как-spring-integration-связан-с-spring-boot)
- [36. Spring Cloud — микросервисы](#36-spring-cloud--микросервисы)
  - [36.1. Service Discovery (Eureka / Consul)](#361-service-discovery-eureka--consul)
  - [36.2. Load Balancing (Spring Cloud LoadBalancer)](#362-load-balancing-spring-cloud-loadbalancer)
  - [36.3. Circuit Breaker (Resilience4j)](#363-circuit-breaker-resilience4j)
  - [36.4. OpenFeign](#364-openfeign)
  - [36.5. Circuit Breaker + OpenFeign](#365-circuit-breaker--openfeign)
- [37. Spring Cloud — Config, Gateway, Tracing](#37-spring-cloud--config-gateway-tracing)
  - [37.1. Spring Cloud Config](#371-spring-cloud-config)
  - [37.2. Spring Cloud Gateway](#372-spring-cloud-gateway)
  - [37.3. Distributed Tracing (Micrometer Tracing)](#373-distributed-tracing-micrometer-tracing)
- [38. Spring GraphQL](#38-spring-graphql)
  - [38.1. Как работает Spring GraphQL?](#381-как-работает-spring-graphql)
  - [38.2. GraphQL vs REST](#382-graphql-vs-rest)
- [39. Spring — реактивное программирование (WebFlux, R2DBC)](#39-spring--реактивное-программирование-webflux-r2dbc)
  - [39.1. Что такое WebFlux?](#391-что-такое-webflux)
  - [39.2. Когда WebFlux, а когда Spring MVC?](#392-когда-webflux-а-когда-spring-mvc)
  - [39.3. R2DBC vs JDBC](#393-r2dbc-vs-jdbc)
  - [39.4. Модель потоков WebFlux](#394-модель-потоков-webflux)
- [40. Spring — интеграция с Kafka / RabbitMQ](#40-spring--интеграция-с-kafka--rabbitmq)
  - [40.1. Spring Kafka](#401-spring-kafka)
  - [40.2. Spring AMQP (RabbitMQ)](#402-spring-amqp-rabbitmq)
  - [40.3. Kafka vs RabbitMQ](#403-kafka-vs-rabbitmq)
- [41. Spring — gRPC, Kotlin Coroutines](#41-spring--grpc-kotlin-coroutines)
  - [41.1. Spring gRPC](#411-spring-grpc)
  - [41.2. Kotlin Coroutines в Spring](#412-kotlin-coroutines-в-spring)
- [42. Spring Boot 3 — миграция и изменения](#42-spring-boot-3--миграция-и-изменения)
  - [42.1. Основные изменения в Spring Boot 3](#421-основные-изменения-в-spring-boot-3)
  - [42.2. Как мигрировать с Spring Boot 2 на Spring Boot 3?](#422-как-мигрировать-с-spring-boot-2-на-spring-boot-3)
- [43. Разное (SpEL, @Value, @Lookup, RestTemplate vs WebClient)](#43-разное-spel-value-lookup-resttemplate-vs-webclient)
  - [43.1. Что такое SpEL (Spring Expression Language)?](#431-что-такое-spel-spring-expression-language)
  - [43.2. Как работает @Value?](#432-как-работает-value)
  - [43.3. Как работает @EventListener?](#433-как-работает-eventlistener)
  - [43.4. Как работает @AliasFor?](#434-как-работает-aliasfor)
  - [43.5. RestTemplate vs WebClient — что выбрать?](#435-resttemplate-vs-webclient--что-выбрать)
  - [43.6. Как оптимизировать старт Spring Boot приложения?](#436-как-оптимизировать-старт-spring-boot-приложения)

---

## 1. IoC, DI и основы Spring

### 1.1. Что такое IoC (Inversion of Control) и DI (Dependency Injection)?

Если вы когда-нибудь писали `new Service()` прямо внутри класса — вы управляли зависимостями вручную. **IoC (Inversion of Control)** переворачивает эту модель: теперь не вы создаёте объекты, а фреймворк. Вы говорите «мне нужен Service», а контейнер сам решает когда и как его создать, настроить и отдать вам.

**DI (Dependency Injection)** — это конкретный способ реализовать IoC. Контейнер не просто создаёт объекты, а «впрыскивает» их туда, где они нужны. В Spring это может происходить через конструктор, сеттер или напрямую в поле. Звучит просто, но за этим стоит целый механизм разрешения зависимостей, о котором дальше.

### 1.2. Какие есть способы внедрения зависимостей в Spring? Как работает @Autowired?

В Spring три способа получить зависимость, и выбор между ними влияет на тестируемость, читаемость и архитектуру:

- **Constructor Injection** — золотой стандарт. Зависимости приходят через конструктор, поля можно сделать `final`. Объект физически не может быть создан в невалидном состоянии — это огромный плюс. В тестах вы просто вызываете `new Service(mockRepo)` без всякого Spring. Кстати, с версии 4.3, если конструктор всего один, `@Autowired` можно вообще не писать — Spring догадается сам.

- **Setter Injection** — нишевый вариант. Полезен когда зависимость опциональна или может меняться во время жизни объекта. Но честно: в 90% случаев вы будете использовать конструктор.

- **Field Injection** (`@Autowired` над полем) — выглядит коротко и соблазнительно, но создаёт проблемы. В тестах без Spring вы ничего не внедрите кроме как через рефлексию. Зависимости класса не видны снаружи — сигнатура конструктора ничего не говорит. На код-ревью вас за это пожурят.

**Как Spring ищет бин для @Autowired:** сначала по типу. Если нашлось несколько — пытается по имени поля или параметра. Если и так не выходит — ждёт `@Qualifier`. Не нашёл ничего и `required = true` (по умолчанию) — исключение.

### 1.3. Чем отличаются @Component, @Service, @Repository, @Controller?

Все четыре — стереотипные аннотации, и технически все они наследуются от `@Component`. Каждая регистрирует бин в контексте. Разница — семантическая, но у двух из них есть реальное поведение под капотом:

- **@Component** — просто «это бин». Никакой дополнительной логики, чистый маркер.
- **@Service** — «это бизнес-логика». Технически не отличается от `@Component`. Но когда вы открываете класс и видите `@Service`, вы сразу понимаете с чем имеете дело. Плюс Spring может добавить сюда поведение в будущих версиях.
- **@Repository** — вот тут уже не просто семантика. Spring автоматически оборачивает все низкоуровневые исключения (SQLException, HibernateException и т.д.) в свою иерархию `DataAccessException`. Работает через `PersistenceExceptionTranslationPostProcessor`. На практике: вы получаете читаемые исключения вместо простыней стектрейса от JDBC-драйвера.
- **@Controller** — маркер для веб-слоя. `DispatcherServlet` сканирует именно эти бины для маппинга URL на методы. Без этой аннотации (или `@RestController`) ваш контроллер просто не будет обрабатывать запросы.

### 1.4. Какой бин создастся, если есть два @Bean одного типа?

Никакой — Spring упадёт с `NoUniqueBeanDefinitionException` ещё на старте. Он честно говорит: «Я не знаю какой из двух ты хочешь». Решения: повесить `@Primary` на одного из кандидатов (типа «вот этого бери по умолчанию») или использовать `@Qualifier` в точке инъекции. Если имена методов `@Bean` разные, оба бина создадутся и будут жить в контексте, но внедрить их без уточнения не выйдет.

### 1.5. Как Spring обрабатывает @Order, @Priority и Ordered?

Эти штуки вступают в игру когда вы внедряете не один бин, а коллекцию (`List<MyInterface>`):

- **@Order** — спринговый способ сказать «вот этот — первый, этот — второй». Чем меньше число, тем ближе к началу списка.
- **@Priority** — стандарт JSR-250, делает примерно то же самое, но ещё и влияет на выбор из нескольких кандидатов при обычной инъекции.
- **Ordered** — интерфейс с методом `getOrder()`. Программный вариант, удобен когда порядок зависит от каких-то условий.

### 1.6. Как работает @Lookup и когда он полезен?

Классическая проблема: у вас singleton-бин, которому иногда нужен prototype. Если вы просто заинжектите prototype через `@Autowired`, singleton получит один-единственный экземпляр при создании и будет использовать его вечно — никакого тебе «нового на каждый вызов».

`@Lookup` решает это элегантно: Spring через CGLIB создаёт прокси, который переопределяет метод с `@Lookup`, и при каждом вызове метода честно идёт в контейнер и достаёт свежий экземпляр prototype. Сам метод должен быть `abstract` (или с пустым телом если не abstract) и возвращать нужный тип. Выглядит как магия, но работает надёжно.

### 1.7. Как можно динамически регистрировать бины в runtime?

Иногда статической конфигурации не хватает — нужно добавить бин на лету. Способов несколько:

- **`BeanDefinitionRegistryPostProcessor`** — позволяет вклиниться до того как фабрика начнёт создавать бины и добавить свои `BeanDefinition`. Самый правильный путь: бины пройдут полный цикл BPP.
- **`ImportBeanDefinitionRegistrar`** — то же самое, но через `@Import` на конфигурации.
- **`context.getBeanFactory().registerSingleton(name, instance)`** — быстро, грязно: объект попадает в контекст, но **минует все BeanPostProcessor-ы**. Ни тебе `@Autowired`, ни `@PostConstruct`, ни проксирования.
- **`GenericApplicationContext.registerBean()`** (Spring 5+) — современный fluent-API, совмещающий удобство и полный жизненный цикл.

---

## 2. Spring Context и жизненный цикл бинов

### 2.1. Что такое Spring Context (ApplicationContext) и как его создать?

**Spring Context** — это сердце всего Spring. Если совсем просто: это огромная Map-а, где ключи — имена бинов, а значения — готовые объекты. Но `ApplicationContext` умеет гораздо больше чем просто хранить объекты:

- **AOP** — оборачивает бины проксями для транзакций, кэширования, безопасности
- **i18n** — разрешает сообщения на разных языках через `MessageSource`
- **События** — позволяет бинам общаться через `ApplicationEventPublisher`, не связываясь напрямую
- **Eager-инициализация** — в отличие от `BeanFactory`, создаёт все singleton-бины сразу при старте, а не когда к ним впервые обратились. Ошибки конфигурации вы увидите сразу, а не через неделю в проде

Создать контекст можно по-разному, но в Spring Boot вы обычно даже не задумываетесь об этом — `SpringApplication.run()` делает всё сам. Для ручного создания: `AnnotationConfigApplicationContext` для Java-конфигураций, `ClassPathXmlApplicationContext` для XML (если вы всё ещё используете XML в 2026-м).

### 2.2. Как Spring создаёт и управляет бинами? (Полный жизненный цикл)

За каждой строчкой `@Component` скрывается целый конвейер. Вот как выглядит путь бина от аннотации до готового объекта:

**На уровне кода** всем заправляет `AbstractAutowireCapableBeanFactory.doCreateBean()`. Держитесь, сейчас будет самая мякотка:

```
doCreateBean(beanName, bd, args):
  1. createBeanInstance()           — конструктор (или фабричный метод)
  2. applyMergedBeanDefinitionPostProcessors()  — сбор метаданных @Autowired/@Value
  3. addSingletonFactory()          — регистрация фабрики в L3-кэш (важно для циклических ссылок)
  4. populateBean()                 — внедрение зависимостей (сеттеры, поля)
  5. initializeBean()               — инициализация:
     a. invokeAwareMethods()           — BeanNameAware, BeanFactoryAware, ApplicationContextAware
     b. applyBeanPostProcessorsBeforeInitialization() — все BPP.postProcessBeforeInitialization()
        └─ CommonAnnotationBeanPostProcessor → вызывает @PostConstruct
     c. invokeInitMethods()            — InitializingBean.afterPropertiesSet() → кастомный init-method
     d. applyBeanPostProcessorsAfterInitialization() — все BPP.postProcessAfterInitialization()
        └─ AbstractAutoProxyCreator → создаёт AOP/транзакционные прокси
  6. registerDisposableBean()       — регистрация destroy-методов
```

**Разрушение** при закрытии контекста — симметрично созданию, но в обратном порядке:
1. `@PreDestroy` (через `CommonAnnotationBeanPostProcessor.postProcessBeforeDestruction()`)
2. `DisposableBean.destroy()`
3. Кастомный destroy-method
4. `DestructionAwareBeanPostProcessor.postProcessBeforeDestruction()`

**Важные промежуточные шаги, которые стоит запомнить:**

- **`MergedBeanDefinitionPostProcessor`** (шаг 2) — тихо сканирует класс на `@Autowired`, `@Value`, `@PostConstruct` и складывает метаданные в кэш, чтобы потом не лазить через reflection на каждом бине. Этим занимаются `AutowiredAnnotationBeanPostProcessor` и `CommonAnnotationBeanPostProcessor`.

- **`SmartInstantiationAwareBeanPostProcessor`** — вызывается при циклических зависимостях. Его метод `getEarlyBeanReference()` может вернуть «ранний» прокси объекта ещё до того как бин полностью собран. Без этого AOP и циклические зависимости несовместимы в принципе.

- **`DestructionAwareBeanPostProcessor`** — для кастомной логики при уничтожении бина. Например, пул соединений HikariCP использует его чтобы корректно закрыть все Connection-ы.

### 2.3. Почему @PostConstruct вызывается после инъекции зависимостей, но до InitializingBean.afterPropertiesSet()?

Потому что так зашито в порядке вызовов внутри `initializeBean()`. `CommonAnnotationBeanPostProcessor` (который отвечает за `@PostConstruct`) — это обычный BeanPostProcessor. А по контракту жизненного цикла **все** BPP перед инициализацией отрабатывают до того как вызывается `afterPropertiesSet()` и init-method самого бина. 

То есть порядок жёстко фиксирован: сначала Spring даёт шанс всем BPP обработать бин до инициализации, потом вызывает init-методы самого бина, потом даёт шанс BPP после инициализации. `@PostConstruct` технически находится в первой фазе, а `afterPropertiesSet()` — во второй.

### 2.4. Почему @PostConstruct метод не может быть @Transactional и как обойти?

Короткий ответ: потому что на момент `@PostConstruct` прокси для `@Transactional` ещё не существует. Длинный: прокси создаются на шаге 5d — `postProcessAfterInitialization`. А `@PostConstruct` срабатывает на шаге 5b — `postProcessBeforeInitialization`. То есть когда вызывается ваш `@PostConstruct`, бин ещё «голый», без обёртки.

Как быть если очень нужно:
- **`@EventListener(ContextRefreshedEvent.class)`** — ваш метод выполнится после того как весь контекст поднят и все прокси на месте.
- **`CommandLineRunner` / `ApplicationRunner`** — тоже пост-старт, удобно для одноразовых операций.
- **Self-injection** — внедрить самого себя через `@Autowired` и дёрнуть транзакционный метод. Но это костыль, честно.

---

## 3. BeanFactory, ApplicationContext, BeanPostProcessor

### 3.1. Расскажите про BeanFactory, ApplicationContext, их различия и иерархию

Если совсем просто: **BeanFactory** — это «голый» контейнер, умеющий создавать бины по требованию. **ApplicationContext** — тот же контейнер, но с довеском из AOP, событий, интернационализации и web-фич.

На практике `BeanFactory` в чистом виде почти никто не использует — он слишком минималистичен. `ApplicationContext` добавляет самое важное: eager-инициализацию. Это когда все singleton-бины создаются сразу при старте, а не при первом обращении. Звучит медленнее, но на деле вы получаете мгновенный фидбек о проблемах конфигурации — лучше упасть при старте чем через три дня в проде.

Иерархия интерфейсов: `ApplicationContext → ListableBeanFactory → BeanFactory`. `ListableBeanFactory` добавляет возможность перечислять бины, `ApplicationContext` — всё остальное.

### 3.2. Как работает DefaultListableBeanFactory?

Это та самая реализация, которая делает всю работу. Когда вы пишете `@Component`, именно `DefaultListableBeanFactory` решает когда и как создать объект. Внутри у неё целый арсенал структур данных:

| Структура | Назначение |
|---|---|
| `Map<String, BeanDefinition> beanDefinitionMap` | Имя бина → метаданные (scope, класс, зависимости) |
| `Map<String, BeanDefinition> mergedBeanDefinitions` | Слитые с родительскими определения |
| `Map<String, Object> singletonObjects` | L1-кэш готовых синглтонов |
| `Map<String, ObjectFactory<?>> singletonFactories` | L3-кэш фабрик для ранних ссылок |
| `Map<String, Set<String>> dependentBeanMap` | Какие бины зависят от данного |
| `Map<String, Set<String>> dependenciesForBeanMap` | От каких бинов зависит данный |
| `Map<String, Object> disposableBeans` | Бины с destroy-методами |

Центральный алгоритм — `doGetBean()`. Когда кто-то просит бин (прямо или через инъекцию), происходит примерно следующее:

```java
protected <T> T doGetBean(String name, Class<T> requiredType, Object[] args) {
    String beanName = transformedBeanName(name);

    // 1. Может, уже есть готовый?
    Object sharedInstance = getSingleton(beanName);
    if (sharedInstance != null) return ...;

    // 2. Не создаётся ли он прямо сейчас? (циклическая зависимость)
    if (isPrototypeCurrentlyInCreation(beanName)) throw ...;

    // 3. Ищем BeanDefinition
    BeanDefinition bd = getMergedLocalBeanDefinition(beanName);

    // 4. Сначала создаём depends-on бины
    for (String dep : bd.getDependsOn()) getBean(dep);

    // 5. Создаём сам бин
    if (bd.isSingleton())
        sharedInstance = getSingleton(beanName, () -> createBean(beanName, bd, args));
    else if (bd.isPrototype())
        sharedInstance = createBean(beanName, bd, args);

    return ...;
}
```

Ключевой момент: лямбда-фабрика `() -> createBean(...)` регистрируется в L3-кэш **до** того как `createBean()` начинает работу. Это критично для циклических зависимостей — другой бин может «заглянуть» в L3 и получить ссылку на ещё не готовый объект.

### 3.3. Как работает BeanPostProcessor и BeanFactoryPostProcessor?

Два брата-акробата, которые делают Spring гибким:

- **BeanFactoryPostProcessor (BFPP)** — работает на уровне метаданных, до того как создан хоть один бин. Его задача — подправить `BeanDefinition`-ы: подставить значения из properties (`PropertySourcesPlaceholderConfigurer`), зарегистрировать новые определения. После BFPP определения заморожены.

- **BeanPostProcessor (BPP)** — работает с уже созданными объектами. У него два хука:
  - `postProcessBeforeInitialization` — до init-методов. Здесь `@PostConstruct` отрабатывает.
  - `postProcessAfterInitialization` — после init-методов. Здесь создаются прокси для `@Transactional`, `@Cacheable`, AOP.

Контейнер регистрирует BPP как обычные бины, потом `PostProcessorRegistrationDelegate` собирает их, сортирует по `PriorityOrdered` → `Ordered` → plain, и прогоняет через них каждый создаваемый бин.

### 3.4. Как работает BeanDefinitionRegistryPostProcessor и чем отличается от BFPP?

Это «старший брат» BFPP, который может не только менять существующие определения, но и **добавлять новые**. Его метод `postProcessBeanDefinitionRegistry()` даёт доступ к `BeanDefinitionRegistry`, через который можно зарегистрировать что угодно.

Самый известный пример — `ConfigurationClassPostProcessor`. Именно он сканирует пакеты на `@Component`, обрабатывает `@Configuration` классы, `@Import`, `@ComponentScan` — и регистрирует все найденные бины. Без него Spring Boot не знал бы о существовании ваших сервисов.

### 3.5. Как добавить кастомную аннотацию с обработкой через BeanPostProcessor?

Допустим, вы хотите свою аннотацию `@InjectLogger`, которая автоматически подставляет логгер в поле. Вот рецепт:

1. Создаёте аннотацию с `@Retention(RUNTIME)` и `@Target(FIELD)`
2. Пишете `BeanPostProcessor`, который в `postProcessBeforeInitialization`:
   - Находит все поля с вашей аннотацией через Reflection
   - Создаёт логгер (`LoggerFactory.getLogger(bean.getClass())`)
   - Делает `field.setAccessible(true)` и `field.set(bean, logger)`
3. Регистрируете BPP как `@Component` — Spring подхватит его автоматически

Всё. Теперь любой бин с полем `@InjectLogger` получит логгер без ручного создания.

### 3.6. Как можно создать кастомный Scope?

Интерфейс `Scope` — три метода: `get()`, `remove()`, `getConversationId()`. В `get()` вы решаете: создать новый объект или вернуть существующий. Например, для «ThreadScope» вы хранили бы Map с ключом-именем потока.

Регистрируется через `ConfigurableBeanFactory.registerScope("myScope", new MyScope())`. После этого можно писать `@Scope("myScope")` над бинами.

Зачем это нужно? Для инфраструктурных штук: scope под批次 обработку в Spring Batch, scope под текущего tenant-а в мультитенантных системах, или просто когда стандартных singleton/prototype не хватает.

---

## 4. Scopes, прокси и циклические зависимости

### 4.1. Какие есть scope-ы бинов в Spring?

Scope бина отвечает на вопрос «сколько экземпляров этого бина будет существовать и как долго они живут?». Spring предлагает несколько вариантов, от вечного singleton до ультракороткого request:

- **singleton** (по умолчанию) — один экземпляр на весь контейнер. Создаётся при старте, живёт пока жив контекст. Кэшируется и раздаётся всем желающим. 95% ваших бинов будут singleton — это быстро и предсказуемо.
- **prototype** — новый экземпляр при каждом запросе. Важно: Spring **не управляет полным жизненным циклом** prototype — destroy-методы не вызываются. Если вы создали prototype с `@PreDestroy`, он никогда не сработает. Убирать за собой придётся вручную.
- **request** — один экземпляр на HTTP-запрос. Живёт от начала запроса до его завершения. Только в веб-приложениях.
- **session** — один экземпляр на HTTP-сессию. Удобно для хранения пользовательского контекста.
- **application** — один на `ServletContext`. Похож на singleton, но привязан к веб-окружению.
- **websocket** — один на WebSocket-сессию.

### 4.2. Как Spring разрешает циклические зависимости? (Трёхуровневый кэш)

Это один из самых элегантных механизмов в Spring. Проблема: бину А нужен Б, а бину Б нужен А. Обычный конструктор в такой ситуации уйдёт в бесконечную рекурсию. Spring решает это через трёхуровневый кэш, и делает это настолько хитро, что стоит разобрать по шагам.

Сначала — главный метод. `DefaultSingletonBeanRegistry.getSingleton()` с лямбдой-фабрикой:

```java
public Object getSingleton(String beanName, ObjectFactory<?> singletonFactory) {
    synchronized (this.singletonObjects) {
        Object singletonObject = this.singletonObjects.get(beanName);
        if (singletonObject == null) {
            beforeSingletonCreation(beanName);  // помечаем «в процессе»
            try {
                singletonObject = singletonFactory.getObject();
            } finally {
                afterSingletonCreation(beanName);  // снимаем метку
            }
            if (newSingleton) {
                addSingleton(beanName, singletonObject);  // → L1, удалить из L2/L3
            }
        }
        return singletonObject;
    }
}
```

Ключевой трюк: фабрика регистрируется в L3-кэш **до** вызова `createBean()`. Вот этот момент в `doCreateBean()`:

```java
instance = createBeanInstance(beanName, mbd, args);    // конструктор — объект готов!
addSingletonFactory(beanName, () -> getEarlyBeanReference(beanName, mbd, instance));
// ↑ фабрика в L3: теперь другие бины могут получить ссылку на этот (ещё сырой) объект
populateBean(beanName, mbd, instance);                  // теперь заполняем зависимости
```

Обратите внимание на `getEarlyBeanReference()`. Если бин должен быть проксирован (AOP), фабрика вернёт уже прокси, а не сырой объект. Иначе циклическая зависимость сломала бы AOP — бин Б получил бы не прокси А, а оригинал.

**Полный сценарий (А ↔ Б):**
1. Создаём А: конструктор выполнен → фабрика А в L3
2. Начинаем заполнять зависимости А → нужен Б
3. Создаём Б: конструктор выполнен → фабрика Б в L3
4. Заполняем зависимости Б → нужен А
5. Ищем А: в L1 нет (не готов), но он помечен `inCreation` → смотрим L2 → пусто → смотрим L3 → **нашли фабрику!** Вызываем → получаем А (возможно, прокси) → помещаем в L2
6. Б заполнен → Б готов → Б → L1
7. Возвращаемся к А: получаем готовый Б из L1 → А заполнен → А → L1

Красиво, правда? Но есть ограничения. С **конструкторной инъекцией** это не работает: `addSingletonFactory()` вызывается только **после** конструктора. Если конструктору А нужен Б, а конструктору Б — А, ни один конструктор не может завершиться → фабрики не регистрируются.

Начиная с Spring Boot 2.6 циклические зависимости **запрещены по умолчанию** (`spring.main.allow-circular-references=false`). Они почти всегда — признак плохого дизайна. Если очень нужно: `spring.main.allow-circular-references=true`, но лучше потратить время на рефакторинг.

### 4.3. Почему конструкторная инъекция не поддерживает циклические зависимости?

По фундаментальной причине: JVM не может создать объект не выполнив его конструктор. Если конструктору А нужен готовый Б, а конструктору Б — готовый А, мы в тупике. Ни один не может завершиться первым. `StackOverflowError` — лучшее что вы получите, худшее — зависание.

Это не баг Spring, это ограничение Java. Именно поэтому трёхуровневый кэш работает только с сеттерами и полями — там объект уже создан (конструктор отработал), и можно передать ссылку на «полуфабрикат».

### 4.4. JDK Dynamic Proxy vs CGLIB: когда что используется?

Два механизма проксирования, и Spring выбирает между ними автоматически:

- **JDK Dynamic Proxy** — родной для Java, лежит в `java.lang.reflect`. Создаёт прокси, реализующий **интерфейсы** целевого объекта. Быстрый, не требует сторонних библиотек, но есть нюанс: внедрять такой бин можно только по интерфейсу. Попытка внедрить по классу → `NoSuchBeanDefinitionException`.

- **CGLIB** — библиотека, встроенная прямо в Spring Core. Работает через наследование: создаёт подкласс вашего класса и переопределяет методы, добавляя прокси-логику. Можно внедрять по классу. Минус: `final`-методы и `final`-классы не проксируются — их нельзя переопределить.

**Правило выбора:** если класс реализует интерфейс → JDK Proxy. Если нет → CGLIB. В Spring Boot по умолчанию форсирован CGLIB через `spring.aop.proxy-target-class=true`, чтобы избежать сюрпризов при инъекции по классу.

### 4.5. Почему final-методы нельзя проксировать через CGLIB?

CGLIB создаёт подкласс (`class UserService$$CGLIB extends UserService`) и переопределяет каждый метод, добавляя свою логику. `final`-метод **нельзя** переопределить — это фундаментальное правило Java. Поэтому вызов на прокси пройдёт мимо CGLIB-логики прямиком в оригинальный метод. Ни транзакции, ни кэширования, ни AOP на таком методе не будет.

### 4.6. Как работает Scope-прокси для request/session бинов в синглтонах?

Представьте: у вас singleton-сервис, которому нужен request-scoped бин (например, данные текущего пользователя). Singleton создаётся один раз при старте, а request-бинов в этот момент ещё не существует. Как быть?

Spring решает это через scope-прокси. Вы говорите: `@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)`, и Spring создаёт не сам бин, а CGLIB-прокси. Этот прокси внедряется в singleton. Когда кто-то дёргает метод прокси, тот идёт в контекст текущего запроса, находит реальный request-бин и делегирует вызов ему.

По сути, прокси работает как «умный указатель» — каждый вызов переадресуется в правильный контекст. `TARGET_CLASS` использует CGLIB, `INTERFACES` — JDK Proxy. Первый вариант надёжнее.

---

## 5. Конфигурация (@Configuration, @Bean, @Import)

### 5.1. Как работает @Bean в @Configuration классе?

Методы `@Bean` производят бины. Класс `@Configuration` проксируется CGLIB, что гарантирует: при вызове метода `@Bean` внутри другого метода `@Bean`, Spring **не выполняет код метода заново**, а возвращает существующий экземпляр из контейнера — соблюдение Singleton scope.

### 5.2. Как работает @Configuration и чем отличается от @Component? (Full mode vs Lite mode)

- **@Configuration (Full mode)**: Класс оборачивается CGLIB-прокси. Вызов `beanA()` → `beanB()` перехватывается прокси и возвращает существующий бин.
- **@Component (Lite mode)**: Методы `@Bean` внутри `@Component` — обычные Java-методы. Вызов `beanA()` → `beanB()` создаст новый экземпляр при каждом вызове. Семантика синглтона не соблюдается.

Full mode — для конфигураций, Lite mode — достаточно для простых фабричных методов.

### 5.3. Как @Import и @ImportResource работают на уровне загрузки контекста?

- **@Import**: Регистрирует `@Configuration` классы или обычные компоненты напрямую в `BeanDefinitionRegistry`. Работает на этапе `ConfigurationClassPostProcessor`.
- **@ImportResource**: Загружает XML-конфиги. Spring использует `BeanDefinitionReader`, соответствующий расширению файла.

---

## 6. Аннотации и их обработка

### 6.1. Как Spring обрабатывает аннотации (@Component, @Autowired)?

Под капотом работают два механизма, принципиально разных по своей природе:

- **Поиск компонентов** — этим занимается `ClassPathBeanDefinitionScanner`. Он не загружает классы в JVM чтобы не тратить память, а читает байт-код напрямую через ASM. Находит аннотации `@Component` (и все производные — `@Service`, `@Repository`, `@Controller`), создаёт `BeanDefinition` и регистрирует в фабрике. Сами объекты пока не создаются — только метаданные.

- **Внедрение зависимостей** — `AutowiredAnnotationBeanPostProcessor` на этапе `postProcessProperties` проходит по всем полям, методам и конструкторам с `@Autowired`. Для каждого находит подходящий бин в `BeanFactory` (по типу, затем по имени) и внедряет через Reflection. Именно здесь происходит то самое «связывание» бинов.

### 6.2. Как работает @AliasFor?

Элегантный механизм, который позволяет двум атрибутам аннотации быть синонимами. Два сценария:

- **Внутри одной аннотации** — хотите чтобы `value` и `path` делали одно и то же (как в `@RequestMapping`). `@AliasFor` делает их взаимозаменяемыми.
- **Через мета-аннотации** — когда у вас составная аннотация, и нужно «пробросить» атрибут в одну из её частей. Например, `@SpringBootApplication` содержит `@ComponentScan`, и через `@AliasFor` вы можете задать `scanBasePackages` прямо на `@SpringBootApplication` — Spring сам передаст этот атрибут в `@ComponentScan`.

Внутри Spring использует `AnnotationUtils.synthesizeAnnotation()` чтобы собрать итоговую аннотацию из нескольких уровней. Если атрибуты-синонимы имеют разные значения — исключение.

### 6.3. Как работает @Enable* семейство аннотаций?

Все аннотации семейства `@Enable*` работают по одному шаблону: `@Import(КакойТоИмпортСелектор.class)`. Сам ImportSelector решает какие бины нужно зарегистрировать для включения фичи. Вот основные:

- `@EnableCaching` → `CachingConfigurationSelector` → регистрирует `CacheInterceptor` (AOP-перехватчик для `@Cacheable`) и `BeanFactoryPostProcessor` для настройки
- `@EnableAsync` → `AsyncConfigurationSelector` → `AsyncAnnotationBeanPostProcessor` — обрабатывает `@Async`, отправляя методы в TaskExecutor
- `@EnableScheduling` → `SchedulingConfiguration` → `ScheduledAnnotationBeanPostProcessor`
- `@EnableTransactionManagement` → `TransactionManagementConfigurationSelector` → `TransactionInterceptor`
- `@EnableAspectJAutoProxy` → включает AOP-проксирование (без него `@Aspect` не работает)
- `@EnableWebMvc` → загружает всю MVC-конфигурацию

Сам паттерн простой и расширяемый: если вы пишете свою фичу, можно сделать `@EnableMyFeature` с такой же механикой.

---

## 7. Профили (@Profile) и @Lazy

### 7.1. Как работает @Profile?

Позволяет регистрировать бины только при активации определённого профиля (dev, test, prod). Можно ставить над `@Configuration` или отдельным `@Bean`.

**Механизм**: При старте контекста Spring проверяет активные профили. Если профиль бина не совпадает — определение бина пропускается (не регистрируется в `BeanDefinitionRegistry`).

**Активация**: `spring.profiles.active=dev` в properties, `-Dspring.profiles.active=prod` или `SPRING_PROFILES_ACTIVE` в переменных окружения.

### 7.2. Как работает @Lazy?

Бин не создаётся при старте, а только при первом обращении. Spring создаёт CGLIB-прокси, который при первом вызове инициализирует реальный объект.

**Оправдано**: для разруливания циклических зависимостей; для тяжёлых бинов (генерация отчётов), которые нужны редко.

**Оптимизация старта**: `spring.main.lazy-initialization=true` делает все бины ленивыми. Ускоряет старт, но ошибки конфигурации проявляются только в runtime.

### 7.3. Почему @Value не работает в static полях и как обойти?

Spring внедряет зависимости в экземпляры бинов. Статические поля принадлежат классу, а не объекту. Обход:
- Нестатический сеттер с `@Value`, внутри которого запись в static поле
- `@PostConstruct`: записать значение из нестатического поля в статическое

---

## 8. AOP (Aspect-Oriented Programming)

### 8.1. Что такое AOP и как он реализован в Spring?

AOP — парадигма вынесения сквозной функциональности (логирование, транзакции, безопасность) в отдельные модули — аспекты.

**Внутреннее устройство Spring AOP:**

**Фаза 1 — Создание прокси (`AbstractAutoProxyCreator`):**

`AbstractAutoProxyCreator` — это `SmartInstantiationAwareBeanPostProcessor`, который на этапе `postProcessAfterInitialization` решает, нужен ли бину прокси:

```java
// Упрощённая логика AbstractAutoProxyCreator.wrapIfNecessary():
Object wrapIfNecessary(Object bean, String beanName) {
    // 1. Найти все Advice/Advisor, pointcut которых совпадает с методами бина
    Object[] specificInterceptors = getAdvicesAndAdvisorsForBean(bean.getClass(), beanName);
    if (specificInterceptors == DO_NOT_PROXY) return bean; // не нужно проксировать

    // 2. Создать прокси через ProxyFactory
    ProxyFactory proxyFactory = new ProxyFactory();
    proxyFactory.copyFrom(this);
    proxyFactory.setTarget(bean);
    proxyFactory.addAdvisors(specificInterceptors);
    return proxyFactory.getProxy(); // → DefaultAopProxyFactory.createAopProxy()
}
```

**Выбор JDK vs CGLIB** (`DefaultAopProxyFactory`):
- Если класс реализует интерфейс и не задан флаг `proxyTargetClass` → `JdkDynamicAopProxy`
- Иначе → `CglibAopProxy` (работает через Enhancer от ByteBuddy в Spring 6+)

**Фаза 2 — Выполнение (цепочка Advice):**

При вызове метода на прокси:
```java
// JdkDynamicAopProxy.invoke():
public Object invoke(Object proxy, Method method, Object[] args) {
    // 1. Получить цепочку интерсепторов для метода
    List<Object> chain = advised.getInterceptorsAndDynamicInterceptionAdvice(method, targetClass);
    if (chain.isEmpty()) return method.invoke(target, args); // без Advice

    // 2. Построить ReflectiveMethodInvocation — цепочка вызовов
    MethodInvocation invocation = new ReflectiveMethodInvocation(
        proxy, target, method, args, targetClass, chain);
    // 3. Запустить цепочку
    return invocation.proceed();
}
```

**`ReflectiveMethodInvocation.proceed()`** идёт по цепочке интерсепторов:
```
Interceptor1.invoke() → Interceptor2.invoke() → ... → InterceptorN.invoke() → method.invoke(target)
```
Каждый Advice становится `MethodInterceptor`: `@Before` → `MethodBeforeAdviceInterceptor`, `@Around` → `AspectJAroundAdvice`, `@After` → `AspectJAfterAdvice`.

Работает только для публичных методов Spring-бинов. Self-invocation (`this.method()`) обходит прокси.

### 8.2. Типы Advice в Spring AOP

- **@Before**: выполняется до метода
- **@AfterReturning**: после успешного возврата
- **@AfterThrowing**: после исключения
- **@After (Finally)**: в любом случае (finally)
- **@Around**: самый мощный. Оборачивает метод, получает `ProceedingJoinPoint`, может контролировать выполнение (изменить аргументы, пропустить вызов, изменить результат)

### 8.3. Spring AOP vs AspectJ

- **Spring AOP**: на уровне прокси, только public-методы бинов. Проще, но ограничен.
- **AspectJ**: полноценный AOP-фреймворк. Работает на уровне байт-кода (weaving на этапе компиляции или загрузки класса). Может перехватывать private-методы, конструкторы, поля. Не требует Spring-контейнера.

### 8.4. Как Spring AOP создаёт прокси для бинов?

1. После `postProcessAfterInitialization` Spring проверяет, есть ли для бина подходящие аспекты
2. Если есть — создаётся прокси (JDK/CGLIB), оборачивающий оригинальный бин
3. В контекст возвращается прокси вместо оригинального бина
4. При вызове метода прокси выполняет цепочку Advice'ов и делегирует оригинальному бину

### 8.5. Как работает @DeclareParents?

Позволяет динамически добавить новую реализацию интерфейса к существующему бину. Например, заставить все бины `UserService` также реализовывать `Auditable` без изменения кода.

---

## 9. Транзакции (@Transactional)

### 9.1. Как работает @Transactional?

`@Transactional` реализован через AOP. При старте `@EnableTransactionManagement` регистрирует `TransactionInterceptor` (реализует `MethodInterceptor`).

**Цепочка при вызове метода:**

```
Прокси → TransactionInterceptor.invoke() → TransactionAspectSupport.invokeWithinTransaction():
  1. TransactionAttributeSource получает настройки @Transactional (propagation, isolation, ...)
  2. PlatformTransactionManager.getTransaction():
     a. Проверяет TransactionSynchronizationManager — есть ли активная транзакция?
     b. Если REQUIRED и есть → присоединяется
     c. Если REQUIRES_NEW → приостанавливает текущую (сохраняет ресурсы) → создаёт новую
     d. DataSourceTransactionManager: connection = dataSource.getConnection()
        connection.setAutoCommit(false)
        connection.setTransactionIsolation(isolationLevel)
        TransactionSynchronizationManager.bindResource(dataSource, connectionHolder)
  3. Выполняется target-метод
  4. При успехе: tm.commit() → connection.commit() → unbindResource → connection.close()
  5. При исключении: tm.rollback() → connection.rollback() → unbindResource → connection.close()
```

**Ключевые внутренние механизмы:**

- **`TransactionSynchronizationManager`**: хранит ресурсы в `ThreadLocal<Map<Object, Object>> resources` — привязывает Connection/EntityManager к текущему потоку. Это позволяет разным методам в одной транзакции использовать один и тот же Connection.
- **`TransactionSynchronization`**: callback-и для хуков в жизненном цикле транзакции:
  - `beforeCommit()` / `beforeCompletion()` / `afterCommit()` / `afterCompletion()`
  - Используются `@TransactionalEventListener` и Hibernate для flush-логики
- **`AbstractPlatformTransactionManager`**:
  - `getTransaction()` — начинает или присоединяется с учётом propagation
  - `commit()` — вызывает `triggerBeforeCommit()` → `doCommit()` → `triggerAfterCommit()`
  - `rollback()` — вызывает `doRollback()` + `triggerAfterCompletion()`
  - `suspend()` / `resume()` — для REQUIRES_NEW и NOT_SUPPORTED

**Почему не работает self-invocation:** Прокси создаётся на уровне бина (внешняя обёртка). Вызов `this.method()` идёт напрямую к `this` (таргет), минуя прокси → ни `TransactionInterceptor`, ни `TransactionSynchronizationManager` не активируются.

### 9.2. Почему @Transactional не работает при вызове метода внутри того же класса?

Из-за прокси. `this.innerMethod()` вызывает метод на реальном объекте, минуя прокси → транзакционная логика не срабатывает.

**Решения:**
- Self-injection: `@Autowired private MyService self` и вызов `self.innerMethod()`
- Вынести метод в отдельный бин
- `((MyService) AopContext.currentProxy()).innerMethod()` (нужен `@EnableAspectJAutoProxy(exposeProxy = true)`)

### 9.3. Propagation-уровни

**Механизм «приостановки» (suspension):** `TransactionSynchronizationManager.unbindResource()` + сохранение текущего состояния ресурсов. При возобновлении — `bindResource()` восстанавливает привязку. Это работает на уровне ThreadLocal — физический Connection не закрывается, а «откладывается» и позже восстанавливается.

| Уровень | Поведение | Типичный Use Case |
|---|---|---|
| **REQUIRED** (по умолчанию) | Использует существующую транзакцию или создаёт новую | Стандартный метод сервиса |
| **REQUIRES_NEW** | Всегда создаёт новую транзакцию, приостанавливая текущую | Аудит/логирование (не должен откатываться с основной транзакцией) |
| **SUPPORTS** | Есть транзакция — использует, нет — работает без | Чтение, которому транзакция не критична |
| **NOT_SUPPORTED** | Всегда без транзакции, приостанавливая текущую | Тяжёлые операции, которые не должны держать Connection |
| **MANDATORY** | Требует существующей транзакции, иначе исключение | Методы, которые всегда должны вызываться внутри транзакционного контекста |
| **NEVER** | Требует отсутствия транзакции, иначе исключение | Операции, несовместимые с транзакциями |
| **NESTED** | Создаёт savepoint внутри существующей транзакции | Частичный откат внутри большой транзакции |

**Важные детали:**

- **REQUIRES_NEW**: старая транзакция ставится на паузу — её изменения не видны в новой, и наоборот. Если новая транзакция закоммитится, а старая откатится — изменения новой останутся. Если обе меняют одну строку → deadlock (новая ждёт старую, или `OptimisticLockException` при коммите старой).

- **NESTED и JPA**: JPA/Hibernate **не поддерживают** savepoints. `NESTED` работает только с `JdbcTransactionManager` (чистый JDBC). Причина: JPA EntityManager не умеет сохранять и восстанавливать состояние Persistence Context при savepoint-операциях. С JPA используйте `REQUIRES_NEW` вместо `NESTED`.

- **Self-invocation и propagation**: `this.method()` обходит прокси → propagation не работает. Вызов должен идти через другой бин или self-injection.

### 9.4. Isolation-уровни

| Уровень | Dirty Read | Non-repeatable Read | Phantom Read |
|---|---|---|---|
| `READ_UNCOMMITTED` | Да | Да | Да |
| `READ_COMMITTED` (PG default) | Нет | Да | Да |
| `REPEATABLE_READ` (MySQL default) | Нет | Нет | В PG — нет, в MySQL — да |
| `SERIALIZABLE` | Нет | Нет | Нет |

**Как реализовано в БД:**
- **PostgreSQL**: MVCC (Multiversion Concurrency Control) — каждая транзакция видит снимок данных на момент начала. `REPEATABLE_READ` в PG уже защищает от фантомов (в отличие от стандарта SQL).
- **MySQL/InnoDB**: блокировки + MVCC. `REPEATABLE_READ` защищает от неповторяющегося чтения, но не от фантомов (нужен `SERIALIZABLE` или gap locks).

**Практическое применение:**
- **Lost Update** (потеря обновления): Т1 читает x=100, Т2 читает x=100, Т1 пишет x=110, Т2 пишет x=90 → изменение Т1 потеряно. Решается `@Version` (оптимистичная блокировка) на уровне приложения или `SELECT FOR UPDATE` (пессимистичная).
- **Write Skew**: две транзакции читают пересекающиеся данные и обновляют разные строки, нарушая инвариант. Решается `SERIALIZABLE` или явной блокировкой.
- **@Version + READ_COMMITTED** — стандартный production-подход: быстрая изоляция чтения + защита записи через версионирование.

### 9.5. Как работает rollback?

По умолчанию откат только при `RuntimeException` и `Error` (unchecked). Checked exceptions (`Exception`) НЕ вызывают откат. Настройка:
- `rollbackFor = Exception.class` — откат для всех исключений
- `noRollbackFor = SomeException.class` — не откатывать при конкретном исключении

### 9.6. Как работает @Transactional(readOnly = true)?

- Устанавливает флаг «только чтение»
- Hibernate оптимизирует: отключает dirty checking, может использовать read-only connection
- На уровне БД (PostgreSQL) может использоваться для маршрутизации на реплики

### 9.7. Как работает @Transactional с несколькими DataSource?

**Конфигурация:**

```java
@Configuration
public class DataSourceConfig {
    @Primary @Bean @ConfigurationProperties("app.datasource.orders")
    public DataSource ordersDataSource() { return DataSourceBuilder.create().build(); }

    @Bean @ConfigurationProperties("app.datasource.users")
    public DataSource usersDataSource() { return DataSourceBuilder.create().build(); }

    @Primary @Bean
    public PlatformTransactionManager ordersTxManager(@Qualifier("ordersDataSource") DataSource ds) {
        return new DataSourceTransactionManager(ds);
    }

    @Bean
    public PlatformTransactionManager usersTxManager(@Qualifier("usersDataSource") DataSource ds) {
        return new DataSourceTransactionManager(ds);
    }
}

// Использование
@Transactional("ordersTxManager")
public void createOrder() { ... }

@Transactional("usersTxManager")
public void createUser() { ... }
```

**Проблемы и решения:**

- **Несколько ТМ в одном методе?** `@Transactional` позволяет указать только один `transactionManager`. Если метод пишет в две БД, ни один из стандартных TM не даёт атомарности (каждый управляет своим Connection).

- **`ChainedTransactionManager` (удалён!)**: был в Spring Data Commons, удалён из-за опасного дизайна — коммитил по очереди, откатывал в обратном порядке. Проблема: если первый закоммитился, а второй упал — первый уже не откатить. **Не использовать.**

- **JTA (Java Transaction API)**: распределённые транзакции через двухфазный коммит (2PC). Реализации: Atomikos, Narayana, Bitronix. Дают гарантию ACID между несколькими ресурсами, но дорого по производительности и сложности.

- **Saga (современный подход)**: цепочка локальных транзакций с компенсирующими действиями. Каждый шаг — отдельная транзакция в своей БД. При ошибке выполняются компенсирующие транзакции. Реализуется через Orchestration (Spring Batch, Camunda) или Choreography (события Kafka/RabbitMQ). Минус: eventual consistency вместо ACID.

- **Transactional Outbox**: запись в основную БД + в outbox-таблицу в одной транзакции. Отдельный процесс читает outbox и шлёт во вторую БД / очередь. Гарантирует at-least-once доставку.

### 9.8. Как работает @Transactional(timeout = N)?

Устанавливает таймаут в секундах. Если транзакция длится дольше — автоматический откат. Реализуется через `Statement.setQueryTimeout()`.

---

## 10. Spring Boot — основы

### 10.1. В чём отличие Spring от Spring Boot?

- **Spring Framework**: Набор модулей (IoC, MVC, Security, Data). Требует явной конфигурации (Java Config / XML) и ручного управления версиями зависимостей.
- **Spring Boot**: Надстройка над Spring. Предоставляет:
  - Автоконфигурацию (convention over configuration)
  - Стартеры (управление транзитивными зависимостями)
  - Встроенный веб-сервер (Tomcat/Jetty/Undertow)
  - Production-ready фичи (Actuator, метрики)

### 10.2. Что такое Starter POM?

Набор транзитивных зависимостей. Например, `spring-boot-starter-web` подтягивает Spring MVC, Jackson, Tomcat, валидатор. Версии согласованы в BOM (Bill of Materials) — решает проблему «dependency hell».

### 10.3. Как работает @SpringBootApplication?

Композитная аннотация, объединяющая:
1. `@SpringBootConfiguration` (специализация `@Configuration`) — класс является конфигурацией
2. `@EnableAutoConfiguration` — включает механизм автоконфигурации
3. `@ComponentScan` — сканирует пакет и подпакеты на компоненты

`@AliasFor` используется для проброса параметров между составляющими аннотациями.

### 10.4. Как создать свой Spring Boot Starter?

Обычно два модуля:
- **`my-lib-autoconfigure`**: код автоконфигурации с `@AutoConfiguration` классом и `@ConditionalOn*` аннотациями
- **`my-lib-starter`**: пустой модуль, в pom.xml подтягивает autoconfigure и нужные зависимости

Файл регистрации: `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (вместо устаревшего `spring.factories`).

### 10.5. Как переопределить стандартные бины Spring Boot (например, ObjectMapper)?

Spring Boot использует `@ConditionalOnMissingBean`. Если вы объявите свой бин того же типа — автоконфигурация отступит. Способы:
1. Объявить `@Bean` того же типа
2. Использовать `Jackson2ObjectMapperBuilder` для тонкой настройки
3. `@Primary` если нужно переопределить, оставив другие бины

---

## 11. Spring Boot — автоконфигурация и стартеры

### 11.1. Как работает @EnableAutoConfiguration?

1. Импортирует `AutoConfigurationImportSelector`
2. Селектор читает `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` из всех jar (в старых версиях: `META-INF/spring.factories`)
3. Загружает классы конфигураций с учётом `@Conditional*` аннотаций
4. Для оптимизации используется `spring-autoconfigure-metadata.json` — пре-проверка условий без загрузки классов

### 11.2. Какие @Conditional аннотации существуют?

- `@ConditionalOnClass` / `@ConditionalOnMissingClass` — наличие/отсутствие класса в classpath
- `@ConditionalOnBean` / `@ConditionalOnMissingBean` — наличие/отсутствие бина в контексте
- `@ConditionalOnProperty` — значение свойства
- `@ConditionalOnResource` — наличие ресурса
- `@ConditionalOnWebApplication` / `@ConditionalOnNotWebApplication` — тип приложения (web/не-web)
- `@ConditionalOnExpression` — SpEL-выражение
- `@ConditionalOnJava` — версия Java
- `@ConditionalOnJndi` — доступность JNDI

### 11.3. Как отключить автоконфигурацию?

- Аннотация: `@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)`
- Properties: `spring.autoconfigure.exclude=org...DataSourceAutoConfiguration`

### 11.4. Как управлять порядком автоконфигураций?

Через аннотации:
- `@AutoConfigureAfter(SomeConfig.class)`
- `@AutoConfigureBefore(SomeConfig.class)`
- `@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)`

---

## 12. Spring Boot — запуск и жизненный цикл

### 12.1. Как работает SpringApplication.run()?

1. Создаётся экземпляр `SpringApplication`
2. Определяется тип приложения: Servlet / Reactive / None (через `WebApplicationType.deduceFromClasspath()`)
3. Загружаются `SpringApplicationRunListener` (события старта)
4. Подготавливается `Environment` (properties, переменные окружения)
5. Создаётся `ApplicationContext` нужного типа:
   - `AnnotationConfigServletWebServerApplicationContext` — для Servlet (Spring MVC)
   - `AnnotationConfigReactiveWebServerApplicationContext` — для Reactive (WebFlux)
   - `AnnotationConfigApplicationContext` — не веб
6. Загружаются определения бинов
7. `context.refresh()` — создание бинов, BPP, запуск веб-сервера
8. Вызываются `CommandLineRunner` / `ApplicationRunner`

### 12.2. Что такое ApplicationContextInitializer?

Интерфейс, вызываемый до `refresh()` контекста. Позволяет программно добавить PropertySource, зарегистрировать бины или изменить Environment до начала основной работы.

### 12.3. Что такое SpringApplicationRunListener?

Интерфейс для прослушивания событий жизненного цикла запуска:
- `starting()` — начало
- `environmentPrepared()` — environment готов
- `contextPrepared()` — контекст создан, но пуст
- `contextLoaded()` — бины загружены
- `started()` — контекст поднят
- `running()` / `failed()` — приложение запущено / ошибка

---

## 13. Spring Boot — конфигурация и свойства

### 13.1. Как Spring Boot обрабатывает application.properties/yml?

1. `SpringApplication` создаёт `Environment` через `StandardEnvironment`
2. Ищет файлы `application.properties` и `application.yml` в locations (по приоритету):
   - `file:./config/`
   - `file:./`
   - `classpath:config/`
   - `classpath:`
3. Загружает через `PropertiesPropertySourceLoader` / `YamlPropertySourceLoader`
4. `PropertySourcesPlaceholderConfigurer` (BFPP) заменяет `${property}` в определениях бинов на значения из Environment

### 13.2. Как @ConfigurationProperties биндит свойства в объекты?

`ConfigurationPropertiesBindingPostProcessor` связывает свойства из Environment с полями Java-бина через сеттеры/конструктор, используя relaxed binding (kebab-case → camelCase: `my-property` → `myProperty`).

### 13.3. @ConfigurationProperties vs @Value — что выбрать?

| Характеристика | @ConfigurationProperties | @Value |
|---|---|---|
| Группировка | Да (целый класс свойств) | Нет (одно свойство) |
| Relaxed binding | Да (`my-prop` → `myProp`) | Частично |
| Validation | `@Validated` + Bean Validation | Нет |
| SpEL | Нет | Да (`#{expression}`) |
| Перезагрузка | Да (через `@RefreshScope`) | Нет |
| Использование | Внешние конфигурации, префиксы | Точечные значения |

**Совет**: `@ConfigurationProperties` для группированных настроек (database, mail, cache), `@Value` для одного-двух свойств или SpEL-выражений.

### 13.4. Как валидировать @ConfigurationProperties?

```java
@Validated
@ConfigurationProperties(prefix = "app.mail")
public class MailProperties {
    @NotBlank
    private String host;

    @Min(1) @Max(65535)
    private int port;

    @Email
    private String from;
}
```

Требует `spring-boot-starter-validation` (Hibernate Validator). При невалидных значениях — приложение не стартует.

### 13.5. Приоритет свойств (от высшего к низшему)

1. Аргументы командной строки (`--server.port=8081`)
2. System Properties (`-Dkey=value`)
3. Переменные окружения ОС (`SPRING_DATASOURCE_URL`)
4. Профильные `application-{profile}.properties`
5. Основной `application.properties`
6. `@PropertySource` в конфигурации
7. Дефолтные свойства (`SpringApplication.setDefaultProperties`)

### 13.6. Как реализовать кастомный PropertySource?

1. Унаследовать `PropertySource<T>`
2. Реализовать `getProperty(String name)`
3. Добавить в окружение: `environment.getPropertySources().addLast(new MySource(...))`

Используется для чтения конфигов из БД, Redis, внешних API.

---

## 14. Spring Boot — встроенные серверы и сервлеты

### 14.1. Как Spring Boot встраивает Tomcat/Jetty/Undertow?

Встроенный сервер — это не отдельный процесс, а бин внутри Spring Context:
1. Автоконфигурация `ServletWebServerFactoryAutoConfiguration` ищет классы серверов в classpath
2. Создаёт `ServletWebServerFactory`:
   - `TomcatServletWebServerFactory` (по умолчанию)
   - `JettyServletWebServerFactory`
   - `UndertowServletWebServerFactory`
3. В `onRefresh()` веб-контекста вызывается `factory.getWebServer()`
4. Фабрика программно создаёт сервер, настраивает порты, запускает

### 14.2. Как DispatcherServlet регистрируется автоматически?

1. `DispatcherServletAutoConfiguration` создаёт бин `DispatcherServlet`
2. Создаётся `DispatcherServletRegistrationBean`
3. Регистратор добавляет сервлет в `ServletContext` встроенного Tomcat, маппя на `/` — программный аналог `web.xml`

### 14.3. Как заменить встроенный сервер?

- Jetty: исключить `spring-boot-starter-tomcat`, добавить `spring-boot-starter-jetty`
- Undertow: исключить Tomcat, добавить `spring-boot-starter-undertow`

---

## 15. Spring Boot — Actuator и мониторинг

### 15.1. Что такое Spring Boot Actuator?

Библиотека (`spring-boot-starter-actuator`) для мониторинга и управления приложением в production.

**Основные endpoints:**
- `/actuator/health` — здоровье (БД, диск, внешние сервисы)
- `/actuator/info` — информация о приложении
- `/actuator/metrics` — метрики для Prometheus/Grafana
- `/actuator/env` — свойства окружения
- `/actuator/loggers` — управление уровнями логирования в runtime
- `/actuator/threaddump` — дамп потоков
- `/actuator/beans` — список бинов в контексте
- `/actuator/mappings` — все маппинги запросов

### 15.2. Как Micrometer собирает метрики HTTP-запросов?

1. `WebMvcMetricsFilter` (или `WebFluxMetricsFilter`) перехватывает каждый HTTP-запрос
2. Собирает: время выполнения, статус, URI, метод
3. Сохраняет в `MeterRegistry` под именем `http.server.requests`
4. Теги: `method`, `status`, `uri`, `exception`

---

## 16. Spring Boot — Native Image (GraalVM)

### 16.1. Как Spring AOT компилирует приложение в Native Image?

1. **Spring AOT Processing**: на этапе сборки плагин анализирует код, генерирует оптимизированный байт-код — заменяет рефлексию прямыми вызовами, предсобирает граф бинов
2. **GraalVM Native Image Builder**: выполняет статический анализ от `main()`, удаляет мёртвый код, создаёт исполняемый файл с Substrate VM вместо полноценной JVM

### 16.2. Ограничения GraalVM

- Рефлексия, прокси, сериализация требуют предварительной конфигурации (Hints)
- Community Edition: только Serial GC (G1 — Oracle GraalVM)
- Инструменты профилирования работают иначе
- Библиотеки с runtime bytecode enhancement могут не работать

### 16.3. Как настроить Reflection Hints для JPA?

Реализовать `RuntimeHintsRegistrar`, зарегистрировать через `@ImportRuntimeHints(MyHints.class)`:

```java
public class MyHints implements RuntimeHintsRegistrar {
    @Override
    public void registerHints(RuntimeHints hints, ClassLoader classLoader) {
        hints.reflection().registerType(UserEntity.class,
            MemberCategory.INVOKE_PUBLIC_CONSTRUCTORS,
            MemberCategory.INVOKE_PUBLIC_METHODS);
    }
}
```

### 16.4. Влияние AOT на стартап

- Нет интерпретации/JIT-разогрева — код уже скомпилирован
- Готовый граф бинов — не нужно classpath scanning
- Потребление памяти снижается в 3–5 раз
- Время старта: с 5–10 сек до 50–100 мс

---

## 17. Spring Boot — DevTools

### 17.1. Что такое Spring Boot DevTools?

Модуль (`spring-boot-devtools`) для ускорения разработки:
- **Automatic Restart**: при изменении классов в classpath приложение перезагружается (быстрее холодного старта за счёт двух ClassLoader-ов)
- **LiveReload**: встроенный сервер для автоматического обновления браузера
- **Отключение кэширования**: Thymeleaf, статика не кэшируются в dev-режиме
- **Remote Debug**: туннелирование для удалённой отладки
- **H2 Console**: доступ к встроенной БД через браузер

### 17.2. Как работает Automatic Restart?

DevTools использует два ClassLoader-а:
- **Base ClassLoader**: загружает стабильные библиотеки (jar-файлы)
- **Restart ClassLoader**: загружает классы проекта

При изменении файла выбрасывается только Restart ClassLoader и создаётся новый — это значительно быстрее полного перезапуска JVM.

---

## 18. Сервлеты (Servlet API)

### 18.1. Что такое сервлет и как он работает?

**Сервлет** — Java-класс, обрабатывающий HTTP-запросы и генерирующий HTTP-ответы. Работает внутри Servlet-контейнера (Tomcat, Jetty). Определён в спецификации Jakarta Servlet (ранее Java Servlet).

**Жизненный цикл:**
1. **Инициализация**: контейнер вызывает `init(ServletConfig)` — один раз при создании
2. **Обслуживание**: для каждого запроса вызывается `service(ServletRequest, ServletResponse)` → делегирует в `doGet()`/`doPost()` и т.д.
3. **Уничтожение**: `destroy()` — перед выгрузкой сервлета

### 18.2. Что такое ServletContext и ServletConfig?

- **ServletContext**: один на веб-приложение. Общий контекст для всех сервлетов. Позволяет получать информацию о сервере, устанавливать атрибуты, доступные всем сервлетам.
- **ServletConfig**: один на сервлет. Содержит параметры инициализации конкретного сервлета из `web.xml` или аннотаций.

### 18.3. Как работает FilterChain?

**Filter** — компонент для перехвата запросов ДО того как они достигнут сервлета. Образуют цепочку (Chain of Responsibility):
1. `Filter1.doFilter()` → pre-processing → `chain.doFilter()` → `Filter2.doFilter()` → ... → `Servlet.service()` → ... → post-processing (в обратном порядке)
2. Каждый фильтр может модифицировать request/response или прервать цепочку

### 18.4. Что такое асинхронные сервлеты и зачем они нужны?

Асинхронные сервлеты (Servlet 3.0+) позволяют обрабатывать запросы без блокировки потока контейнера:
- `request.startAsync()` — освобождает поток контейнера
- Работа завершается в другом потоке через `asyncContext.complete()`
- Актуально для long-polling, Server-Sent Events, WebSocket-подобных сценариев

### 18.5. Сервлеты vs Реактивный стек (WebFlux)

| Характеристика | Servlet (Spring MVC) | Reactive (WebFlux) |
|---|---|---|
| Модель | Один поток на запрос (Thread pool) | Event loop, неблокирующий I/O |
| Стандарт | Jakarta Servlet API | Reactive Streams |
| Сервер | Tomcat, Jetty (Servlet-контейнер) | Netty, Undertow (реактивный) |
| БД | JDBC (блокирующий) | R2DBC (реактивный) |
| Подходит для | Типичные CRUD-приложения | Высоконагруженные, streaming |

---

## 19. Spring MVC — DispatcherServlet и обработка запросов

### 19.1. Как работает DispatcherServlet?

**DispatcherServlet** — фронт-контроллер Spring MVC, точка входа для всех HTTP-запросов.

**Полный алгоритм `doDispatch()` (упрощённо):**

```java
protected void doDispatch(HttpServletRequest request, HttpServletResponse response) {
    HttpServletRequest processedRequest = request;
    HandlerExecutionChain mappedHandler = null;
    boolean multipartRequestParsed = false;

    try {
        // 1. Проверить multipart (файлы)
        processedRequest = checkMultipart(request);
        multipartRequestParsed = (processedRequest != request);

        // 2. Найти Handler (контроллер) через HandlerMapping
        mappedHandler = getHandler(processedRequest);
        if (mappedHandler == null) {
            noHandlerFound(processedRequest, response); return;
        }

        // 3. Найти HandlerAdapter (может выполнить этот Handler)
        HandlerAdapter ha = getHandlerAdapter(mappedHandler.getHandler());

        // 4. PreHandle — перехватчики (может прервать)
        if (!mappedHandler.applyPreHandle(processedRequest, response)) return;

        // 5. Выполнить контроллер → ModelAndView
        mv = ha.handle(processedRequest, response, mappedHandler.getHandler());

        // 6. Установить имя View по умолчанию (если null)
        applyDefaultViewName(processedRequest, mv);

        // 7. PostHandle — перехватчики после контроллера
        mappedHandler.applyPostHandle(processedRequest, response, mv);

    } catch (Exception ex) {
        dispatchException = ex;  // будет обработан в processDispatchResult
    }

    // 8. Рендеринг View + триггер afterCompletion
    processDispatchResult(processedRequest, response, mappedHandler, mv, dispatchException);
}
```

**В `processDispatchResult()`:**
1. Если было исключение → `HandlerExceptionResolver` (три по очереди):
   - `ExceptionHandlerExceptionResolver` — методы с `@ExceptionHandler`
   - `ResponseStatusExceptionResolver` — `@ResponseStatus` на исключениях
   - `DefaultHandlerExceptionResolver` — стандартные Spring исключения → HTTP-статусы
2. Если есть `ModelAndView` → рендеринг через `ViewResolver` → `View.render()`
3. Если `@ResponseBody` → `HttpMessageConverter.write()` (сериализация в JSON)
4. `mappedHandler.triggerAfterCompletion()` — завершающий callback перехватчиков

**Асинхронная обработка:** если контроллер возвращает `Callable<>` или `DeferredResult`, `DispatcherServlet` освобождает поток контейнера через `AsyncContext.startAsync()`, а результат отправляется позже из другого потока (через `AsyncTaskExecutor`).

**Multipart:** `MultipartResolver` проверяет запрос, и если это multipart — оборачивает request в `StandardMultipartHttpServletRequest`, предоставляя доступ к файлам.

### 19.2. Как работает HandlerMapping?

Интерфейс, определяющий какой контроллер обработает запрос. Реализации:
- `RequestMappingHandlerMapping` — аннотации `@RequestMapping` и производные
- `BeanNameUrlHandlerMapping` — имена бинов как URL
- `SimpleUrlHandlerMapping` — явный маппинг

### 19.3. Как работает HandlerAdapter?

Адаптирует контроллер к DispatcherServlet:
- `RequestMappingHandlerAdapter` — для `@RequestMapping` методов
- `HttpRequestHandlerAdapter` — для `HttpRequestHandler`
- `SimpleControllerHandlerAdapter` — для старого `Controller` интерфейса

HandlerAdapter отвечает за вызов метода с правильными аргументами (`@RequestParam`, `@PathVariable`, `@RequestBody`...) через `HandlerMethodArgumentResolver`.

### 19.4. Как работает ViewResolver?

Преобразует логическое имя view в реальный View-объект:
- `InternalResourceViewResolver` — JSP
- `ThymeleafViewResolver` — Thymeleaf
- `FreeMarkerViewResolver` — FreeMarker
- `BeanNameViewResolver` — имена бинов как View

### 19.5. Что такое ModelAndView?

Объект-контейнер, объединяющий модель (данные) и представление (view). Контроллер возвращает `ModelAndView`, DispatcherServlet использует ViewResolver для рендеринга. В REST-контроллерах (`@RestController`) не используется — данные возвращаются напрямую через `@ResponseBody`.

---

## 20. Spring MVC — контроллеры и аннотации

### 20.1. @RequestMapping, @GetMapping, @PostMapping etc.

- **@RequestMapping**: базовый маппинг (value, method, params, headers, consumes, produces)
- **@GetMapping** = `@RequestMapping(method = GET)`
- **@PostMapping** = `@RequestMapping(method = POST)`
- **@PutMapping** = `@RequestMapping(method = PUT)`
- **@DeleteMapping** = `@RequestMapping(method = DELETE)`
- **@PatchMapping** = `@RequestMapping(method = PATCH)`

### 20.2. @RequestParam, @PathVariable, @RequestBody, @ResponseBody

- **@RequestParam**: параметры запроса (`?key=value`). `required`, `defaultValue`
- **@PathVariable**: переменные из URL (`/users/{id}`)
- **@RequestBody**: тело запроса → Java-объект (через `HttpMessageConverter`, обычно Jackson)
- **@ResponseBody**: возвращаемое значение → тело ответа (сериализация в JSON/XML)
- **@RestController** = `@Controller` + `@ResponseBody` на всех методах

### 20.3. @RequestHeader, @CookieValue, @RequestAttribute, @SessionAttribute

- **@RequestHeader("User-Agent")**: значение заголовка запроса
- **@CookieValue("sessionId")**: значение cookie
- **@RequestAttribute("userId")**: атрибут запроса (установленный фильтром/перехватчиком)
- **@SessionAttribute("user")**: атрибут HTTP-сессии

### 20.4. @MatrixVariable

Извлечение матричных переменных из URL: `/cars/color=red;year=2020`

### 20.5. @CrossOrigin

Включает CORS для контроллера/метода:
- `origins` — разрешённые домены
- `methods` — разрешённые HTTP-методы
- `allowedHeaders` / `exposedHeaders`
- `allowCredentials` — куки и заголовки авторизации
- `maxAge` — время кэширования preflight-ответа

### 20.6. Как работает HttpMessageConverter?

`HttpMessageConverter` — стратегия преобразования HTTP-запроса/ответа в Java-объекты и обратно. Основные реализации:

| Конвертер | Тип контента |
|---|---|
| `MappingJackson2HttpMessageConverter` | `application/json` |
| `StringHttpMessageConverter` | `text/plain` |
| `Jaxb2RootElementHttpMessageConverter` | `application/xml` |
| `FormHttpMessageConverter` | `application/x-www-form-urlencoded` |

**Как Spring выбирает конвертер для @RequestBody:**
1. Проверяет `Content-Type` запроса
2. Ищет подходящий `HttpMessageConverter.canRead(Class, MediaType)`
3. Вызывает `converter.read()` для десериализации

**Для @ResponseBody:**
1. Проверяет `Accept` заголовок запроса (content negotiation)
2. Ищет `HttpMessageConverter.canWrite(Class, MediaType)`
3. Сериализует через `converter.write()`

---

## 21. Spring MVC — валидация и обработка ошибок

### 21.1. Как работает @Valid и @Validated?

- **@Valid (JSR-380 / Bean Validation)**: стандартная Java-аннотация, активирует валидацию параметра
- **@Validated (Spring)**: расширение, поддерживает группы валидации

При неудаче выбрасывается `MethodArgumentNotValidException` (для `@RequestBody`) или `ConstraintViolationException` (для параметров).

### 21.2. Как работают группы валидации (@Validated с группами)?

Позволяет применять разные правила для разных сценариев:

```java
public class User {
    @NotNull(groups = Create.class)
    @Null(groups = Update.class)
    private Long id;
    @NotBlank(groups = {Create.class, Update.class})
    private String name;
}

@PostMapping public User create(@Validated(Create.class) @RequestBody User u) { }
@PutMapping("/{id}") public User update(@Validated(Update.class) @RequestBody User u) { }
```

### 21.3. Основные аннотации Bean Validation

- `@NotNull`, `@Null` — null/не null
- `@NotEmpty` — не null и не пустая строка/коллекция
- `@NotBlank` — не null и не пустая строка (с учётом пробелов)
- `@Size(min, max)` — размер строки/коллекции/массива
- `@Min` / `@Max` — границы для чисел
- `@Pattern(regexp)` — регулярное выражение
- `@Email` — валидация email
- `@Positive`, `@Negative`, `@PositiveOrZero`, `@NegativeOrZero`

### 21.4. Как работает @ControllerAdvice / @RestControllerAdvice?

Глобальный обработчик для всех (REST-)контроллеров:
- **@ExceptionHandler**: перехват исключений и возврат структурированного ответа
- **@InitBinder**: глобальная настройка WebDataBinder (кастомные редакторы, форматтеры)
- **@ModelAttribute**: глобальное добавление атрибутов в модель

### 21.5. Как работает @ResponseStatusException?

Исключение для ручного проброса HTTP-ошибки из любого слоя:

```java
throw new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found");
```

Автоматически преобразуется в HTTP-ответ с указанным статусом. Может быть перехвачено в `@ExceptionHandler` для кастомной обработки.

### 21.6. Как работает ProblemDetail (RFC 7807)?

Начиная со Spring 6 / Boot 3, стандартизированный формат ошибок:

```java
@ExceptionHandler(ResourceNotFoundException.class)
public ProblemDetail handleNotFound(ResourceNotFoundException ex) {
    ProblemDetail pd = ProblemDetail.forStatusAndDetail(HttpStatus.NOT_FOUND, ex.getMessage());
    pd.setTitle("Resource Not Found");
    pd.setProperty("timestamp", Instant.now());
    return pd;
}
```

---

## 22. Spring MVC — CORS, сессии, фильтры, перехватчики

### 22.1. Filter vs HandlerInterceptor vs OncePerRequestFilter

- **Filter (Servlet API)**: работает на уровне HTTP (до Spring). Может модифицировать request/response. Не имеет доступа к Spring-контексту (кроме как через `WebApplicationContextUtils`).

- **HandlerInterceptor (Spring)**: работает на уровне контроллера. Методы:
  - `preHandle()` — до контроллера (может прервать обработку)
  - `postHandle()` — после контроллера, до рендеринга view
  - `afterCompletion()` — после рендеринга view

- **OncePerRequestFilter (Spring)**: абстрактный класс, гарантирующий выполнение фильтра ровно один раз за запрос (даже при forward/include). Часто используется в Spring Security.

### 22.2. @SessionAttributes vs @SessionAttribute

- **@SessionAttributes**: на контроллере — указывает что атрибуты модели нужно хранить в HTTP-сессии между запросами
- **@SessionAttribute**: на параметре метода — извлекает атрибут из HTTP-сессии

### 22.3. Глобальная конфигурация CORS

Через `WebMvcConfigurer`:

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/api/**")
            .allowedOrigins("http://example.com")
            .allowedMethods("GET", "POST", "PUT", "DELETE")
            .allowCredentials(true);
    }
}
```

### 22.4. @Order для фильтров и перехватчиков

- `@Order` для Filter — задаёт порядок в цепочке
- `FilterRegistrationBean.setOrder()` — альтернативный способ
- `WebMvcConfigurer.addInterceptors()` — порядок перехватчиков
- Фильтры всегда выполняются **до** перехватчиков

---

## 23. Spring Security — аутентификация

### 23.1. Как работает Security Filter Chain?

**Архитектура цепочки:**

```
HTTP-запрос
  → DelegatingFilterProxy (в Servlet-контейнере)
    → FilterChainProxy (Spring-бин, содержит список SecurityFilterChain)
      → Сопоставление RequestMatcher для каждого SecurityFilterChain
        → Первая совпавшая цепочка:
          → SecurityContextHolderFilter (загрузка SecurityContext из сессии)
          → CsrfFilter (если включён)
          → Authentication Filter (UsernamePassword/Basic/Bearer/OAuth2)
          → AuthorizationFilter (проверка прав)
          → ExceptionTranslationFilter (перехват 401/403)
          → ... контроллер ...
          → SecurityContextHolderFilter (сохранение изменённого SecurityContext)
```

**Ключевые компоненты:**

- **`DelegatingFilterProxy`**: бин в `web.xml` или авторегистрируемый. Не делает ничего сам — делегирует всё Spring-бину `FilterChainProxy` (имя бина = "springSecurityFilterChain"). Это мост между Servlet API и Spring DI.

- **`FilterChainProxy`**: получает список `SecurityFilterChain`-бинов. Каждый `SecurityFilterChain` содержит список фильтров и `RequestMatcher`. Для каждого запроса находит **первый** совпавший `SecurityFilterChain` и выполняет только его фильтры. Порядок `SecurityFilterChain` регулируется `@Order`.

- **`SecurityContextHolderFilter`** (замена `SecurityContextPersistenceFilter` с Spring Security 5.7+):
  - На входе: `SecurityContextRepository.loadContext(request)` → извлекает `SecurityContext` из HttpSession (по умолчанию `HttpSessionSecurityContextRepository`)
  - Устанавливает в `SecurityContextHolder`
  - На выходе: если `SecurityContext` изменился → `SecurityContextRepository.saveContext(context, request, response)` + `SecurityContextHolder.clearContext()`

- **`ExceptionTranslationFilter`**: перехватывает `AuthenticationException` → запускает `AuthenticationEntryPoint` (редирект на логин или 401 JSON), и `AccessDeniedException` → запускает `AccessDeniedHandler` (403).

**Конфигурация нескольких цепочек:**

```java
@Bean
@Order(1)
public SecurityFilterChain apiFilterChain(HttpSecurity http) {
    http.securityMatcher("/api/**")  // применяется только к /api/**
        .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
        .oauth2ResourceServer(oauth2 -> oauth2.jwt(Customizer.withDefaults()));
    return http.build();
}

@Bean
@Order(2)
public SecurityFilterChain webFilterChain(HttpSecurity http) {
    http.securityMatcher("/**")  // всё остальное
        .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
        .formLogin(Customizer.withDefaults());
    return http.build();
}
```

`FilterChainProxy` пройдёт по цепочкам в порядке `@Order` и выполнит первую совпавшую.

### 23.2. Как работает SecurityContextHolder?

Хранит контекст безопасности для текущего потока. Стратегии:
- `MODE_THREADLOCAL` (по умолчанию) — ThreadLocal
- `MODE_INHERITABLETHREADLOCAL` — передаётся дочерним потокам
- `MODE_GLOBAL` — глобально (для standalone-приложений)

**Важно**: в `@Async` методах контекст не передаётся автоматически — нужно настроить `SecurityContextHolder.setStrategyName(MODE_INHERITABLETHREADLOCAL)` или использовать `DelegatingSecurityContextAsyncTaskExecutor`.

### 23.3. Как работает AuthenticationManager и AuthenticationProvider?

- **AuthenticationManager** (`ProviderManager`): делегирует одному или нескольким `AuthenticationProvider` через цепочку
- **AuthenticationProvider**: конкретная логика аутентификации:
  - `DaoAuthenticationProvider` — БД через `UserDetailsService` + `PasswordEncoder`
  - `LdapAuthenticationProvider` — LDAP
  - `JwtAuthenticationProvider` — JWT
  - `OAuth2LoginAuthenticationProvider` — OAuth2 Login

Метод `authenticate()` возвращает `Authentication` с `isAuthenticated = true` или выбрасывает `AuthenticationException`.

### 23.4. Как работает UserDetailsService?

Интерфейс для загрузки пользователя: `UserDetails loadUserByUsername(String username)`. Возвращаемый `UserDetails` содержит: username, password (хеш), authorities, accountExpired, credentialsExpired, locked, enabled. Используется `DaoAuthenticationProvider`.

### 23.5. Что такое PasswordEncoder?

Интерфейс для работы с паролями:
- `encode(rawPassword)` → хеш
- `matches(rawPassword, encodedPassword)` → проверка

Рекомендуемые реализации:
- **BCryptPasswordEncoder** (наиболее распространён)
- **SCryptPasswordEncoder**
- **Argon2PasswordEncoder** (победитель Password Hashing Competition)
- **Pbkdf2PasswordEncoder**
- **DelegatingPasswordEncoder** (поддерживает несколько форматов: `{bcrypt}...`, `{noop}...`)

### 23.6. Как работает @EnableWebSecurity и SecurityFilterChain?

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .formLogin(Customizer.withDefaults())
            .oauth2Login(Customizer.withDefaults());
        return http.build();
    }
}
```

`SecurityFilterChain` заменил устаревший `WebSecurityConfigurerAdapter` (удалён в Spring Security 6).

---

## 24. Spring Security — авторизация и защита

### 24.1. @PreAuthorize, @PostAuthorize, @Secured, @RolesAllowed

- **@PreAuthorize("hasRole('ADMIN')")**: проверка ДО вызова метода (SpEL). Самый гибкий.
- **@PostAuthorize("returnObject.owner == authentication.name")**: проверка ПОСЛЕ вызова (имеет доступ к возвращаемому объекту)
- **@Secured("ROLE_ADMIN")**: проверка ролей. Требует `@EnableMethodSecurity(securedEnabled = true)`.
- **@RolesAllowed("ADMIN")**: JSR-250, только роли. Требует `@EnableMethodSecurity(jsr250Enabled = true)`.

### 24.2. @EnableMethodSecurity vs @EnableGlobalMethodSecurity

**@EnableGlobalMethodSecurity** — deprecated начиная с Spring Security 6.x. Заменён на `@EnableMethodSecurity`, который:
- По умолчанию включает `@PreAuthorize`/`@PostAuthorize`
- Использует модель авторизации на основе `AuthorizationManager` (вместо `AccessDecisionManager`)
- Поддерживает `@Secured` и `@RolesAllowed` через флаги

### 24.3. Как работает CSRF-защита?

CSRF-токен генерируется сервером, отправляется клиенту (в форме или cookie). Клиент включает токен в каждый изменяющий запрос (POST/PUT/DELETE). Сервер проверяет токен.

Для REST API обычно отключается (`http.csrf(csrf -> csrf.disable())`), так как используется stateless-аутентификация через JWT.

### 24.4. CORS в Spring Security

Настраивается через `HttpSecurity.cors()`:

```java
http.cors(cors -> cors.configurationSource(request -> {
    CorsConfiguration config = new CorsConfiguration();
    config.setAllowedOrigins(List.of("http://localhost:3000"));
    config.setAllowedMethods(List.of("GET", "POST"));
    config.setAllowCredentials(true);
    return config;
}));
```

---

## 25. Spring Security — OAuth2 / JWT

### 25.1. Как работает JWT (JSON Web Token)?

JWT — компактный токен из трёх Base64URL-кодированных частей: `header.payload.signature`.

**Структура:**
- **Header**: `{"alg": "RS256", "typ": "JWT"}`
- **Payload**: claims — `sub` (субъект), `exp` (истечение), `iat` (выпущен), `roles`, `email`
- **Signature**: подпись для проверки целостности

**Алгоритмы подписи:**
| Тип | Алгоритмы | Ключ | Когда использовать |
|---|---|---|---|
| Симметричный | HS256, HS384, HS512 | Один общий секрет | Внутренние сервисы, простое API |
| Асимметричный | RS256, ES256, PS256 | Пара private/public ключей | Микросервисы, OAuth2/OIDC (проверять может любой) |

**Асимметричные ключи предпочтительнее** для микросервисов: Auth Server подписывает private-ключом, все Resource Server проверяют public-ключом (через JWKS endpoint: `/.well-known/jwks.json`).

**Проблема инвалидации ( revocation):**
JWT самодостаточен — сервер не хранит состояние. Если токен скомпрометирован, его нельзя «отозвать» без внешнего механизма. Стратегии:
1. **Короткий TTL (15 мин) + Refresh Token**: access-токен живёт мало, refresh — долго (недели). Refresh хранится в БД и может быть отозван.
2. **Token Blacklist (Redis)**: при логауте JTI (JWT ID) добавляется в blacklist со временем жизни = оставшийся TTL токена. Каждый запрос проверяет blacklist. Минус: теряется stateless-природа JWT.
3. **Token Version (БД)**: у пользователя поле `tokenVersion`. В JWT включается версия. При логауте/смене пароля версия инкрементится → все старые токены невалидны.

**Refresh Token Rotation:** при каждом использовании refresh-токена выдаётся новый refresh и старый инвалидируется. Если старый refresh использован повторно → признак компрометации → инвалидация всей цепочки.

**Безопасность:**
- **Хранение на клиенте**: httpOnly Secure SameSite cookie (защита от XSS: JS не может читать httpOnly) для BFF-архитектур; localStorage для SPA (уязвим к XSS, но позволяет чистый stateless)
- **`alg: none` атака**: злоумышленник меняет `alg` на `none` → подпись не проверяется. Защита: явно указывать ожидаемый алгоритм на сервере (не доверять заголовку).
- **Слабый HMAC-секрет**: секрет должен быть ≥256 бит.
- **Не хранить пароли в payload**: payload не шифруется, только кодируется Base64URL. Для конфиденциальности — JWE (JSON Web Encryption).

### 25.2. Как работает OAuth2?

Протокол авторизации (НЕ аутентификации). Роли:
- **Resource Owner** — пользователь
- **Client** — приложение
- **Authorization Server** — выдаёт токены (Keycloak, Auth0)
- **Resource Server** — принимает токены

**Гранты:**
- **Authorization Code + PKCE** — современный стандарт для веб/SPA
- **Client Credentials** — server-to-server
- **Refresh Token** — обновление access-токена
- Password и Implicit — **deprecated**

### 25.3. Как работает Resource Server (Bearer Token)?

```java
@Configuration
@EnableWebSecurity
public class ResourceServerConfig {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .oauth2ResourceServer(oauth2 -> oauth2
                .jwt(jwt -> jwt.jwtAuthenticationConverter(jwtAuthenticationConverter()))
            );
        return http.build();
    }
}
```

`JwtAuthenticationProvider` декодирует JWT → `JwtDecoder` проверяет подпись → `JwtAuthenticationConverter` извлекает authorities → создаётся `JwtAuthenticationToken`.

### 25.4. JwtDecoder и JwtEncoder

- **JwtDecoder**: проверяет подпись и декодирует JWT. `NimbusJwtDecoder.withJwkSetUri(...)`.
- **JwtEncoder**: создаёт и подписывает JWT. `NimbusJwtEncoder`.

---

## 26. Spring Data JPA — репозитории

### 26.1. Как Spring Data JPA создаёт прокси для репозиториев?

1. Spring Data сканирует интерфейсы, расширяющие `Repository`
2. Для каждого создаётся `JpaRepositoryFactoryBean`
3. Фабрика создаёт JDK Dynamic Proxy (`JdkDynamicAopProxy`)
4. Прокси перехватывает вызовы и делегирует:
   - Если метод кастомный → `QueryExecutorMethodInterceptor` (парсинг имени метода)
   - Если стандартный CRUD → `SimpleJpaRepository`

### 26.2. Как работает PartTree (парсинг имени метода)?

`PartTree` разбирает имя метода на части запроса:
- `findByNameAndAge` → `WHERE name = ?1 AND age = ?2`
- `findByNameOrAge` → `WHERE name = ?1 OR age = ?2`
- `findByNameLike` → `WHERE name LIKE ?1`
- `findByAgeBetween` → `WHERE age BETWEEN ?1 AND ?2`
- `findByOrders_ProductName` → JOIN + условие

### 26.3. QueryLookupStrategy

Определяет стратегию поиска запроса:
- `CREATE` — из имени метода
- `USE_DECLARED_QUERY` — из `@Query` / `@NamedQuery`
- `CREATE_IF_NOT_FOUND` (по умолчанию) — сначала `@Query`, потом из имени

### 26.4. Иерархия репозиториев

- `Repository<T, ID>` — маркерный интерфейс
- `CrudRepository<T, ID>` — CRUD-операции
- `PagingAndSortingRepository<T, ID>` — пагинация и сортировка
- `JpaRepository<T, ID>` — JPA-специфичные методы (flush, deleteAllInBatch, getReferenceById)

### 26.5. @Query — JPQL и нативный SQL

```java
// JPQL
@Query("SELECT u FROM User u WHERE u.email = :email")
User findByEmail(@Param("email") String email);

// Нативный SQL
@Query(value = "SELECT * FROM users WHERE status = ?1", nativeQuery = true)
List<User> findByStatus(String status);

// UPDATE/DELETE требуют @Modifying
@Modifying
@Query("UPDATE User u SET u.status = :status WHERE u.id = :id")
int updateStatus(@Param("id") Long id, @Param("status") String status);

// SpEL для имени сущности
@Query("SELECT u FROM #{#entityName} u WHERE u.email = :email")
User findByEmail(@Param("email") String email);
```

### 26.6. @NoRepositoryBean и @EnableJpaRepositories

- **@NoRepositoryBean**: Spring Data не создаёт прокси для этого промежуточного интерфейса. Используется для базовых репозиториев.
- **@EnableJpaRepositories**: включает сканирование репозиториев с параметрами `basePackages`, `entityManagerFactoryRef`, `transactionManagerRef`.

### 26.7. Как работает аудит (@CreatedDate, @LastModifiedDate)?

Включается через `@EnableJpaAuditing`:
- `@CreatedDate` / `@LastModifiedDate` — автоматическое заполнение дат
- `@CreatedBy` / `@LastModifiedBy` — пользователь через `AuditorAware`
- `@EntityListeners(AuditingEntityListener.class)` — подключает слушатель к сущности

---

## 27. Spring Data JPA — запросы и оптимизация

### 27.1. Как работает Specification (Criteria API)?

Для динамических запросов:

```java
public interface UserRepo extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {}

Specification<User> spec = (root, query, cb) -> cb.and(
    cb.equal(root.get("status"), "ACTIVE"),
    cb.like(root.get("name"), "%John%")
);
List<User> users = repo.findAll(spec);
```

### 27.2. Как работает ExampleMatcher (Query by Example)?

Поиск по образцу:

```java
User probe = new User();
probe.setStatus("ACTIVE");
ExampleMatcher matcher = ExampleMatcher.matching()
    .withIgnoreCase()
    .withStringMatcher(StringMatcher.CONTAINING);
List<User> users = repo.findAll(Example.of(probe, matcher));
```

### 27.3. @EntityGraph — решение N+1 в Spring Data JPA

```java
// Ad-hoc EntityGraph
@EntityGraph(attributePaths = {"orders", "profile"})
Optional<User> findById(Long id);

// Named EntityGraph
@EntityGraph("User.orders")
@Query("SELECT u FROM User u WHERE u.id = :id")
Optional<User> findByIdWithOrders(@Param("id") Long id);
```

Типы: `LOAD` — указанные атрибуты EAGER, остальные по умолчанию; `FETCH` — только указанные EAGER, остальные LAZY.

### 27.4. Другие стратегии решения N+1

- `JOIN FETCH` в JPQL/criteria
- Hibernate `@BatchSize` на коллекциях
- Hibernate `@Fetch(FetchMode.SUBSELECT)`

### 27.5. @Procedure — вызов хранимых процедур

```java
@Procedure("GET_USER_COUNT")
int getUserCount();

@Procedure(procedureName = "CALC_BONUS", outputParameterName = "result")
BigDecimal calculateBonus(@Param("emp_id") Long empId);
```

---

## 28. Spring Data — NoSQL

### 28.1. Spring Data MongoDB

`MongoRepository<T, ID>` — аналогичен JPA, но для MongoDB. Поддерживает:
- `@Document`, `@Id`, `@Field` — маппинг на коллекции
- `@Query` в JSON-синтаксисе MongoDB
- `MongoTemplate` — программный доступ
- Транзакции (MongoDB 4.0+, replica set) через `MongoTransactionManager`

### 28.2. Spring Data Redis

`RedisTemplate` и репозитории через `@RedisHash`. Поддерживает:
- `RedisTemplate.opsForValue/Hash/List/Set/ZSet`
- `@RedisHash` для маппинга объектов на хэши
- Транзакции через `MULTI/EXEC` (`RedisTransactionManager`)
- Pub/Sub messaging, кэширование, блокировки

### 28.3. Spring Data Elasticsearch

`ElasticsearchRepository` поверх `ElasticsearchOperations` (RestHighLevelClient / новый ElasticsearchClient). Поддерживает:
- `@Document(indexName = "...")`, `@Field`
- `NativeSearchQuery` / `CriteriaQuery`
- Агрегации, suggest, highlighting
- Транзакции **не поддерживаются**

### 28.4. Spring Data Cassandra

`CassandraRepository` — `@Table`, `@PrimaryKey`, `@Column`. `CassandraTemplate` для CQL. Поддерживает легковесные транзакции (LWT) через `IF`-условия.

### 28.5. Spring Data R2DBC

Реактивный доступ к реляционным БД. `R2dbcRepository`, `DatabaseClient`. Транзакции через `R2dbcTransactionManager`. **Не JPA** — нет ленивой загрузки, кэша, dirty checking.

---

## 29. Кэширование в Spring (@Cacheable)

### 29.1. Как работает @Cacheable, @CacheEvict, @CachePut?

Аннотации обрабатываются `CacheInterceptor` (аналог `TransactionInterceptor`):
- **@Cacheable**: перед вызовом метода проверяет кэш → если есть — возвращает из кэша (метод не вызывается), если нет — вызывает и сохраняет результат
- **@CachePut**: всегда вызывает метод и обновляет кэш (не проверяет наличие)
- **@CacheEvict**: удаляет из кэша. `allEntries = true` — очистить весь кэш. `beforeInvocation = true` — удалить до вызова метода (даже при исключении)

### 29.2. CacheManager и провайдеры

`CacheManager` управляет коллекцией `Cache`. Реализации:
- `ConcurrentMapCacheManager` — в памяти (dev/тесты)
- `RedisCacheManager` — Redis
- `CaffeineCacheManager` — Caffeine (высокопроизводительный in-memory)
- `EhCacheCacheManager` — EhCache
- `HazelcastCacheManager` — Hazelcast (распределённый)

### 29.3. Как работает кэширование на уровне аннотаций?

`@EnableCaching` импортирует `CachingConfigurationSelector` → регистрирует `CacheInterceptor` и `CacheAnnotationBeanPostProcessor`. Кэш работает через AOP-прокси — те же ограничения что и `@Transactional` (self-invocation не работает).

---

## 30. Асинхронность (@Async, @Scheduled)

### 30.1. Как работает @Async?

`@EnableAsync` регистрирует `AsyncAnnotationBeanPostProcessor`. Метод с `@Async` выполняется в отдельном потоке из `TaskExecutor`. Возвращаемые типы:
- `void` — fire-and-forget
- `Future<T>` — блокирующий результат
- `CompletableFuture<T>` — рекомендуется, неблокирующая композиция

Ограничения: self-invocation не работает, метод должен быть public, не может быть `private` (прокси).

### 30.2. TaskExecutor — конфигурация

Реализации:
- `SimpleAsyncTaskExecutor` — новый поток на каждую задачу (не для production)
- `ThreadPoolTaskExecutor` — пул потоков, рекомендуется
- `ConcurrentTaskExecutor` — обёртка над `java.util.concurrent.Executor`

Типовые настройки: `corePoolSize`, `maxPoolSize`, `queueCapacity`, `RejectedExecutionHandler`.

### 30.3. Как работает @Scheduled?

`@EnableScheduling` регистрирует `ScheduledAnnotationBeanPostProcessor`. Параметры:
- `fixedRate` — интервал между началами выполнений
- `fixedDelay` — интервал между окончанием и следующим началом
- `cron` — cron-выражение
- `initialDelay` — задержка перед первым запуском

Можно настроить пул потоков планировщика: `spring.task.scheduling.pool.size=N`.

### 30.4. Как передать SecurityContext в @Async?

- `SecurityContextHolder.setStrategyName(MODE_INHERITABLETHREADLOCAL)` — глобально
- `DelegatingSecurityContextAsyncTaskExecutor` — обёртка над TaskExecutor
- `DelegatingSecurityContextRunnable` / `DelegatingSecurityContextCallable`

### 30.5. Как работает @Retryable (Spring Retry)?

Аннотация для автоматических повторных попыток при transient-ошибках:

```java
@Retryable(
    retryFor = {HttpServerErrorException.class, TimeoutException.class},
    maxAttempts = 3,
    backoff = @Backoff(delay = 1000, multiplier = 2.0)  // 1s → 2s → 4s
)
public String callExternalService() {
    return restTemplate.getForObject("http://api.example.com", String.class);
}

@Recover
public String fallback(HttpServerErrorException e) {
    return "Fallback data";
}
```

Требует `@EnableRetry` и `spring-retry` в зависимостях. Работает через AOP-прокси (аналогично `@Transactional`), поэтому self-invocation не работает.

**Основные параметры:**
- `retryFor` / `noRetryFor` — для каких исключений повторять
- `maxAttempts` — максимум попыток (включая первую)
- `backoff` — задержка между попытками (fixed/exponential/random)
- `@Recover` — метод fallback после исчерпания попыток

---

## 31. Spring Events

### 31.1. Как работает механизм событий в Spring?

Spring предоставляет встроенный event-driven механизм на основе `ApplicationEventPublisher`:

```java
// Публикация
@Autowired private ApplicationEventPublisher publisher;
publisher.publishEvent(new UserCreatedEvent(user));

// Подписка
@EventListener
public void handleUserCreated(UserCreatedEvent event) {
    // обработка
}
```

Под капотом: `ApplicationEventMulticaster` (обычно `SimpleApplicationEventMulticaster`) рассылает события всем зарегистрированным слушателям.

### 31.2. @TransactionalEventListener

Привязывает обработку события к фазе транзакции:

```java
@TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT)
public void handleUserCreated(UserCreatedEvent event) {
    // выполнится только после успешного коммита
}
```

Фазы: `BEFORE_COMMIT`, `AFTER_COMMIT` (по умолчанию), `AFTER_ROLLBACK`, `AFTER_COMPLETION`.

### 31.3. Асинхронная обработка событий

```java
@Async
@EventListener
public void handleAsync(UserCreatedEvent event) { }

// Или через конфигурацию
@Bean
public ApplicationEventMulticaster applicationEventMulticaster() {
    SimpleApplicationEventMulticaster m = new SimpleApplicationEventMulticaster();
    m.setTaskExecutor(new SimpleAsyncTaskExecutor());
    return m;
}
```

---

## 32. Пул соединений (HikariCP)

### 32.1. Почему HikariCP и как он работает?

HikariCP — пул соединений по умолчанию в Spring Boot 2.x+. Выбран за максимальную производительность и минимальный overhead.

**Ключевые оптимизации:**
- Прямой доступ к `java.util.concurrent` структурам (без обёрток)
- `ConcurrentBag` — lock-free коллекция для хранения соединений
- Отказ от `ThreadLocal` и `synchronized` в пользу CAS
- Оптимизированное использование `PreparedStatement` кэша
- Быстрая валидация соединений

### 32.2. Основные параметры конфигурации

```properties
spring.datasource.hikari.connection-timeout=30000      # таймаут получения соединения
spring.datasource.hikari.maximum-pool-size=10          # макс. размер пула
spring.datasource.hikari.minimum-idle=10               # мин. простаивающих соединений
spring.datasource.hikari.idle-timeout=600000           # таймаут простоя
spring.datasource.hikari.max-lifetime=1800000          # макс. время жизни соединения
spring.datasource.hikari.leak-detection-threshold=2000 # детекция утечек (мс)
```

### 32.3. Как мониторить пул?

HikariCP предоставляет метрики через JMX и Micrometer:
- `hikaricp.connections.active` / `idle` / `pending`
- `hikaricp.connections.timeout` — счётчик таймаутов
- `hikaricp.connections.creation` / `acquire` / `usage` — тайминги

---

## 33. Тестирование Spring-приложений

### 33.1. @SpringBootTest

Загружает полный ApplicationContext. Используется для интеграционных тестов:
- `webEnvironment` — MOCK, RANDOM_PORT, DEFINED_PORT
- Можно указать конкретный класс конфигурации: `@SpringBootTest(classes = MyConfig.class)`
- Тяжёлый, запускается медленнее срезанных тестов

### 33.2. Срезанные тесты (Slice Tests)

- **@WebMvcTest**: только веб-слой (контроллеры). Не загружает сервисы/репозитории. Использует `MockMvc`.
- **@DataJpaTest**: только JPA-репозитории. Использует in-memory БД (H2) или TestContainers.
- **@JsonTest**: тестирование JSON-сериализации/десериализации.
- **@RestClientTest**: тестирование RestTemplate/WebClient.
- **@JdbcTest**: только JDBC-слой.

### 33.3. MockMvc

Тестирование веб-слоя без запуска сервера:

```java
@WebMvcTest(UserController.class)
class UserControllerTest {
    @Autowired private MockMvc mockMvc;
    @MockBean private UserService userService;

    @Test
    void getUser() throws Exception {
        when(userService.findById(1L)).thenReturn(new User(1L, "John"));
        mockMvc.perform(get("/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("John"));
    }
}
```

### 33.4. TestContainers

Интеграционное тестирование с реальными сервисами в Docker:

```java
@SpringBootTest
@Testcontainers
class UserRepositoryTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15");

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry reg) {
        reg.add("spring.datasource.url", postgres::getJdbcUrl);
        reg.add("spring.datasource.username", postgres::getUsername);
        reg.add("spring.datasource.password", postgres::getPassword);
    }
}
```

### 33.5. @MockBean vs @SpyBean

- **@MockBean**: заменяет существующий бин в контексте на Mockito-мок
- **@SpyBean**: частичный мок — оборачивает реальный бин, позволяя переопределять отдельные методы

---

## 34. Spring Batch

### 34.1. Архитектура Spring Batch

- **Job**: единица работы, состоит из последовательности Step-ов
- **Step**: фаза Job-а — chunk-oriented или tasklet
- **ItemReader / ItemProcessor / ItemWriter**: компоненты chunk-обработки
- **JobRepository**: хранит метаданные о выполнении в БД (статусы, счётчики)
- **JobLauncher**: запускает Job

### 34.2. Chunk-oriented processing

Читает порциями (chunk) и обрабатывает в транзакциях:

```java
@Bean
public Step step(JobRepository repo, PlatformTransactionManager tm) {
    return new StepBuilder("step", repo)
        .<User, User>chunk(10, tm)  // 10 записей за транзакцию
        .reader(reader)
        .processor(processor)
        .writer(writer)
        .faultTolerant()
        .skip(Exception.class)
        .skipLimit(100)
        .build();
}
```

### 34.3. Повторный запуск и восстановление

Spring Batch сохраняет состояние каждого Step-а в `JobRepository`. При падении и перезапуске — продолжает с последней успешной позиции в chunk-е.

---

## 35. Spring Integration

### 35.1. Что такое Spring Integration?

Фреймворк для интеграции приложений на основе паттернов Enterprise Integration Patterns (EIP). Строится на каналах (MessageChannel) и адаптерах.

**Компоненты:**
- **Message**: сообщение с payload и headers
- **Channel**: транспорт для сообщений (DirectChannel, QueueChannel, PublishSubscribeChannel)
- **Adapter**: подключение к внешним системам (JMS, FTP, HTTP, Kafka, ...)
- **Filter / Transformer / Router / Splitter / Aggregator**: компоненты преобразования

### 35.2. Как Spring Integration связан с Spring Boot?

Spring Boot предоставляет автоконфигурации для адаптеров (`spring-boot-starter-integration`). Интеграционные потоки можно описывать в Java DSL:

```java
@Bean
public IntegrationFlow fileReaderFlow() {
    return IntegrationFlow.from(Files.inboundAdapter(new File("/tmp/input")),
            spec -> spec.poller(Pollers.fixedDelay(1000)))
        .transform(Files.toStringTransformer())
        .handle(message -> System.out.println(message.getPayload()))
        .get();
}
```

---

## 36. Spring Cloud — микросервисы

### 36.1. Service Discovery (Netflix Eureka / Consul)

- **Eureka Server** (`@EnableEurekaServer`): реестр сервисов
- **Eureka Client**: регистрируется в Eureka, периодически шлёт heartbeat
- **Consul / Zookeeper**: альтернативы Eureka (Consul также предоставляет Key-Value хранилище и Health Checks)

### 36.2. Load Balancing (Spring Cloud LoadBalancer)

Замена устаревшего Netflix Ribbon. Интегрирован с `RestTemplate` / `WebClient`:

```java
@Bean
@LoadBalanced
public RestTemplate restTemplate() {
    return new RestTemplate();
}

// Вызов через имя сервиса
restTemplate.getForObject("http://user-service/users/1", User.class);
```

### 36.3. Circuit Breaker (Resilience4j)

Замена устаревшего Hystrix. Предотвращает каскадные отказы:

```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallback")
public User getUser(Long id) {
    return restTemplate.getForObject("http://user-service/users/" + id, User.class);
}

public User fallback(Long id, Exception e) {
    return new User(id, "Fallback User");
}
```

Состояния Circuit Breaker: **CLOSED** (норма) → **OPEN** (обрыв) → **HALF_OPEN** (проверка) → CLOSED/OPEN.

Также предоставляет: **Retry**, **RateLimiter**, **Bulkhead**, **TimeLimiter**.

### 36.4. OpenFeign

Декларативный HTTP-клиент:

```java
@FeignClient(name = "user-service")
public interface UserClient {
    @GetMapping("/users/{id}")
    User getUser(@PathVariable Long id);
}
```

Spring Cloud Feign автоматически создаёт реализацию интерфейса, интегрируется с Service Discovery и Load Balancer.

### 36.5. Circuit Breaker + OpenFeign

```java
@FeignClient(name = "user-service", fallbackFactory = UserClientFallbackFactory.class)
public interface UserClient {
    @GetMapping("/users/{id}")
    User getUser(@PathVariable Long id);
}
```

---

## 37. Spring Cloud — Config, Gateway, Tracing

### 37.1. Spring Cloud Config

Централизованное управление конфигурацией:
- **Config Server** (`@EnableConfigServer`): хранит конфигурации в Git/файловой системе/хранилище
- **Config Client**: запрашивает конфигурацию при старте
- **Refresh**: `/actuator/refresh` или Spring Cloud Bus для динамического обновления

### 37.2. Spring Cloud Gateway

API Gateway на реактивном стеке (WebFlux). Замена Netflix Zuul:

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: users
          uri: lb://user-service
          predicates:
            - Path=/api/users/**
          filters:
            - StripPrefix=1
            - name: CircuitBreaker
              args:
                name: userServiceCB
```

Фильтры: rate limiting, authentication, logging, request/response modification.

### 37.3. Distributed Tracing (Micrometer Tracing / Sleuth)

- Micrometer Tracing (замена Spring Cloud Sleuth в Boot 3.x) добавляет `traceId` и `spanId` в логи и заголовки (`X-Brave-Trace-Id`)
- Интегрируется с **Zipkin** или **Jaeger** для визуализации
- Автоматически распространяет контекст через HTTP/Messaging

---

## 38. Spring GraphQL

### 38.1. Как работает Spring GraphQL?

Spring for GraphQL предоставляет поддержку GraphQL API на основе `graphql-java`:

- **@Controller** с аннотациями:
  - `@QueryMapping` — запросы
  - `@MutationMapping` — мутации
  - `@SubscriptionMapping` — подписки
  - `@SchemaMapping(typeName = "User", field = "orders")` — резолверы связей
- Поддержка `@ExceptionHandler` для GraphQL-ошибок
- Интеграция с `@PreAuthorize` для безопасности

### 38.2. GraphQL vs REST

GraphQL позволяет клиенту запрашивать только нужные данные и связи за один запрос — решает over-fetching и under-fetching. Но сложнее в кэшировании и требует больше серверных ресурсов на резолвинг.

---

## 39. Spring — реактивное программирование (WebFlux, R2DBC)

### 39.1. Что такое WebFlux?

Реактивный веб-стек на основе Project Reactor:
- **Неблокирующий I/O** через Netty (по умолчанию) или Servlet 3.1+ контейнеры
- **Типы**: `Mono<T>` (0-1 элементов) и `Flux<T>` (0-N элементов)
- **Контроллеры** — как в MVC, но возвращают `Mono`/`Flux`
- **Router Functions** — функциональный стиль

### 39.2. Когда WebFlux, а когда Spring MVC?

**WebFlux**:
- Высоконагруженные streaming-приложения
- Реактивный стек (R2DBC, reactive Kafka, reactive Redis)
- Ограниченные ресурсы (меньше потоков)

**Spring MVC**:
- Типичные CRUD-приложения
- JDBC/блокирующие библиотеки
- Проще в отладке и понимании

### 39.3. R2DBC vs JDBC

R2DBC — реактивный драйвер для реляционных БД. Не является реактивным JDBC — это новый API. Нет JPA/Hibernate, нет ленивой загрузки, нет dirty checking. Вместо ORM — прямой маппинг.

### 39.4. Модель потоков WebFlux

Основан на event loop (как Node.js). Малое количество потоков (обычно = количество ядер CPU) обрабатывают множество соединений неблокирующим образом. Блокирующий вызов в WebFlux-приложении может заблокировать весь event loop.

---

## 40. Spring — интеграция с Kafka / RabbitMQ

### 40.1. Spring Kafka

- **KafkaTemplate**: отправка сообщений
- **@KafkaListener**: приём сообщений (concurrency, batch-режим)
- **KafkaTransactionManager**: транзакции ровно-один-раз (exactly-once semantics)
- **ConsumerFactory / ProducerFactory**: конфигурация

```java
@KafkaListener(topics = "orders", groupId = "order-group")
public void listen(Order order) {
    process(order);
}
```

### 40.2. Spring AMQP (RabbitMQ)

- **RabbitTemplate**: отправка и приём
- **@RabbitListener**: асинхронный приём
- Поддержка: подтверждений (ack/nack), повторных попыток (retry), dead-letter exchange
- `RabbitTransactionManager` для транзакционной отправки

```java
@RabbitListener(queues = "orders.queue")
public void process(Order order) {
    // обработка
}
```

### 40.3. Kafka vs RabbitMQ

| Характеристика | Kafka | RabbitMQ |
|---|---|---|
| Модель | Pull-based (consumer polls) | Push-based (broker pushes) |
| Хранение | Долговременное (log-based, replay) | Кратковременное (после ack удаляется) |
| Производительность | Выше (миллионы msg/s) | Ниже (десятки тысяч msg/s) |
| Маршрутизация | Ограниченная (топики + партиции) | Гибкая (exchanges + routing keys) |
| Основной кейс | Потоковая обработка, event sourcing | Сервисная интеграция, RPC |

---

## 41. Spring — gRPC, Kotlin Coroutines

### 41.1. Spring gRPC

Spring предоставляет `@GrpcService` для создания gRPC-сервисов. gRPC использует Protocol Buffers для сериализации и HTTP/2 для транспорта.

```java
@GrpcService
public class UserServiceImpl extends UserServiceGrpc.UserServiceImplBase {
    @Override
    public void getUser(GetUserRequest req, StreamObserver<User> response) {
        // реализация
    }
}
```

### 41.2. Kotlin Coroutines в Spring

Spring поддерживает корутины Kotlin нативно в WebFlux:
- `suspend` функции в контроллерах
- `Flow<T>` для реактивных потоков
- `@Transactional` работает с корутинами через `CoroutineCrudRepository`

```kotlin
@RestController
class UserController(val repo: UserRepository) {
    @GetMapping("/{id}")
    suspend fun getUser(@PathVariable id: Long): User = repo.findById(id) ?: throw NotFoundException()
}
```

---

## 42. Spring Boot 3 — миграция и изменения

### 42.1. Основные изменения в Spring Boot 3

- **Java 17 baseline**: минимальная версия Java — 17 (вместо Java 8/11)
- **Jakarta EE 9+**: пакеты `javax.*` → `jakarta.*` (самое болезненное изменение)
- **Spring Security 6**: удалён `WebSecurityConfigurerAdapter`, `@EnableGlobalMethodSecurity` → `@EnableMethodSecurity`
- **Observability**: Micrometer Tracing (замена Spring Cloud Sleuth)
- **AOT и Native**: поддержка GraalVM Native Image из коробки
- **ProblemDetail**: встроенная поддержка RFC 7807 для ошибок
- **HTTP Interface**: декларативные HTTP-клиенты через `@HttpExchange`
- **Virtual Threads**: поддержка виртуальных потоков Java 21+ для `@Async` и WebMVC

### 42.2. Как мигрировать с Spring Boot 2 на Spring Boot 3?

1. **Обновить Java до 17+**
2. **Заменить javax → jakarta**: `javax.persistence` → `jakarta.persistence`, `javax.servlet` → `jakarta.servlet`, `javax.validation` → `jakarta.validation` и т.д.
3. **Обновить Spring Security**: заменить `WebSecurityConfigurerAdapter` на `SecurityFilterChain` бин, `@EnableGlobalMethodSecurity` → `@EnableMethodSecurity`
4. **Обновить Hibernate**: версия 6.x, изменения в API (именование Sequence, UUID-генерация, `hibernate.id.new_generator_mappings=true` по умолчанию)
5. **Переименовать properties**: многие `spring.flyway.*` / `spring.liquibase.*` свойства изменились
6. **Actuator endpoints**: `/actuator/health` теперь требует авторизации по умолчанию (если есть Spring Security)
7. **Проверить Deprecated API**: `RestTemplate` в режиме ожидания замены на `WebClient` / `RestClient`

---

## 43. Разное (SpEL, @Value, @Lookup, RestTemplate vs WebClient)

### 43.1. Что такое SpEL (Spring Expression Language)?

Язык выражений для Spring. Используется в:
- `@Value("#{systemProperties['user.region']}")` — динамические значения
- `@PreAuthorize("hasRole('ADMIN') and #user.id == authentication.principal.id")` — security
- `@Query("SELECT u FROM #{#entityName} u")` — в JPQL
- XML/Java конфигурации

### 43.2. Как работает @Value?

Внедряет значения из properties или SpEL-выражений:
- `@Value("${server.port}")` — из properties
- `@Value("#{2 * T(java.lang.Math).PI}")` — SpEL
- Обрабатывается `AutowiredAnnotationBeanPostProcessor` (тот же BPP что и `@Autowired`)

### 43.3. Как работает @EventListener?

Альтернатива реализации `ApplicationListener` интерфейса:

```java
@EventListener
public void handleContextStart(ContextRefreshedEvent event) { }

@EventListener(condition = "#event.user.age > 18")
public void handleAdult(UserCreatedEvent event) { }
```

Spring сам определит тип события по параметру метода. Поддерживает не-void возврат (публикация нового события), `@Async`, `@Order`.

### 43.4. Как работает @AliasFor?

Позволяет атрибутам аннотаций быть синонимами:
- Внутри аннотации: `value` и `path` эквивалентны
- Мета-аннотации: проброс атрибутов из составной аннотации в компоненты

**Пример**: `@SpringBootApplication` через `@AliasFor` пробрасывает `scanBasePackages` в `@ComponentScan`.

### 43.5. RestTemplate vs WebClient — что выбрать?

| Характеристика | RestTemplate | WebClient |
|---|---|---|
| Стек | Servlet (блокирующий) | Reactive (неблокирующий) |
| Статус | В режиме поддержки (maintenance mode) | Рекомендуется для нового кода |
| Асинхронность | Нет (только sync) | Да (async, reactive) |
| Streaming | Нет | Да (Flux<DataBuffer>) |
| Интеграция | Service Discovery, LoadBalancer | Service Discovery, LoadBalancer, Reactive |

В Spring Boot 3.x также доступен **RestClient** — новый синхронный HTTP-клиент с fluent API (замена RestTemplate для sync-сценариев).

```java
// RestClient (Spring 6.1+)
RestClient client = RestClient.create();
User user = client.get()
    .uri("http://user-service/users/{id}", 1L)
    .retrieve()
    .body(User.class);
```

### 43.6. Как оптимизировать старт Spring Boot приложения?

1. `spring.main.lazy-initialization=true` — ленивая инициализация всех бинов
2. Исключение ненужных автоконфигураций
3. Spring AOT + GraalVM Native Image
4. Отключение ненужных endpoint-ов Actuator
5. Class Data Sharing (CDS) в JVM
6. Отключение JMX: `spring.jmx.enabled=false`
7. Отключение DevTools в production
8. Использование Virtual Threads (Java 21+) для I/O-bound задач
