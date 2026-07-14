# SOLID — Принципы объектно-ориентированного проектирования

## Оглавление

1. [Введение](#введение)
   - [Что такое SOLID](#что-такое-solid)
   - [Зачем нужны принципы SOLID](#зачем-нужны-принципы-solid)
   - [Историческая справка](#историческая-справка)
2. [S — Single Responsibility Principle (Принцип единственной ответственности)](#s--single-responsibility-principle-принцип-единственной-ответственности)
   - [Суть принципа](#суть-принципа)
   - [Почему это важно](#почему-это-важно)
   - [Признаки нарушения SRP](#признаки-нарушения-srp)
   - [Примеры на Java](#примеры-на-java)
   - [Как соблюдать SRP на практике](#как-соблюдать-srp-на-практике)
3. [O — Open/Closed Principle (Принцип открытости/закрытости)](#o--openclosed-principle-принцип-открытостизакрытости)
   - [Суть принципа](#суть-принципа-1)
   - [Почему это важно](#почему-это-важно-1)
   - [Признаки нарушения OCP](#признаки-нарушения-ocp)
   - [Примеры на Java](#примеры-на-java-1)
   - [Способы реализации OCP](#способы-реализации-ocp)
4. [L — Liskov Substitution Principle (Принцип подстановки Барбары Лисков)](#l--liskov-substitution-principle-принцип-подстановки-барбары-лисков)
   - [Суть принципа](#суть-принципа-2)
   - [Формальное определение](#формальное-определение)
   - [Почему это важно](#почему-это-важно-2)
   - [Признаки нарушения LSP](#признаки-нарушения-lsp)
   - [Примеры на Java](#примеры-на-java-2)
   - [LSP и контрактное программирование](#lsp-и-контрактное-программирование)
5. [I — Interface Segregation Principle (Принцип разделения интерфейсов)](#i--interface-segregation-principle-принцип-разделения-интерфейсов)
   - [Суть принципа](#суть-принципа-3)
   - [Почему это важно](#почему-это-важно-3)
   - [Признаки нарушения ISP](#признаки-нарушения-isp)
   - [Примеры на Java](#примеры-на-java-3)
   - [ISP и эволюция API](#isp-и-эволюция-api)
6. [D — Dependency Inversion Principle (Принцип инверсии зависимостей)](#d--dependency-inversion-principle-принцип-инверсии-зависимостей)
   - [Суть принципа](#суть-принципа-4)
   - [Два ключевых правила](#два-ключевых-правила)
   - [Почему это важно](#почему-это-важно-4)
   - [Признаки нарушения DIP](#признаки-нарушения-dip)
   - [Примеры на Java](#примеры-на-java-4)
   - [DIP и внедрение зависимостей (DI)](#dip-и-внедрение-зависимостей-di)
   - [DIP и принцип Голливуда](#dip-и-принцип-голливуда)
7. [SOLID в реальных проектах](#solid-в-реальных-проектах)
   - [Пример модуля до Clean Architecture](#пример-модуля-до-clean-architecture)
   - [Связь с паттернами проектирования](#связь-с-паттернами-проектирования)
8. [Антипаттерны и типичные ошибки](#антипаттерны-и-типичные-ошибки)
9. [Заключение](#заключение)

---

## Введение

### Что такое SOLID

**SOLID** — это акроним пяти фундаментальных принципов объектно-ориентированного программирования и проектирования, сформулированных Робертом Мартином (Robert C. Martin, «Дядюшка Боб»). Каждая буква обозначает один принцип:

| Буква | Принцип (EN) | Принцип (RU) |
|-------|-------------|--------------|
| **S** | Single Responsibility Principle | Принцип единственной ответственности |
| **O** | Open/Closed Principle | Принцип открытости/закрытости |
| **L** | Liskov Substitution Principle | Принцип подстановки Барбары Лисков |
| **I** | Interface Segregation Principle | Принцип разделения интерфейсов |
| **D** | Dependency Inversion Principle | Принцип инверсии зависимостей |

Эти принципы — не жёсткие правила, а **рекомендации**, которые помогают писать код, устойчивый к изменениям, легко тестируемый и расширяемый. SOLID учит проектировать систему так, чтобы с течением времени она не превращалась в неподдерживаемый «большой ком грязи» (Big Ball of Mud).

### Зачем нужны принципы SOLID

Соблюдение SOLID даёт следующие преимущества:

- **Снижение связанности (Coupling).** Компоненты системы слабо зависят друг от друга, что позволяет изменять один компонент, не ломая остальные.
- **Повышение связности (Cohesion).** Код внутри одного класса или модуля логически сгруппирован — он делает одну вещь и делает её хорошо.
- **Упрощение тестирования.** Зависимости легко подменять заглушками (mocks/stubs), интерфейсы узкие — тесты изолированы.
- **Ускорение онбординга.** Новый разработчик быстрее понимает, за что отвечает конкретный класс.
- **Облегчение рефакторинга.** Система спроектирована так, что изменения инкапсулируются в минимальном количестве файлов.

### Историческая справка

Термин SOLID предложил Michael Feathers в начале 2000-х. Сами принципы собраны из работ:
- Barbara Liskov — принцип подстановки (1987)
- Bertrand Meyer — принцип открытости/закрытости (1988)
- Robert C. Martin — остальные принципы, сформулированные в книге «Agile Software Development: Principles, Patterns, and Practices» (2002)

---

## S — Single Responsibility Principle (Принцип единственной ответственности)

### Суть принципа

> **У класса должна быть только одна причина для изменения.**
>
> *— Robert C. Martin*

Класс должен решать **одну**, чётко определённую задачу и, как следствие, иметь только одну причину для изменения. Вся его функциональность должна быть сгруппирована вокруг этой задачи, а ответственность за смежные операции — вынесена в отдельные классы.

**Ключевая идея:** изменение требований, затрагивающее одну область бизнес-логики, не должно требовать изменения класса, отвечающего за другую область.

### Почему это важно

Представьте класс, который одновременно:
- Обрабатывает бизнес-логику заказа
- Пишет логи в файл
- Отправляет email-уведомления
- Сохраняет данные в БД

При изменении формата логов вы рискуете сломать бизнес-логику заказа. При смене почтового провайдера — затронуть код сохранения в БД. Это приводит к **регрессионным ошибкам** и замедляет разработку.

### Признаки нарушения SRP

1. **Класс имеет более 200–300 строк кода** (эвристика, не догма).
2. **В описании класса используется союз «и»:** «Класс управляет заказами **и** отправляет уведомления».
3. **Разные методы класса обращаются к разным слоям:** часть методов работает с HTTP-запросами, часть — с SQL-запросами.
4. **При модификации одного сценария вы вынуждены править методы, которые к нему не относятся.**
5. **Класс имеет более одного поля-зависимости, которые не используются одновременно в одном сценарии.**

### Примеры на Java

#### ❌ Нарушение SRP

```java
/**
 * Класс-нарушитель: смешивает бизнес-логику, валидацию, сохранение
 * и уведомления. Четыре причины для изменения!
 */
public class OrderProcessor {

    private final DataSource dataSource;
    private final EmailSender emailSender;
    private final Logger logger;

    public OrderProcessor(DataSource dataSource,
                          EmailSender emailSender,
                          Logger logger) {
        this.dataSource = dataSource;
        this.emailSender = emailSender;
        this.logger = logger;
    }

    // ── Валидация ──────────────────────────────────────
    public boolean validateOrder(Order order) {
        if (order.getItems().isEmpty()) {
            logger.warn("Order " + order.getId() + " has no items");
            return false;
        }
        if (order.getCustomerEmail() == null) {
            logger.warn("Order " + order.getId() + " has no email");
            return false;
        }
        return true;
    }

    // ── Бизнес-логика ──────────────────────────────────
    public BigDecimal calculateTotal(Order order) {
        BigDecimal total = BigDecimal.ZERO;
        for (OrderItem item : order.getItems()) {
            total = total.add(item.getPrice()
                    .multiply(BigDecimal.valueOf(item.getQuantity())));
        }
        // Применяем скидку
        if (order.hasDiscount()) {
            total = total.multiply(
                    BigDecimal.ONE.subtract(order.getDiscount()));
        }
        return total;
    }

    // ── Сохранение в БД ────────────────────────────────
    public void saveOrder(Order order) throws SQLException {
        String sql = "INSERT INTO orders (id, customer_email, total) "
                   + "VALUES (?, ?, ?)";
        try (Connection conn = dataSource.getConnection();
             PreparedStatement ps = conn.prepareStatement(sql)) {
            ps.setString(1, order.getId());
            ps.setString(2, order.getCustomerEmail());
            ps.setBigDecimal(3, order.getTotal());
            ps.executeUpdate();
        }
        logger.info("Order " + order.getId() + " saved to DB");
    }

    // ── Уведомления ────────────────────────────────────
    public void sendConfirmation(Order order) {
        String subject = "Order #" + order.getId() + " confirmed";
        String body = "Thank you for your order! Total: "
                    + order.getTotal();
        emailSender.send(order.getCustomerEmail(), subject, body);
        logger.info("Confirmation sent for order " + order.getId());
    }
}
```

**Проблемы этого кода:**
- Смена БД (например, с PostgreSQL на MongoDB) требует правки `OrderProcessor`.
- Изменение формата письма требует правки `OrderProcessor`.
- Добавление новых правил валидации требует правки `OrderProcessor`.
- Любой рефакторинг логгирования требует правки `OrderProcessor`.

#### ✅ Соблюдение SRP

```java
// ──────────────────────────────────────────────────────
// Каждый класс теперь имеет ровно одну ответственность
// ──────────────────────────────────────────────────────

/** Отвечает только за валидацию заказа */
public class OrderValidator {

    private final Logger logger;

    public OrderValidator(Logger logger) {
        this.logger = logger;
    }

    public boolean validate(Order order) {
        if (order.getItems().isEmpty()) {
            logger.warn("Order {} has no items", order.getId());
            return false;
        }
        if (order.getCustomerEmail() == null) {
            logger.warn("Order {} has no email", order.getId());
            return false;
        }
        return true;
    }
}

/** Отвечает только за расчёт стоимости */
public class OrderCalculator {

    public BigDecimal calculateTotal(Order order) {
        BigDecimal total = order.getItems().stream()
                .map(item -> item.getPrice()
                        .multiply(BigDecimal.valueOf(item.getQuantity())))
                .reduce(BigDecimal.ZERO, BigDecimal::add);

        if (order.hasDiscount()) {
            total = total.multiply(
                    BigDecimal.ONE.subtract(order.getDiscount()));
        }
        return total;
    }
}

/** Отвечает только за сохранение заказа */
public class OrderRepository {

    private final DataSource dataSource;
    private final Logger logger;

    public OrderRepository(DataSource dataSource, Logger logger) {
        this.dataSource = dataSource;
        this.logger = logger;
    }

    public void save(Order order) throws SQLException {
        String sql = """
            INSERT INTO orders (id, customer_email, total)
            VALUES (?, ?, ?)
            """;
        try (Connection conn = dataSource.getConnection();
             PreparedStatement ps = conn.prepareStatement(sql)) {
            ps.setString(1, order.getId());
            ps.setString(2, order.getCustomerEmail());
            ps.setBigDecimal(3, order.getTotal());
            ps.executeUpdate();
        }
        logger.info("Order {} saved to DB", order.getId());
    }
}

/** Отвечает только за отправку уведомлений */
public class OrderNotifier {

    private final EmailSender emailSender;
    private final Logger logger;

    public OrderNotifier(EmailSender emailSender, Logger logger) {
        this.emailSender = emailSender;
        this.logger = logger;
    }

    public void sendConfirmation(Order order) {
        String subject = "Order #" + order.getId() + " confirmed";
        String body = "Thank you for your order! Total: "
                    + order.getTotal();
        emailSender.send(order.getCustomerEmail(), subject, body);
        logger.info("Confirmation sent for order {}", order.getId());
    }
}

/**
 * Оркестратор — координирует работу остальных классов.
 * Его единственная ответственность — сценарий обработки заказа.
 */
public class OrderProcessingFacade {

    private final OrderValidator validator;
    private final OrderCalculator calculator;
    private final OrderRepository repository;
    private final OrderNotifier notifier;

    public OrderProcessingFacade(OrderValidator validator,
                                  OrderCalculator calculator,
                                  OrderRepository repository,
                                  OrderNotifier notifier) {
        this.validator = validator;
        this.calculator = calculator;
        this.repository = repository;
        this.notifier = notifier;
    }

    public void process(Order order) throws SQLException {
        if (!validator.validate(order)) {
            throw new OrderValidationException("Order validation failed");
        }
        order.setTotal(calculator.calculateTotal(order));
        repository.save(order);
        notifier.sendConfirmation(order);
    }
}

/** Исключение валидации заказа — часть доменного слоя */
public class OrderValidationException extends RuntimeException {
    public OrderValidationException(String message) {
        super(message);
    }
}
```

**Что изменилось:**
- `OrderValidator` меняется только при изменении правил валидации.
- `OrderCalculator` меняется только при изменении логики расчёта.
- `OrderRepository` меняется только при изменении схемы хранения.
- `OrderNotifier` меняется только при изменении формата уведомлений.
- `OrderProcessingFacade` — тонкий оркестратор, который меняется только при изменении самого сценария обработки.

### Как соблюдать SRP на практике

1. **Используйте паттерн Фасад (Facade)** для оркестрации: сам фасад ничего не делает, только делегирует.
2. **Выделяйте сервисы по бизнес-операциям,** а не по сущностям. Не `UserService` на 2000 строк, а `UserRegistrationService`, `UserProfileService`, `UserDeactivationService`.
3. **Применяйте принцип «Разделения команд и запросов» (CQRS)** на уровне классов: классы-команды меняют состояние, классы-запросы читают.
4. **Периодически перечитывайте свой код** и задавайте вопрос: «Сколько у этого класса причин для изменения?»

---

## O — Open/Closed Principle (Принцип открытости/закрытости)

### Суть принципа

> **Программные сущности (классы, модули, функции) должны быть открыты для расширения, но закрыты для модификации.**
>
> *— Bertrand Meyer, 1988*

Вы должны иметь возможность добавлять новое поведение в систему, **не изменяя существующий код**. Изменение существующего кода всегда несёт риск внесения регрессионных ошибок — OCP предлагает архитектурный подход, который этот риск минимизирует.

**Ключевая метафора:** представьте, что вы достраиваете дом. Чтобы добавить новую комнату, вы не ломаете несущие стены — вы пристраиваете к имеющемуся фундаменту.

### Почему это важно

- **Стабильность.** Код, который уже протестирован и работает в продакшене, остаётся нетронутым.
- **Минимизация регрессий.** Новые фичи не ломают старые.
- **Упрощение code-review.** Рецензент видит только новые файлы — старые не изменились.
- **Гибкость.** Система легко адаптируется к новым требованиям.

### Признаки нарушения OCP

1. **Цепочки `if-else` или `switch`, проверяющие тип или enum** в бизнес-логике.
2. **При добавлении новой фичи приходится править несколько классов в разных слоях** (контроллер, сервис, репозиторий).
3. **Использование `instanceof` для выбора поведения.**
4. **Методы, которые знают о конкретных подклассах.**

### Примеры на Java

#### ❌ Нарушение OCP

```java
/**
 * При добавлении нового способа доставки нужно модифицировать
 * этот класс — нарушение OCP.
 */
public class ShippingCalculator {

    public BigDecimal calculate(Order order, String shippingMethod) {
        BigDecimal totalWeight = order.getTotalWeight();

        // Каждый новый способ доставки = новый if-else!
        if ("standard".equals(shippingMethod)) {
            return totalWeight.multiply(new BigDecimal("5.0"))
                    .add(new BigDecimal("10.0")); // базовая ставка

        } else if ("express".equals(shippingMethod)) {
            return totalWeight.multiply(new BigDecimal("15.0"))
                    .add(new BigDecimal("25.0"));

        } else if ("pickup".equals(shippingMethod)) {
            return BigDecimal.ZERO;

        } else if ("international".equals(shippingMethod)) {
            return totalWeight.multiply(new BigDecimal("50.0"))
                    .add(new BigDecimal("100.0"));

        } else {
            throw new IllegalArgumentException(
                "Unknown shipping method: " + shippingMethod);
        }
    }
}
```

**Почему это плохо:**
- Добавление нового способа доставки (например, «доставка дроном») требует правки метода `calculate`. Риск: можно случайно сломать расчёт для `express`.
- Класс растёт с каждым новым требованием.
- Нарушается SRP: класс знает детали реализации **всех** способов доставки.

#### ✅ Соблюдение OCP через полиморфизм (паттерн «Стратегия»)

```java
// ── Абстракция: контракт для всех способов доставки ──
public interface ShippingStrategy {
    BigDecimal calculate(Order order);
    String getName();
}

// ── Конкретные реализации (закрытые для модификации) ──

public class StandardShipping implements ShippingStrategy {

    private static final BigDecimal RATE_PER_KG = new BigDecimal("5.0");
    private static final BigDecimal BASE_FEE = new BigDecimal("10.0");

    @Override
    public BigDecimal calculate(Order order) {
        return order.getTotalWeight()
                .multiply(RATE_PER_KG)
                .add(BASE_FEE);
    }

    @Override
    public String getName() {
        return "standard";
    }
}

public class ExpressShipping implements ShippingStrategy {

    private static final BigDecimal RATE_PER_KG = new BigDecimal("15.0");
    private static final BigDecimal BASE_FEE = new BigDecimal("25.0");

    @Override
    public BigDecimal calculate(Order order) {
        return order.getTotalWeight()
                .multiply(RATE_PER_KG)
                .add(BASE_FEE);
    }

    @Override
    public String getName() {
        return "express";
    }
}

public class PickupShipping implements ShippingStrategy {

    @Override
    public BigDecimal calculate(Order order) {
        return BigDecimal.ZERO;
    }

    @Override
    public String getName() {
        return "pickup";
    }
}

public class InternationalShipping implements ShippingStrategy {

    private static final BigDecimal RATE_PER_KG = new BigDecimal("50.0");
    private static final BigDecimal BASE_FEE = new BigDecimal("100.0");

    @Override
    public BigDecimal calculate(Order order) {
        return order.getTotalWeight()
                .multiply(RATE_PER_KG)
                .add(BASE_FEE);
    }

    @Override
    public String getName() {
        return "international";
    }
}

// ── Калькулятор ЗАКРЫТ для модификации ──
public class ShippingCalculator {

    private final Map<String, ShippingStrategy> strategies;

    /**
     * Все стратегии внедряются извне (через Spring DI, например).
     * При добавлении нового способа доставки этот класс НЕ меняется!
     */
    public ShippingCalculator(List<ShippingStrategy> strategies) {
        this.strategies = strategies.stream()
                .collect(Collectors.toMap(
                        ShippingStrategy::getName,
                        Function.identity()));
    }

    public BigDecimal calculate(Order order, String shippingMethod) {
        ShippingStrategy strategy = strategies.get(shippingMethod);
        if (strategy == null) {
            throw new IllegalArgumentException(
                "Unknown shipping method: " + shippingMethod);
        }
        return strategy.calculate(order);
    }
}

// ── Добавление нового способа доставки БЕЗ изменения старого кода ──

/**
 * Новый способ доставки дроном.
 * Мы просто добавляем новый класс — ShippingCalculator не трогаем!
 */
public class DroneShipping implements ShippingStrategy {

    private static final BigDecimal RATE_PER_KM = new BigDecimal("2.0");

    @Override
    public BigDecimal calculate(Order order) {
        return order.getDeliveryDistance()
                .multiply(RATE_PER_KM);
    }

    @Override
    public String getName() {
        return "drone";
    }
}
```

**Что изменилось:**
- `ShippingCalculator` закрыт для изменений — его код не меняется при добавлении нового способа доставки.
- Каждая стратегия изолирована — баг в `DroneShipping` не затронет `ExpressShipping`.
- Spring автоматически подхватит новый бин `DroneShipping` и добавит его в `Map`.

### Способы реализации OCP

1. **Полиморфизм + паттерн «Стратегия»** — как в примере выше.
2. **Паттерн «Декоратор»** — оборачивание объекта для добавления поведения «поверх».
3. **Паттерн «Цепочка обязанностей»** — каждый обработчик решает, может ли он обработать запрос.
4. **Паттерн «Наблюдатель»** — подписчики добавляются без изменения издателя.
5. **Паттерн «Посетитель»** — добавление новых операций к иерархии классов без изменения самих классов.
6. **Точки расширения (Extension Points)** — явно предусмотренные места в архитектуре, куда можно «подключить» новый код (например, `SPI` в Java).

---

## L — Liskov Substitution Principle (Принцип подстановки Барбары Лисков)

### Суть принципа

> **Объекты в программе должны быть заменяемы экземплярами их подтипов без нарушения корректности программы.**
>
> *— Barbara Liskov, 1987*

Проще говоря: **наследник должен уметь делать всё то же, что и родитель, и не должен ломать ожидания клиентского кода.** Если у вас есть метод, принимающий `List`, он должен работать одинаково корректно и с `ArrayList`, и с `LinkedList`, и с `ImmutableList`.

### Формальное определение

Барбара Лисков сформулировала принцип математически строго. В упрощённой форме:

> Если `S` — подтип `T`, то объекты типа `T` могут быть заменены объектами типа `S` без изменения желаемых свойств программы.

Для языка Java это означает, что подкласс должен:
1. **Не усиливать предусловия** (preconditions) — не требовать от клиента больше, чем требует родитель.
2. **Не ослаблять постусловия** (postconditions) — гарантировать не меньше, чем гарантирует родитель.
3. **Сохранять инварианты** родительского класса.
4. **Не выбрасывать исключения, которые не описаны в сигнатуре родительского метода** (кроме случаев, когда они являются подтипами уже объявленных).

### Почему это важно

- **Корректность полиморфизма.** Без LSP весь полиморфизм рушится: вы не можете доверять абстракции, потому что подтип может вести себя неожиданно.
- **Безопасность рефакторинга.** Вы можете заменить одну реализацию интерфейса другой без страха сломать систему.
- **Тестируемость.** Вы можете замокать зависимость, и код будет вести себя предсказуемо.

### Признаки нарушения LSP

1. **Метод подкласса выбрасывает `UnsupportedOperationException`.**
2. **Метод подкласса ничего не делает (пустое тело) в ответ на вызов.**
3. **Подкласс добавляет новые проверки, отсутствующие в базовом классе** (усиление предусловий).
4. **Подкласс возвращает `null` там, где базовый класс гарантирует not-null.**
5. **`instanceof` или проверка типа перед вызовом метода.**
6. **Жёсткие проверки в клиентском коде:** «если это `ArrayList`, то работаем так, а если `LinkedList` — иначе».

### Примеры на Java

#### ❌ Классическое нарушение: Прямоугольник и Квадрат

Это самый известный пример нарушения LSP, который часто приводят в литературе.

```java
/** Базовый класс */
public class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int getWidth() {
        return width;
    }

    public int getHeight() {
        return height;
    }

    public int getArea() {
        return width * height;
    }
}

/**
 * Квадрат ЯВЛЯЕТСЯ прямоугольником в математике,
 * но не в ООП при таком дизайне!
 */
public class Square extends Rectangle {

    @Override
    public void setWidth(int width) {
        this.width = width;
        this.height = width;  // ← принудительно синхронизируем
    }

    @Override
    public void setHeight(int height) {
        this.width = height;  // ← принудительно синхронизируем
        this.height = height;
    }
}

// ── Клиентский код ломается при подстановке Square ──

public class RectangleTest {

    /**
     * Этот тест ПРОЙДЁТ для Rectangle, но УПАДЁТ для Square.
     *
     * Мы ожидаем, что после setWidth и setHeight
     * ширина и высота будут независимы.
     * Square нарушает это ожидание!
     */
    public void testArea(Rectangle rectangle) {
        rectangle.setWidth(5);
        rectangle.setHeight(4);

        // Для Rectangle: area = 5 * 4 = 20  ✅
        // Для Square:    area = 4 * 4 = 16  ❌ Ожидали 20!
        assert rectangle.getArea() == 20
            : "Expected area 20, but got " + rectangle.getArea();
    }
}
```

**В чём проблема:** Квадрат накладывает дополнительное ограничение (`width == height`), которого нет в контракте `Rectangle`. Клиентский код, рассчитанный на `Rectangle`, не ожидает, что изменение ширины повлияет на высоту.

**Вывод:** `Square` не должен наследовать `Rectangle` при таком дизайне. Это показывает, что наследование должно основываться на **поведении**, а не на математическом отношении «является».

#### ✅ Исправление: выделение неизменяемой абстракции

```java
/** Интерфейс только для чтения — LSP соблюдён */
public interface Shape {
    int getArea();
}

/** Прямоугольник как неизменяемый объект (value object) */
public record Rectangle(int width, int height) implements Shape {

    public Rectangle {
        if (width <= 0 || height <= 0) {
            throw new IllegalArgumentException(
                "Dimensions must be positive");
        }
    }

    @Override
    public int getArea() {
        return width * height;
    }
}

/** Квадрат как отдельная реализация Shape */
public record Square(int side) implements Shape {

    public Square {
        if (side <= 0) {
            throw new IllegalArgumentException(
                "Side must be positive");
        }
    }

    @Override
    public int getArea() {
        return side * side;
    }
}

// Клиентский код работает с любым Shape одинаково корректно:
public void printArea(Shape shape) {
    System.out.println("Area: " + shape.getArea());  // ✅ LSP соблюдён
}
```

#### ❌ Нарушение LSP: выброс непредусмотренных исключений

```java
public interface PaymentProcessor {
    /**
     * Обрабатывает платёж.
     * @throws PaymentException если платёж отклонить банк
     */
    void process(Payment payment) throws PaymentException;
}

public class CreditCardProcessor implements PaymentProcessor {
    @Override
    public void process(Payment payment) throws PaymentException {
        // Логика обработки карты
    }
}

/**
 * Нарушение LSP: выбрасывает исключение, которое не является
 * подклассом PaymentException и не ожидается клиентом!
 */
public class CryptoPaymentProcessor implements PaymentProcessor {
    @Override
    public void process(Payment payment) {
        if (!isWalletConnected()) {
            throw new WalletNotConnectedException();  // ← RuntimeException
            //   клиент не ожидает такого типа ошибки!
        }
        // ...
    }
}
```

#### ✅ Исправление: единая иерархия исключений

```java
public class PaymentException extends Exception {
    public PaymentException(String message) {
        super(message);
    }
}

// Все специфичные исключения — подтипы PaymentException
public class InsufficientFundsException extends PaymentException { /* ... */ }
public class WalletNotConnectedException extends PaymentException { /* ... */ }

// Клиент может обрабатывать все ошибки единообразно:
public void pay(PaymentProcessor processor, Payment payment) {
    try {
        processor.process(payment);
    } catch (PaymentException e) {
        // Обрабатываем любую ошибку платежа
        handlePaymentError(e);
    }
}
```

### LSP и контрактное программирование

LSP тесно связан с понятием **контракта** (design by contract, Bertrand Meyer):

| Элемент контракта | Правило LSP |
|-------------------|-------------|
| **Предусловия** (preconditions) | Подтип не должен усиливать. Нельзя требовать *больше*, чем родитель. |
| **Постусловия** (postconditions) | Подтип не должен ослаблять. Нельзя гарантировать *меньше*, чем родитель. |
| **Инварианты** | Подтип должен сохранять все инварианты родительского типа. |

**Пример контракта в Java через аннотации:**

```java
import javax.annotation.Nullable;
import javax.annotation.Nonnull;

public interface UserRepository {

    /**
     * @param id идентификатор пользователя, не может быть null
     * @return пользователь, не может быть null
     * @throws UserNotFoundException если пользователь не найден
     */
    @Nonnull
    User findById(@Nonnull Long id) throws UserNotFoundException;
}

// ✅ Корректная реализация — не ослабляет постусловие
public class DatabaseUserRepository implements UserRepository {
    @Override
    @Nonnull
    public User findById(@Nonnull Long id) throws UserNotFoundException {
        User user = jdbcTemplate.queryForObject(...);
        if (user == null) {
            throw new UserNotFoundException(id);
        }
        return user;
    }
}

// ❌ Нарушение LSP — ослабляет постусловие, возвращая null
public class CachedUserRepository implements UserRepository {
    @Override
    @Nullable  // ← контракт говорит @Nonnull!
    public User findById(@Nonnull Long id) {
        return cache.get(id);  // может вернуть null — нарушение!
    }
}
```

---

## I — Interface Segregation Principle (Принцип разделения интерфейсов)

### Суть принципа

> **Клиенты не должны зависеть от методов, которые они не используют.**
>
> *— Robert C. Martin*

Интерфейсы должны быть **узкими и специализированными**. Лучше иметь много маленьких интерфейсов, каждый из которых описывает ровно одно поведение, чем один «толстый» (fat) интерфейс на все случаи жизни.

**Ключевая идея:** если класс реализует интерфейс с десятью методами, но использует только два, то изменения в любом из оставшихся восьми методов могут заставить этот класс перекомпилироваться (в Java) или даже сломать его.

### Почему это важно

- **Снижение связанности.** Класс не зависит от методов, которые ему не нужны.
- **Упрощение реализации.** Не нужно писать заглушки для неиспользуемых методов.
- **Упрощение тестирования.** При мокировании интерфейса нужно замокать только 2 метода, а не 10.
- **Повышение читаемости.** По набору интерфейсов класса сразу понятно, какое поведение он предоставляет.
- **Облегчение эволюции API.** Добавление метода в «толстый» интерфейс ломает всех его реализаторов. Добавление метода в новый узкий интерфейс никого не ломает.

### Признаки нарушения ISP

1. **Реализация интерфейса с методами, выбрасывающими `UnsupportedOperationException`.**
2. **Реализация методов с пустым телом.**
3. **Клиент зависит от интерфейса, в котором ему нужны 1–2 метода из 10+.**
4. **Интерфейс с названием `*Service` или `*Repository` содержит методы для разных сценариев** (чтение, запись, удаление, отчёты) вперемешку.
5. **При мокировании приходится создавать реализации для методов, не относящихся к тесту.**

### Примеры на Java

#### ❌ Нарушение ISP: толстый интерфейс

```java
/**
 * "Толстый" интерфейс.
 * Представьте, что его реализуют: кнопка, текстовое поле,
 * изображение, видео-плеер, таблица...
 */
public interface UIComponent {
    void render();
    void onClick();
    void onDoubleClick();
    void onDrag();
    void onHover();
    void setText(String text);
    String getText();
    void setImage(byte[] imageData);
    void playVideo(String videoUrl);
    void pauseVideo();
    void resize(int width, int height);
    void scrollTo(int position);
    void sortByColumn(String columnName);
    void filterRows(String query);
}
```

**Проблемы:**
- Класс `Button` вынужден реализовывать `playVideo()`, `pauseVideo()`, `sortByColumn()` — выбрасывая `UnsupportedOperationException`.
- Класс `VideoPlayer` вынужден реализовывать `setText()`, `sortByColumn()` — методы, которые к видео не имеют отношения.
- Добавление метода `exportToPdf()` в интерфейс заставит перекомпилироваться **все** UI-компоненты, даже те, которые никогда не будут экспортироваться в PDF.

#### ✅ Соблюдение ISP: узкие, сфокусированные интерфейсы

```java
// ── Базовый интерфейс: то, что умеет каждый UI-компонент ──
public interface Renderable {
    void render();
}

// ── Специализированные интерфейсы ──

public interface Clickable {
    void onClick();
}

public interface DoubleClickable {
    void onDoubleClick();
}

public interface Draggable {
    void onDrag();
}

public interface Hoverable {
    void onHover();
}

public interface TextContainer {
    void setText(String text);
    String getText();
}

public interface ImageContainer {
    void setImage(byte[] imageData);
}

public interface Playable {
    void play();
    void pause();
    void stop();
}

public interface Resizable {
    void resize(int width, int height);
}

public interface Scrollable {
    void scrollTo(int position);
}

public interface Sortable {
    void sortByColumn(String columnName);
}

public interface Filterable {
    void filterRows(String query);
}

// ── Классы реализуют ТОЛЬКО те интерфейсы, которые им нужны ──

public class Button implements Renderable, Clickable, Hoverable {
    @Override public void render() { /* отрисовка кнопки */ }
    @Override public void onClick() { /* обработка клика */ }
    @Override public void onHover() { /* эффект при наведении */ }
}

public class Label implements Renderable, TextContainer {
    private String text;

    @Override public void render() { /* отрисовка текста */ }
    @Override public void setText(String text) { this.text = text; }
    @Override public String getText() { return text; }
}

public class VideoPlayer implements Renderable, Playable, Resizable {
    @Override public void render() { /* отрисовка плеера */ }
    @Override public void play() { /* запуск видео */ }
    @Override public void pause() { /* пауза */ }
    @Override public void stop() { /* остановка */ }
    @Override public void resize(int w, int h) { /* изменение размера */ }
}

public class DataTable implements Renderable, Sortable, Filterable,
                                    Scrollable, Resizable {
    @Override public void render() { /* отрисовка таблицы */ }
    @Override public void sortByColumn(String col) { /* сортировка */ }
    @Override public void filterRows(String query) { /* фильтрация */ }
    @Override public void scrollTo(int pos) { /* скролл */ }
    @Override public void resize(int w, int h) { /* ресайз */ }
}
```

**Что изменилось:**
- `Button` реализует только то, что действительно умеет. Никаких заглушек.
- При добавлении интерфейса `Accessible` (для screen-reader'ов) `Button` может реализовать его, а `VideoPlayer` — пока нет.
- Тесты на `Button` мокают только `Clickable` и `Hoverable`.

#### Ещё один пример: нарушение ISP в слое доступа к данным

```java
// ❌ Толстый репозиторий
public interface UserRepository {
    User findById(Long id);
    List<User> findAll();
    void save(User user);
    void update(User user);
    void delete(Long id);
    List<User> search(String query);
    UserStatistics getStatistics();
    byte[] exportToCsv();
    void importFromCsv(byte[] csvData);
}

// Клиенту, который только читает данные, приходится
// зависеть от методов записи, экспорта, импорта...
```

```java
// ✅ Разделённые интерфейсы (паттерн CQRS на уровне интерфейсов)
public interface UserReader {
    User findById(Long id);
    List<User> findAll();
    List<User> search(String query);
    UserStatistics getStatistics();
}

public interface UserWriter {
    void save(User user);
    void update(User user);
    void delete(Long id);
}

public interface UserExporter {
    byte[] exportToCsv();
}

public interface UserImporter {
    void importFromCsv(byte[] csvData);
}

// Сервис отчётов зависит только от чтения:
public class ReportService {
    private final UserReader userReader;  // ← только то, что нужно
    // ...
}

// Административный сервис зависит от всего:
public class AdminService {
    private final UserReader userReader;
    private final UserWriter userWriter;
    private final UserExporter userExporter;
    private final UserImporter userImporter;
    // ...
}
```

### ISP и эволюция API

Один из главных аргументов в пользу ISP — **безопасная эволюция API**:

```java
// Версия 1.0
public interface PaymentGateway {
    void processPayment(Payment payment);
    PaymentStatus checkStatus(String transactionId);
}

// Версия 2.0 — хотим добавить refund (возврат средств)

// ❌ Без ISP: добавляем метод в существующий интерфейс
public interface PaymentGateway {  // ← ВСЕ реализации сломались!
    void processPayment(Payment payment);
    PaymentStatus checkStatus(String transactionId);
    void refund(String transactionId);  // ← новый метод
}

// ✅ С ISP: создаём новый интерфейс
public interface Refundable {
    void refund(String transactionId);
}

// StripePaymentGateway implements PaymentGateway, Refundable — обновляется
// OldPaymentGateway implements PaymentGateway — остаётся без изменений
```

---

## D — Dependency Inversion Principle (Принцип инверсии зависимостей)

### Суть принципа

> **Модули верхнего уровня не должны зависеть от модулей нижнего уровня. И те, и другие должны зависеть от абстракций.**
>
> **Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.**
>
> *— Robert C. Martin*

DIP — самый мощный и самый сложный для понимания принцип SOLID. Он переворачивает традиционное представление о зависимостях в программе. В классической многослойной архитектуре слой бизнес-логики зависит от слоя доступа к данным, который зависит от конкретной БД. DIP говорит: **оба слоя должны зависеть от абстракции**, которую определяет бизнес-логика.

### Два ключевых правила

1. **Модули верхнего уровня не должны зависеть от модулей нижнего уровня. Оба должны зависеть от абстракций.**
2. **Абстракции не должны зависеть от деталей. Детали должны зависеть от абстракций.**

**Ключевая метафора:** не лампа зависит от стены, а и лампа, и стена зависят от стандарта розетки (абстракция). Вы можете заменить лампу на любую другую, подходящую к розетке.

### Почему это важно

- **Заменяемость реализации.** Вы можете сменить БД, не меняя бизнес-логику.
- **Тестируемость.** Вы можете тестировать бизнес-логику изолированно, подставляя in-memory реализации.
- **Порядок разработки.** Вы можете разрабатывать модули параллельно, договорившись об интерфейсах.
- **Устойчивость к изменениям.** Изменения в деталях (БД, UI, сторонние API) не затрагивают ядро системы.

### Признаки нарушения DIP

1. **Прямое создание объектов через `new` в бизнес-логике** (жёсткая зависимость от конкретного класса).
2. **Импорт классов из слоя инфраструктуры в слой бизнес-логики.**
3. **Бизнес-логика знает о `HttpServletRequest`, `ResultSet`, `PreparedStatement`.**
4. **Использование статических методов для получения зависимостей** (Service Locator).
5. **Наследование класса бизнес-логики от фреймворкового класса.**

### Примеры на Java

#### ❌ Нарушение DIP: жёсткая зависимость от конкретной реализации

```java
/**
 * Класс высокого уровня (бизнес-логика) напрямую зависит
 * от класса низкого уровня (работа с MySQL).
 */
public class UserService {

    // ❌ Прямая зависимость от конкретной реализации БД
    private final MySQLUserRepository repository;

    public UserService() {
        // ❌ Жёсткое создание зависимости внутри класса
        this.repository = new MySQLUserRepository(
            "jdbc:mysql://localhost:3306/mydb",
            "root",
            "password"
        );
    }

    public void registerUser(User user) {
        // Бизнес-логика регистрации
        if (user.getEmail() == null) {
            throw new IllegalArgumentException("Email is required");
        }
        user.setCreatedAt(Instant.now());
        user.setStatus(UserStatus.ACTIVE);

        // Сохранение — зависит от MySQL-реализации
        repository.save(user);

        // Если мы захотим перейти на PostgreSQL, MongoDB или
        // замокать репозиторий для теста — этот класс придётся менять!
    }

    public User getUserById(Long id) {
        return repository.findById(id);
    }
}
```

**Проблемы:**
- `UserService` нельзя протестировать без поднятой MySQL.
- При переходе на другую БД нужно переписывать `UserService`.
- `UserService` знает о деталях подключения к БД (`url`, `user`, `password`).

#### ✅ Соблюдение DIP: зависимость от абстракции

```java
// ── Абстракция: определяется в слое бизнес-логики ──
// ── (домен/ядро не зависит от инфраструктуры!) ──

public interface UserRepository {
    void save(User user);
    Optional<User> findById(Long id);
    List<User> findAll();
}

// ── Бизнес-логика зависит ТОЛЬКО от абстракции ──

public class UserService {

    private final UserRepository repository;  // ← абстракция!

    /**
     * Зависимость внедряется ИЗВНЕ (через конструктор).
     * UserService не знает и не хочет знать,
     * КАКАЯ ИМЕННО реализация UserRepository используется.
     */
    public UserService(UserRepository repository) {
        this.repository = repository;
    }

    public void registerUser(User user) {
        if (user.getEmail() == null) {
            throw new IllegalArgumentException("Email is required");
        }
        user.setCreatedAt(Instant.now());
        user.setStatus(UserStatus.ACTIVE);
        repository.save(user);
    }

    public Optional<User> getUserById(Long id) {
        return repository.findById(id);
    }
}

// ── Реализации НИЗКОГО уровня (детали) ──

/** MySQL-реализация */
public class MySQLUserRepository implements UserRepository {

    private final JdbcTemplate jdbcTemplate;

    public MySQLUserRepository(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    @Override
    public void save(User user) {
        jdbcTemplate.update(
            "INSERT INTO users (id, email, name, status) VALUES (?,?,?,?)",
            user.getId(), user.getEmail(), user.getName(),
            user.getStatus().name());
    }

    @Override
    public Optional<User> findById(Long id) {
        List<User> users = jdbcTemplate.query(
            "SELECT * FROM users WHERE id = ?",
            new UserRowMapper(), id);
        return users.stream().findFirst();
    }

    @Override
    public List<User> findAll() {
        return jdbcTemplate.query("SELECT * FROM users",
                                   new UserRowMapper());
    }
}

/** PostgreSQL-реализация (может использоваться вместо MySQL) */
public class PostgresUserRepository implements UserRepository {
    // Аналогичная реализация, но с PostgreSQL-синтаксисом
    // ...
}

/** In-memory реализация для тестов */
public class InMemoryUserRepository implements UserRepository {

    private final Map<Long, User> storage = new ConcurrentHashMap<>();

    @Override
    public void save(User user) {
        storage.put(user.getId(), user);
    }

    @Override
    public Optional<User> findById(Long id) {
        return Optional.ofNullable(storage.get(id));
    }

    @Override
    public List<User> findAll() {
        return List.copyOf(storage.values());
    }
}

// ── Тестирование с InMemory-реализацией ──

class UserServiceTest {

    private UserService userService;
    private UserRepository repository;

    @BeforeEach
    void setUp() {
        repository = new InMemoryUserRepository();  // ← подставная реализация
        userService = new UserService(repository);
    }

    @Test
    void shouldRegisterUser() {
        User user = new User("test@example.com", "Test User");
        userService.registerUser(user);

        Optional<User> found = userService.getUserById(user.getId());
        assertThat(found).isPresent();
        assertThat(found.get().getStatus()).isEqualTo(UserStatus.ACTIVE);
    }
}
```

**Что изменилось:**
- `UserService` (высокоуровневый модуль) больше не зависит от MySQL, PostgreSQL или чего-либо ещё.
- И `UserService`, и `MySQLUserRepository` зависят от абстракции `UserRepository`.
- Для тестов используется `InMemoryUserRepository` — быстро, без поднятия БД.
- Для продакшена можно переключиться на `PostgresUserRepository` без изменения `UserService`.

### DIP и внедрение зависимостей (DI)

DIP часто путают с **Dependency Injection (DI)**. Давайте разграничим:

| Концепция | Определение |
|-----------|-------------|
| **DIP (принцип)** | Рекомендация: зависьте от абстракций, а не от конкретики |
| **DI (техника)** | Способ передачи зависимостей объекту извне (через конструктор, сеттер, поле) |
| **IoC Container** | Фреймворк (Spring, Guice, Micronaut), который автоматически создаёт и связывает объекты |

**DIP — это «что делать», DI — «как делать».**

```java
// DIP соблюдён, DI через конструктор:
public class OrderService {
    private final PaymentGateway paymentGateway;  // ← DIP: абстракция

    public OrderService(PaymentGateway paymentGateway) {  // ← DI: внедрение
        this.paymentGateway = paymentGateway;
    }
}

// Spring автоматически внедрит нужную реализацию:
@Service
public class OrderService {
    private final PaymentGateway paymentGateway;

    public OrderService(PaymentGateway paymentGateway) {  // Spring найдёт бин
        this.paymentGateway = paymentGateway;
    }
}
```

### DIP и принцип Голливуда

> **«Не звоните нам — мы вам позвоним.»** (Don't call us, we'll call you.)

DIP тесно связан с принципом Голливуда (Hollywood Principle). Низкоуровневые компоненты регистрируются в системе, а высокоуровневые компоненты **вызывают** их через абстракции, когда это необходимо. Низкоуровневый код не управляет потоком выполнения — он лишь предоставляет реализацию контракта.

```java
// Высокоуровневый модуль: "Я решаю, КОГДА отправлять уведомление"
// Низкоуровневый модуль: "Я знаю, КАК отправить email"

public interface NotificationSender {       // ← абстракция
    void send(String recipient, String message);
}

public class EmailNotificationSender implements NotificationSender {
    @Override
    public void send(String recipient, String message) {
        // SMTP-логика
    }
}

public class SmsNotificationSender implements NotificationSender {
    @Override
    public void send(String recipient, String message) {
        // SMS-шлюз
    }
}

// Высокоуровневый модуль управляет потоком выполнения:
public class AlertService {                  // ← "голливудский" режиссёр
    private final NotificationSender sender;

    public AlertService(NotificationSender sender) {
        this.sender = sender;
    }

    public void sendAlert(User user, String message) {
        // Бизнес-логика: решаем, когда и кому слать
        if (user.hasAlertsEnabled()) {
            sender.send(user.getPhone(), message);  // ← "мы вам позвоним"
        }
    }
}
```

---

## SOLID в реальных проектах

### Пример модуля до Clean Architecture

Рассмотрим, как все пять принципов SOLID работают вместе на примере простого модуля «Управление заказами»:

```java
// ─────────────────────────────────────────────────────────
//  Слой домена (ядро) — НЕ зависит ни от чего
// ─────────────────────────────────────────────────────────

// ISP: узкий интерфейс только для сохранения
public interface OrderRepository {
    void save(Order order);                        // команда
    Optional<Order> findById(OrderId id);          // запрос
}

// ISP: отдельный интерфейс для уведомлений
public interface OrderNotifier {
    void notifyOrderPlaced(Order order);
}

// SRP: класс отвечает только за логику размещения заказа
// DIP: зависит от абстракций, а не от реализаций
// OCP: можно расширить через декораторы/стратегии, не меняя этот класс
public class PlaceOrderUseCase {

    private final OrderRepository repository;
    private final OrderNotifier notifier;

    // DIP + DI: зависимости внедряются через конструктор
    public PlaceOrderUseCase(OrderRepository repository,
                              OrderNotifier notifier) {
        this.repository = repository;
        this.notifier = notifier;
    }

    public OrderId execute(PlaceOrderCommand command) {
        // LSP: метод работает с любой реализацией OrderRepository,
        //      не зная деталей. Любая реализация должна сохранять
        //      заказ корректно — иначе это нарушение LSP.
        Order order = Order.create(command);
        repository.save(order);
        notifier.notifyOrderPlaced(order);
        return order.getId();
    }
}

// ─────────────────────────────────────────────────────────
//  Слой инфраструктуры — зависит от домена
// ─────────────────────────────────────────────────────────

// SRP: отвечает только за SQL-запросы к таблице orders
public class JdbcOrderRepository implements OrderRepository {

    private final JdbcTemplate jdbc;

    public JdbcOrderRepository(DataSource ds) {
        this.jdbc = new JdbcTemplate(ds);
    }

    @Override
    public void save(Order order) { /* SQL INSERT */ }

    @Override
    public Optional<Order> findById(OrderId id) { /* SQL SELECT */ }
}

// SRP: отвечает только за отправку email
// DIP: реализует интерфейс, определённый в домене
public class EmailOrderNotifier implements OrderNotifier {

    private final JavaMailSender mailSender;

    public EmailOrderNotifier(JavaMailSender mailSender) {
        this.mailSender = mailSender;
    }

    @Override
    public void notifyOrderPlaced(Order order) { /* отправка email */ }
}
```

### Связь с паттернами проектирования

Многие паттерны «GoF» (Gang of Four) естественным образом реализуют принципы SOLID:

| Принцип SOLID | Паттерны, реализующие принцип |
|---------------|-------------------------------|
| **SRP** | Facade, Proxy, Adapter |
| **OCP** | Strategy, Decorator, Visitor, Chain of Responsibility, Observer, Template Method |
| **LSP** | Все паттерны на основе полиморфизма: Strategy, State, Command |
| **ISP** | Adapter (при адаптации толстого интерфейса), Bridge, Role Interfaces |
| **DIP** | Abstract Factory, Factory Method, Dependency Injection (через IoC) |

---

## Антипаттерны и типичные ошибки

### 1. «Божественный объект» (God Object)
Класс, который знает и делает всё. Нарушает SRP.

**Решение:** разделить на несколько классов, каждый с одной ответственностью.

### 2. «Синглтон как глобальная переменная»
```java
// ❌ Антипаттерн: жёсткая связь + скрытая зависимость
public class OrderService {
    public void process(Order order) {
        Database.getInstance().save(order);    // ← DIP нарушен
        EmailService.getInstance().send(order); // ← DIP нарушен
    }
}
```

**Решение:** внедряйте зависимости явно через конструктор.

### 3. «Интерфейс-маркер» без методов
Пустой интерфейс типа `Serializable` или `RandomAccess` формально не нарушает ISP, потому что у него нет методов, от которых кто-то может зависеть. Однако многие специалисты считают маркерные интерфейсы кодом с запахом (code smell) и предпочитают аннотации (`@FunctionalInterface`, `@Entity` и др.) — они не добавляют методов в контракт класса и лучше разделяют мета-информацию и поведение. Злоупотребление маркерами может привести к путанице.

### 4. «Преждевременная абстракция»
Создание абстракций «на вырост», когда у вас всего одна реализация:
```java
// Одна реализация — зачем интерфейс?
public interface UserRepository { /* ... */ }
public class DatabaseUserRepository implements UserRepository { /* ... */ }
```

**Правило трёх:** YAGNI (You Aren't Gonna Need It) говорит, что абстракция оправдана, когда есть **минимум две разные реализации**. Тестовый мок/стаб — это уже вторая реализация, поэтому интерфейс для репозитория практически всегда оправдан. Однако если тесты пишутся через integration-тесты с поднятием реальной БД (Testcontainers) и второй реализации не предвидится, создание интерфейса может быть избыточным — здесь важно оценивать контекст.

### 5. «Слепое следование SOLID без понимания»
Превращение каждого класса из 50 строк в 10 классов по 5 строк — это не SOLID, это фетишизм. Принципы должны упрощать жизнь, а не усложнять её. Здравый смысл превыше всего.

### 6. «Смешение DIP и DI»
Использование `@Autowired` на полях не делает ваш код соответствующим DIP:
```java
// ❌ DI есть, а DIP — нет (зависимость от конкретного класса)
@Autowired
private MySQLUserRepository repository;  // ← конкретная реализация!
```

---

## Заключение

Принципы SOLID — это не самоцель, а **инструмент** для создания качественного, поддерживаемого кода. Вот краткая шпаргалка:

| Принцип | Суть одной фразой |
|---------|-------------------|
| **S** | Один класс — одна причина для изменения |
| **O** | Добавляем новое через расширение, а не через правку старого |
| **L** | Наследник должен быть полноценной заменой родителя |
| **I** | Много узких интерфейсов лучше, чем один толстый |
| **D** | Зависим от абстракций, а не от конкретных реализаций |

Ключевые выводы:

1. **SOLID — это про управление зависимостями.** Все пять принципов так или иначе сводятся к тому, чтобы зависимости в коде были направлены к стабильным, абстрактным сущностям, а не к конкретным, изменчивым деталям.

2. **Начинайте с S и D.** Эти два принципа дают самый ощутимый эффект. SRP дисциплинирует мышление («за что отвечает этот класс?»), а DIP переворачивает проектирование с ног на голову, заставляя думать об абстракциях в первую очередь.

3. **Принципы взаимосвязаны.** Соблюдение одного часто помогает соблюдать другие. Например, применяя DIP, вы естественным образом приходите к ISP (узкие интерфейсы проще абстрагировать) и к OCP (легко подменить реализацию).

4. **Не догма, а ориентир.** SOLID — это компас, а не карта. В реальных проектах бывают обоснованные отступления от принципов. Главное — понимать, **почему** вы отступаете и какую цену за это платите.

5. **Читабельность важнее «правильности».** Код читают в десятки раз чаще, чем пишут. Если чрезмерное разделение интерфейсов (ISP) делает код непонятным — вы зашли слишком далеко.
