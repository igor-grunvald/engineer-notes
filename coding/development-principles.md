# Принципы и паттерны разработки программного обеспечения

## Оглавление

### Введение

1. [Введение](#введение)
   - [О документе](#о-документе)
   - [Почему принципы важны](#почему-принципы-важны)
   - [Как читать этот документ](#как-читать-этот-документ)

### Базовые принципы проектирования

2. [KISS — Keep It Simple, Stupid](#kiss--keep-it-simple-stupid)
   - [Суть принципа](#суть-принципа-kiss)
   - [Почему простота — это сложно](#почему-простота--это-сложно)
   - [Признаки нарушения KISS](#признаки-нарушения-kiss)
   - [Примеры на Java](#примеры-на-java-kiss)
   - [KISS и рефакторинг](#kiss-и-рефакторинг)
3. [DRY — Don't Repeat Yourself](#dry--dont-repeat-yourself)
   - [Суть принципа](#суть-принципа-dry)
   - [DRY vs дублирование знаний vs дублирование кода](#dry-vs-дублирование-знаний-vs-дублирование-кода)
   - [Признаки нарушения DRY](#признаки-нарушения-dry)
   - [Примеры на Java](#примеры-на-java-dry)
   - [Опасность «WET»-кода](#опасность-wet-кода)
   - [Ловушки DRY: когда не стоит объединять](#ловушки-dry-когда-не-стоит-объединять)
4. [YAGNI — You Ain't Gonna Need It](#yagni--you-aint-gonna-need-it)
   - [Суть принципа](#суть-принципа-yagni)
   - [YAGNI и овер-инжиниринг](#yagni-и-овер-инжиниринг)
   - [Признаки нарушения YAGNI](#признаки-нарушения-yagni)
   - [Примеры на Java](#примеры-на-java-yagni)
   - [Границы YAGNI: когда предусмотрительность оправдана](#границы-yagni-когда-предусмотрительность-оправдана)
5. [BDUF — Big Design Up Front](#bduf--big-design-up-front)
   - [Суть принципа](#суть-принципа-bduf)
   - [BDUF vs Agile-подход](#bduf-vs-agile-подход)
   - [Когда BDUF оправдан](#когда-bduf-оправдан)
   - [Примеры из практики](#примеры-из-практики-bduf)
   - [Золотая середина: Enough Design Up Front](#золотая-середина-enough-design-up-front)

### Принципы организации кода

6. [SoC — Separation of Concerns](#soc--separation-of-concerns)
   - [Суть принципа](#суть-принципа-soc)
   - [Уровни разделения ответственности](#уровни-разделения-ответственности)
   - [Примеры на Java](#примеры-на-java-soc)
   - [SoC и архитектурные стили](#soc-и-архитектурные-стили)
7. [Law of Demeter — Закон Деметры](#law-of-demeter--закон-деметры)
   - [Суть принципа](#суть-принципа-lod)
   - [Правило одной точки](#правило-одной-точки)
   - [Примеры на Java](#примеры-на-java-lod)
   - [Train Wreck — антипаттерн](#train-wreck--антипаттерн)
   - [Исключения из закона Деметры](#исключения-из-закона-деметры)
8. [Composition over Inheritance](#composition-over-inheritance)
   - [Суть принципа](#суть-принципа-coi)
   - [Проблемы наследования](#проблемы-наследования)
   - [Примеры на Java](#примеры-на-java-coi)
   - [Паттерны на основе композиции](#паттерны-на-основе-композиции)
9. [TDA — Tell, Don't Ask](#tda--tell-dont-ask)
   - [Суть принципа](#суть-принципа-tda)
   - [Процедурный vs объектный стиль](#процедурный-vs-объектный-стиль)
   - [Примеры на Java](#примеры-на-java-tda)
   - [Связь с инкапсуляцией](#связь-с-инкапсуляцией)
10. [Encapsulate What Varies](#encapsulate-what-varies)
    - [Суть принципа](#суть-принципа-ewv)
    - [Техники инкапсуляции изменений](#техники-инкапсуляции-изменений)
    - [Примеры на Java](#примеры-на-java-ewv)
11. [Program to Interface, Not Implementation](#program-to-interface-not-implementation)
    - [Суть принципа](#суть-принципа-pini)
    - [Интерфейс как контракт](#интерфейс-как-контракт)
    - [Примеры на Java](#примеры-на-java-pini)
    - [Связь с DIP из SOLID](#связь-с-dip-из-solid)
12. [Fail Fast](#fail-fast)
    - [Суть принципа](#суть-принципа-ff)
    - [Fail Fast vs Fail Safe](#fail-fast-vs-fail-safe)
    - [Примеры на Java](#примеры-на-java-ff)
    - [Fail Fast на разных уровнях системы](#fail-fast-на-разных-уровнях-системы)
13. [Convention over Configuration](#convention-over-configuration)
    - [Суть принципа](#суть-принципа-coc)
    - [Примеры из экосистемы Java](#примеры-из-экосистемы-java-coc)
    - [Плюсы и минусы](#плюсы-и-минусы-coc)
14. [Single Source of Truth](#single-source-of-truth)
    - [Суть принципа](#суть-принципа-ssot)
    - [SSOT vs децентрализация](#ssot-vs-децентрализация)
    - [Примеры на Java](#примеры-на-java-ssot)
15. [Robustness Principle — Postel's Law](#robustness-principle--postels-law)
    - [Суть принципа](#суть-принципа-pol)
    - [Почему это работает](#почему-это-работает)
    - [Примеры на Java](#примеры-на-java-pol)
    - [Границы применимости](#границы-применимости)

### Принципы управления сложностью

16. [Occam's Razor — Бритва Оккама](#occams-razor--бритва-оккама)
    - [Суть принципа](#суть-принципа-or)
    - [Применение в разработке](#применение-в-разработке)
    - [Примеры](#примеры-or)
17. [Worse is Better](#worse-is-better)
    - [Суть принципа](#суть-принципа-wib)
    - [The MIT Approach vs The New Jersey Approach](#the-mit-approach-vs-the-new-jersey-approach)
    - [Влияние на индустрию](#влияние-на-индустрию)
18. [Gall's Law — Закон Голла](#galls-law--закон-голла)
    - [Суть принципа](#суть-принципа-gl)
    - [Почему это фундаментально](#почему-это-фундаментально)
    - [Примеры из индустрии](#примеры-из-индустрии-gl)
    - [Примеры на Java](#примеры-на-java-gl)
19. [Pareto Principle — Принцип Парето (80/20)](#pareto-principle--принцип-парето-8020)
    - [Суть принципа](#суть-принципа-pp)
    - [Применение 80/20 в разработке](#применение-8020-в-разработке)
20. [Rule of Three — Правило трёх](#rule-of-three--правило-трёх)
    - [Суть принципа](#суть-принципа-rot)
    - [Дублирование vs абстракция](#дублирование-vs-абстракция)
    - [Примеры](#примеры-rot)
21. [The Law of Leaky Abstractions — Закон дырявых абстракций](#the-law-of-leaky-abstractions--закон-дырявых-абстракций)
    - [Суть принципа](#суть-принципа-lola)
    - [Суть проблемы](#суть-проблемы)
    - [Примеры утечек абстракций](#примеры-утечек-абстракций)
    - [Примеры на Java](#примеры-на-java-lola)
    - [Следствия для разработчика](#следствия-для-разработчика)

### Командные и процессные принципы

22. [Boy Scout Rule](#boy-scout-rule)
    - [Суть принципа](#суть-принципа-bsr)
    - [Практическое применение](#практическое-применение-bsr)
23. [Broken Windows Theory — Теория разбитых окон](#broken-windows-theory--теория-разбитых-окон)
    - [Суть принципа](#суть-принципа-bwt)
    - [Примеры проявления в кодовой базе](#примеры-проявления-в-кодовой-базе)
    - [Как бороться с разбитыми окнами](#как-бороться-с-разбитыми-окнами)
    - [Связь с другими принципами](#связь-с-другими-принципами-broken-windows)
24. [Brooks' Law — Закон Брукса](#brooks-law--закон-брукса)
    - [Суть принципа](#суть-принципа-bl)
    - [Мифический человеко-месяц](#мифический-человеко-месяц)
    - [Следствия для управления проектами](#следствия-для-управления-проектами)
25. [Conway's Law — Закон Конвея](#conways-law--закон-конвея)
    - [Суть принципа](#суть-принципа-cl)
    - [Обратный закон Конвея](#обратный-закон-конвея)
    - [Влияние на микросервисную архитектуру](#влияние-на-микросервисную-архитектуру)
26. [Parkinson's Law — Закон Паркинсона](#parkinsons-law--закон-паркинсона)
    - [Суть принципа](#суть-принципа-pl)
    - [Применение в разработке](#применение-в-разработке-pl)
27. [Principle of Least Privilege](#principle-of-least-privilege)
    - [Суть принципа](#суть-принципа-polp)
    - [Применение в архитектуре безопасности](#применение-в-архитектуре-безопасности)
28. [Principle of Least Astonishment](#principle-of-least-astonishment)
    - [Суть принципа](#суть-принципа-pola)
    - [Примеры нарушения](#примеры-нарушения-pola)
    - [Рекомендации](#рекомендации-pola)

### CQS, IoC и Design by Contract

29. [CQS — Command Query Separation](#cqs--command-query-separation)
    - [Суть принципа](#суть-принципа-cqs)
    - [CQS vs CQRS](#cqs-vs-cqrs)
    - [Примеры на Java](#примеры-на-java-cqs)
    - [Связь с функциональным программированием](#связь-с-функциональным-программированием)
30. [IoC — Inversion of Control](#ioc--inversion-of-control)
    - [Суть принципа](#суть-принципа-ioc)
    - [Hollywood Principle](#hollywood-principle)
    - [IoC-контейнеры](#ioc-контейнеры)
    - [Примеры на Java](#примеры-на-java-ioc)
    - [IoC и Dependency Injection](#ioc-и-dependency-injection)
31. [Design by Contract — Проектирование по контракту](#design-by-contract--проектирование-по-контракту)
    - [Суть принципа](#суть-принципа-dbc)
    - [Три столпа контракта](#три-столпа-контракта)
    - [Связь с другими принципами](#связь-с-другими-принципами-dbc)
    - [Примеры на Java](#примеры-на-java-dbc)
    - [DbC на практике](#dbc-на-практике)

### GRASP-паттерны

32. [GRASP — General Responsibility Assignment Software Patterns](#grasp--general-responsibility-assignment-software-patterns)
    - [Обзор GRASP](#обзор-grasp)
    - [Information Expert](#information-expert)
    - [Creator](#creator)
    - [Controller](#controller)
    - [Low Coupling](#low-coupling)
    - [High Cohesion](#high-cohesion)
    - [Polymorphism](#polymorphism)
    - [Pure Fabrication](#pure-fabrication)
    - [Indirection](#indirection)
    - [Protected Variations](#protected-variations)

### Двенадцатифакторное приложение

33. [The Twelve-Factor App](#the-twelve-factor-app)
    - [Обзор методологии](#обзор-методологии)
    - [12 факторов](#12-факторов)
    - [Ключевые факторы с Java-примерами](#ключевые-факторы-с-java-примерами)
    - [Применимость за пределами Heroku](#применимость-за-пределами-heroku)

### Принципы тестирования

34. [Принципы тестирования](#принципы-тестирования)
    - [TDD — Test-Driven Development](#tdd--test-driven-development-разработка-через-тестирование)
    - [F.I.R.S.T. — Принципы хороших тестов](#first--принципы-хороших-тестов)
    - [Test Pyramid — Пирамида тестирования](#test-pyramid--пирамида-тестирования)
    - [Testing Trophy (Кент Доддс)](#testing-trophy-кент-доддс)

### Заключение

35. [Взаимосвязь принципов](#взаимосвязь-принципов)
36. [Антипаттерны и типичные ошибки](#антипаттерны-и-типичные-ошибки)
37. [Рекомендуемая литература](#рекомендуемая-литература)

---

## Введение

### О документе

Данный документ представляет собой исчерпывающий справочник по ключевым принципам, законам и паттернам разработки программного обеспечения — помимо SOLID (вынесен в отдельный файл), GoF-паттернов (вынесены в отдельный файл) и архитектурных паттернов (вынесены в отдельный файл).

Материал охватывает:

- **Принципы проектирования кода** — KISS, DRY, YAGNI, Composition over Inheritance, TDA, Postel's Law и др.
- **Принципы управления сложностью** — Occam's Razor, Worse is Better, Gall's Law, Pareto Principle, Rule of Three, Law of Leaky Abstractions.
- **Командные и процессные принципы** — Boy Scout Rule, Broken Windows Theory, законы Брукса, Конвея, Паркинсона.
- **Принципы распределения ответственности** — GRASP-паттерны, SoC, Law of Demeter.
- **Принципы тестирования** — TDD (Red-Green-Refactor), F.I.R.S.T., Test Pyramid.
- **Архитектурные ориентиры** — IoC, CQS/CQRS, Design by Contract, Twelve-Factor App.

Каждый принцип сопровождается примерами на **Java** (в силу специфики проекта), но сами идеи универсальны и применимы к любому языку программирования.

### Почему принципы важны

Принципы разработки — это не догмы, а **накопленный коллективный опыт**, сформулированный в виде кратких правил. Их соблюдение даёт:

- **Предсказуемость кодовой базы.** Разработчик, знакомый с принципами, быстрее читает незнакомый код.
- **Снижение стоимости изменений.** Код спроектирован так, что добавление фичи не ломает существующее поведение.
- **Упрощение онбординга.** Новичок, знающий DRY и KISS, уже «в контексте» команды.
- **Общий язык.** Фраза «здесь нарушен Law of Demeter» объясняет проблему за секунды, а не за минуты.
- **Меньше багов.** Fail Fast, Principle of Least Astonishment и SSOT предотвращают целые классы ошибок.

### Как читать этот документ

Материал организован по тематическим группам:

1. Начните с **базовых принципов проектирования** (KISS, DRY, YAGNI, BDUF) — это фундамент.
2. Перейдите к **принципам организации кода** — они отвечают на вопрос «как расположить код?». Включая Postel's Law для построения надёжных API.
3. Блок **управления сложностью** — философские и прагматические ориентиры: Occam's Razor, Worse is Better, Gall's Law, Pareto Principle, Rule of Three, Law of Leaky Abstractions.
4. **Командные и процессные принципы** — о людях и процессах: Boy Scout Rule, Broken Windows Theory, законы Брукса, Конвея, Паркинсона.
5. Разделы **CQS/IoC/Design by Contract**, **GRASP**, **Twelve-Factor App** — углублённые темы.
6. **Принципы тестирования** — TDD, F.I.R.S.T., Test Pyramid.
7. **Заключение** — взаимосвязь принципов, антипаттерны, литература.

Каждый раздел самодостаточен: можно читать выборочно, возвращаясь к оглавлению.

---

## KISS — Keep It Simple, Stupid

### Суть принципа KISS

> **Делай настолько просто, насколько возможно, но не проще.**

Принцип KISS сформулирован в 1960-х годах в авиастроении (инженер Келли Джонсон, Lockheed Skunk Works). В программировании он означает: из всех возможных решений выбирай то, которое проще для понимания, сопровождения и модификации.

**Простота ≠ примитивность.** Простое решение — то, которое решает задачу минимальным количеством движущихся частей, но не жертвует корректностью.

Две крайности, которых следует избегать:

| Крайность | Описание |
|-----------|----------|
| **Оверинжиниринг** | Слишком сложное решение для простой задачи. FactoryManagerStrategyBean для конвертации строки в число. |
| **Недодизайн** | Наивный подход, игнорирующий реальные требования. Парсинг JSON регулярными выражениями. |

### Почему простота — это сложно

Простота требует **дисциплины**. Разработчики склонны к усложнению по нескольким причинам:

- **Желание показать квалификацию.** Сложный код воспринимается как «умный».
- **Попытка предугадать будущее.** «А вдруг понадобится поддержка 50 валют?» (см. YAGNI).
- **Недостаток времени на рефакторинг.** Первое работающее решение не упрощают.
- **Эффект второй системы.** Второй проект всегда получается перегруженным — синдром, описанный Фредериком Бруксом.

Алан Кей: *«Simple things should be simple, complex things should be possible.»*

### Признаки нарушения KISS

- Код делает больше, чем описано в требованиях.
- Для понимания одного метода нужно прочитать 5 других классов.
- Разработчик говорит: «Это элегантное решение» — но никто, кроме него, не понимает как оно работает.
- Сложность растёт нелинейно с добавлением фич.
- На код-ревью коллеги просят объяснить, «что здесь происходит».

### Примеры на Java KISS

**Нарушение KISS — оверинжиниринг:**

```java
// ❌ Переусложнено: иерархия из 4 классов ради простой конвертации
interface StringConverter {
    String convert(String input);
}

abstract class AbstractStringConverter implements StringConverter {
    protected String preProcess(String input) {
        return input.trim();
    }
}

class UpperCaseConverter extends AbstractStringConverter {
    @Override
    public String convert(String input) {
        return preProcess(input).toUpperCase();
    }
}

class ConverterFactory {
    public static StringConverter createConverter(ConversionType type) {
        return switch (type) {
            case UPPER -> new UpperCaseConverter();
            // ...
        };
    }
}

// Использование:
String result = ConverterFactory
    .createConverter(ConversionType.UPPER)
    .convert("  hello  ");
```

```java
// ✅ KISS: ровно одна строка там, где она нужна
String result = "  hello  ".trim().toUpperCase();
```

**Нарушение KISS — неоправданная гибкость:**

```java
// ❌ Конфигурируемый парсер с поддержкой плагинов для двух полей JSON
@PluginCapable
@Configurable(prefix = "parser")
public class EnterpriseJsonParser {
    private final PluginRegistry pluginRegistry;
    private final ConfigService configService;

    public <T> T parse(String json, Class<T> targetClass, ParsingStrategy strategy) {
        // 200 строк кода...
    }
}

// Использование:
User user = enterpriseJsonParser.parse(json, User.class, ParsingStrategy.LENIENT);
```

```java
// ✅ KISS: стандартный ObjectMapper для задачи парсинга JSON
ObjectMapper mapper = new ObjectMapper();
User user = mapper.readValue(json, User.class);
```

**Соблюдение KISS — простой метод с понятным потоком выполнения:**

```java
// ✅ Понятный, линейный код без сюрпризов
public Optional<User> findActiveUserById(Long id) {
    if (id == null) {
        log.warn("Attempt to find user with null id");
        return Optional.empty();
    }
    return userRepository.findById(id)
        .filter(User::isActive);
}
```

### KISS и рефакторинг

KISS не означает «пиши как попало, потом перепишем». Правильный подход:

1. Напиши простейшее решение, которое проходит тесты.
2. Если код дублируется — примени DRY.
3. Если код стал сложнее требований — упрости.
4. Регулярно спрашивай себя: «Поймёт ли это мой коллега с первого прочтения?»

**Хороший KISS-рефакторинг:** замена вложенных `if-else` (5 уровней) на guard clauses + выделение метода.

---

## DRY — Don't Repeat Yourself

### Суть принципа DRY

> **Каждая единица знания должна иметь единственное, однозначное, авторитетное представление в системе.**

Принцип сформулирован Энди Хантом и Дейвом Томасом в книге «Программист-прагматик» (1999). Ключевое слово — **знание**, а не «код». DRY — не про то, чтобы убрать любое повторение символов. Это про то, чтобы бизнес-правило, алгоритм или константа были определены ровно в одном месте.

### DRY vs дублирование знаний vs дублирование кода

| Понятие | Описание | Пример |
|---------|----------|--------|
| **Дублирование знаний** | Одно и то же бизнес-правило описано в двух местах | Максимальная длина пароля = 64 задана и в `UserService`, и в `ValidationFilter` |
| **Дублирование кода** | Одинаковые последовательности инструкций | Два метода с идентичным телом в разных классах |
| **Случайное совпадение** | Два участка кода выглядят одинаково сейчас, но могут измениться по разным причинам | Метод `calculateTax()` и `calculateDiscount()` оба умножают на 0.2 |

DRY нацелен именно на **дублирование знаний**. Дублирование кода — лишь симптом.

### Признаки нарушения DRY

- Чтобы изменить одно правило, нужно править код в нескольких файлах/классах.
- При поиске константы по проекту находится 3+ одинаковых значения в разных пакетах.
- После копипасты метода вы забыли обновить одну из копий — и появился баг.
- Разработчики спорят, какая из двух реализаций одного и того же алгоритма «правильная».

### Примеры на Java DRY

**Дублирование знаний — бизнес-правило размазано по коду:**

```java
// ❌ Нарушение DRY: правило валидации email duplication
// Файл: UserController.java
if (email != null && !email.isBlank() && email.contains("@") && email.length() <= 255) {
    // ...
}

// Файл: RegistrationService.java
if (email != null && !email.isBlank() && email.contains("@") && email.length() <= 255) {
    // ...
}

// Файл: ProfileUpdateValidator.java
if (email != null && !email.isBlank() && email.contains("@") && email.length() <= 255) {
    // ...
}
```

```java
// ✅ Соблюдение DRY: правило определено в одном месте
public final class EmailValidator {
    private static final int MAX_EMAIL_LENGTH = 255;
    private static final Pattern EMAIL_PATTERN =
        Pattern.compile("^[A-Za-z0-9+_.-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}$");

    private EmailValidator() { }

    public static boolean isValid(String email) {
        return email != null
            && !email.isBlank()
            && email.length() <= MAX_EMAIL_LENGTH
            && EMAIL_PATTERN.matcher(email).matches();
    }
}

// Использование везде:
if (EmailValidator.isValid(email)) { /* ... */ }
```

**Дублирование алгоритмического знания:**

```java
// ❌ Два сервиса считают скидку по-разному для одного и того же правила
// OrderService.java
public BigDecimal applyDiscount(Order order) {
    if (order.getTotal().compareTo(new BigDecimal("1000")) > 0) {
        return order.getTotal().multiply(new BigDecimal("0.9")); // 10%
    }
    return order.getTotal();
}

// CartService.java — 5% вместо 10% (разработчик скопипастил и забыл исправить?)
public BigDecimal calculateCartDiscount(Cart cart) {
    if (cart.getTotal().compareTo(new BigDecimal("1000")) > 0) {
        return cart.getTotal().multiply(new BigDecimal("0.95"));
    }
    return cart.getTotal();
}
```

```java
// ✅ Единый источник истины для правила скидки
@Component
public class DiscountPolicy {
    private static final BigDecimal DISCOUNT_THRESHOLD = new BigDecimal("1000");
    private static final BigDecimal DISCOUNT_RATE = new BigDecimal("0.10");

    public BigDecimal applyDiscount(BigDecimal amount) {
        if (amount.compareTo(DISCOUNT_THRESHOLD) > 0) {
            return amount.multiply(BigDecimal.ONE.subtract(DISCOUNT_RATE));
        }
        return amount;
    }
}
```

**DRY через выделение общего кода:**

```java
// ❌ Дублирование логики чтения файла с обработкой ошибок
// FileUserReader.java
public List<User> readUsers(Path path) {
    try {
        String content = Files.readString(path);
        return parseUsers(content);
    } catch (NoSuchFileException e) {
        log.error("File not found: {}", path, e);
        throw new FileProcessingException("File not found", e);
    } catch (IOException e) {
        log.error("IO error reading: {}", path, e);
        throw new FileProcessingException("IO error", e);
    }
}

// FileProductReader.java — точно такая же обёртка ошибок
public List<Product> readProducts(Path path) {
    try {
        String content = Files.readString(path);
        return parseProducts(content);
    } catch (NoSuchFileException e) {
        log.error("File not found: {}", path, e);
        throw new FileProcessingException("File not found", e);
    } catch (IOException e) {
        log.error("IO error reading: {}", path, e);
        throw new FileProcessingException("IO error", e);
    }
}
```

```java
// ✅ DRY: общий метод чтения с обработкой ошибок
public class FileReader {
    public static <T> List<T> read(Path path, Function<String, List<T>> parser) {
        try {
            String content = Files.readString(path);
            return parser.apply(content);
        } catch (NoSuchFileException e) {
            log.error("File not found: {}", path, e);
            throw new FileProcessingException("File not found", e);
        } catch (IOException e) {
            log.error("IO error reading: {}", path, e);
            throw new FileProcessingException("IO error", e);
        }
    }
}

// Использование:
List<User> users = FileReader.read(userPath, this::parseUsers);
List<Product> products = FileReader.read(productPath, this::parseProducts);
```

### Опасность «WET»-кода

Акроним **WET** расшифровывается как:

- **W**rite **E**verything **T**wice (пиши всё дважды)
- **W**e **E**njoy **T**yping (нам нравится печатать)
- **W**aste **E**veryone's **T**ime (трата времени каждого)

WET-код — это код с высоким уровнем дублирования. Последствия:

- Исправление бага требует правок в N местах — какое-то забудут.
- Onboarding нового разработчика затруднён: какую из 4 реализаций считать канонической?
- Тесты пишутся на каждую копию отдельно — комбинаторный взрыв.

### Ловушки DRY: когда не стоит объединять

Не всякое повторение — нарушение DRY. Преждевременное объединение двух разных концепций создаёт **ложную общность** (false generality):

```java
// ❌ Анти-DRY: объединение разных сущностей, которые меняются по разным причинам
public class EntityUtils {
    public static String formatLabel(User user) {
        return user.getFirstName() + " " + user.getLastName();
    }

    public static String formatLabel(Product product) {
        return product.getBrand() + " - " + product.getModel();
    }

    public static String formatLabel(Order order) {
        return "Order #" + order.getId();
    }
}
// Три разных правила форматирования в одном классе — они не дублируют знание,
// они просто синтаксически похожи. Изменение формата для User не должно
// требовать правки класса, который также отвечает за Product и Order.
```

**Правило Sandi Metz** (из Practical Object-Oriented Design in Ruby):

> Если вы видите дублирование во второй раз — **пока не трогайте**. Если видите в третий раз — **рефакторите** (см. Rule of Three).

---

## YAGNI — You Ain't Gonna Need It

### Суть принципа YAGNI

> **Не добавляй функциональность, пока она тебе действительно не понадобится.**

YAGNI — один из ключевых принципов экстремального программирования (XP), сформулированный Роном Джеффрисом. Его суть: не реализуй фичи «на вырост», не пиши код «на всякий случай». Любая добавленная заранее функциональность имеет ненулевую стоимость:

- **Стоимость написания** — время разработчика.
- **Стоимость тестирования** — каждый if требует минимум 2 теста.
- **Стоимость поддержки** — код нужно читать, рефакторить, документировать.
- **Стоимость удаления** — удалять код труднее, чем не писать его.

По данным Standish Group (CHAOS Report), **~45%** функциональности никогда не используется, а ещё **~19%** — используется редко. Таким образом, до **64%** функциональности, добавленной «на будущее», не приносит реальной ценности. В некоторых исследованиях эта цифра доходит до 80%.

### YAGNI и овер-инжиниринг

YAGNI — главное лекарство от овер-инжиниринга. Типичный сценарий:

> Разработчик: «Давай сделаем абстрактный DataExporter с поддержкой CSV, XML, JSON, Parquet, Avro и Excel — вдруг понадобится?»
>
> Бизнес: «Нам нужен CSV. За последние 5 лет мы ни разу не экспортировали ни в чём другом.»

**Результат:** потрачено 2 недели, протестирован только CSV (остальные форматы «как-нибудь потом»), баги в неиспользуемых экспортёрах висят годами.

### Признаки нарушения YAGNI

- В коде есть параметры конфигурации с единственным значением, которое никогда не менялось.
- Метод принимает `Strategy` параметром, но в проекте существует ровно одна стратегия.
- Абстрактный класс имеет ровно одного наследника.
- Комментарии вида «на будущее», «пока не используется, но пригодится», «TODO: поддержать».
- Таблицы в БД с колонками, которые всегда `NULL`.

### Примеры на Java YAGNI

**«Универсальный» парсер на все случаи жизни:**

```java
// ❌ Нарушение YAGNI: парсер, который поддерживает форматы, не нужные бизнесу
public class UniversalDataParser {
    public <T> List<T> parse(String input, Format format, Class<T> targetClass,
                              Encoding encoding, Compression compression,
                              ValidationStrategy validation) {
        // 300 строк кода, 15 классов-помощников
        // Из всего этого реально используется только format=CSV, encoding=UTF-8
    }
}
```

```java
// ✅ YAGNI: пишем только то, что нужно прямо сейчас
public class CsvParser {
    public List<User> parseUsers(String csvContent) {
        return Arrays.stream(csvContent.split("\n"))
            .skip(1) // заголовок
            .map(this::lineToUser)
            .toList();
    }

    private User lineToUser(String line) {
        String[] fields = line.split(",");
        return new User(fields[0], fields[1], fields[2]);
    }
}
// Когда (и если!) потребуется XML — добавим XmlParser.
// Когда потребуется CSV для Product — сделаем CsvParser<T>.
```

**Абстракция с единственной реализацией:**

```java
// ❌ YAGNI: интерфейс + единственная реализация без причины
public interface GreetingService {
    String greet(String name);
}

@Service
public class GreetingServiceImpl implements GreetingService {
    @Override
    public String greet(String name) {
        return "Hello, " + name + "!";
    }
}
// Интерфейс не нужен, пока нет второй реализации или моков для тестов.
```

```java
// ✅ YAGNI: простой класс. Интерфейс появится, когда понадобится
@Service
public class GreetingService {
    public String greet(String name) {
        return "Hello, " + name + "!";
    }
}
```

**«Защита от дурака», которая не нужна:**

```java
// ❌ Проверка на null для параметра, который никогда не может быть null
public void processOrder(Order order) {
    if (order == null) {
        throw new IllegalArgumentException("Order cannot be null"); // никогда не случится
    }
    if (order.getItems() == null) {
        order.setItems(new ArrayList<>()); // скрывает баг вместо того, чтобы найти его
    }
    // ...
}
```

```java
// ✅ YAGNI + Fail Fast: если контракт метода говорит, что order не null —
//    используем Objects.requireNonNull для отлова багов, а не для «безопасности»
public void processOrder(Order order) {
    Objects.requireNonNull(order, "order must not be null");
    // Если getItems() вернул null — это баг в Order, пусть упадёт с NPE,
    // чтобы мы нашли и исправили причину
    for (Item item : order.getItems()) {
        // ...
    }
}
```

### Границы YAGNI: когда предусмотрительность оправдана

YAGNI не означает «никогда не думай о будущем». Существуют ситуации, когда разумная предусмотрительность окупается:

| Ситуация | Почему это оправдано |
|----------|---------------------|
| **API / публичный контракт** | Изменить сигнатуру публичного метода после релиза — breaking change. Продумать контракт заранее критически важно. |
| **Модель данных** | Миграция схемы БД на продакшене — дорого. Лучше продумать основные сущности сразу. |
| **Известное требование через 1-2 спринта** | Если Product Owner подтвердил, что фича X будет в следующем спринте, можно заложить точки расширения. |
| **Регуляторные требования** | Если через 3 месяца вступает в силу закон — готовьтесь сейчас. |
| **Горизонтальное масштабирование** | Stateless-сервис спроектировать с самого начала так же легко, как stateful, но переписывать stateful в stateless — огромные затраты. |

**Золотое правило:** предусмотрительность оправдана, если стоимость добавления гибкости сейчас **ниже**, чем стоимость рефакторинга потом, И потребность в гибкости подтверждена (а не hypothetична).

---

## BDUF — Big Design Up Front

### Суть принципа BDUF

> **BDUF — это практика создания полного, детального дизайна системы до начала написания кода.**

Термин получил негативную окраску с распространением Agile-методологий. BDUF — это подход, при котором архитекторы и аналитики неделями (или месяцами) проектируют систему «на бумаге»: UML-диаграммы, ER-диаграммы, документы с описанием каждого класса и метода — и только потом разработчики приступают к кодированию.

Проблема BDUF в том, что он исходит из **ошибочного предположения**, что все требования известны заранее и не изменятся.

### BDUF vs Agile-подход

| Аспект | BDUF | Agile / Эволюционный дизайн |
|--------|------|-----------------------------|
| **Когда принимаются решения** | Все — до первой строки кода | Распределены по времени, по мере необходимости |
| **Реакция на изменения** | Изменение требований = перепроектирование | Изменение требований = адаптация ближайшего инкремента |
| **Документация** | Многостраничные спецификации | Living documentation, тесты как документация |
| **Риски** | Система может не соответствовать реальным потребностям | Требуется дисциплина рефакторинга |
| **Примеры** | RUP, водопадная модель | Scrum, XP, Kanban |

### Когда BDUF оправдан

Полное отрицание любого проектирования «вверх по течению» (upfront design) — такая же крайность, как и BDUF. Ситуации, где значительное предварительное проектирование оправдано:

1. **High-integrity systems** — авионика, медицинское оборудование, системы жизнеобеспечения. Цена ошибки слишком высока.
2. **Проекты с фиксированной ценой** — заказчику нужен точный план и смета до начала работ.
3. **Кросс-системная интеграция** — когда несколько независимых команд должны согласовать API/контракты.
4. **Регуляторные требования** — сертификация требует документированного дизайна (например, FDA для медицинского ПО).
5. **Сложные алгоритмические задачи** — иногда нужно доказать корректность алгоритма до реализации.

### Примеры из практики BDUF

**Классический провал BDUF:** Проект FBI Virtual Case File (2000-2005). $170 млн потрачено, 0 работающего кода. Причина: 5 лет проектирования без итеративной обратной связи.

**Успех BDUF:** Разработка программного обеспечения для космических аппаратов NASA. Каждая строка кода проходит многоуровневую верификацию, потому что обновление по воздуху невозможно.

### Золотая середина: Enough Design Up Front

Современный подход — **EDUF (Enough Design Up Front)**: достаточно проектирования для снижения ключевых рисков, но не больше.

Практические рекомендации:

- **Инцепция (Inception)** — 1-2 недели на high-level архитектуру: основные компоненты, границы, ключевые технологические решения.
- **Just-in-time детализация** — детальный дизайн конкретного модуля откладывается до спринта, в котором он будет разрабатываться.
- **Архитектурные каньоны** (Architectural Runway) — закладывайте только те архитектурные элементы, которые понадобятся в ближайших 2-3 итерациях.
- **Spike-решения** — если решение неочевидно, сделайте технический spike (исследовательскую задачу) на 1-3 дня вместо месяцев проектирования.

---

## SoC — Separation of Concerns

### Суть принципа SoC

> **Разделяй программу на логические секции так, чтобы каждая секция отвечала за одну и только одну задачу (concern).**

Separation of Concerns — один из старейших принципов в программировании, сформулированный Эдсгером Дейкстрой в 1974 году в статье «On the role of scientific thought».

**Concern** (ответственность, задача, аспект) — это причина для изменения кода. Если у класса есть две причины для изменения, значит, у него две ответственности (concerns), и они должны быть разделены.

SoC — это **родительский принцип** для:
- **SRP** (Single Responsibility Principle) из SOLID — SoC на уровне классов.
- **Многоуровневой архитектуры** — SoC на уровне системы.
- **Модульности** — SoC на уровне пакетов/модулей.

### Уровни разделения ответственности

| Уровень | Пример разделения |
|---------|-------------------|
| **Системный** | Frontend / Backend / База данных |
| **Архитектурный** | Presentation Layer / Business Logic Layer / Data Access Layer |
| **Модульный** | Модуль аутентификации / Модуль биллинга / Модуль уведомлений |
| **Классовый (SRP)** | `UserRepository` (доступ к данным) / `UserValidator` (валидация) / `UserNotifier` (отправка писем) |
| **Методов** | Метод `calculateTotal()` не должен заодно отправлять email |

### Примеры на Java SoC

**Нарушение SoC на уровне класса:**

```java
// ❌ Класс смешивает бизнес-логику, доступ к данным, валидацию и логирование
public class OrderProcessor {

    public void processOrder(Order order) {
        // Валидация
        if (order.getItems().isEmpty()) {
            throw new IllegalArgumentException("Order must have at least one item");
        }

        // Бизнес-логика
        BigDecimal total = order.getItems().stream()
            .map(Item::getPrice)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
        order.setTotal(total);

        // Доступ к данным (прямой JDBC в бизнес-методе!)
        try (Connection conn = DriverManager.getConnection("jdbc:...")) {
            PreparedStatement stmt = conn.prepareStatement(
                "INSERT INTO orders (id, total) VALUES (?, ?)"
            );
            stmt.setLong(1, order.getId());
            stmt.setBigDecimal(2, order.getTotal());
            stmt.executeUpdate();
        } catch (SQLException e) {
            // Логирование
            System.err.println("Failed to save order: " + e.getMessage());
        }

        // Отправка email
        sendEmail(order.getCustomerEmail(), "Order confirmed", "Your order #"
            + order.getId() + " has been processed.");
    }

    private void sendEmail(String to, String subject, String body) {
        // SMTP логика...
    }
}
```

```java
// ✅ SoC: ответственности разделены по отдельным классам

// Класс 1: Только валидация
@Component
public class OrderValidator {
    public void validate(Order order) {
        if (order.getItems().isEmpty()) {
            throw new IllegalArgumentException("Order must have at least one item");
        }
    }
}

// Класс 2: Только бизнес-логика
@Component
public class OrderCalculator {
    public BigDecimal calculateTotal(Order order) {
        return order.getItems().stream()
            .map(Item::getPrice)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
    }
}

// Класс 3: Только доступ к данным
@Repository
public class OrderRepository {
    private final JdbcTemplate jdbc;

    public void save(Order order) {
        jdbc.update("INSERT INTO orders (id, total) VALUES (?, ?)",
            order.getId(), order.getTotal());
    }
}

// Класс 4: Только уведомления
@Component
public class NotificationService {
    private final EmailSender emailSender;

    public void sendOrderConfirmation(Order order) {
        emailSender.send(order.getCustomerEmail(),
            "Order confirmed",
            "Your order #" + order.getId() + " has been processed.");
    }
}

// Оркестратор — собирает всё вместе, но сам не содержит логики
@Service
public class OrderProcessor {
    private final OrderValidator validator;
    private final OrderCalculator calculator;
    private final OrderRepository repository;
    private final NotificationService notification;

    public void processOrder(Order order) {
        validator.validate(order);
        order.setTotal(calculator.calculateTotal(order));
        repository.save(order);
        notification.sendOrderConfirmation(order);
    }
}
```

### SoC и архитектурные стили

Принцип SoC проявляется на всех уровнях архитектуры:

| Архитектурный стиль | Как реализуется SoC |
|---------------------|---------------------|
| **Многоуровневая архитектура** (Layered) | Presentation → Business → Persistence |
| **Гексагональная архитектура** (Hexagonal / Ports & Adapters) | Домен изолирован от инфраструктуры через порты и адаптеры |
| **Clean Architecture** | Entities → Use Cases → Interface Adapters → Frameworks |
| **Микросервисы** | Каждый сервис отвечает за одну бизнес-возможность (bounded context) |
| **Model-View-Controller** | Model (данные) / View (отображение) / Controller (обработка ввода) |

---

## Law of Demeter — Закон Деметры

### Суть принципа LoD

> **Разговаривай только с ближайшими друзьями; не разговаривай с незнакомцами.**

Закон Деметры (Law of Demeter, LoD), также известный как **Principle of Least Knowledge** (Принцип наименьшего знания), сформулирован в 1987 году в Northeastern University (проект «Деметра»). Он ограничивает взаимодействие между объектами для достижения слабой связанности (low coupling).

### Правило одной точки

Метод `m` объекта `A` может вызывать методы только следующих объектов:

1. Самого объекта `A` (`this`).
2. Параметров метода `m`.
3. Объектов, созданных внутри метода `m`.
4. Полей (компонентов) объекта `A`.

Другими словами: **не более одной точки** при навигации по объектному графу: `a.b.c.d()` — нарушение.

### Примеры на Java LoD

**Классическое нарушение — «Train Wreck»:**

```java
// ❌ Нарушение Закона Деметры: цепочка из 4 вызовов
public class ReportGenerator {
    public String getManagerPhone(Employee employee) {
        return employee
            .getDepartment()        // получаем Department
            .getManager()           // получаем Manager
            .getContactInfo()       // получаем ContactInfo
            .getPhoneNumber();      // наконец, телефон — 4 точки!
    }
}
// ReportGenerator знает о внутренней структуре Employee, Department, Manager, ContactInfo.
// Изменение любого из этих классов может сломать ReportGenerator.
```

```java
// ✅ Соблюдение Закона Деметры: каждый объект скрывает свою внутреннюю структуру
public class Employee {
    private Department department;

    // Employee предоставляет метод, инкапсулирующий навигацию
    public String getManagerPhoneNumber() {
        return department.getManagerPhoneNumber();
    }
}

public class Department {
    private Manager manager;

    public String getManagerPhoneNumber() {
        return manager.getPhoneNumber();
    }
}

public class Manager {
    private String phoneNumber;

    public String getPhoneNumber() {
        return phoneNumber;
    }
}

// ReportGenerator теперь знает только об Employee
public class ReportGenerator {
    public String getManagerPhone(Employee employee) {
        return employee.getManagerPhoneNumber(); // одна точка!
    }
}
```

**Нарушение в условиях и циклах:**

```java
// ❌ Нарушение: глубокий доступ в условии
public boolean isEligibleForDiscount(Order order) {
    return order.getCustomer().getAccount().getType() == AccountType.PREMIUM
        && order.getCustomer().getAccount().getCreatedAt().isBefore(LocalDate.now().minusYears(1));
}
```

```java
// ✅ Исправление: инкапсуляция условия в объекте
public class Customer {
    public boolean isPremiumForAtLeast(Duration duration) {
        return account.getType() == AccountType.PREMIUM
            && account.getCreatedAt().isBefore(LocalDate.now().minus(duration));
    }
}

public boolean isEligibleForDiscount(Order order) {
    return order.getCustomer().isPremiumForAtLeast(Duration.ofYears(1));
}
```

### Train Wreck — антипаттерн

**Train Wreck** (крушение поезда) — код с длинными цепочками вызовов методов:

```java
object.getA().getB().getC().doSomething()
```

Почему это плохо:

- **Хрупкость.** Изменение любого звена цепочки ломает код клиента.
- **Нарушение инкапсуляции.** Клиент знает о внутренней структуре объекта.
- **Null-безопасность.** Любое звено может вернуть `null` → NPE.
- **Тестирование.** Для unit-теста нужно замокать всю цепочку, а не один объект.

**Исправление Train Wreck:**

```java
// Вместо:
String city = order.getCustomer().getAddress().getCity();

// Определите метод на верхнем уровне:
String city = order.getCustomerCity();
// Реализация скрыта внутри Customer/Order
```

### Исключения из закона Деметры

Не всякая цепочка вызовов — нарушение. Исключения:

1. **Fluent API / Builder-паттерн:**
   ```java
   // Это не нарушение, т.к. каждый метод возвращает this (тот же объект)
   Order order = Order.builder()
       .customerId(123L)
       .status(OrderStatus.NEW)
       .item("Widget", 2)
       .build();
   ```

2. **Stream API:**
   ```java
   // Каждый вызов возвращает Stream — не нарушение, т.к. это один и тот же тип
   list.stream()
       .filter(...)
       .map(...)
       .collect(...);
   ```

3. **Внутренние DSL / jOOQ / QueryDSL:**
   ```java
   // fluent API библиотек — возвращают тот же тип
   dsl.select(...).from(...).where(...).fetch();
   ```

4. **Структуры данных (DTO, Record):**
   ```java
   // Если Address — чистый DTO без поведения, то цепочка допустима
   String city = order.getShippingAddress().getCity();
   // Но лучше: order.getShippingCity() — инкапсуляция не повредит
   ```

---

## Composition over Inheritance

### Суть принципа CoI

> **Предпочитай композицию наследованию. Отношение HAS-A часто лучше, чем IS-A.**

Принцип популяризован «Бандой четырёх» (GoF) в книге «Design Patterns» (1994), где он звучит как:

> *«Favor object composition over class inheritance.»*

**Композиция** — объект содержит другой объект как поле и делегирует ему поведение.
**Наследование** — класс расширяет другой класс, наследуя его поля и методы.

### Проблемы наследования

| Проблема | Описание |
|----------|----------|
| **Хрупкий базовый класс** | Изменение в родительском классе может сломать всех наследников — даже если изменения корректны для родителя. |
| **Нарушение инкапсуляции** | Наследник имеет доступ к `protected` полям и методам родителя — внутреннее состояние становится доступным извне. |
| **Жёсткая иерархия** | Нельзя изменить поведение во время выполнения. Если `Bird` extends `Animal`, объект `Bird` всегда будет `Animal`. С композицией поведение можно подменить динамически (паттерн Strategy). |
| **Проблема алмаза** | Множественное наследование классов невозможно в Java (и не случайно). |
| **Раздувание API** | Наследник получает все публичные методы родителя, даже если они не имеют смысла в контексте наследника. Пример: `Stack extends Vector` — у `Stack` есть методы `add(int, E)`, `remove(int)`, нарушающие семантику стека (LIFO). |

### Примеры на Java CoI

**Проблема наследования:**

```java
// ❌ Наследование: Stack наследует Vector, но нарушает его контракт
public class Stack<E> extends Vector<E> {
    public E push(E item) {
        addElement(item);
        return item;
    }

    public synchronized E pop() {
        E obj = peek();
        removeElementAt(size() - 1);
        return obj;
    }
}
// Проблема: любой код может сделать stack.add(1, element) — вставка в середину,
// что нарушает LIFO-семантику стека.
```

```java
// ✅ Композиция: Stack содержит Vector (или ArrayList) и делегирует операции
public class Stack<E> {
    private final List<E> elements = new ArrayList<>();

    public void push(E item) {
        elements.add(item);
    }

    public E pop() {
        if (elements.isEmpty()) {
            throw new EmptyStackException();
        }
        return elements.remove(elements.size() - 1);
    }

    public E peek() {
        if (elements.isEmpty()) {
            throw new EmptyStackException();
        }
        return elements.get(elements.size() - 1);
    }

    public boolean isEmpty() {
        return elements.isEmpty();
    }
    // API стека минимален и корректен — никаких add(int, E), remove(int) и т.д.
}
```

**Стратегия через композицию вместо наследования:**

```java
// ❌ Наследование: разные типы уток через иерархию классов
// (классический пример из Head First Design Patterns)
abstract class Duck {
    abstract void display();
    void quack() { System.out.println("Quack!"); }
    void fly() { System.out.println("Flying..."); }
}

class MallardDuck extends Duck { ... }
class RedheadDuck extends Duck { ... }
class RubberDuck extends Duck {
    @Override void quack() { System.out.println("Squeak!"); }
    @Override void fly() { /* резиновая утка не летает — нарушение LSP! */ }
}
// Добавляем WoodenDuck — снова override fly() на "ничего не делать".
// С каждой новой разновидностью иерархия разрастается.
```

```java
// ✅ Композиция: поведение вынесено в отдельные объекты (Strategy)
interface QuackBehavior { void quack(); }
interface FlyBehavior { void fly(); }

class Quack implements QuackBehavior {
    public void quack() { System.out.println("Quack!"); }
}
class Squeak implements QuackBehavior {
    public void quack() { System.out.println("Squeak!"); }
}
class MuteQuack implements QuackBehavior {
    public void quack() { System.out.println("..."); }
}

class FlyWithWings implements FlyBehavior {
    public void fly() { System.out.println("Flying..."); }
}
class FlyNoWay implements FlyBehavior {
    public void fly() { /* ничего */ }
}

class Duck {
    private final QuackBehavior quackBehavior;
    private final FlyBehavior flyBehavior;

    public Duck(QuackBehavior qb, FlyBehavior fb) {
        this.quackBehavior = qb;
        this.flyBehavior = fb;
    }

    public void performQuack() { quackBehavior.quack(); }
    public void performFly() { flyBehavior.fly(); }

    // Можно даже менять поведение в рантайме:
    public void setQuackBehavior(QuackBehavior qb) { ... }
}

// Создание разных уток — комбинацией, а не наследованием
Duck mallard = new Duck(new Quack(), new FlyWithWings());
Duck rubber = new Duck(new Squeak(), new FlyNoWay());
Duck wooden = new Duck(new MuteQuack(), new FlyNoWay());
```

### Паттерны на основе композиции

Следующие GoF-паттерны основаны на композиции:

| Паттерн | Суть композиции |
|---------|-----------------|
| **Strategy** | Алгоритм — отдельный объект, подставляемый в контекст |
| **Decorator** | Обёртка (wrapper) добавляет поведение, делегируя обёрнутому объекту |
| **Composite** | Древовидная структура, где и лист, и узел реализуют общий интерфейс |
| **Adapter** | Адаптер содержит адаптируемый объект и преобразует его интерфейс |
| **Proxy** | Прокси содержит реальный объект и контролирует доступ к нему |
| **Observer** | Subject содержит коллекцию Observer'ов |

Во всех этих паттернах именно композиция (HAS-A), а не наследование (IS-A), обеспечивает гибкость.

**Когда наследование всё же уместно:**

- IS-A отношение действительно выполняется (всегда, без исключений): `Square` IS-A `Shape`.
- Базовый класс спроектирован для наследования (документирован, с protected-хуками).
- Нужно соблюсти контракт абстрактного класса с шаблонным методом (Template Method).
- Иерархия стабильна и не планирует расширяться вширь.

---

## TDA — Tell, Don't Ask

### Суть принципа TDA

> **Сообщай объекту, что ты хочешь; не спрашивай его о состоянии, чтобы самому принять решение.**

Tell, Don't Ask (TDA) — принцип, популяризованный в мире Smalltalk и экстремального программирования. Его суть: объекты должны быть умными, они должны инкапсулировать не только данные, но и поведение, связанное с этими данными.

### Процедурный vs объектный стиль

Принцип TDA разделяет два стиля программирования:

**Процедурный стиль (Ask — нарушение TDA):**
Код запрашивает данные у объекта, анализирует их, принимает решение и выполняет действие.

**Объектный стиль (Tell — соблюдение TDA):**
Код сообщает объекту, что нужно сделать; объект сам анализирует своё состояние и выполняет действие.

### Примеры на Java TDA

**Процедурный стиль (нарушение TDA):**

```java
// ❌ Ask: клиент запрашивает состояние и сам принимает решение
public class AlarmService {

    public void checkAlarm(Alarm alarm) {
        // Спрашиваем состояние...
        Time currentTime = alarm.getCurrentTime();
        Time alarmTime = alarm.getAlarmTime();
        boolean isEnabled = alarm.isEnabled();
        boolean isWeekday = alarm.isWeekday();
        int snoozeCount = alarm.getSnoozeCount();
        DayOfWeek today = alarm.getToday();

        // ...и принимаем решение снаружи объекта
        if (isEnabled && !isWeekday && snoozeCount < 3) {
            if (currentTime.equals(alarmTime)) {
                alarm.trigger();
            }
        }
    }
}
// Проблема: AlarmService знает ВСЮ внутреннюю логику Alarm.
// Если правило срабатывания изменится, придётся менять AlarmService.
// Если появится второй клиент, логика будет дублироваться.
```

```java
// ✅ Tell: клиент говорит, ЧТО нужно, а объект сам решает, КАК
public class Alarm {

    public void checkAndTrigger() {
        if (shouldTrigger()) {
            trigger();
        }
    }

    private boolean shouldTrigger() {
        return enabled
            && !isWeekday()
            && snoozeCount < 3
            && currentTime.equals(alarmTime);
    }
}

// Клиент: просто говорит — проверь и сработай если нужно
public class AlarmService {
    public void checkAlarm(Alarm alarm) {
        alarm.checkAndTrigger();
    }
}
```

**Ещё один пример — обработка состояния заказа:**

```java
// ❌ Ask: внешний код проверяет статус заказа и решает, что делать
public class OrderService {
    public void cancelOrder(Order order) {
        if (order.getStatus() == OrderStatus.NEW
            || order.getStatus() == OrderStatus.PROCESSING) {
            order.setStatus(OrderStatus.CANCELLED);
            order.setCancelledAt(LocalDateTime.now());
            notificationService.sendCancellationEmail(order);
        } else if (order.getStatus() == OrderStatus.SHIPPED) {
            throw new IllegalStateException("Cannot cancel shipped order");
        } else {
            throw new IllegalStateException(
                "Cannot cancel order in status: " + order.getStatus());
        }
    }
}
```

```java
// ✅ Tell: Order сам знает, можно ли его отменить, и как это сделать
public class Order {
    public CancellationResult cancel() {
        if (!canBeCancelled()) {
            return CancellationResult.failure(
                "Order in status " + status + " cannot be cancelled");
        }
        status = OrderStatus.CANCELLED;
        cancelledAt = LocalDateTime.now();
        return CancellationResult.success(this);
    }

    private boolean canBeCancelled() {
        return status == OrderStatus.NEW || status == OrderStatus.PROCESSING;
    }
}

// Клиент:
public class OrderService {
    public void cancelOrder(Order order) {
        CancellationResult result = order.cancel();
        if (result.isSuccess()) {
            notificationService.sendCancellationEmail(order);
        } else {
            throw new IllegalStateException(result.getReason());
        }
    }
}
```

### Связь с инкапсуляцией

TDA — прямое следствие инкапсуляции:

- Данные объекта — `private`.
- Методы объекта — `public` и выражают поведение, а не доступ к данным.
- Клиент не знает и не должен знать, как объект устроен внутри.

Антипаттерн, связанный с нарушением TDA: **Anemic Domain Model** (анемичная модель предметной области). Это когда объекты домена — просто набор геттеров/сеттеров без поведения, а вся логика находится в сервисах. Мартин Фаулер называет это антипаттерном, потому что такой код теряет преимущества ООП.

---

## Encapsulate What Varies

### Суть принципа EWV

> **Инкапсулируй то, что изменяется. Отделяй стабильное от изменчивого.**

Принцип «Encapsulate What Varies» — один из фундаментальных принципов дизайна, лежащий в основе многих GoF-паттернов. Его суть: определи аспекты системы, которые могут измениться, и изолируй их так, чтобы их изменение не влияло на остальную систему.

### Техники инкапсуляции изменений

| Техника | Описание | Пример |
|---------|----------|--------|
| **Интерфейс + реализации** | Стабильный контракт, изменяемая реализация | `PaymentGateway` интерфейс, реализации `StripePayment`, `PaypalPayment` |
| **Паттерн Strategy** | Алгоритм как отдельный объект | Сортировка с разными компараторами |
| **Шаблонный метод** | Инвариантный алгоритм в базовом классе, изменяемые шаги в наследниках | `DataProcessor` с абстрактным `transform()` |
| **Конфигурация вместо кода** | Изменяемое поведение через внешние настройки | `application.yml`, feature flags |
| **Plugin-архитектура** | Изменяемое поведение через подключаемые модули | IDE-плагины |
| **Dependency Injection** | Изменяемые зависимости внедряются извне | Spring DI |

### Примеры на Java EWV

**Инкапсуляция алгоритма расчёта налога:**

```java
// ✅ Стабильный интерфейс
public interface TaxCalculator {
    BigDecimal calculate(BigDecimal amount, String region);
}

// ✅ Изменяемые реализации инкапсулированы
@Component
public class USTaxCalculator implements TaxCalculator {
    @Override
    public BigDecimal calculate(BigDecimal amount, String region) {
        // Правила налогообложения США (могут меняться)
        return amount.multiply(getRateForState(region));
    }
}

@Component
public class EUTaxCalculator implements TaxCalculator {
    @Override
    public BigDecimal calculate(BigDecimal amount, String region) {
        // Правила НДС ЕС (могут меняться независимо от США)
        return amount.multiply(getVatRateForCountry(region));
    }
}

// ✅ Клиентский код стабилен и не меняется при добавлении новых стран
@Service
public class InvoiceService {
    // Spring внедряет Map<String, TaxCalculator> — все бины TaxCalculator
    private final Map<String, TaxCalculator> calculators;

    public BigDecimal calculateTax(BigDecimal amount, String region) {
        TaxCalculator calculator = resolveCalculator(region);
        return calculator.calculate(amount, region);
    }
}
```

**Feature Flags вместо условной компиляции:**

```java
// ❌ Изменения требуют перекомпиляции и деплоя
public String getGreeting() {
    // Меняем true на false → редеплой
    if (true) { // старая версия: false — новая версия
        return "Hello!";
    } else {
        return "Welcome to our new platform!";
    }
}
```

```java
// ✅ Поведение управляется конфигурацией — меняется без редеплоя
public class GreetingService {
    private final FeatureFlags featureFlags;

    public String getGreeting() {
        if (featureFlags.isEnabled("new-welcome-message")) {
            return "Welcome to our new platform!";
        }
        return "Hello!";
    }
}
```

---

## Program to Interface, Not Implementation

### Суть принципа PINI

> **Пиши код, который зависит от интерфейсов (абстракций), а не от конкретных реализаций.**

Этот принцип тесно связан с **Dependency Inversion Principle** (DIP) из SOLID, но формулируется более практически: переменные, параметры методов и возвращаемые типы должны быть объявлены как интерфейсы (или абстрактные классы), а не как конкретные классы.

### Интерфейс как контракт

Интерфейс определяет **«что»** делает компонент. Реализация определяет **«как»**. Код, написанный против интерфейса, работает с **любой** реализацией этого интерфейса.

### Примеры на Java PINI

```java
// ❌ Зависимость от конкретной реализации
public class ReportService {
    // Жёсткая привязка к конкретному классу
    private final MySQLReportRepository repository = new MySQLReportRepository();
    private final SmtpEmailSender emailSender = new SmtpEmailSender();

    // Тип параметра — конкретный класс
    public void exportToCsv(FileSystemStorage storage) { ... }
}
// Последствия:
// - Невозможно подменить MySQLReportRepository на PostgresReportRepository
// - Невозможно протестировать ReportService с моком репозитория
// - Невозможно использовать InMemoryStorage для тестов
```

```java
// ✅ Зависимость от интерфейсов (абстракций)
@Service
public class ReportService {
    private final ReportRepository repository;     // интерфейс
    private final EmailSender emailSender;          // интерфейс

    // Spring внедрит любую реализацию интерфейсов
    public ReportService(ReportRepository repository, EmailSender emailSender) {
        this.repository = repository;
        this.emailSender = emailSender;
    }

    // Тип параметра — интерфейс
    public void exportToCsv(Storage storage) { ... }
}
// Преимущества:
// - Можно передать MySQLReportRepository, PostgresReportRepository, InMemoryReportRepository
// - В тестах: new ReportService(new InMemoryReportRepository(), new MockEmailSender())
// - Можно передать FileSystemStorage, S3Storage, AzureBlobStorage
```

**Осторожность с коллекциями:**

```java
// ❌ Привязка к конкретной реализации коллекции
public ArrayList<User> getActiveUsers() { ... }
public HashSet<String> getUniqueTags() { ... }

// ✅ Программируйте против интерфейса коллекции
public List<User> getActiveUsers() { ... }
public Set<String> getUniqueTags() { ... }
// Возвращаемый тип — интерфейс. Реализация может измениться
// с ArrayList на LinkedList без влияния на клиентов.
```

### Связь с DIP из SOLID

DIP (Dependency Inversion Principle) формулирует два правила:

1. Высокоуровневые модули не должны зависеть от низкоуровневых. Оба должны зависеть от абстракций.
2. Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.

«Program to Interface» — это практическое воплощение DIP на уровне написания кода.

---

## Fail Fast

### Суть принципа FF

> **Обнаруживай ошибку как можно раньше — на этапе компиляции, запуска или в первой же строчке метода. Не позволяй некорректному состоянию распространяться.**

Принцип Fail Fast гласит: система должна немедленно сообщать об ошибке, а не пытаться «продолжить работу с тем, что есть», маскируя проблему и усложняя отладку.

### Fail Fast vs Fail Safe

| Стратегия | Описание | Пример |
|-----------|----------|--------|
| **Fail Fast** | Немедленный отказ при некорректном состоянии | `Objects.requireNonNull(param)` — кидает NPE сразу |
| **Fail Safe** | Попытка продолжить работу несмотря на ошибку | Вернуть `null` или значение по умолчанию и надеяться, что проблема рассосётся |

Fail Safe не означает «безопасный». В большинстве бизнес-приложений Fail Safe приводит к тому, что ошибка маскируется, некорректные данные сохраняются в БД, а настоящая причина проявляется через часы/дни в совершенно другом месте системы.

### Примеры на Java FF

**Валидация на входе метода:**

```java
// ❌ Fail Safe: метод «терпит» некорректные аргументы
public void transfer(BigDecimal amount, Account from, Account to) {
    if (amount == null) {
        amount = BigDecimal.ZERO; // скрывает баг вызывающего кода
    }
    if (from == null || to == null) {
        return; // тихо выходим — никто не узнает, что перевод не выполнен
    }
    // перевод...
}
```

```java
// ✅ Fail Fast: некорректные аргументы → исключение сразу
public void transfer(BigDecimal amount, Account from, Account to) {
    Objects.requireNonNull(amount, "amount must not be null");
    Objects.requireNonNull(from, "from account must not be null");
    Objects.requireNonNull(to, "to account must not be null");

    if (amount.compareTo(BigDecimal.ZERO) <= 0) {
        throw new IllegalArgumentException("amount must be positive: " + amount);
    }
    if (from.equals(to)) {
        throw new IllegalArgumentException("cannot transfer to the same account");
    }
    // перевод...
}
```

**Fail Fast при старте приложения:**

```java
// ❌ Ленивая инициализация: ошибка конфигурации обнаруживается
//    только при первом обращении (возможно, через месяц после деплоя)
@Component
public class PaymentService {
    private String apiKey;

    public void processPayment(Payment payment) {
        if (apiKey == null) {
            apiKey = System.getenv("PAYMENT_API_KEY");
            if (apiKey == null) {
                throw new IllegalStateException("API key not configured");
            }
        }
        // ...
    }
}
```

```java
// ✅ Fail Fast на старте: приложение не запустится с некорректной конфигурацией
@Component
public class PaymentService {
    private final String apiKey;

    public PaymentService(@Value("${payment.api-key}") String apiKey) {
        if (apiKey == null || apiKey.isBlank()) {
            throw new IllegalStateException(
                "payment.api-key must be configured. "
                + "Set PAYMENT_API_KEY environment variable.");
        }
        this.apiKey = apiKey;
    }
    // Приложение упадёт при старте, а не через месяц на проде
}
```

**Использование типа вместо null:**

```java
// ❌ Возврат null — клиент может не проверить, NPE через 10 методов
public User findUser(Long id) {
    return database.get(id); // может вернуть null
}

// ✅ Возврат Optional — клиент ВЫНУЖДЕН обработать случай отсутствия
public Optional<User> findUser(Long id) {
    return Optional.ofNullable(database.get(id));
}
```

### Fail Fast на разных уровнях системы

| Уровень | Техника |
|---------|---------|
| **Компиляция** | Строгая типизация, `sealed` классы, exhaustive `switch`, аннотации `@NonNull` |
| **Старт приложения** | Валидация конфигурации, проверка подключения к БД/брокерам |
| **Вход метода** | `Objects.requireNonNull()`, precondition checks |
| **Сериализация/десериализация** | Валидация DTO сразу после десериализации |
| **Сохранение в БД** | `NOT NULL` constraints, `CHECK` constraints |

---

## Convention over Configuration

### Суть принципа CoC

> **Разумные значения по умолчанию, соглашения о структуре и именовании уменьшают количество явной конфигурации.**

Convention over Configuration (CoC) — принцип, популяризованный фреймворком Ruby on Rails (Дэвид Хайнемайер Ханссон). Суть: если все в сообществе следуют одним и тем же соглашениям, фреймворк может автоматически выводить конфигурацию из структуры кода, следуя этим соглашениям.

### Примеры из экосистемы Java CoC

**Spring Boot:**

```java
// Без CoC: явная конфигурация всего (Spring XML эпохи)
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource">
    <property name="driverClassName" value="org.postgresql.Driver"/>
    <property name="url" value="jdbc:postgresql://localhost:5432/mydb"/>
    <property name="username" value="user"/>
    <property name="password" value="pass"/>
</bean>
<bean id="entityManagerFactory" class="...LocalContainerEntityManagerFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="packagesToScan" value="com.example.domain"/>
    <!-- ... ещё 20 строк -->
</bean>

// С CoC (Spring Boot): spring-boot-starter-data-jpa + application.yml
// spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
// spring.datasource.username=user
// spring.datasource.password=pass
// Всё остальное — автоматически:
// - Пулы соединений (HikariCP)
// - EntityManagerFactory
// - TransactionManager
// - Репозитории (Spring Data JPA сканирует и создаёт реализации автоматически)
```

**Spring Data JPA — соглашения об именовании методов:**

```java
// Без CoC: пишем SQL/JPQL вручную для каждого запроса
@Query("SELECT u FROM User u WHERE u.email = :email")
Optional<User> findByEmail(@Param("email") String email);

@Query("SELECT u FROM User u WHERE u.age > :minAge AND u.active = true")
List<User> findActiveAdults(@Param("minAge") int minAge);

// С CoC (Spring Data JPA): имя метода → автоматический JPQL
public interface UserRepository extends JpaRepository<User, Long> {
    // Конвенция: findBy + поле → запрос генерируется автоматически
    Optional<User> findByEmail(String email);

    // Конвенция: findBy + поле + условие + And + поле + условие
    List<User> findByAgeGreaterThanAndActiveTrue(int minAge);

    // Сортировка тоже из имени:
    List<User> findByActiveTrueOrderByLastNameAsc();
}
// Spring Data парсит имя метода и строит запрос. Никакого boilerplate.
```

**Lombok — соглашение через аннотации:**

```java
// Без CoC: ручной boilerplate
public class User {
    private Long id;
    private String name;
    private String email;

    public User() { }
    public User(Long id, String name, String email) { this.id = id; this.name = name; this.email = email; }
    public Long getId() { return id; }
    public void setId(Long id) { this.id = id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
    @Override public boolean equals(Object o) { /* ... */ }
    @Override public int hashCode() { /* ... */ }
    @Override public String toString() { return "User{id=" + id + ", name='" + name + '\'' + '}'; }
}

// С CoC (Lombok): конвенция через аннотации — код генерируется при компиляции
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Long id;
    private String name;
    private String email;
}
// @Data генерирует: getters, setters, equals, hashCode, toString
// @AllArgsConstructor — конструктор со всеми полями
// @NoArgsConstructor — пустой конструктор
```

**MapStruct — соглашение об именовании методов маппинга:**

```java
// Без CoC: ручной маппинг DTO ↔ Entity
public class UserMapper {
    public UserDTO toDto(User user) {
        UserDTO dto = new UserDTO();
        dto.setId(user.getId());
        dto.setFullName(user.getFirstName() + " " + user.getLastName());
        dto.setEmailAddress(user.getEmail());
        dto.setCreatedAt(user.getCreatedAt().toString());
        return dto;
    }
}

// С CoC (MapStruct): интерфейс + конвенция — реализация генерируется при компиляции
@Mapper
public interface UserMapper {
    @Mapping(source = "firstName", target = "fullName",
             qualifiedByName = "fullName")
    @Mapping(source = "email", target = "emailAddress")
    UserDTO toDto(User user);

    @Named("fullName")
    static String fullName(User user) {
        return user.getFirstName() + " " + user.getLastName();
    }
}
// MapStruct генерирует реализацию на основе соглашения:
// поля с одинаковыми именами мапятся автоматически,
// для несовпадающих — указываем @Mapping явно (только исключения!)
```

### Плюсы и минусы CoC

| Плюсы | Минусы |
|-------|--------|
| Меньше кода конфигурации | «Магия» — трудно понять, что происходит под капотом |
| Быстрый старт новых проектов | Отклонение от конвенции требует явной конфигурации |
| Единообразие между проектами | Соглашения могут не подходить для нестандартных задач |
| Меньше багов из-за опечаток в конфигах | Разработчик должен знать конвенции |

---

## Single Source of Truth

### Суть принципа SSOT

> **Каждая единица информации должна иметь один авторитетный источник. Все остальные представления — производные.**

Single Source of Truth (SSOT) — принцип, пришедший из управления данными и архитектуры предприятия. В разработке ПО он означает: для каждого факта (данных, конфигурации, состояния) существует ровно одно место, где этот факт хранится и откуда он распространяется в остальную систему.

SSOT тесно связан с DRY, но DRY — про код и знания, а SSOT — про данные и состояние.

### SSOT vs децентрализация

| Подход | Описание | Когда применять |
|--------|----------|-----------------|
| **SSOT** | Одно каноническое хранилище | Финансовые транзакции, учётные системы, мастер-данные |
| **Eventual Consistency** | Данные реплицируются и синхронизируются с задержкой | Распределённые системы, микросервисы |
| **CQRS** | Отдельные модели на чтение и запись | Высоконагруженные системы с разными паттернами доступа |

### Примеры на Java SSOT

**Конфигурация из одного источника:**

```java
// ❌ Дублирование конфигурации в разных файлах и классах
// application.yml
app:
  page-size: 20
  max-upload-size: 10MB

// SomeService.java
private static final int PAGE_SIZE = 20; // дубликат!

// another-config.properties
page.size=20 // ещё один дубликат!
```

```java
// ✅ SSOT: единый источник конфигурации
@ConfigurationProperties(prefix = "app")
@Validated
public record AppProperties(
    @Min(1) @Max(100) int pageSize,
    @NotNull DataSize maxUploadSize
) { }

// Все сервисы используют один и тот же объект AppProperties
@Service
public class SomeService {
    private final AppProperties props;
    // использует props.pageSize() — единственный источник значения
}
```

**Кеш как производная от SSOT (БД):**

```java
// ✅ SSOT: БД — источник истины, кеш — производная
@Service
public class UserService {
    private final UserRepository repository;  // SSOT
    private final Cache<Long, User> cache;    // производная

    public User getUser(Long id) {
        return cache.get(id, () ->
            repository.findById(id)
                .orElseThrow(() -> new UserNotFoundException(id))
        );
    }

    // При изменении SSOT — инвалидируем кеш
    @Transactional
    public User updateUser(User user) {
        User saved = repository.save(user); // обновляем SSOT
        cache.invalidate(saved.getId());     // инвалидируем производную
        return saved;
    }
}
```

---

## Robustness Principle — Postel's Law

### Суть принципа PoL

> **Будь консервативен в том, что отправляешь, и либерален в том, что принимаешь.**

Принцип надёжности (Robustness Principle), также известный как **Закон Постела** (Postel's Law), сформулирован Джоном Постелом в RFC 1122 (1989) — одной из спецификаций TCP/IP. Постел был одним из отцов интернета и автором многих ключевых RFC.

В контексте разработки ПО принцип означает:

- **Отправитель (консервативен):** генерируй строго соответствующие спецификации данные. Не полагайся на «особенности» реализации получателя.
- **Получатель (либерален):** принимай и обрабатывай данные, даже если они не идеально соответствуют спецификации, но понятны по смыслу. Будь толерантен к ошибкам.

### Почему это работает

Принцип Постела — одна из причин успеха интернета. Если бы каждый узел требовал идеального соответствия спецификации, сеть бы не работала: реализации разные, версии протоколов множатся, баги неизбежны. Но благодаря толерантности получателей пакеты доходят даже при незначительных отклонениях.

### Примеры на Java PoL

**Нарушение — хрупкий парсер JSON:**

```java
// ❌ Хрупкий получатель: требует строгого порядка полей и отсутствия unknown-полей
public class StrictUserParser {
    public User parse(String json) {
        // Ломается, если поле name идёт после age
        // Ломается, если есть неизвестное поле phoneNumber
        // Ломается, если email в другом регистре
        JsonObject obj = Json.createReader(new StringReader(json)).readObject();
        return new User(
            obj.getString("name"),   // порядок жёстко задан
            obj.getInt("age"),
            obj.getString("email")   // требует точного имени поля
        );
    }
}
```

```java
// ✅ Либеральный получатель + консервативный отправитель
public class RobustUserParser {
    private static final ObjectMapper MAPPER = new ObjectMapper()
        .configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, false) // либерален
        .configure(SerializationFeature.ORDER_MAP_ENTRIES_BY_KEYS, true);    // консервативен

    public User parse(String json) {
        return MAPPER.readValue(json, User.class);
    }

    public String toJson(User user) {
        return MAPPER.writeValueAsString(user); // всегда строго по спецификации
    }
}
```

**HTTP API — консервативный сервер, либеральный клиент:**

```java
// ✅ Консервативный контроллер (отправляет строго по контракту)
@RestController
public class UserController {

    @GetMapping("/users/{id}")
    public ResponseEntity<UserResponse> getUser(@PathVariable Long id) {
        // Ответ всегда содержит ВСЕ поля контракта, даже если некоторые null
        UserResponse response = userService.getUser(id);
        return ResponseEntity.ok(response); // Jackson сериализует строго по DTO
    }

    // ✅ Либеральный приём запросов
    @PostMapping("/users")
    public ResponseEntity<UserResponse> createUser(@RequestBody UserRequest request) {
        // Принимаем даже если клиент прислал лишние поля (игнорируем)
        // Принимаем если поле отсутствует — подставляем default
        User user = userService.create(request);
        return ResponseEntity.status(CREATED).body(UserResponse.from(user));
    }
}

// DTO с защитой от неизвестных полей:
@JsonIgnoreProperties(ignoreUnknown = true) // ← либеральный приём
public record UserRequest(
    @NotBlank String name,
    @Email String email,
    @Min(0) @Max(150) Integer age
) { }
```

**Семантическое версионирование как применение принципа Постела:**

```java
// ✅ Консервативный отправитель: строго соблюдаем semver
// - MAJOR: breaking changes
// - MINOR: обратно совместимые дополнения
// - PATCH: обратно совместимые исправления

// ✅ Либеральный получатель: принимаем совместимые версии
@Client("user-service")
public interface UserClient {
    // Клиент принимает ответы от сервера с любой совместимой версией API
    @GetMapping("/api/v1/users/{id}")
    UserResponse getUser(@PathVariable Long id);
    // Сервер может быть v1.0, v1.1, v1.5 — клиент работает со всеми
}
```

### Границы применимости

Принцип Постела имеет и критику: излишняя толерантность получателей может привести к тому, что ошибки в реализациях становятся «де-факто стандартом», и новые реализации вынуждены их воспроизводить (см. **Hyrum's Law**). Поэтому:

- Будь либерален к тому, что **понятно по смыслу**, но отличается формой (порядок полей, лишние поля, регистр).
- **Не будь либерален** к семантически некорректным данным (отрицательный возраст, невалидный email) — здесь применяй **Fail Fast**.
- Логируй случаи «либерального приёма» — они указывают на проблемы у отправителя.

---

## Occam's Razor — Бритва Оккама

### Суть принципа OR

> **Не умножай сущности без необходимости. Из нескольких объяснений выбирай простейшее.**

Бритва Оккама (Occam's Razor) — философский принцип Уильяма из Оккама (XIV век). В разработке ПО он интерпретируется так:

- Если есть два решения задачи, выбирай то, которое требует меньше предположений, классов и зависимостей.
- Не вводи новую абстракцию, если задача решается без неё.
- Отдавай предпочтение решению с меньшим количеством движущихся частей.

### Применение в разработке

| Ситуация | Применение Бритвы Оккама |
|----------|--------------------------|
| **Выбор технологии** | Введи микросервисы, только если монолит реально не справляется |
| **Отладка** | Начни с самой простой и вероятной причины бага, а не с экзотической |
| **Архитектурное решение** | Сначала без очереди сообщений, добавляй когда понадобится |
| **Оценка задачи** | Временная оценка должна исходить из простейшего варианта реализации |

### Примеры OR

```
Задача: нужно хранить настройки пользователя.

❌ Усложнение:
   - Распределённое key-value хранилище (etcd/Consul)
   - Сервис конфигураций с REST API
   - Кеширующий слой с инвалидацией
   - Подписка на изменения через WebSocket

✅ Простейшее решение (Бритва Оккама):
   - Таблица user_settings в существующей БД
   - Прямой запрос при логине пользователя
```

**Java-пример — простая реализация vs переусложнение:**

```java
// Задача: проверить, что строка является валидным email.

// ❌ Переусложнение (нарушение Бритвы Оккама):
//    - Цепочка из 3 классов
//    - Паттерн Chain of Responsibility
//    - Конфигурация через внешний файл
interface ValidationRule { boolean validate(String input); }

class NotNullRule implements ValidationRule {
    public boolean validate(String input) { return input != null; }
}
class NotEmptyRule implements ValidationRule {
    public boolean validate(String input) { return !input.isBlank(); }
}
class EmailFormatRule implements ValidationRule {
    private static final Pattern PATTERN = Pattern.compile("^[\\w-.]+@[\\w-]+\\.[a-z]{2,}$");
    public boolean validate(String input) { return PATTERN.matcher(input).matches(); }
}

class ValidatorChain {
    private final List<ValidationRule> rules;
    public ValidatorChain(List<ValidationRule> rules) { this.rules = rules; }
    public boolean validate(String input) {
        return rules.stream().allMatch(r -> r.validate(input));
    }
}
// Использование:
ValidatorChain chain = new ValidatorChain(List.of(
    new NotNullRule(), new NotEmptyRule(), new EmailFormatRule()
));
boolean valid = chain.validate(email);
```

```java
// ✅ Бритва Оккама: простейшее решение, решающее задачу
public final class EmailValidator {
    private static final Pattern EMAIL = Pattern.compile("^[\\w-.]+@[\\w-]+\\.[a-z]{2,}$");

    public static boolean isValid(String email) {
        return email != null && EMAIL.matcher(email).matches();
    }
}
// Использование:
boolean valid = EmailValidator.isValid(email);
// Одна строчка использования, один метод, никакой иерархии классов.
// Если в будущем понадобится Chain of Responsibility для сложной валидации
// разных типов данных — добавим. Но не сейчас (YAGNI + Бритва Оккама).
```

**Практическое правило:** если на решение простой задачи ушло больше одного класса — остановись и спроси себя: «Можно ли проще?».

---

## Worse is Better

### Суть принципа WIB

> **Правильно работающая система с ограниченной функциональностью лучше, чем амбициозная система, которая не завершена.**

«Worse is Better» — эссе Ричарда Гэбриела (Richard P. Gabriel, 1989), в котором он описал философию дизайна, характерную для Unix и C (The New Jersey Approach), в противовес академическому подходу MIT (The MIT Approach).

### The MIT Approach vs The New Jersey Approach

| Аспект | MIT Approach (The Right Thing) | New Jersey Approach (Worse is Better) |
|--------|-------------------------------|--------------------------------------|
| **Простота** | Дизайн должен быть простым | **Реализация** должна быть простой; дизайн может быть сложным |
| **Корректность** | Дизайн должен быть корректным во всех аспектах | Достаточно корректности в 90% случаев |
| **Завершённость** | Дизайн должен покрывать все сценарии | Можно пожертвовать завершённостью ради простоты |
| **Консистентность** | Важна | Можно пожертвовать консистентностью ради простоты |

**Эссе заканчивается выводом:** подход «Worse is Better» побеждает, потому что простая в реализации система быстрее выходит на рынок, быстрее распространяется и эволюционирует, в то время как «идеальная» система всё ещё проектируется.

### Влияние на индустрию

- **Unix vs Multics.** Multics была амбициозной, «правильной» ОС. Unix была «упрощённым Multics». Победила Unix.
- **C vs Ada.** C — простой язык, Ada — язык с мощной системой типов, контрактами, многозадачностью. C распространился шире.
- **HTTP/1.0 vs OSI.** HTTP — простой текстовый протокол. OSI — семиуровневая модель. HTTP захватил мир.
- **JSON vs XML.** JSON проще, без схем, без неймспейсов. Стал стандартом де-факто.
- **JavaScript vs Java в браузере.** JavaScript был написан за 10 дней. Он победил Java-апплеты.

**Ключевой урок:** не стремись к совершенству в первой версии. Выпусти работающий продукт и итерируй.

---

## Gall's Law — Закон Голла

### Суть принципа GL

> **Работающая сложная система неизменно развилась из работающей простой системы. Сложная система, спроектированная «с нуля», не будет работать и не может быть заставлена работать. Начинайте с работающей простой системы.**

Джон Голл (John Gall), «Systemantics: How Systems Work and Especially How They Fail» (1975). Закон Голла — один из самых глубоких и недооценённых принципов системного мышления.

### Почему это фундаментально

Gall's Law объясняет, почему:

- **BDUF проваливается.** Невозможно спроектировать сложную систему upfront — слишком много неизвестных переменных.
- **Agile работает.** Инкрементальная разработка повторяет естественный путь эволюции сложных систем.
- **Микросервисы нельзя «внедрить».** Они должны вырасти из монолита, когда команда поймёт границы bounded context.
- **Переписывание с нуля рискованно.** Вы теряете все неявные знания, накопленные работающей системой (см. также **Law of Leaky Abstractions**).

### Примеры из индустрии

| Успех (эволюция) | Провал (big bang) |
|------------------|-------------------|
| **Amazon:** микросервисы выросли из монолита Obidos постепенно, сервис за сервисом | **FBI Virtual Case File:** $170M, 5 лет проектирования, 0 работающего кода |
| **Netflix:** миграция в облако заняла 7 лет пошагово | **Healthcare.gov:** запуск «всё и сразу» обернулся катастрофой |
| **Unix:** простая ОС для PDP-7 эволюционировала десятилетиями | **Multics:** амбициозная ОС, так и не ставшая мейнстримом |

### Примеры на Java GL

**Эволюция кеширования — от простого к сложному:**

```java
// Версия 1: простая, работающая — без кеша
public class ProductService {
    private final ProductRepository repository;

    public Product getProduct(Long id) {
        return repository.findById(id)
            .orElseThrow(() -> new ProductNotFoundException(id));
    }
}
```

```java
// Версия 2: добавляем простой HashMap-кеш (система всё ещё простая и работает)
public class ProductService {
    private final ProductRepository repository;
    private final Map<Long, Product> cache = new ConcurrentHashMap<>();

    public Product getProduct(Long id) {
        return cache.computeIfAbsent(id, key ->
            repository.findById(key)
                .orElseThrow(() -> new ProductNotFoundException(key))
        );
    }
}
```

```java
// Версия 3: добавляем TTL-инвалидацию (только когда понадобилось)
public class ProductService {
    private final ProductRepository repository;
    private final Cache<Long, Product> cache = Caffeine.newBuilder()
        .expireAfterWrite(10, TimeUnit.MINUTES)
        .maximumSize(10_000)
        .build();

    public Product getProduct(Long id) {
        return cache.get(id, key ->
            repository.findById(key)
                .orElseThrow(() -> new ProductNotFoundException(key))
        );
    }
}
// Ключевой момент: мы не начинали с Redis, распределённого кеша и инвалидации
// через Kafka. Мы начинали с простого и добавляли сложность по мере необходимости.
```

**Как применить Gall's Law на практике:**

1. **Начните с монолита**, если вы стартап. Разбейте на сервисы, когда появятся независимые команды.
2. **Первый прототип должен быть embarrassingly simple.** Он доказывает, что идея работает.
3. **Не оптимизируйте преждевременно.** Профилировщик покажет, что оптимизировать (см. Pareto Principle).
4. **Добавляйте абстракции по Rule of Three**, а не заранее.

---

## Pareto Principle — Принцип Парето (80/20)

### Суть принципа PP

> **80% следствий происходят из 20% причин.**

Принцип Парето назван в честь итальянского экономиста Вильфредо Парето, который наблюдал, что 80% земли в Италии принадлежит 20% населения. В разработке ПО этот принцип проявляется повсеместно:

- **80% пользователей используют 20% функциональности.**
- **80% багов находятся в 20% кода.**
- **80% времени выполнения занимает 20% кода.**
- **80% дохода приносят 20% клиентов.**
- **80% проблем производительности вызваны 20% запросов/операций.**

### Применение 80/20 в разработке

| Область | Как применить |
|---------|---------------|
| **Приоритизация фич** | Сфокусируйся на 20% фич, которые принесут 80% ценности. Не распыляйся на «длинный хвост». |
| **Оптимизация** | Найди 20% кода, который занимает 80% времени (profiling), и оптимизируй только его. |
| **Исправление багов** | Исправь 20% багов, на которые приходится 80% жалоб пользователей. |
| **Тестирование** | Покрой тестами 20% самых критичных путей — они выполняются 80% времени. |
| **Код-ревью** | Тщательно ревьюи 20% самого сложного/критичного кода. |

---

## Rule of Three — Правило трёх

### Суть принципа RoT

> **Дублирование допустимо один раз. При третьем появлении — абстрагируйся.**

Правило трёх — практическое руководство, балансирующее между DRY и YAGNI:

1. **Первый раз:** пишешь код как есть — это не дублирование, это первое использование.
2. **Второй раз:** видишь похожий код — делаешь заметку, но пока не трогаешь. Возможно, это случайное совпадение.
3. **Третий раз:** появляется то же самое снова — теперь точно ясно, что это паттерн. Абстрагируйся.

Это правило защищает от **преждевременной абстракции** — когда разработчик видит два похожих куска кода и немедленно создаёт иерархию из 5 классов, которая потом не подходит для третьего случая.

### Дублирование vs абстракция

> *«Duplication is far cheaper than the wrong abstraction.»* — Sandi Metz

Неправильная абстракция дороже дублирования, потому что:

- Её сложнее распознать как проблему (она выглядит «правильно»).
- Она искажает дизайн системы, притягивая под себя новые требования.
- Её сложнее удалить — от неё уже зависят другие части системы.

### Примеры RoT

```java
// Первый раз — для User
public class UserCsvExporter {
    public String export(User user) {
        return user.getId() + "," + user.getName() + "," + user.getEmail();
    }
}

// Второй раз — для Product (похоже, но пока не трогаем — Pattern не подтверждён)
public class ProductCsvExporter {
    public String export(Product product) {
        return product.getId() + "," + product.getName() + "," + product.getPrice();
    }
}

// Третий раз — для Order. Паттерн подтверждён — абстрагируемся!
public class OrderCsvExporter {
    public String export(Order order) {
        return order.getId() + "," + order.getStatus() + "," + order.getTotal();
    }
}

// ✅ После третьего раза — обобщаем:
public interface CsvExportable {
    String[] toCsvFields();
}

public class CsvExporter {
    public String export(CsvExportable entity) {
        return String.join(",", entity.toCsvFields());
    }
}
```

---

## The Law of Leaky Abstractions — Закон дырявых абстракций

### Суть принципа LoLA

> **Все нетривиальные абстракции, в той или иной степени, протекают. Абстракция не скрывает сложность полностью — она лишь отодвигает её.**

Закон сформулирован Джоэлем Спольски (Joel Spolsky) в эссе «The Law of Leaky Abstractions» (2002). Это одно из самых важных эссе в истории разработки ПО, объясняющее фундаментальное ограничение любых абстракций.

### Суть проблемы

Абстракция обещает: «Тебе не нужно знать, как это работает внутри. Просто используй этот интерфейс». И пока всё идёт нормально — это правда. Но когда что-то идёт не так, абстракция «протекает» — детали реализации просачиваются наружу и **пользователь ВЫНУЖДЕН разбираться в нижележащем слое**, чтобы решить проблему.

### Примеры утечек абстракций

| Абстракция | Что обещает | Как протекает |
|-----------|-------------|---------------|
| **SQL** | «Пиши декларативные запросы, не думай о том, как данные хранятся» | Медленный запрос → ты изучаешь B-tree, планы выполнения, индексы |
| **TCP** | «Гарантированная доставка пакетов» | Сетевой шторм, таймауты → ты лезешь в TCP congestion control |
| **ORM (Hibernate)** | «Работай с объектами, забудь о SQL» | N+1 запрос → ты лезешь в SQL, который Hibernate сгенерировал |
| **Garbage Collector** | «Не думай об управлении памятью» | Stop-the-world паузы → ты настраиваешь GC, изучаешь поколения |
| **Виртуальная машина** | «Пиши один раз, запускай везде» | Разное поведение на разных ОС → ты читаешь баг-репорты JVM |
| **React/Virtual DOM** | «Не думай о реальном DOM» | Проблемы производительности → ты лезешь в React DevTools, изучаешь reconciliation |

### Примеры на Java LoLA

**Утечка ORM-абстракции — N+1 проблема:**

```java
// ❌ Абстракция протекает: невинный вызов порождает 101 SQL-запрос
@Entity
public class Order {
    @OneToMany(mappedBy = "order", fetch = FetchType.LAZY)
    private List<OrderItem> items;
}

// Сервис:
public List<Order> getCustomerOrders(Long customerId) {
    List<Order> orders = orderRepository.findByCustomerId(customerId); // 1 запрос
    for (Order order : orders) {
        // Каждый вызов order.getItems() генерирует ещё один SQL-запрос!
        log.info("Order {} has {} items", order.getId(), order.getItems().size());
    }
    return orders;
    // Итого: 1 + N запросов. Для 100 заказов = 101 запрос к БД.
    // Разработчик должен знать, как работает FetchType.LAZY — абстракция протекла.
}
```

```java
// ✅ Понимая утечку, используем JOIN FETCH:
@Query("SELECT DISTINCT o FROM Order o JOIN FETCH o.items WHERE o.customer.id = :customerId")
List<Order> findByCustomerId(@Param("customerId") Long customerId);
// Теперь 1 запрос с JOIN, но разработчик вынужден думать на уровне SQL.
```

**Утечка абстракции GC — stop-the-world паузы:**

```java
// ❌ Невинный код создаёт тонны мусора — GC-паузы убивают latency
public List<UserDTO> getActiveUsers() {
    return userRepository.findAll().stream()
        .filter(User::isActive)
        .map(user -> new UserDTO(           // новый объект на каждый User
            user.getId(),
            user.getName(),
            user.getEmail(),
            user.getCreatedAt().toString()   // новый String
        ))
        .toList();                           // новый List
}
// Для 100K пользователей: создаётся 100K UserDTO + 100K String — мусор,
// который GC должен собрать. В высоконагруженной системе это вызывает
// измеримые stop-the-world паузы. Абстракция GC протекает.
```

```java
// ✅ Учёт реальности GC: пулинг объектов, переиспользование
public List<UserDTO> getActiveUsers() {
    // Используем проекцию на уровне БД, не создавая промежуточные User
    return userRepository.findActiveUserDTOs(); // только нужные поля
}
```

### Следствия для разработчика

1. **Знай слой под абстракцией.** Разработчик на Spring должен понимать, как работает JDBC и SQL. Разработчик на React должен понимать DOM.
2. **Абстракции экономят время, но не освобождают от понимания.** Они — ускоритель, а не замена знаний.
3. **Не наращивай слои без необходимости.** Каждый новый слой абстракции — ещё одна потенциальная утечка.
4. **Full-stack полезен не потому, что ты пишешь и frontend, и backend.** А потому, что, зная весь стек, ты видишь утечки и понимаешь корневые причины.

> *«One of the reasons that engineering is hard is that abstractions leak, and the only way to cope with them is to understand the layers beneath.»* — Joel Spolsky

---

## Boy Scout Rule

### Суть принципа BSR

> **Оставь код чище, чем он был до твоего прихода.**

Правило бойскаута сформулировано Робертом Мартином в книге «Clean Code». Идея проста: каждый раз, когда ты работаешь с участком кода (фикс бага, добавление фичи, код-ревью), сделай небольшое улучшение — такое, которое не меняет поведение, но делает код чище.

### Практическое применение BSR

**Примеры небольших улучшений:**

- Переименование неясной переменной (`d` → `daysSinceLastLogin`).
- Извлечение магического числа в константу (`if (status == 3)` → `if (status == OrderStatus.CANCELLED)`).
- Разделение метода, который делает «и то, и это», на два.
- Добавление `final` к переменной, которая не должна переприсваиваться.
- Удаление закомментированного кода.
- Добавление javadoc к публичному методу.
- Замена `for`-цикла на `Stream API`, где это уместно.
- Добавление недостающего unit-теста на граничный случай.

**Что НЕ является Boy Scout Rule:**

- Полный рефакторинг модуля (это отдельная задача).
- Изменение поведения (это фича или баг-фикс).
- Переписывание «потому что мне не нравится стиль» (без объективных причин).

---

## Broken Windows Theory — Теория разбитых окон

### Суть принципа BWT

> **Одно «разбитое окно» в коде (грязный хак, пропущенный тест, закомментированный код) провоцирует появление новых «разбитых окон». Беспорядок распространяется экспоненциально.**

Теория разбитых окон (Broken Windows Theory) пришла из криминологии (Джеймс Уилсон, Джордж Келлинг, 1982). Суть: если в здании разбито одно окно и его не заменяют, вскоре будут разбиты все окна. Видимые признаки беспорядка провоцируют дальнейший вандализм.

В разработке ПО этот принцип работает точно так же:

- В модуле с 50% покрытия тестами никто не будет писать тесты на новую фичу.
- В классе с методом на 300 строк никто не будет рефакторить — проще добавить ещё 50 строк.
- В проекте без статического анализатора никто не исправляет мелкие warning'и — их накапливаются тысячи.

### Примеры проявления в кодовой базе

| Признак | Цепная реакция |
|---------|---------------|
| Один `System.out.println` вместо логгера | Через месяц — десятки `println` в разных классах |
| Один метод без теста (в модуле с покрытием 95%) | Через месяц — 10 методов без тестов. «Ну, здесь же тоже не покрыто» |
| Один комментарий `// FIXME: переделать потом` | Через год — 50 FIXME, ни один не исправлен |
| Один `@SuppressWarnings("unchecked")` | Через месяц — десятки suppressor'ов, реальные проблемы скрыты |

### Как бороться с разбитыми окнами

1. **Boy Scout Rule — главный инструмент.** Каждый коммит оставляет код чище. Разбитое окно, замеченное при ревью, должно быть immediately исправлено.
2. **Zero-tolerance к определённым нарушениям.** Договоритесь в команде: 「`System.out.println` в production-коде = автоматический -1 на code review」.
3. **Статический анализ в CI.** Checkstyle, SonarQube, SpotBugs не дают «разбитым окнам» попасть в `main`. Падение билда при новом warning'е — мощный сдерживающий фактор.
4. **Выделяйте время на «уборку».** 10-20% каждого спринта на устранение технического долга. Если этого не делать, долг растёт экспоненциально.
5. **Лидерство примером.** Если техлид рефакторит и чистит код — команда будет делать то же. Если техлид говорит «потом» — команда последует примеру.

### Связь с другими принципами (Broken Windows): каждое действие разработчика либо чинит, либо разбивает окно.
- **Technical Debt** — накопленные «разбитые окна» и есть технический долг. Проценты по нему — замедление разработки.
- **Principle of Least Astonishment** — «разбитое окно» в API удивляет пользователя и провоцирует его писать обходные пути (новые разбитые окна).

---

## Brooks' Law — Закон Брукса

### Суть принципа BL

> **Если проект не укладывается в сроки, добавление рабочей силы задержит его ещё больше.**

Фредерик Брукс, «Мифический человеко-месяц» (The Mythical Man-Month, 1975).

### Мифический человеко-месяц

Брукс наблюдал, что в программировании **человеко-месяцы нельзя просто складывать**. Причины:

| Причина | Описание |
|---------|----------|
| **Накладные расходы на коммуникацию** | N разработчиков имеют N(N-1)/2 каналов коммуникации. 5 чел = 10 каналов, 50 чел = 1225 каналов. |
| **Время на onboarding** | Новый разработчик тратит недели/месяцы на вхождение в проект, отвлекая опытных коллег. |
| **Распараллеливание не бесконечно** | Некоторые задачи последовательны по природе (sequential constraints): нельзя построить крышу до фундамента. |
| **Дробление задач** | Не всякую задачу можно разделить на N независимых подзадач. |

**Формула Брукса:**

> Время = (Объём работы) / (Количество разработчиков) + Накладные расходы(Количество разработчиков)

Накладные расходы растут нелинейно, поэтому после некоторого порога добавление людей **увеличивает** общее время.

### Следствия для управления проектами

- **Не пытайся «добавить людей» в горящий проект** — это типичная ошибка менеджмента.
- **Инвестируй в качество и автоматизацию**, а не в количество разработчиков.
- **Малые команды эффективнее.** Amazon «Two-Pizza Team» — команда, которую можно накормить двумя пиццами (6-8 человек).
- **1/3 времени — проектирование.** Брукс рекомендовал тратить 1/3 времени на дизайн, 1/6 на написание кода, 1/4 на тестирование компонентов, 1/4 на системное тестирование.

---

## Conway's Law — Закон Конвея

### Суть принципа CL

> **Организации проектируют системы, которые повторяют структуру коммуникации в этих организациях.**

Мелвин Конвей, 1968. Закон Конвея гласит: архитектура программной системы будет отражать организационную структуру компании, которая её создаёт.

**Примеры:**

- Компания с 4 независимыми командами разработает систему из 4 модулей/сервисов.
- Если команда frontend отделена от backend — API между ними будет жёстким и формальным.
- Если разработчики и тестировщики в разных командах — появится формальный процесс передачи сборок.

### Обратный закон Конвея

> **Если вы хотите изменить архитектуру системы — измените структуру команд.**

Обратный закон Конвея (Reverse Conway's Law / Inverse Conway Maneuver) — стратегия, популяризованная в микросервисном движении. Если вы хотите микросервисную архитектуру — организуйте кросс-функциональные команды вокруг бизнес-возможностей (business capabilities), а не вокруг технологических слоёв (frontend-команда, backend-команда, БД-команда).

### Влияние на микросервисную архитектуру

Закон Конвея — один из аргументов в пользу микросервисов: если у вас несколько независимых команд, они естественным образом создадут независимо развёртываемые сервисы. Монолит же требует тесной координации между командами, что противоречит автономии.

---

## Parkinson's Law — Закон Паркинсона

### Суть принципа PL

> **Работа занимает всё время, отпущенное на неё.**

Сирил Норткот Паркинсон, 1955. Если задаче выделено 2 дня, она будет сделана за 2 дня. Если той же задаче выделено 2 недели, она тоже будет сделана за 2 недели — но с большим количеством «важных» совещаний, рефакторингов и доработок, не увеличивающих ценность.

### Применение в разработке PL

- **Оценки должны быть честными, но не завышенными.** Разработчик, оценивший задачу в 5 дней и получивший 10, потратит 10.
- **Спринты фиксированной длины** (Scrum) создают естественный ограничитель: работа должна быть завершена за спринт.
- **Timeboxing.** Выдели фиксированное время на задачу (spike, исследование) и остановись, когда время вышло.
- **Правило 90/90.** Первые 90% работы занимают 90% времени. Оставшиеся 10% работы занимают ещё 90% времени. (Шутка с глубоким смыслом.)

---

## Principle of Least Privilege

### Суть принципа PoLP

> **Каждый компонент системы должен иметь минимальный набор прав, необходимый для выполнения его функций.**

Принцип наименьших привилегий — фундаментальный принцип безопасности. В контексте разработки ПО он применим не только к правам доступа, но и к видимости кода.

### Применение в архитектуре безопасности

**На уровне кода (модификаторы доступа):**

```java
// ✅ Минимальные права: поля private, доступ через методы
public class BankAccount {
    private BigDecimal balance; // private — недоступен извне

    public void deposit(BigDecimal amount) {
        // Контролируемое изменение
        balance = balance.add(amount);
    }

    // Геттер есть, сеттера нет — баланс нельзя изменить произвольно
    public BigDecimal getBalance() {
        return balance;
    }
}
```

**На уровне системы:**

| Уровень | Применение |
|---------|------------|
| **База данных** | Сервис заказов имеет доступ к таблице orders, но не к таблице payments |
| **Сеть** | Микросервис A может обращаться к микросервису B, но не к C |
| **CI/CD** | Сборка имеет доступ к репозиторию исходного кода, но не к production-окружению |
| **Пользователи** | Пользователь с ролью «менеджер» видит отчёты своего отдела, но не всех отделов |

---

## Principle of Least Astonishment

### Суть принципа PoLA

> **Система должна вести себя так, как ожидает пользователь (или разработчик). Не удивляй.**

Принцип наименьшего удивления (PoLA, также Principle of Least Surprise) применим как к пользовательским интерфейсам, так и к API, библиотекам и поведению кода.

### Примеры нарушения PoLA

**Неожиданное поведение API:**

```java
// ❌ Нарушение PoLA: метод getActiveUsers() возвращает null, а не пустой список
public List<User> getActiveUsers() {
    List<User> users = repository.findByActive(true);
    if (users.isEmpty()) {
        return null; // ПОЧЕМУ? Никто не ожидает null из метода, начинающегося с get...
    }
    return users;
}
// Клиент:
List<User> users = userService.getActiveUsers();
users.forEach(...); // NPE! Никто не ожидал null из метода, возвращающего List
```

```java
// ✅ Ожидаемо: пустая коллекция
public List<User> getActiveUsers() {
    List<User> users = repository.findByActive(true);
    return users != null ? users : List.of(); // или return emptyList()
}
```

**Побочный эффект в геттере:**

```java
// ❌ Нарушение PoLA: геттер изменяет состояние
public class Counter {
    private int count = 0;

    public int getCount() {
        logAccess();       // побочный эффект
        return count++;
    }
}
// Разработчик ожидает, что getCount() просто возвращает значение.
// Он вызывает его в логах, в дебаге, в условиях — и ломает логику счётчика.
```

**Соглашение об именовании:**

```java
// ❌ Нарушение PoLA: createUser возвращает boolean (успех/неудача)
//    Ожидается, что create... возвращает созданный объект
public boolean createUser(UserDto dto) { ... }

// ✅ Ожидаемо:
public User createUser(UserDto dto) throws UserCreationException { ... }
// или
public Try<User> createUser(UserDto dto) { ... }
```

### Рекомендации PoLA

- **Следуй конвенциям платформы.** В Java: геттеры — `getX()`, сеттеры — `setX()`, билдеры — `Builder`, фабрики — `of()`, `create()`.
- **Не mixing уровни абстракции.** Метод не должен делать «грязную работу», если его название обещает чистое действие.
- **Документируй неожиданное.** Если метод бросает `UncheckedException` — укажи это в javadoc `@throws`.
- **Симметричность.** Если есть `open()` — должен быть `close()`. Если есть `acquire()` — должен быть `release()`.

---

## CQS — Command Query Separation

### Суть принципа CQS

> **Каждый метод должен быть либо командой (изменяет состояние, не возвращает значение), либо запросом (возвращает значение, не изменяет состояние). Но не тем и другим одновременно.**

Command Query Separation (CQS) сформулирован Бертраном Мейером в книге «Object-Oriented Software Construction» (1988).

- **Command (команда)** — метод, который изменяет состояние системы и **не возвращает значение** (void). Побочные эффекты допустимы и ожидаемы.
- **Query (запрос)** — метод, который **возвращает значение** и не изменяет наблюдаемое состояние системы. Побочных эффектов быть не должно.

**Простое правило:** спрашивая вопрос, ты не должен менять ответ.

### CQS vs CQRS

CQS и CQRS — разные концепции, хотя и связанные:

| | CQS | CQRS |
|---|-----|------|
| **Уровень** | Метод | Архитектура системы |
| **Разделение** | Методы делятся на команды и запросы | Модель на запись (Command Model) и модель на чтение (Query Model) — разные БД |
| **Сложность** | Дисциплина написания методов | Архитектурный паттерн |
| **Применение** | Всегда и везде | Высоконагруженные системы со сложными запросами |

### Примеры на Java CQS

**Нарушение CQS — метод и возвращает, и изменяет:**

```java
// ❌ Нарушение CQS: pop() и извлекает элемент, и удаляет его из стека
public class BrokenStack<T> {
    private final Deque<T> items = new ArrayDeque<>();

    public T pop() {
        if (items.isEmpty()) {
            throw new EmptyStackException();
        }
        T item = items.removeLast(); // команда: удаление
        log.debug("Popped: {}", item); // ещё один побочный эффект
        return item; // запрос: возврат значения
    }
    // Проблема: нельзя просто проверить верхний элемент, не изменив стек.
    // Отладка: вызов stack.pop() в дебаггере меняет состояние!
}
```

```java
// ✅ CQS: разделение на команду (pop) и запрос (peek)
public class Stack<T> {
    private final Deque<T> items = new ArrayDeque<>();

    // Query: только возвращает, не изменяет
    public T peek() {
        if (items.isEmpty()) {
            throw new EmptyStackException();
        }
        return items.peekLast();
    }

    // Command: только изменяет, не возвращает (void)
    public void pop() {
        if (items.isEmpty()) {
            throw new EmptyStackException();
        }
        items.removeLast();
    }

    // Command + Query вместе, когда это действительно нужно
    // (нарушение CQS, но осознанное и задокументированное):
    public T popAndGet() {
        T item = peek();
        pop();
        return item;
    }
}
```

**Соблюдение CQS в сервисах:**

```java
// ✅ Команды — void, изменяют состояние
@Service
public class OrderService {

    // Command: изменяет состояние БД
    @Transactional
    public void placeOrder(OrderRequest request) {
        Order order = orderFactory.create(request);
        orderRepository.save(order);
        eventPublisher.publish(new OrderPlacedEvent(order));
    }

    // Command: изменяет состояние БД
    @Transactional
    public void cancelOrder(Long orderId, String reason) {
        Order order = findOrderOrThrow(orderId);
        order.cancel(reason);
        orderRepository.save(order);
    }

    // Query: возвращает данные, не изменяет состояние
    @Transactional(readOnly = true)
    public OrderDTO getOrder(Long orderId) {
        return orderRepository.findById(orderId)
            .map(orderMapper::toDto)
            .orElseThrow(() -> new OrderNotFoundException(orderId));
    }
}
```

### Связь с функциональным программированием

CQS естественным образом реализуется в функциональном программировании, где:

- **Чистые функции** — это Queries (нет побочных эффектов, возвращают значение).
- **Побочные эффекты** изолируются и явно обозначаются (монады IO, Effect).

В Java это отражается в использовании `@Transactional(readOnly = true)` для запросов и `@Transactional` для команд.

---

## IoC — Inversion of Control

### Суть принципа IoC

> **Не ты управляешь потоком исполнения — фреймворк управляет. Не ты создаёшь зависимости — контейнер их предоставляет.**

Inversion of Control (IoC) — принцип, при котором поток управления программы инвертирован: вместо того чтобы пользовательский код вызывал библиотечные функции, фреймворк вызывает пользовательский код в нужный момент.

IoC проявляется в нескольких формах:

1. **Dependency Injection (DI)** — зависимости предоставляются извне.
2. **Template Method** — базовый класс определяет скелет алгоритма, наследники заполняют шаги.
3. **Event-driven architecture** — код реагирует на события, а не вызывает функции напрямую.
4. **Callback-функции / лямбды** — передача поведения как параметра.

### Hollywood Principle

> **«Don't call us, we'll call you.»** — Не звоните нам, мы сами вам позвоним.

Принцип Голливуда — это метафора IoC: ваш код не вызывает фреймворк; фреймворк вызывает ваш код, когда сочтёт нужным.

**Примеры «звонков» фреймворка:**

- Spring вызывает ваш `@PostConstruct` метод после создания бина.
- JUnit вызывает ваш `@Test` метод, когда запускается тест.
- Servlet-контейнер вызывает ваш `doGet()`, когда приходит HTTP-запрос.
- Hibernate вызывает ваши `@PrePersist` / `@PostLoad` колбэки в нужные моменты жизненного цикла сущности.

### IoC-контейнеры

IoC-контейнер (в Java-мире — Spring IoC Container) — это фабрика, которая:

1. Создаёт объекты (бины).
2. Разрешает их зависимости.
3. Управляет их жизненным циклом.

```java
// Без IoC: класс сам управляет своими зависимостями
public class OrderService {
    private final OrderRepository repository;

    public OrderService() {
        // Класс сам создаёт зависимость — жёсткая связь
        this.repository = new MySQLOrderRepository(
            new DataSource(),
            new Logger(),
            new CacheManager()
        );
    }
}
```

```java
// С IoC (Spring): зависимости предоставляются извне
@Service
public class OrderService {
    private final OrderRepository repository;

    // Конструктор принимает зависимость — Spring её предоставит
    public OrderService(OrderRepository repository) {
        this.repository = repository;
    }
}
// Spring контейнер:
// 1. Находит все @Component/@Service/@Repository
// 2. Создаёт экземпляры
// 3. Разрешает зависимости и внедряет их (constructor injection)
// 4. Управляет скоупами (singleton, prototype, request, session)
```

### Примеры на Java IoC

**IoC через Template Method:**

```java
// IoC: execute() вызывает абстрактные шаги в нужном порядке
public abstract class DataMigration {
    // Шаблонный метод — скелет алгоритма
    public final void execute() {
        logStart();
        validateSource();
        List<Record> records = extract();
        List<Record> transformed = transform(records);
        load(transformed);
        logCompletion();
    }

    // Шаги, которые будут реализованы в подклассах (их «вызовет» execute())
    protected abstract List<Record> extract();
    protected abstract List<Record> transform(List<Record> records);
    protected abstract void load(List<Record> records);

    // Общие шаги в базовом классе
    private void logStart() { /* ... */ }
    private void validateSource() { /* ... */ }
    private void logCompletion() { /* ... */ }
}

// Пользовательский код: только специфичная логика
public class UserMigration extends DataMigration {
    @Override
    protected List<Record> extract() { /* из старой БД */ }
    @Override
    protected List<Record> transform(List<Record> r) { /* маппинг полей */ }
    @Override
    protected void load(List<Record> records) { /* в новую БД */ }
}

// Фреймворк «вызывает» пользовательский код:
new UserMigration().execute();
```

### IoC и Dependency Injection

**IoC — принцип. DI — одна из реализаций IoC.** Другие реализации IoC:

| Реализация IoC | Пример |
|----------------|--------|
| **Dependency Injection** | Spring DI, Guice, CDI |
| **Service Locator** | JNDI, OSGi Service Registry |
| **Template Method** | `AbstractApplicationContext.refresh()` в Spring |
| **Events / Callbacks** | `@EventListener`, `ApplicationListener` |
| **Aspect-Oriented Programming** | `@Transactional`, `@Cacheable` — фреймворк перехватывает вызовы |

---

## Design by Contract — Проектирование по контракту

### Суть принципа DbC

> **Каждый метод — это контракт. Предусловия — что метод требует от вызывающего. Постусловия — что метод гарантирует в результате. Инварианты — что всегда истинно для объекта.**

Design by Contract (DbC) — концепция, сформулированная Бертраном Мейером в книге «Object-Oriented Software Construction» (1988) и реализованная в языке Eiffel. Хотя в Java нет встроенной поддержки DbC, принцип применим через аннотации, валидацию и дисциплину кодирования.

### Три столпа контракта

| Элемент | Определение | Нарушение означает |
|---------|-------------|-------------------|
| **Предусловия** (preconditions) | Что должно быть истинно ДО вызова метода | Баг в вызывающем коде |
| **Постусловия** (postconditions) | Что гарантирует метод ПОСЛЕ выполнения | Баг в методе |
| **Инварианты** (invariants) | Что всегда истинно для объекта (до и после каждого публичного метода) | Баг в классе |

### Связь с другими принципами (DbC)

Design by Contract — это **объединяющая концепция** для многих принципов:

| Принцип | Как связан с DbC |
|---------|-----------------|
| **LSP** | Подтип не должен усиливать предусловия и ослаблять постусловия родителя |
| **Fail Fast** | Проверка предусловий в начале метода = Fail Fast |
| **CQS** | Команды меняют состояние (постусловие: состояние изменилось), запросы — нет (постусловие: состояние неизменно) |
| **PoLA** | Контракт делает поведение предсказуемым — не удивляет |
| **TDA** | Объект инкапсулирует проверку своих инвариантов |

### Примеры на Java DbC

**Контракт через аннотации (JSR 380 — Bean Validation):**

```java
// Контракт через аннотации: предусловия + постусловия
public class BankAccount {
    private BigDecimal balance = BigDecimal.ZERO;

    /**
     * Предусловия:
     * - amount > 0
     * - amount не null
     *
     * Постусловия:
     * - balance увеличится ровно на amount
     * - транзакция будет записана в историю
     */
    public void deposit(@NotNull @Positive BigDecimal amount) {
        BigDecimal oldBalance = this.balance; // для проверки постусловия
        this.balance = this.balance.add(amount);
        history.record(TransactionType.DEPOSIT, amount);

        // Постусловие: balance увеличился ровно на amount
        assert this.balance.equals(oldBalance.add(amount))
            : "Postcondition failed: balance should increase by " + amount;
    }

    /**
     * Предусловия:
     * - amount > 0
     * - amount <= balance (достаточно средств)
     *
     * Постусловия:
     * - balance уменьшится ровно на amount
     * - возвращённый результат > 0
     */
    public WithdrawalResult withdraw(@NotNull @Positive BigDecimal amount) {
        // Проверка предусловия
        if (amount.compareTo(balance) > 0) {
            throw new InsufficientFundsException(balance, amount);
        }

        BigDecimal oldBalance = this.balance;
        this.balance = this.balance.subtract(amount);
        history.record(TransactionType.WITHDRAWAL, amount);

        // Проверка постусловия
        assert this.balance.equals(oldBalance.subtract(amount))
            : "Postcondition failed";

        return new WithdrawalResult(amount, this.balance);
    }

    // Инвариант: баланс никогда не может быть отрицательным
    // (может проверяться в assert или через AOP)
}
```

**Контракт через javadoc + assertions:**

```java
/**
 * Сортирует список и возвращает новый (не модифицирует оригинал).
 *
 * @param list исходный список, не null
 * @param <T> тип элементов, реализующий Comparable
 * @return новый отсортированный список (не null, тот же размер)
 * @throws NullPointerException если list == null
 */
public <T extends Comparable<T>> List<T> sortCopy(@NotNull List<T> list) {
    Objects.requireNonNull(list, "precondition: list != null"); // предусловие

    List<T> sorted = new ArrayList<>(list);
    Collections.sort(sorted);

    // Постусловия (assert, не выполняются в production по умолчанию):
    assert sorted != null : "postcondition: result != null";
    assert sorted.size() == list.size() : "postcondition: same size";
    assert isSorted(sorted) : "postcondition: result is sorted";

    return sorted;
}
```

**Контракт с проверкой инвариантов:**

```java
public class Temperature {
    private static final double ABSOLUTE_ZERO_CELSIUS = -273.15;
    private double celsius;

    public Temperature(double celsius) {
        // Предусловие конструктора
        if (celsius < ABSOLUTE_ZERO_CELSIUS) {
            throw new IllegalArgumentException(
                "Temperature cannot be below absolute zero: " + celsius);
        }
        this.celsius = celsius;
        checkInvariant(); // проверяем инвариант после создания
    }

    public void setCelsius(double celsius) {
        if (celsius < ABSOLUTE_ZERO_CELSIUS) {
            throw new IllegalArgumentException(
                "Temperature cannot be below absolute zero: " + celsius);
        }
        this.celsius = celsius;
        checkInvariant();
    }

    public double getCelsius() {
        return celsius;
    }

    // Инвариант: температура никогда не ниже абсолютного нуля
    private void checkInvariant() {
        if (celsius < ABSOLUTE_ZERO_CELSIUS) {
            throw new IllegalStateException(
                "Invariant violated: temperature " + celsius + " below absolute zero");
        }
    }
}
```

### DbC на практике

1. **Документируй контракт в javadoc** — `@param`, `@return`, `@throws`.
2. **Используй `Objects.requireNonNull()`** как минимальную проверку предусловий.
3. **Используй `assert`** для проверки постусловий и инвариантов в development/test.
4. **Bean Validation (`@NotNull`, `@Positive`, `@Size`)** — декларативные предусловия.
5. **Не проверяй предусловия, которые не являются частью контракта.** Например, не проверяй `null` на результат `Collections.sort()` — он никогда не возвращает `null`.

---

## GRASP — General Responsibility Assignment Software Patterns

### Обзор GRASP

**GRASP** (General Responsibility Assignment Software Patterns) — набор из 9 принципов (паттернов), описывающих, как распределять ответственности между классами в объектно-ориентированной системе. Сформулированы Крэйгом Ларманом в книге «Applying UML and Patterns» (2004).

В отличие от GoF-паттернов (которые решают конкретные задачи дизайна), GRASP отвечает на фундаментальный вопрос: **какому классу поручить ту или иную ответственность?**

Девять GRASP-паттернов:

1. **Information Expert** (Информационный эксперт)
2. **Creator** (Создатель)
3. **Controller** (Контроллер)
4. **Low Coupling** (Низкая связанность)
5. **High Cohesion** (Высокая связность)
6. **Polymorphism** (Полиморфизм)
7. **Pure Fabrication** (Чистая выдумка / Искусственный класс)
8. **Indirection** (Косвенность / Посредник)
9. **Protected Variations** (Защита от изменений)

---

### Information Expert

> **Ответственность должна быть назначена тому объекту, который обладает информацией, необходимой для её выполнения.**

Information Expert — базовый принцип: метод должен находиться в том классе, у которого есть данные для его реализации.

```java
// ❌ Нарушение: OrderCalculator имеет ответственность, но не имеет данных
public class OrderCalculator {
    public BigDecimal calculateTotal(Order order) {
        // Вытягивает все данные из Order — нарушение инкапсуляции
        BigDecimal total = BigDecimal.ZERO;
        for (Item item : order.getItems()) {
            total = total.add(
                item.getPrice().multiply(BigDecimal.valueOf(item.getQuantity()))
            );
        }
        return total;
    }
}

// ✅ Information Expert: Order сам считает свой итог — у него есть данные
public class Order {
    private List<Item> items;

    public BigDecimal calculateTotal() {
        return items.stream()
            .map(Item::getSubtotal)
            .reduce(BigDecimal.ZERO, BigDecimal::add);
    }
}
```

---

### Creator

> **Класс B должен создавать экземпляры класса A, если B содержит A, агрегирует A, использует A или имеет данные для инициализации A.**

Принцип определяет, кто отвечает за создание объектов.

```java
// ✅ Creator: Order создаёт OrderItem, потому что агрегирует их
public class Order {
    private final List<OrderItem> items = new ArrayList<>();

    public OrderItem addItem(Product product, int quantity) {
        OrderItem item = new OrderItem(product, quantity); // Order — Creator
        items.add(item);
        return item;
    }
}

// ✅ Creator: фабрика создаёт объекты, потому что имеет данные для инициализации
public class InvoiceFactory {
    public Invoice createInvoice(Order order) {
        // Фабрика знает, как собрать Invoice из Order
        return Invoice.builder()
            .orderId(order.getId())
            .items(order.getItems())
            .total(order.calculateTotal())
            .build();
    }
}
```

---

### Controller

> **Назначайте ответственность за обработку внешних событий (запросов) классу, который представляет собой сценарий использования (use case) или фасад системы.**

Controller — это точка входа для обработки запроса. Он НЕ выполняет бизнес-логику, а делегирует её.

Два типа контроллеров:

1. **Facade Controller** — один контроллер на всю подсистему (подходит для небольших систем).
2. **Use-Case Controller** — отдельный контроллер на каждый сценарий использования (предпочтительнее для крупных систем).

```java
// ✅ Use-Case Controller: обрабатывает запрос, делегирует работу
@RestController
@RequestMapping("/orders")
public class OrderController { // ← Controller (GRASP)
    private final PlaceOrderUseCase placeOrderUseCase;

    @PostMapping
    public ResponseEntity<OrderResponse> placeOrder(@Valid @RequestBody OrderRequest req) {
        // Контроллер не содержит бизнес-логики — он только делегирует
        OrderResult result = placeOrderUseCase.execute(req);
        return ResponseEntity.ok(OrderResponse.from(result));
    }
}
```

**Признаки «раздутого контроллера» (Bloated Controller):**

- Контроллер содержит бизнес-логику (расчёты, валидацию бизнес-правил).
- Контроллер напрямую работает с репозиториями.
- Контроллер имеет более 5-7 зависимостей.

---

### Low Coupling

> **Распределяйте ответственность так, чтобы связанность (coupling) между классами была минимальной.**

Low Coupling — цель, к которой ведут многие другие принципы (DIP, Law of Demeter, Program to Interface).

```java
// ❌ High Coupling: сервис жёстко привязан к конкретным реализациям
public class ReportGenerator {
    private final MySQLDataSource dataSource = new MySQLDataSource();
    private final SmtpEmailSender emailSender = new SmtpEmailSender();
    private final FileSystemStorage storage = new FileSystemStorage("/tmp");
}

// ✅ Low Coupling: зависит от абстракций
public class ReportGenerator {
    private final DataSource dataSource;      // интерфейс
    private final EmailSender emailSender;     // интерфейс
    private final Storage storage;             // интерфейс
}
```

---

### High Cohesion

> **Распределяйте ответственности так, чтобы элементы внутри класса были тесно связаны по смыслу.**

High Cohesion — противоположность «классу-свалке». Все методы и поля класса должны относиться к одной предметной области.

```java
// ❌ Low Cohesion: класс делает всё подряд
public class UserManager {
    public void registerUser(UserDto dto) { /* ... */ }
    public void sendEmail(String to, String subject, String body) { /* ... */ }
    public void generatePdfReport(List<User> users) { /* ... */ }
    public void backupDatabase() { /* ... */ }
    public BigDecimal calculateTax(BigDecimal amount) { /* ... */ }
}

// ✅ High Cohesion: разделено по ответственностям
public class UserRegistrationService {
    public void registerUser(UserDto dto) { /* ... */ }
}
public class EmailService {
    public void sendEmail(String to, String subject, String body) { /* ... */ }
}
public class ReportService {
    public byte[] generateUserReport(List<User> users) { /* ... */ }
}
```

---

### Polymorphism

> **Когда поведение зависит от типа, назначайте ответственность за это поведение полиморфным методам типа, а не условным операторам клиента.**

```java
// ❌ Условная логика по типу — признак нарушения полиморфизма
public BigDecimal calculateDiscount(Customer customer) {
    return switch (customer.getType()) {
        case REGULAR -> BigDecimal.ZERO;
        case SILVER -> new BigDecimal("0.05");
        case GOLD -> new BigDecimal("0.10");
        case PLATINUM -> new BigDecimal("0.15");
    };
    // При добавлении DIAMOND-уровня нужно искать все switch по CustomerType
}

// ✅ Полиморфизм: каждый тип сам знает свою скидку
public interface CustomerType {
    BigDecimal getDiscountRate();
}

public class RegularCustomer implements CustomerType {
    public BigDecimal getDiscountRate() { return BigDecimal.ZERO; }
}
public class GoldCustomer implements CustomerType {
    public BigDecimal getDiscountRate() { return new BigDecimal("0.10"); }
}
// Новый DIAMOND-уровень — просто новый класс, существующий код не меняется
```

---

### Pure Fabrication

> **Если назначение ответственности через Information Expert нарушает Low Coupling/High Cohesion, создайте искусственный класс, который не соответствует никакой сущности предметной области.**

Pure Fabrication — это «выдуманный» класс, существующий только для того, чтобы сохранить дизайн чистым. Примеры: репозитории, фабрики, сервисы.

```java
// ✅ Pure Fabrication: OrderRepository не существует в реальном мире,
//    но он спасает Order от зависимости от JDBC
public interface OrderRepository {
    void save(Order order);
    Optional<Order> findById(Long id);
    List<Order> findByCustomerId(Long customerId);
}
// Без Pure Fabrication: Order сам бы сохранял себя в БД,
// нарушая High Cohesion (заказ + SQL = две разные ответственности)
```

---

### Indirection

> **Введите промежуточный объект для связи между двумя компонентами, которые не должны зависеть друг от друга напрямую.**

Indirection — это паттерн «посредник». Он проявляется в:

- Controller из MVC (между UI и моделью).
- Репозиторий (между доменом и БД).
- Event Bus / Message Queue (между сервисами).
- Adapter из GoF.

```java
// ✅ Indirection: репозиторий как посредник между сервисом и БД
@Service
public class UserService {
    private final UserRepository repository; // Посредник

    public User findUser(Long id) {
        return repository.findById(id).orElseThrow(...);
    }
    // UserService не знает о JDBC, JPA, SQL — только о репозитории
}
```

---

### Protected Variations

> **Защитите систему от изменений в нестабильных компонентах с помощью абстракций.**

Protected Variations — обобщение принципов OCP (Open/Closed Principle) и Encapsulate What Varies.

```java
// ✅ Protected Variations: интерфейс защищает от смены платёжного провайдера
public interface PaymentGateway {
    PaymentResult process(PaymentRequest request);
}

// Если завтра сменится Stripe на PayPal — меняется только реализация,
// клиентский код (OrderService) не трогается
```

---

## The Twelve-Factor App

### Обзор методологии

**The Twelve-Factor App** — методология построения Software-as-a-Service приложений, сформулированная разработчиками Heroku (2011). Она описывает 12 принципов, которым должно следовать современное облачное приложение.

### 12 факторов

| # | Фактор | Суть |
|---|--------|------|
| **I. Codebase** | Один код, отслеживаемый в системе контроля версий, — много развёртываний | Одно приложение = один репозиторий. Несколько приложений не делят один репозиторий. |
| **II. Dependencies** | Явно объявляйте и изолируйте зависимости | Maven/Gradle для Java. Никаких «системных» библиотек, на которые рассчитывает код. |
| **III. Config** | Конфигурация — в переменных окружения | Никаких `application-prod.yml` в репозитории. Конфиги хранятся в среде выполнения (`env vars`). |
| **IV. Backing Services** | Внешние сервисы — подключаемые ресурсы | БД, очереди, SMTP — всё это ресурсы, подключаемые через URL. Смена PostgreSQL на MySQL = смена URL. |
| **V. Build, Release, Run** | Строго разделяйте стадии сборки и выполнения | Build → Release → Run. Релиз — иммутабельный артефакт (jar + конфиг). |
| **VI. Processes** | Приложение — один или несколько stateless-процессов | Никаких sticky-сессий. Состояние — во внешнем хранилище (БД, Redis). |
| **VII. Port Binding** | Экспортируйте сервисы через привязку портов | Приложение само слушает порт (embedded Tomcat/Netty), а не делегирует это внешнему серверу (Tomcat как WAR). |
| **VIII. Concurrency** | Масштабируйтесь через модель процессов | Горизонтальное масштабирование: больше процессов, а не больше потоков в одном процессе. |
| **IX. Disposability** | Процессы должны запускаться и останавливаться быстро и корректно | Graceful shutdown: завершить текущие запросы, освободить ресурсы. |
| **X. Dev/Prod Parity** | Сокращайте разрыв между разработкой и продакшеном | Одинаковые БД, одинаковые брокеры сообщений, одинаковые ОС. Никаких «на проде Oracle, а локально H2». |
| **XI. Logs** | Логи — это потоки событий | Приложение пишет в stdout. Агрегация, хранение, анализ — забота платформы (ELK, Loki, CloudWatch). |
| **XII. Admin Processes** | Административные задачи — одноразовые процессы | Миграции БД, скрипты — запускаются как отдельные процессы в том же окружении, что и приложение. |

### Ключевые факторы с Java-примерами

**Фактор III — Config (строгое отделение конфигурации от кода):**

```java
// ❌ Нарушение: конфигурация в коде или в репозитории
@Component
public class PaymentService {
    private static final String API_KEY = "sk_live_abc123";   // секрет в коде!
    private static final String API_URL = "https://api.stripe.com"; // может, но жёстко
}
```

```java
// ✅ Twelve-Factor: конфигурация из переменных окружения
@Component
public class PaymentService {
    private final String apiKey;
    private final String apiUrl;

    public PaymentService(
        @Value("${PAYMENT_API_KEY}") String apiKey,        // из env vars (K8s Secret / vault)
        @Value("${PAYMENT_API_URL:https://api.stripe.com}") String apiUrl // с default
    ) {
        this.apiKey = apiKey;
        this.apiUrl = apiUrl;
    }
}
// application.yml содержит ТОЛЬКО значения по умолчанию для локальной разработки.
// Боевые конфигурации — в переменных окружения, недоступных из репозитория.
```

**Фактор VI — Processes (stateless):**

```java
// ❌ Нарушение: состояние в памяти приложения
@Service
public class SessionService {
    private final Map<String, UserSession> sessions = new ConcurrentHashMap<>();
    // При рестарте — все сессии потеряны.
    // При масштабировании на 3 инстанса — сессия есть только на одном.
}

// ✅ Stateless: состояние вынесено во внешнее хранилище
@Service
public class SessionService {
    private final RedisTemplate<String, UserSession> redis;

    public UserSession getSession(String sessionId) {
        return redis.opsForValue().get("session:" + sessionId);
    }
    // Любой инстанс приложения может обработать запрос.
    // При рестарте сессии не теряются.
}
```

**Фактор IX — Disposability (graceful shutdown):**

```java
// ✅ Приложение быстро и корректно завершает работу
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication app = new SpringApplication(Application.class);

        // Enables graceful shutdown (Spring Boot 2.3+):
        // - останавливает приём новых запросов
        // - завершает текущие запросы в течение заданного таймаута
        // - освобождает ресурсы (пулы соединений, etc.)
        app.setDefaultProperties(Map.of(
            "server.shutdown", "graceful",
            "spring.lifecycle.timeout-per-shutdown-phase", "30s"
        ));
        app.run(args);
    }
}
// Контейнер (Docker/K8s) отправляет SIGTERM → Spring корректно завершает работу.
// Время остановки: секунды, а не минуты.
```

**Фактор X — Dev/Prod Parity (одинаковые окружения):**

```java
// ❌ Разные БД локально и на проде
// application.yml (локально):
// spring.datasource.url=jdbc:h2:mem:testdb
// application-prod.yml:
// spring.datasource.url=jdbc:oracle:thin:@prod-db:1521:ORCL
// → Баги, которые проявляются только на Oracle, не ловятся локально!

// ✅ Testcontainers: тесты запускаются против РЕАЛЬНОЙ БД
@Testcontainers
@SpringBootTest
class UserRepositoryTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15")
        .withDatabaseName("testdb")
        .withUsername("test")
        .withPassword("test");

    @DynamicPropertySource
    static void configure(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Autowired private UserRepository repository;

    @Test
    void shouldPersistAndFindUser() {
        // Этот тест выполняется на РЕАЛЬНОМ PostgreSQL,
        // с реальными ограничениями, реальным синтаксисом SQL!
        User user = new User("test@example.com", "Test");
        repository.save(user);
        assertThat(repository.findByEmail("test@example.com")).isPresent();
    }
}
// Никаких сюрпризов «на проде не работает»: локально та же БД, что и на проде.
```

### Применимость за пределами Heroku

Хотя Twelve-Factor App был создан для Heroku, эти принципы стали **индустриальным стандартом**:

- **Docker-контейнеры** реализуют факторы VI (stateless), VII (port binding), IX (disposability).
- **Kubernetes** — факторы VIII (concurrency), IX, XII.
- **Spring Boot** из коробки поддерживает факторы II (Maven/Gradle), III (externalized config), VII (embedded server).
- **Cloud Native** — весь список является частью определения Cloud Native приложения.

---

## Принципы тестирования

Тестирование — неотъемлемая часть разработки ПО. Следующие принципы формируют фундамент культуры качества.

### TDD — Test-Driven Development (Разработка через тестирование)

> **Red → Green → Refactor. Сначала тест, потом код.**

TDD — практика, популяризованная Кентом Беком (Kent Beck) в книге «Test-Driven Development: By Example» (2002). Это не техника тестирования, а **дизайн-подход**: тесты пишутся ДО реализации и управляют дизайном кода.

**Цикл Red-Green-Refactor:**

| Фаза | Действие | Цель |
|------|----------|------|
| **Red** 🔴 | Напиши падающий тест на новую функциональность | Зафиксировать требование в виде исполняемой спецификации |
| **Green** 🟢 | Напиши минимальный код, чтобы тест прошёл | Реализовать функциональность (не заботясь об элегантности) |
| **Refactor** 🔵 | Улучши код: устрани дублирование, упрости | Сохранить качество кодовой базы при растущей функциональности |

**Пример на Java:**

```java
// 🔴 RED: тест на метод сумматора
@Test
void shouldSumTwoNumbers() {
    Calculator calc = new Calculator();
    int result = calc.add(2, 3);
    assertEquals(5, result);
}
// Компиляция не пройдёт: класса Calculator нет — создаём.

// 🟢 GREEN: минимальная реализация для прохождения теста
public class Calculator {
    public int add(int a, int b) {
        return 5; // Жёстко зашитый результат — но тест проходит!
    }
}
// Это выглядит глупо, но это ВЕРНЫЙ TDD-подход: минимум кода для зелёного теста.

// Добавляем второй тест:
@Test
void shouldSumDifferentNumbers() {
    Calculator calc = new Calculator();
    assertEquals(7, calc.add(3, 4));
}
// 🔴 RED — предыдущая реализация возвращает только 5

// 🟢 GREEN: обобщаем
public int add(int a, int b) {
    return a + b;
}

// 🔵 REFACTOR: пока рефакторить нечего, но с ростом тестов появятся возможности
```

**Что даёт TDD:**

- **Исполняемая спецификация.** Тесты = документация, которая не устаревает.
- **Дизайн, удобный для тестирования.** Если код трудно тестировать — значит, он слишком связан.
- **Уверенность при рефакторинге.** 1000 зелёных тестов после рефакторинга = ничего не сломано.
- **Минимум лишнего кода.** Пишем только то, что нужно для прохождения теста (YAGNI на практике).

**Что TDD НЕ даёт:**

- Не гарантирует отсутствие багов. Тесты пишет человек, и он может не подумать о граничном случае.
- Не заменяет другие виды тестирования (интеграционные, E2E).

### F.I.R.S.T. — Принципы хороших тестов

Акроним F.I.R.S.T. (сформулирован в книге «Clean Code» Роберта Мартина) описывает пять свойств качественных unit-тестов:

| Принцип | Описание |
|---------|----------|
| **F — Fast** (Быстрые) | Тесты должны выполняться быстро (миллисекунды, а не секунды). Медленные тесты не запускают часто — они бесполезны. |
| **I — Independent** (Независимые) | Тесты не должны зависеть друг от друга. Порядок выполнения не должен влиять на результат. |
| **R — Repeatable** (Повторяемые) | Тест должен давать одинаковый результат в любое время, на любом окружении. Без зависимостей от времени, сети, случайных чисел. |
| **S — Self-Validating** (Самопроверяемые) | Тест должен иметь бинарный результат: прошёл/не прошёл. Никакого ручного анализа логов. |
| **T — Timely** (Своевременные) | Тесты должны писаться вовремя (до кода — TDD, сразу после — не через месяц). |

**Пример нарушения FIRST:**

```java
// ❌ Не F.I.R.S.T.
@Test
void shouldProcessOrder() throws InterruptedException {
    // F — не Fast: спит 500 мс
    Thread.sleep(500);

    // I — не Independent: зависит от статического поля предыдущего теста
    OrderService.setNextOrderId(OrderService.getNextOrderId() + 1);

    // R — не Repeatable: зависит от системного времени
    Order order = new Order(LocalDateTime.now());

    // S — не Self-Validating: нужно смотреть в консоль
    System.out.println("Order created: " + order);

    // T — не Timely: тест написан через 3 месяца после кода
}
```

```java
// ✅ F.I.R.S.T.
@Test
void shouldCalculateOrderTotal() {
    // F: никаких sleep'ов, только CPU
    // I: каждый тест создаёт свои данные
    Order order = new Order(
        LocalDateTime.of(2025, 1, 15, 10, 0) // R: фиксированное время
    );
    order.addItem(new Item("Widget", new BigDecimal("10.0"), 2));
    order.addItem(new Item("Gadget", new BigDecimal("15.0"), 1));

    BigDecimal total = order.calculateTotal();

    // S: assert, а не println
    assertEquals(new BigDecimal("35.0"), total);
}
```

### Test Pyramid — Пирамида тестирования

Пирамида тестирования (Майк Кон, «Succeeding with Agile», 2009) — модель распределения усилий по разным видам тестов:

```
       /\
      /E2E\          ▼ Мало: медленные, хрупкие, дорогие
     /------\
    /Integration\    ▼ Средне: проверяют взаимодействие компонентов
   /------------\
  /   Unit Tests  \  ▼ МНОГО: быстрые, стабильные, дешёвые
 /------------------\
```

| Уровень | Что проверяем | Скорость | Количество |
|---------|--------------|----------|------------|
| **Unit** | Отдельные классы/методы в изоляции | Миллисекунды | 70-80% |
| **Integration** | Взаимодействие с БД, внешними сервисами, Spring Context | Секунды | 15-25% |
| **E2E** | Сквозные пользовательские сценарии через UI/API | Минуты | 5-10% |

**Антипаттерн — «Мороженое» (Ice Cream Cone):**

```
   ▄▄▄▄▄▄▄▄▄▄▄
   ▐  E2E ▐        ▼ МНОГО ручных/E2E тестов
   ▐▄▄▄▄▄▄▐
   ▐ Int. ▐        ▼ Мало интеграционных
   ▐▄▄▄▄▄▄▐
   ▐ Unit ▐        ▼ Очень мало unit-тестов
   ▐▄▄▄▄▄▄▐
```
Результат: CI работает часами, тесты нестабильны (flaky), разработчики игнорируют упавшие тесты.

**Практические рекомендации:**

1. **Unit-тесты — фундамент.** Пишите их на ВСЮ бизнес-логику. Мокайте внешние зависимости.
2. **Integration-тесты — на критические взаимодействия.** БД, брокеры сообщений, внешние API. Используйте Testcontainers, а не H2 вместо PostgreSQL.
3. **E2E-тесты — только happy path.** 2-3 ключевых пользовательских сценария. Не пытайтесь покрыть E2E все граничные случаи.

### Testing Trophy (Кент Доддс)

Более современная альтернатива пирамиде — Testing Trophy:

```
         /\
        /E2E\
       /------\
      /Integration\
     /--------------\
    /   Component     \
   /------------------\
  /    Unit / Static    \
 /------------------------\
```
Акцент смещён на **интеграционные и компонентные тесты** (без моков на сетевые вызовы), поскольку именно они дают наибольшую уверенность. Фундамент — статический анализ (TypeScript, ESLint).

---

## Взаимосвязь принципов

Принципы разработки не существуют в вакууме — они поддерживают и дополняют друг друга, а иногда входят в противоречие, требующее компромисса.

### Как принципы поддерживают друг друга

| Сочетание | Как работают вместе |
|-----------|---------------------|
| **KISS + YAGNI** | YAGNI убирает лишнее, KISS упрощает оставшееся |
| **DRY + SSOT** | DRY устраняет дублирование в коде, SSOT — в данных |
| **SoC + High Cohesion** | SoC разделяет систему на модули, High Cohesion гарантирует осмысленность каждого модуля |
| **Composition over Inheritance + Strategy** | Композиция даёт гибкость, Strategy — конкретный способ её реализовать |
| **IoC + DIP** | IoC — принцип инвертирования управления, DIP — принцип инвертирования зависимостей. Вместе составляют основу современной DI-based архитектуры |
| **Program to Interface + Protected Variations** | Интерфейс — стабильная точка, за которой скрывается изменчивость |
| **Law of Demeter + Low Coupling** | LoD запрещает навигацию по графу объектов, снижая coupling |
| **TDA + Information Expert** | TDA говорит «сообщай», Information Expert — «сообщай тому, у кого данные» |
| **Fail Fast + Principle of Least Astonishment** | Fail Fast предотвращает скрытые ошибки; PoLA делает ошибки предсказуемыми |
| **TDD + KISS** | TDD заставляет писать минимальный код для прохождения теста — естественный KISS |
| **Gall's Law + Agile** | Gall's Law объясняет, почему инкрементальная разработка работает: сложное вырастает из простого |
| **Law of Leaky Abstractions + KISS** | Каждая абстракция «протекает» — чем их меньше (KISS), тем меньше утечек |
| **Design by Contract + Fail Fast** | Предусловия контракта — это Fail Fast на уровне метода; постусловия — гарантии для вызывающего |
| **Broken Windows Theory + Boy Scout Rule** | Boy Scout Rule — тактический инструмент предотвращения Broken Windows на уровне кода |
| **Postel's Law + Robustness** | Принцип Постела делает систему устойчивой к незначительным отклонениям; Fail Fast — к критическим |
| **Test Pyramid + Pareto Principle** | 80% багов ловится unit-тестами (20% усилий); E2E (80% усилий) — для оставшихся 20% сценариев |

### Потенциальные конфликты

| Конфликт | Как разрешать |
|----------|---------------|
| **DRY vs YAGNI** | DRY говорит «объедини», YAGNI — «не надо, пока не понадобится». Разрешение: Rule of Three — объединяй на третьем дублировании. |
| **KISS vs «правильная» архитектура** | KISS говорит «просто», архитектура — «правильно». Разрешение: EDUF (Enough Design Up Front) — упрощай, но не в ущерб ключевым архитектурным решениям. |
| **BDUF vs Agile** | Разрешение: Inception-фаза для критических решений, детали — just-in-time. |
| **SSOT vs производительность** | Единый источник данных может стать узким местом. Разрешение: CQRS, кеширование (read replicas), eventual consistency. |
| **LoD vs удобство** | Строгое соблюдение Закона Деметры может привести к разрастанию API объектов. Разрешение: для DTO ослабляйте LoD; для доменных объектов — соблюдайте. |
| **Postel's Law vs Fail Fast** | Либеральный приём (Postel) может скрывать ошибки, которые должны быть обнаружены (Fail Fast). Разрешение: будь либерален к форме, строг к семантике. Невалидный email — Fail Fast. Неизвестное поле в JSON — прими. |
| **TDD vs скорость разработки** | Написание тестов до кода занимает время. Разрешение: TDD окупается на дистанции за счёт снижения времени отладки и регрессий. В прототипах и спайках TDD не обязателен. |
| **Law of Leaky Abstractions vs производительность** | Знание утечек может подтолкнуть к написанию «голого» кода без абстракций. Разрешение: используй абстракции, но знай, что под ними. Не отказывайся от ORM — но учи SQL. |

---

## Антипаттерны и типичные ошибки

### Антипаттерны, связанные с принципами

| Антипаттерн | Описание | Нарушаемые принципы |
|-------------|----------|---------------------|
| **Big Ball of Mud** | Система без различимой архитектуры, где всё связано со всем | SoC, Low Coupling, High Cohesion |
| **Anemic Domain Model** | Доменные объекты — только геттеры/сеттеры, вся логика в сервисах | TDA, Information Expert, Encapsulate What Varies |
| **God Object** | Один класс делает всё (более 1000 строк, десятки зависимостей) | SRP, High Cohesion, SoC |
| **Copy-Paste Programming** | Вместо создания общей функции разработчик копирует код | DRY, SSOT |
| **Overengineering / Gold Plating** | Чрезмерное усложнение: абстракции, которых не требуют задачи | KISS, YAGNI |
| **Premature Optimization** | Оптимизация до того, как измерена реальная производительность | YAGNI, Pareto Principle |
| **Lava Flow / Dead Code** | Код, который никто не решается удалить — «а вдруг пригодится» | YAGNI, KISS |
| **Functional Decomposition** | Объектная система разбита по функциям, а не по объектам | TDA, Information Expert, Encapsulate What Varies |
| **Reinventing the Wheel** | Разработка собственного решения вместо использования существующего | KISS (не усложняй), Worse is Better (используй проверенное) |
| **Cargo Cult Programming** | Слепое следование паттернам/практикам без понимания контекста | Все принципы |

### Типичные ошибки при применении принципов

1. **DRY до абсурда.** Два метода с похожим синтаксисом, но разным смыслом — не повод для объединения.
2. **KISS как оправдание халтуры.** «Я написал просто» не означает «я напишу говнокод и не буду рефакторить».
3. **YAGNI как отказ от архитектуры.** «Не будем думать о структуре, YAGNI же» — путь к Big Ball of Mud.
4. **Composition over Inheritance как абсолют.** Иногда наследование — правильный выбор (Template Method, соблюдение IS-A).
5. **Fail Fast без graceful degradation.** На проде недостаточно упасть — нужно залогировать, оповестить и корректно завершить операцию.

---

## Рекомендуемая литература

| Книга | Автор(ы) | Ключевые темы |
|-------|----------|---------------|
| **The Pragmatic Programmer** | Andrew Hunt, David Thomas | DRY, Orthogonality, Tracer Bullets, Broken Windows Theory |
| **Clean Code** | Robert C. Martin | KISS, Boy Scout Rule, комментирование кода |
| **The Mythical Man-Month** | Frederick Brooks | Brooks' Law, No Silver Bullet, концептуальная целостность |
| **Object-Oriented Software Construction** | Bertrand Meyer | CQS, Design by Contract, Open/Closed Principle |
| **Applying UML and Patterns** | Craig Larman | GRASP-паттерны, итеративное проектирование |
| **Refactoring** | Martin Fowler | Code Smells, Rule of Three, техника рефакторинга |
| **Domain-Driven Design** | Eric Evans | Bounded Context, Ubiquitous Language, модель как SSOT |
| **Patterns of Enterprise Application Architecture** | Martin Fowler | CQRS, Service Layer, Domain Model vs Anemic Model |
| **Building Microservices** | Sam Newman | Conway's Law, Twelve-Factor App в контексте микросервисов |
| **The Design of Design** | Frederick Brooks | Второе издание идей из Mythical Man-Month |
| **A Philosophy of Software Design** | John Ousterhout | Complex vs. Simple design, Deep modules |
| **Accelerate** | Nicole Forsgren et al. | DevOps, Continuous Delivery, научный подход к эффективности команд |
| **Test-Driven Development: By Example** | Kent Beck | TDD, Red-Green-Refactor, шаблоны тестирования |
| **Succeeding with Agile** | Mike Cohn | Test Pyramid, пользовательские истории, планирование |
| **Systemantics: How Systems Work and Especially How They Fail** | John Gall | Gall's Law, системное мышление, причины отказов систем |
| **The Law of Leaky Abstractions** (эссе) | Joel Spolsky | Утечки абстракций, пределы абстрагирования |
| **RFC 1122 — Requirements for Internet Hosts** | Jon Postel (ред.) | Robustness Principle, транспортный уровень TCP/IP |
