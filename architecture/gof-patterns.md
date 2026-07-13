# Паттерны проектирования (GoF): Design Patterns

## Оглавление

- [Введение](#введение)
- [1. Порождающие паттерны (Creational)](#1-порождающие-паттерны-creational)
  - [1.1. Singleton (Одиночка)](#11-singleton-одиночка)
  - [1.2. Factory Method (Фабричный метод)](#12-factory-method-фабричный-метод)
  - [1.3. Abstract Factory (Абстрактная фабрика)](#13-abstract-factory-абстрактная-фабрика)
  - [1.4. Builder (Строитель)](#14-builder-строитель)
  - [1.5. Prototype (Прототип)](#15-prototype-прототип)
- [2. Структурные паттерны (Structural)](#2-структурные-паттерны-structural)
  - [2.1. Adapter (Адаптер)](#21-adapter-адаптер)
  - [2.2. Bridge (Мост)](#22-bridge-мост)
  - [2.3. Composite (Компоновщик)](#23-composite-компоновщик)
  - [2.4. Decorator (Декоратор)](#24-decorator-декоратор)
  - [2.5. Facade (Фасад)](#25-facade-фасад)
  - [2.6. Flyweight (Легковес)](#26-flyweight-легковес)
  - [2.7. Proxy (Заместитель)](#27-proxy-заместитель)
- [3. Поведенческие паттерны (Behavioral)](#3-поведенческие-паттерны-behavioral)
  - [3.1. Chain of Responsibility (Цепочка обязанностей)](#31-chain-of-responsibility-цепочка-обязанностей)
  - [3.2. Command (Команда)](#32-command-команда)
  - [3.3. Interpreter (Интерпретатор)](#33-interpreter-интерпретатор)
  - [3.4. Iterator (Итератор)](#34-iterator-итератор)
  - [3.5. Mediator (Посредник)](#35-mediator-посредник)
  - [3.6. Memento (Снимок)](#36-memento-снимок)
  - [3.7. Observer (Наблюдатель)](#37-observer-наблюдатель)
  - [3.8. State (Состояние)](#38-state-состояние)
  - [3.9. Strategy (Стратегия)](#39-strategy-стратегия)
  - [3.10. Template Method (Шаблонный метод)](#310-template-method-шаблонный-метод)
  - [3.11. Visitor (Посетитель)](#311-visitor-посетитель)
- [Шпаргалка для собеседования](#шпаргалка-для-собеседования)

---

## Введение

**Паттерн проектирования (design pattern)** это типовое, многократно проверенное решение часто встречающейся задачи проектирования объектно-ориентированной системы. Паттерн представляет собой не готовый код, а **шаблон**, описывающий идею решения: роли классов, их взаимодействие и распределение ответственности.

### История

В 1994 году четверо авторов (Эрих Гамма, Ричард Хелм, Ральф Джонсон и Джон Влиссидес; известные как **Gang of Four**, «Банда четырёх») опубликовали книгу **«Design Patterns: Elements of Reusable Object-Oriented Software»**. В книге описано 23 паттерна, разбитых на три категории. С тех пор эти паттерны стали фундаментом ОО-проектирования и обязательной темой на технических собеседованиях.

### Три категории паттернов

| Категория | Назначение | Количество |
|-----------|-----------|:----------:|
| **Порождающие (Creational)** | Отвечают за механизмы создания объектов. Позволяют сделать систему независимой от способа создания, композиции и представления объектов. | 5 |
| **Структурные (Structural)** | Описывают способы композиции классов и объектов для образования более крупных структур. Обеспечивают гибкость за счёт правильной организации иерархии. | 7 |
| **Поведенческие (Behavioral)** | Определяют алгоритмы и распределение ответственности между объектами. Описывают сами объекты и схемы их взаимодействия. | 11 |

### Сводная таблица всех паттернов

| # | Паттерн | Категория | Суть одной фразой |
|---|---------|-----------|-------------------|
| 1 | **Singleton** | Порождающий | У класса есть ровно один экземпляр, и к нему предоставлена глобальная точка доступа |
| 2 | **Factory Method** | Порождающий | Делегирует создание объекта подклассам через абстрактный/виртуальный метод |
| 3 | **Abstract Factory** | Порождающий | Создаёт семейства взаимосвязанных объектов без привязки к конкретным классам |
| 4 | **Builder** | Порождающий | Пошаговое конструирование сложного объекта; отделяет процесс строительства от представления |
| 5 | **Prototype** | Порождающий | Создаёт новые объекты путём клонирования существующего экземпляра-прототипа |
| 6 | **Adapter** | Структурный | Преобразует интерфейс одного класса в интерфейс, ожидаемый клиентом |
| 7 | **Bridge** | Структурный | Отделяет абстракцию от реализации так, чтобы они могли изменяться независимо |
| 8 | **Composite** | Структурный | Позволяет единообразно обрабатывать отдельные объекты и их группы (дерево «часть-целое») |
| 9 | **Decorator** | Структурный | Динамически добавляет объекту новую функциональность, оборачивая его |
| 10 | **Facade** | Структурный | Предоставляет унифицированный интерфейс к сложной подсистеме |
| 11 | **Flyweight** | Структурный | Разделяет общее состояние множества мелких объектов для экономии памяти |
| 12 | **Proxy** | Структурный | Предоставляет заместителя (суррогат) для контроля доступа к другому объекту |
| 13 | **Chain of Responsibility** | Поведенческий | Передаёт запрос по цепочке обработчиков, пока один из них не обработает его |
| 14 | **Command** | Поведенческий | Инкапсулирует запрос как объект; даёт возможность параметризовать клиентов, ставить запросы в очередь, логировать и отменять операции |
| 15 | **Interpreter** | Поведенческий | Определяет грамматику языка и интерпретирует предложения этого языка |
| 16 | **Iterator** | Поведенческий | Последовательно обходит элементы коллекции, не раскрывая её внутреннее представление |
| 17 | **Mediator** | Поведенческий | Централизует взаимодействие множества объектов, избавляя их от прямых ссылок друг на друга |
| 18 | **Memento** | Поведенческий | Сохраняет и восстанавливает предыдущее состояние объекта, не нарушая инкапсуляцию |
| 19 | **Observer** | Поведенческий | Определяет зависимость «один-ко-многим»: при изменении состояния одного объекта все зависимые уведомляются |
| 20 | **State** | Поведенческий | Позволяет объекту менять поведение при изменении его внутреннего состояния |
| 21 | **Strategy** | Поведенческий | Определяет семейство взаимозаменяемых алгоритмов, инкапсулируя каждый из них |
| 22 | **Template Method** | Поведенческий | Определяет скелет алгоритма в базовом классе, перекладывая детали на подклассы |
| 23 | **Visitor** | Поведенческий | Добавляет новые операции к объектам, не изменяя их классы |

### Как выбрать подходящий паттерн

> **Простой принцип:** не применяйте паттерн только потому, что вы его знаете. Паттерн это ответ на конкретную проблему. Сначала найдите проблему, потом подходящий паттерн.

- **Проблемы создания объектов** → Порождающие паттерны
- **Проблемы композиции/структуры** → Структурные паттерны
- **Проблемы взаимодействия/распределения ответственности** → Поведенческие паттерны

---

## 1. Порождающие паттерны (Creational)

Порождающие паттерны абстрагируют процесс создания объектов. Они делают систему независимой от того, как именно создаются, компонуются и представляются объекты. Вместо прямого вызова `new Класс()` используется делегирование логики создания специализированным классам или методам.

---

### 1.1. Singleton (Одиночка)

**Назначение:** Гарантирует, что у класса существует ровно один экземпляр, и предоставляет к нему глобальную точку доступа.

**Проблема:** В системе есть ресурс, который должен существовать в единственном экземпляре: подключение к БД, логгер, кэш, менеджер конфигурации. Создание нескольких экземпляров приведёт к некорректному поведению, гонкам за ресурс или перерасходу памяти. При этом доступ к этому единственному экземпляру нужен из любой точки приложения.

**Решение:** Класс сам контролирует создание своего экземпляра: конструктор объявляется приватным, а статический метод возвращает единственный экземпляр, создавая его при первом вызове (lazy) или сразу при загрузке класса (eager).

**Структура (UML):**
```
┌─────────────────────────┐
│       Singleton         │
├─────────────────────────┤
│ - static instance       │
│ - Singleton()  private  │
│ + static getInstance()  │
└─────────────────────────┘
```

**Участники:**
- `Singleton`: класс, который сам хранит ссылку на свой единственный экземпляр и сам решает, когда его создавать.

**Пример на Java:**

```java
/**
 * Потокобезопасный Singleton с double-checked locking.
 * Подходит для большинства случаев в многопоточной среде.
 */
public class DatabaseConnectionPool {

    // volatile гарантирует, что все потоки увидят актуальное значение
    private static volatile DatabaseConnectionPool instance;

    // Приватный конструктор: нельзя создать экземпляр снаружи
    private DatabaseConnectionPool() {
        // Инициализация пула соединений: дорогая операция
        System.out.println("Пул соединений создан (Singleton)");
    }

    // Double-checked locking: потокобезопасно и без лишних блокировок после инициализации
    public static DatabaseConnectionPool getInstance() {
        if (instance == null) {                     // Первая проверка (без блокировки)
            synchronized (DatabaseConnectionPool.class) {
                if (instance == null) {             // Вторая проверка (под блокировкой)
                    instance = new DatabaseConnectionPool();
                }
            }
        }
        return instance;
    }

    public void connect(String url) {
        System.out.println("Подключаюсь к БД: " + url);
    }
}
```

```java
// Демонстрация
public class SingletonDemo {
    public static void main(String[] args) {
        // Нельзя: DatabaseConnectionPool pool = new DatabaseConnectionPool(); // Ошибка компиляции!

        DatabaseConnectionPool pool1 = DatabaseConnectionPool.getInstance();
        DatabaseConnectionPool pool2 = DatabaseConnectionPool.getInstance();

        System.out.println(pool1 == pool2); // true: это один и тот же объект
        pool1.connect("jdbc:postgresql://localhost:5432/mydb");
    }
}
```

**Альтернативные реализации Singleton в Java:**

```java
// --- Вариант 1: Eager initialization (создание при загрузке класса) ---
// Потокобезопасно «из коробки» (JVM гарантирует однократную статическую инициализацию)
public class EagerSingleton {
    private static final EagerSingleton INSTANCE = new EagerSingleton();
    private EagerSingleton() {}
    public static EagerSingleton getInstance() { return INSTANCE; }
}

// --- Вариант 2: Enum Singleton (рекомендован Джошуа Блохом) ---
// 100% защита от рефлексии и сериализации, потокобезопасность «из коробки»
public enum EnumSingleton {
    INSTANCE;

    public void doSomething() {
        System.out.println("Enum Singleton работает");
    }
}
// Использование: EnumSingleton.INSTANCE.doSomething();

// --- Вариант 3: Static Holder (ленивая инициализация без synchronized) ---
public class HolderSingleton {
    private HolderSingleton() {}
    private static class Holder {
        static final HolderSingleton INSTANCE = new HolderSingleton();
    }
    public static HolderSingleton getInstance() { return Holder.INSTANCE; }
}
```

**Плюсы и минусы:**
- [+] Гарантирует единственный экземпляр класса
- [+] Глобальная точка доступа: удобно
- [+] Ленивая инициализация (lazy) экономит ресурсы, если объект не понадобился
- [-] Нарушает **Single Responsibility Principle** (с точки зрения SOLID): класс управляет и своей логикой, и своим созданием
- [-] Усложняет unit-тестирование (глобальное состояние, сложно замокать)
- [-] Это глобальная переменная, что приводит к неявным зависимостям
- [-] В многопоточном коде требует аккуратной реализации (double-checked locking: хрупкий)

**Когда применять:**
- Когда в системе должен быть ровно один экземпляр какого-либо класса (пул соединений, конфигурация, логгер, кэш)
- Когда этот единственный экземпляр должен быть доступен из любой точки приложения
- Когда требуется более гибкий контроль создания, чем глобальная переменная (например, ленивая инициализация)

**Связи с другими паттернами:**
- Часто используется совместно с Facade (фасад сам может быть синглтоном)
- Abstract Factory, Builder и Prototype могут быть реализованы как синглтоны
- Многие паттерны могут использовать синглтон для хранения своего состояния (но это спорная практика)

---

### 1.2. Factory Method (Фабричный метод)

**Назначение:** Определяет интерфейс для создания объекта, но позволяет подклассам решать, экземпляр какого класса создавать. **Делегирует создание подклассам.**

**Проблема:** Предположим, вы разрабатываете библиотеку для работы с отчётами. Вы знаете, что отчёт нужно создать и сохранить, но **не знаете заранее**, в каком формате: PDF, Excel, HTML. Вы не хотите зашивать конкретные классы в код библиотеки: это сделает её нерасширяемой. При этом общий алгоритм работы с отчётом одинаков.

**Решение:** Выделить создание объекта в отдельный метод: **фабричный метод**. Базовый класс определяет абстрактный метод `createReport()`, а конкретные подклассы (PdfReportCreator, ExcelReportCreator) переопределяют его, возвращая нужный тип отчёта.

**Структура (UML):**
```
┌───────────────────────┐         ┌────────────────────┐
│   Creator (abstract)  │         │    Product (intf)   │
├───────────────────────┤         ├────────────────────┤
│ + someOperation()     │────────>│                    │
│ + createProduct()     │         └────────────────────┘
│   abstract            │                  ▲
└───────────────────────┘                  │
            ▲                 ┌────────────┼────────────┐
            │                 │            │            │
   ┌────────┴────────┐  ┌────┴────┐  ┌────┴────┐  ┌────┴────┐
   │ ConcreteCreator  │  │ProductA │  │ProductB │  │ProductC │
   ├──────────────────┤  └─────────┘  └─────────┘  └─────────┘
   │ + createProduct()│
   └──────────────────┘
```

**Участники:**
- `Product`: интерфейс (или абстрактный класс) создаваемых объектов
- `ConcreteProduct`: конкретная реализация продукта
- `Creator`: абстрактный класс с фабричным методом `createProduct()`; может содержать бизнес-логику, использующую продукт
- `ConcreteCreator`: подкласс, переопределяющий `createProduct()` для создания конкретного продукта

**Пример на Java:**

```java
// ===== Продукты =====
interface Report {
    void generate(String data);
}

class PdfReport implements Report {
    @Override
    public void generate(String data) {
        System.out.println("Создаю PDF-отчёт: " + data);
    }
}

class ExcelReport implements Report {
    @Override
    public void generate(String data) {
        System.out.println("Создаю Excel-отчёт: " + data);
    }
}

class HtmlReport implements Report {
    @Override
    public void generate(String data) {
        System.out.println("Создаю HTML-отчёт: " + data);
    }
}

// ===== Создатели =====
abstract class ReportCreator {

    // Фабричный метод: ключевой элемент паттерна
    protected abstract Report createReport();

    // Общая бизнес-логика, не зависящая от конкретного типа отчёта
    public void exportReport(String data) {
        Report report = createReport();       // Создание делегировано подклассам
        report.generate(data);                // Работа с продуктом через общий интерфейс
        System.out.println("Отчёт экспортирован.");
    }
}

class PdfReportCreator extends ReportCreator {
    @Override
    protected Report createReport() {
        return new PdfReport();
    }
}

class ExcelReportCreator extends ReportCreator {
    @Override
    protected Report createReport() {
        return new ExcelReport();
    }
}

// ===== Демонстрация =====
public class FactoryMethodDemo {
    public static void main(String[] args) {
        ReportCreator pdfCreator = new PdfReportCreator();
        pdfCreator.exportReport("Данные для PDF");

        ReportCreator excelCreator = new ExcelReportCreator();
        excelCreator.exportReport("Данные для Excel");

        // Добавление нового формата НЕ требует изменения существующего кода (OCP!)
        // Достаточно создать HtmlReport и HtmlReportCreator
    }
}
```

**Плюсы и минусы:**
- [+] Устраняет жёсткую привязку между Creator и конкретными классами продуктов
- [+] **Open/Closed Principle**: можно добавить новый продукт, не трогая существующий код Creator
- [+] **Single Responsibility Principle**: код создания вынесен в одно место
- [+] Общая бизнес-логика Creator работает с продуктами через единый интерфейс
- [-] Может привести к взрывному росту числа классов (для каждого продукта нужен свой Creator)
- [-] Клиент должен знать, какой именно Creator ему нужен (проблема частично решается Abstract Factory или DI)

**Когда применять:**
- Когда класс не знает заранее, объекты каких конкретных классов ему потребуется создавать
- Когда класс хочет, чтобы его подклассы определяли тип создаваемых объектов
- Когда нужно делегировать создание подклассам, но сохранить общую бизнес-логику в базовом классе

**Связи с другими паттернами:**
- Abstract Factory часто реализуется с помощью нескольких Factory Method
- Factory Method часто вызывается внутри Template Method (базовый алгоритм вызывает фабричный метод)
- Может эволюционировать в Abstract Factory, Builder или Prototype по мере усложнения требований

---

### 1.3. Abstract Factory (Абстрактная фабрика)

**Назначение:** Предоставляет интерфейс для создания **семейств взаимосвязанных или взаимозависимых объектов** без указания их конкретных классов.

**Проблема:** Вы пишете кроссплатформенное GUI-приложение. У вас есть семейства элементов интерфейса: `Button`, `Checkbox`, `TextField`. Для каждой ОС (Windows, Mac, Linux) нужна своя реализация этих элементов. При этом вы не хотите, чтобы код приложения зависел от конкретной ОС: везде должны использоваться абстрактные `Button`, `Checkbox`. И нельзя допустить, чтобы на Mac использовалась Windows-кнопка: все элементы должны быть из одного семейства.

**Решение:** Выделить интерфейс абстрактной фабрики (`GUIFactory`) с методами `createButton()`, `createCheckbox()`, `createTextField()`. Для каждой платформы реализовать свою конкретную фабрику (`WinFactory`, `MacFactory`). Клиент работает только с абстрактной фабрикой и абстрактными продуктами.

**Структура (UML):**
```
┌─────────────────────────┐
│   AbstractFactory (intf)│         ┌──────────────┐    ┌──────────────┐
├─────────────────────────┤         │ ProductA(intf)│    │ ProductB(intf)│
│ + createProductA()      │────────>└──────────────┘    └──────────────┘
│ + createProductB()      │               ▲                     ▲
└─────────────────────────┘         ┌─────┴─────┐         ┌─────┴─────┐
            ▲                       │           │         │           │
   ┌────────┴────────┐        ProductA1  ProductA2    ProductB1  ProductB2
   │                 │
ConcreteFactory1  ConcreteFactory2
```

**Участники:**
- `AbstractFactory`: интерфейс с методами для создания каждого типа продукта из семейства
- `ConcreteFactory`: реализует создание продуктов конкретного семейства (например, Windows-семейства)
- `AbstractProduct`: интерфейс для каждого типа продукта (Button, Checkbox...)
- `ConcreteProduct`: конкретная реализация продукта для определённого семейства

**Пример на Java:**

```java
// ===== Абстрактные продукты =====
interface Button {
    void paint();
}

interface Checkbox {
    void paint();
}

// ===== Конкретные продукты для Windows =====
class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("Рисую кнопку в стиле Windows");
    }
}

class WindowsCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Рисую чекбокс в стиле Windows");
    }
}

// ===== Конкретные продукты для Mac =====
class MacButton implements Button {
    @Override
    public void paint() {
        System.out.println("Рисую кнопку в стиле macOS");
    }
}

class MacCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Рисую чекбокс в стиле macOS");
    }
}

// ===== Абстрактная фабрика =====
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// ===== Конкретные фабрики =====
class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() { return new WindowsButton(); }
    @Override
    public Checkbox createCheckbox() { return new WindowsCheckbox(); }
}

class MacFactory implements GUIFactory {
    @Override
    public Button createButton() { return new MacButton(); }
    @Override
    public Checkbox createCheckbox() { return new MacCheckbox(); }
}

// ===== Клиентский код (не зависит от конкретной платформы!) =====
class Application {
    private final Button button;
    private final Checkbox checkbox;

    public Application(GUIFactory factory) {
        button = factory.createButton();       // Продукты из одного семейства
        checkbox = factory.createCheckbox();   // гарантированы фабрикой
    }

    public void render() {
        button.paint();
        checkbox.paint();
    }
}

// ===== Демонстрация =====
public class AbstractFactoryDemo {
    public static void main(String[] args) {
        GUIFactory factory;

        String os = System.getProperty("os.name").toLowerCase();
        if (os.contains("win")) {
            factory = new WindowsFactory();
        } else {
            factory = new MacFactory();
        }

        Application app = new Application(factory);
        app.render();
        // При смене ОС меняется только одна строка: выбор фабрики.
        // Весь остальной код остаётся неизменным.
    }
}
```

**Плюсы и минусы:**
- [+] Гарантирует совместимость продуктов из одного семейства
- [+] Изолирует клиента от конкретных классов продуктов
- [+] Упрощает замену всего семейства продуктов (поменяли фабрику: поменялось всё)
- [+] **Open/Closed Principle**: можно добавить новое семейство (Linux), не меняя существующий код
- [-] Сложно добавить новый тип продукта: придётся менять интерфейс фабрики и все её реализации
- [-] Увеличивает количество классов и усложняет код

**Когда применять:**
- Когда система должна создавать семейства взаимосвязанных продуктов
- Когда система не должна зависеть от того, как создаются, компонуются и представляются её продукты
- Когда нужно гарантировать, что продукты из разных семейств не будут смешиваться (Windows-кнопка + Mac-чекбокс: недопустимо)

**Связи с другими паттернами:**
- Конкретные фабрики часто реализуются через Factory Method (каждый метод фабрики: фабричный метод)
- Легко превращается в Singleton, если фабрика в системе одна
- Prototype может заменить Abstract Factory, если продукты клонируются, а не создаются с нуля

---

### 1.4. Builder (Строитель)

**Назначение:** Отделяет конструирование сложного объекта от его представления. Один и тот же процесс конструирования может создавать **разные представления** объекта.

**Проблема:** Вы создаёте объект с 10+ параметрами, многие из которых опциональны. Конструктор с 10 параметрами нечитаем (`new House(4, 2, "red", "tile", true, false, ...)`: попробуй пойми, что за что отвечает). Создание через set-методы распыляет логику и позволяет создать «недособранный» объект. Кроме того, бывает нужно создавать разные представления одного и того же набора данных (дом из дерева, дом из кирпича, дом из панелей это всё дома, но собираются по-разному).

**Решение:** Вынести логику сборки в отдельный класс `Builder` с методами-шагами (каждый возвращает самого Builder для цепочечного вызова: fluent interface). Класс `Director` управляет порядком шагов сборки (для стандартных конфигураций). Клиент может работать напрямую с Builder или через Director.

**Структура (UML):**
```
┌──────────────────┐         ┌─────────────────────┐
│     Director     │         │    Builder (intf)    │
├──────────────────┤         ├─────────────────────┤
│ + construct()    │────────>│ + buildPartA()       │
└──────────────────┘         │ + buildPartB()       │
                             │ + getResult()        │
                             └─────────────────────┘
                                       ▲
                              ┌────────┴────────┐
                              │ ConcreteBuilder  │
                              ├──────────────────┤
                              │ + buildPartA()    │
                              │ + buildPartB()    │
                              │ + getResult()     │
                              └──────────────────┘
                                       │
                                       │ создаёт
                                       ▼
                              ┌──────────────────┐
                              │     Product      │
                              └──────────────────┘
```

**Участники:**
- `Product`: сложный конструируемый объект
- `Builder`: интерфейс с шагами конструирования
- `ConcreteBuilder`: конкретная реализация Builder, создающая конкретное представление Product
- `Director` (опционально): управляет порядком шагов для построения стандартных конфигураций

**Пример на Java:**

```java
// ===== Продукт: сложный объект с множеством параметров =====
class Pizza {
    private final String dough;      // Тесто
    private final String sauce;      // Соус
    private final String cheese;     // Сыр
    private final boolean pepperoni; // Пепперони
    private final boolean mushrooms; // Грибы
    private final boolean olives;    // Оливки

    // Приватный конструктор: создаётся только через Builder
    private Pizza(PizzaBuilder builder) {
        this.dough = builder.dough;
        this.sauce = builder.sauce;
        this.cheese = builder.cheese;
        this.pepperoni = builder.pepperoni;
        this.mushrooms = builder.mushrooms;
        this.olives = builder.olives;
    }

    @Override
    public String toString() {
        return "Пицца: тесто=" + dough + ", соус=" + sauce + ", сыр=" + cheese +
               ", пепперони=" + pepperoni + ", грибы=" + mushrooms + ", оливки=" + olives;
    }

    // ===== Builder (статический вложенный класс) =====
    public static class PizzaBuilder {
        // Обязательные параметры
        private final String dough;
        private final String sauce;
        private final String cheese;

        // Опциональные параметры (с разумными значениями по умолчанию)
        private boolean pepperoni = false;
        private boolean mushrooms = false;
        private boolean olives = false;

        // Конструктор Builder принимает только обязательные параметры
        public PizzaBuilder(String dough, String sauce, String cheese) {
            this.dough = dough;
            this.sauce = sauce;
            this.cheese = cheese;
        }

        // Fluent-методы для опциональных параметров (каждый возвращает this)
        public PizzaBuilder addPepperoni() {
            this.pepperoni = true;
            return this;
        }

        public PizzaBuilder addMushrooms() {
            this.mushrooms = true;
            return this;
        }

        public PizzaBuilder addOlives() {
            this.olives = true;
            return this;
        }

        // Финальный метод: создаёт Product
        public Pizza build() {
            return new Pizza(this);
        }
    }
}

// ===== Director (опционально): знает типовые рецепты =====
class PizzaDirector {
    public Pizza makeMargherita() {
        return new Pizza.PizzaBuilder("тонкое", "томатный", "моцарелла").build();
    }

    public Pizza makePepperoni() {
        return new Pizza.PizzaBuilder("тонкое", "томатный", "моцарелла")
                .addPepperoni()
                .build();
    }

    public Pizza makeVegetarian() {
        return new Pizza.PizzaBuilder("толстое", "сливочный", "чеддер")
                .addMushrooms()
                .addOlives()
                .build();
    }
}

// ===== Демонстрация =====
public class BuilderDemo {
    public static void main(String[] args) {
        // Способ 1: напрямую через Builder (полный контроль)
        Pizza customPizza = new Pizza.PizzaBuilder("тонкое", "барбекю", "пармезан")
                .addPepperoni()
                .addMushrooms()
                .build();
        System.out.println(customPizza);

        // Способ 2: через Director (типовые рецепты)
        PizzaDirector chef = new PizzaDirector();
        System.out.println(chef.makeMargherita());
        System.out.println(chef.makePepperoni());
        System.out.println(chef.makeVegetarian());
    }
}
```

**Плюсы и минусы:**
- [+] **Fluent Interface**: код читается как естественный язык
- [+] Позволяет пошагово конструировать сложные объекты
- [+] Один и тот же Builder может создавать разные представления (если изменить шаги)
- [+] Изолирует код сборки от бизнес-логики продукта
- [+] Можно контролировать валидацию в методе `build()`: не дать создать некорректный объект
- [-] Увеличивает количество кода (Builder + Director + Product)
- [-] Объект должен быть мутабельным на этапе сборки (Builder хранит все поля, Product может быть иммутабельным)
- [-] Не подходит для простых объектов с 2-3 параметрами: избыточен

**Когда применять:**
- Когда у объекта много параметров (особенно опциональных)
- Когда процесс создания объекта состоит из нескольких шагов
- Когда нужно создавать разные представления одного и того же объекта (деревянный дом vs кирпичный дом)
- Когда нужно гарантировать консистентность объекта на момент его создания

**Связи с другими паттернами:**
- Abstract Factory создаёт продукт сразу (одним вызовом), Builder: пошагово
- Composite часто создаётся с помощью Builder (рекурсивное построение дерева)
- Builder может быть реализован как Strategy (разные стратегии сборки)

---

### 1.5. Prototype (Прототип)

**Назначение:** Создаёт новые объекты путём **клонирования** существующего объекта-прототипа, вместо вызова конструктора.

**Проблема:** Создание объекта через `new` может быть дорогим (сложная инициализация, запросы к БД, загрузка конфигурации). Кроме того, иногда нужно создать объект, идентичный существующему, но с небольшими изменениями. Или же система должна создавать объекты, чьи конкретные классы неизвестны на этапе компиляции (например, плагины, загружаемые динамически).

**Решение:** Объект-прототип реализует метод `clone()`, который возвращает его глубокую (или поверхностную) копию. Клиент запрашивает у прототипа его копию вместо вызова конструктора. Фабрика прототипов может хранить словарь прототипов и создавать объекты по ключу.

**Структура (UML):**
```
┌───────────────────────┐         ┌────────────────────┐
│       Client          │         │  Prototype (intf)  │
├───────────────────────┤         ├────────────────────┤
│ - prototype: Prototype│────────>│ + clone(): Prototype│
│ + operation()         │         └────────────────────┘
└───────────────────────┘                   ▲
                                   ┌────────┴────────┐
                                   │                 │
                            ConcretePrototype1  ConcretePrototype2
```

**Участники:**
- `Prototype`: интерфейс с методом `clone()`
- `ConcretePrototype`: реализует клонирование самого себя
- `Client`: создаёт новые объекты через вызов `clone()` у прототипа

**Пример на Java:**

```java
// ===== Интерфейс прототипа =====
interface Shape {
    Shape clone();           // Возвращает копию самого себя (используем конструктор копирования, а не Cloneable)
    void draw();
}

// ===== Конкретные прототипы =====
class Circle implements Shape {
    private int radius;
    private String color;

    public Circle(int radius, String color) {
        // Имитация дорогой инициализации (загрузка из БД, вычисления и т.д.)
        System.out.println("Дорогое создание Circle (radius=" + radius + ", color=" + color + ")");
        this.radius = radius;
        this.color = color;
    }

    // Конструктор копирования (альтернатива clone())
    public Circle(Circle source) {
        this.radius = source.radius;
        this.color = source.color;
    }

    @Override
    public Circle clone() {
        // Конструктор копирования: предпочтительная альтернатива Cloneable/super.clone()
        return new Circle(this);   // Не вызывает «дорогую» логику
    }

    @Override
    public void draw() {
        System.out.println("Рисую круг: радиус=" + radius + ", цвет=" + color);
    }

    // Геттеры/сеттеры для тонкой настройки клона
    public void setColor(String color) { this.color = color; }
}

class Rectangle implements Shape {
    private int width, height;
    private String color;

    public Rectangle(int width, int height, String color) {
        System.out.println("Дорогое создание Rectangle (" + width + "x" + height + ")");
        this.width = width;
        this.height = height;
        this.color = color;
    }

    // Конструктор копирования
    public Rectangle(Rectangle source) {
        this.width = source.width;
        this.height = source.height;
        this.color = source.color;
    }

    @Override
    public Rectangle clone() {
        return new Rectangle(this);
    }

    @Override
    public void draw() {
        System.out.println("Рисую прямоугольник: " + width + "x" + height + ", цвет=" + color);
    }

    public void setColor(String color) { this.color = color; }
}

// ===== Фабрика прототипов (хранит эталонные экземпляры) =====
class ShapeRegistry {
    private final Map<String, Shape> prototypes = new HashMap<>();

    public void register(String key, Shape prototype) {
        prototypes.put(key, prototype);
    }

    public Shape create(String key) {
        Shape prototype = prototypes.get(key);
        if (prototype == null) {
            throw new IllegalArgumentException("Прототип не найден: " + key);
        }
        return prototype.clone();   // Клонирование вместо new: быстро!
    }
}

// ===== Демонстрация =====
public class PrototypeDemo {
    public static void main(String[] args) {
        // Один раз «дорого» создаём эталонные прототипы
        ShapeRegistry registry = new ShapeRegistry();
        registry.register("red-circle", new Circle(10, "red"));
        registry.register("blue-rect", new Rectangle(20, 30, "blue"));

        System.out.println("\n--- Создаём клоны (быстро, без дорогой инициализации) ---");

        // Клонирование: «дёшево», конструктор копирования не печатает сообщение
        Shape circle1 = registry.create("red-circle");
        circle1.draw();             // Рисую круг: радиус=10, цвет=red

        Shape circle2 = registry.create("red-circle");
        ((Circle) circle2).setColor("green");  // Тонкая настройка клона
        circle2.draw();             // Рисую круг: радиус=10, цвет=green

        Shape rect = registry.create("blue-rect");
        rect.draw();                // Рисую прямоугольник: 20x30, цвет=blue
    }
}
```

**Плюсы и минусы:**
- [+] Ускоряет создание объектов (клонирование быстрее, чем «дорогой» конструктор)
- [+] Позволяет создавать объекты, не зная их конкретных классов (динамическая загрузка)
- [+] Даёт возможность тонко настраивать клон после клонирования
- [+] Избавляет от разрастания иерархии фабрик
- [-] Сложность реализации глубокого клонирования (объекты со ссылками на другие объекты)
- [-] Каждый подкласс должен переопределять `clone()`: легко забыть в большой иерархии
- [-] `Cloneable` в Java: «broken»-интерфейс (не содержит метода `clone()`, только маркер)

**Когда применять:**
- Когда создание объекта «в лоб» дороже клонирования (загрузка из БД, вычисления)
- Когда система должна создавать объекты, чьи классы неизвестны на этапе компиляции
- Когда нужно создавать множество похожих объектов, отличающихся несколькими параметрами
- Когда иерархия фабрик дублирует иерархию продуктов (Prototype позволяет обойтись без фабрик)

**Связи с другими паттернами:**
- Часто используется вместе с Abstract Factory (Factory хранит прототипы и клонирует их)
- Memento и Prototype оба работают с состоянием объекта, но с разными целями (откат vs создание)
- Может заменить Factory Method в языках с прототипным наследованием (JavaScript)

---

## 2. Структурные паттерны (Structural)

Структурные паттерны решают вопросы композиции классов и объектов. Они помогают собрать из отдельных частей гибкую и расширяемую структуру, которая эффективно работает и легко модифицируется.

---

### 2.1. Adapter (Адаптер)

**Назначение:** Преобразует интерфейс одного класса в интерфейс, ожидаемый клиентом. Позволяет классам с **несовместимыми интерфейсами** работать вместе.

**Проблема:** У вас есть готовый, отлаженный сторонний класс (библиотека, legacy-код), но его интерфейс не совпадает с тем, что ожидает ваш клиентский код. Переписывать библиотеку нельзя (или нежелательно), а менять клиента: дорого и рискованно. Нужен «переходник».

**Решение:** Создать класс-адаптер, который реализует нужный клиенту интерфейс и **делегирует** вызовы адаптируемому классу, попутно преобразуя форматы данных или сигнатуры методов.

Различают два вида адаптеров:
- **Адаптер объекта (Object Adapter)**: использует композицию: хранит ссылку на адаптируемый объект
- **Адаптер класса (Class Adapter)**: использует множественное наследование (в Java: наследование + имплементация интерфейса)

**Структура (UML): Адаптер объекта:**
```
┌─────────────────┐         ┌─────────────────────┐         ┌──────────────────┐
│     Client      │         │  Target (interface)  │         │     Adaptee      │
├─────────────────┤         ├─────────────────────┤         ├──────────────────┤
│                 │────────>│ + request()          │         │ + specificRequest│
└─────────────────┘         └─────────────────────┘         └──────────────────┘
                                       ▲                              ▲
                                       │                              │
                              ┌────────┴────────┐                      │
                              │    Adapter      │──────────────────────┘
                              ├─────────────────┤   (композиция)
                              │ - adaptee       │
                              │ + request()     │───> adaptee.specificRequest()
                              └─────────────────┘
```

**Участники:**
- `Target`: интерфейс, ожидаемый клиентом
- `Client`: использует объекты только через Target
- `Adaptee`: существующий класс с полезным, но несовместимым интерфейсом
- `Adapter`: оборачивает Adaptee и преобразует вызовы Target → Adaptee

**Пример на Java:**

```java
// ===== Target: интерфейс, ожидаемый клиентом =====
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// ===== Adaptee: сторонний класс с несовместимым интерфейсом =====
class AdvancedMediaPlayer {
    public void playMp4(String fileName) {
        System.out.println("Проигрываю MP4: " + fileName);
    }

    public void playAvi(String fileName) {
        System.out.println("Проигрываю AVI: " + fileName);
    }
}

// ===== Adapter: преобразует интерфейс Adaptee в Target =====
class MediaAdapter implements MediaPlayer {
    private final AdvancedMediaPlayer advancedPlayer;   // Композиция

    public MediaAdapter() {
        this.advancedPlayer = new AdvancedMediaPlayer();
    }

    @Override
    public void play(String audioType, String fileName) {
        // Преобразование «старого» интерфейса в «новый»
        if (audioType.equalsIgnoreCase("mp4")) {
            advancedPlayer.playMp4(fileName);
        } else if (audioType.equalsIgnoreCase("avi")) {
            advancedPlayer.playAvi(fileName);
        } else {
            System.out.println("Неподдерживаемый формат: " + audioType);
        }
    }
}

// ===== Client: работает только через Target =====
class AudioPlayer implements MediaPlayer {
    private MediaAdapter adapter;

    @Override
    public void play(String audioType, String fileName) {
        if (audioType.equalsIgnoreCase("mp3")) {
            System.out.println("Проигрываю MP3: " + fileName);
        } else {
            // Используем адаптер для неподдерживаемых «напрямую» форматов
            adapter = new MediaAdapter();
            adapter.play(audioType, fileName);
        }
    }
}

// ===== Демонстрация =====
public class AdapterDemo {
    public static void main(String[] args) {
        AudioPlayer player = new AudioPlayer();

        player.play("mp3", "song.mp3");   // Работает напрямую
        player.play("mp4", "movie.mp4");   // Через адаптер
        player.play("avi", "clip.avi");    // Через адаптер
    }
}
```

**Плюсы и минусы:**
- [+] Позволяет использовать готовый код без его модификации (Open/Closed Principle)
- [+] Разделяет обязанности: адаптер отвечает только за преобразование интерфейса
- [+] Адаптер объекта позволяет адаптировать целую иерархию Adaptee (через композицию)
- [-] Увеличивает количество классов
- [-] Адаптер класса не работает в языках без множественного наследования (в Java: только через интерфейсы)
- [-] Может добавить накладные расходы на делегирование (обычно незначительные)

**Когда применять:**
- Когда нужно использовать существующий класс, но его интерфейс несовместим с ожидаемым
- Когда нужно создать повторно используемый класс, который будет работать с неизвестными заранее классами
- Когда нужно, чтобы несколько существующих подклассов работали через единый интерфейс (адаптер объекта)

**Связи с другими паттернами:**
- Bridge проектируется заранее для независимого развития абстракции и реализации; Adapter применяется post-hoc для уже существующего кода
- Decorator добавляет новое поведение, не меняя интерфейс; Adapter меняет интерфейс на другой
- Facade предоставляет упрощённый интерфейс к подсистеме; Adapter: преобразует один интерфейс в другой
- Proxy имеет тот же интерфейс, что и реальный объект; Adapter: другой

---

### 2.2. Bridge (Мост)

**Назначение:** Отделяет абстракцию от реализации так, чтобы они могли изменяться независимо. Вместо жёсткой привязки через наследование используется композиция: абстракция хранит ссылку на реализацию.

**Проблема:** При использовании наследования для комбинирования двух независимых измерений (например, «тип фигуры» × «способ рисования») количество классов растёт экспоненциально: `Круг_Вектор`, `Круг_Растр`, `Квадрат_Вектор`, `Квадрат_Растр`... При добавлении нового измерения приходится создавать ветку классов для каждой комбинации.

**Решение:** Разделить два измерения на две независимые иерархии: абстракцию (что делаем: фигура) и реализацию (как делаем: способ рисования). Абстракция хранит ссылку на реализацию и делегирует ей конкретную работу.

**Структура (UML):**
```
┌─────────────────────────┐         ┌───────────────────────┐
│   Abstraction           │         │  Implementor (intf)   │
├─────────────────────────┤         ├───────────────────────┤
│ - implementor: Impl     │────────>│ + operationImpl()     │
│ + operation()           │         └───────────────────────┘
└─────────────────────────┘                    ▲
            ▲                       ┌──────────┴──────────┐
   ┌────────┴────────┐              │                     │
   │ RefinedAbstr.   │       ConcreteImplA         ConcreteImplB
   └─────────────────┘
```

**Участники:**
- `Abstraction`: определяет интерфейс высокого уровня; хранит ссылку на `Implementor`
- `RefinedAbstraction`: расширяет/уточняет абстракцию
- `Implementor`: интерфейс низкоуровневой реализации
- `ConcreteImplementor`: конкретная реализация

**Пример на Java:**

```java
// ===== Implementor: интерфейс «реализации» =====
interface Renderer {
    void renderCircle(double radius);
    void renderRectangle(double width, double height);
}

// ===== Concrete Implementors =====
class VectorRenderer implements Renderer {
    @Override
    public void renderCircle(double radius) {
        System.out.println("Рисую круг (вектор), радиус=" + radius);
    }
    @Override
    public void renderRectangle(double width, double height) {
        System.out.println("Рисую прямоугольник (вектор): " + width + "x" + height);
    }
}

class RasterRenderer implements Renderer {
    @Override
    public void renderCircle(double radius) {
        System.out.println("Рисую круг (растр), радиус=" + radius + "px");
    }
    @Override
    public void renderRectangle(double width, double height) {
        System.out.println("Рисую прямоугольник (растр): " + width + "x" + height + "px");
    }
}

// ===== Abstraction: «что» рисуем =====
abstract class Shape {
    protected Renderer renderer;   // Мост к реализации

    protected Shape(Renderer renderer) {
        this.renderer = renderer;
    }

    public abstract void draw();
}

// ===== Refined Abstractions =====
class Circle extends Shape {
    private final double radius;

    public Circle(Renderer renderer, double radius) {
        super(renderer);
        this.radius = radius;
    }

    @Override
    public void draw() {
        renderer.renderCircle(radius);   // Делегирование реализации
    }
}

class Rectangle extends Shape {
    private final double width, height;

    public Rectangle(Renderer renderer, double width, double height) {
        super(renderer);
        this.width = width;
        this.height = height;
    }

    @Override
    public void draw() {
        renderer.renderRectangle(width, height);
    }
}

// ===== Демонстрация =====
public class BridgeDemo {
    public static void main(String[] args) {
        // Комбинируем любую фигуру с любым рендерером: без экспоненциального роста классов!
        Shape vectorCircle = new Circle(new VectorRenderer(), 5.0);
        Shape rasterCircle = new Circle(new RasterRenderer(), 5.0);
        Shape vectorRect = new Rectangle(new VectorRenderer(), 10, 20);
        Shape rasterRect = new Rectangle(new RasterRenderer(), 10, 20);

        vectorCircle.draw();
        rasterCircle.draw();
        vectorRect.draw();
        rasterRect.draw();

        // Добавление нового рендерера (например, 3D): всего 1 класс, не 2^N!
    }
}
```

**Плюсы и минусы:**
- [+] Устраняет экспоненциальный рост иерархии при комбинировании независимых измерений
- [+] Абстракция и реализация могут развиваться независимо (изменения в реализации не ломают абстракцию)
- [+] Клиентский код работает только с абстракцией (не знает о реализации)
- [+] Можно переключать реализацию на лету (setter для Implementor)
- [-] Усложняет код (дополнительный уровень абстракции)
- [-] Требует хорошего проектирования заранее: рефакторить существующее наследование в Bridge сложно

**Когда применять:**
- Когда нужно избежать постоянной привязки между абстракцией и реализацией
- Когда и абстракция, и реализация должны расширяться через наследование
- Когда изменения в реализации не должны влиять на клиентов
- Когда нужно спрятать реализацию от клиента полностью

**Связи с другими паттернами:**
- Adapter адаптирует уже существующие классы; Bridge проектируется заранее
- State и Strategy структурно похожи на Bridge, но решают другие задачи (поведение, а не структура)
- Abstract Factory может использоваться для выбора и настройки конкретной комбинации Bridge

---

### 2.3. Composite (Компоновщик)

**Назначение:** Позволяет единообразно обрабатывать как **отдельные объекты**, так и их **группы (композиции)**, организованные в древовидную структуру «часть-целое».

**Проблема:** В вашем приложении есть иерархия объектов типа «файл-папка», «задача-подзадача» или «элемент GUI: панель с элементами». Клиентский код должен выполнять одни и те же операции (отобразить, вычислить размер, удалить) как над отдельным элементом, так и над группой. Без паттерна клиенту приходится различать `if (obj is Folder)` и `if (obj is File)`, что делает код хрупким и нарушает принцип подстановки Лисков.

**Решение:** Ввести общий интерфейс `Component`, который реализуют и «листья» (отдельные объекты), и «узлы» (контейнеры). Контейнер хранит коллекцию дочерних Component и делегирует им вызовы.

**Структура (UML):**
```
┌───────────────────────────┐
│   Component (interface)   │
├───────────────────────────┤
│ + operation()             │
│ + add(Component)          │
│ + remove(Component)       │
│ + getChild(int)           │
└───────────────────────────┘
            ▲
   ┌────────┴────────┐
   │                 │
┌──┴──────────┐  ┌───┴──────────────┐
│   Leaf      │  │   Composite      │
├─────────────┤  ├──────────────────┤
│ + operation │  │ - children: List │
│   ()        │  │ + operation()    │──> for child: child.operation()
└─────────────┘  │ + add()          │
                 │ + remove()       │
                 └──────────────────┘
```

**Участники:**
- `Component`: общий интерфейс для всех объектов в иерархии
- `Leaf`: конечный объект (не имеет дочерних)
- `Composite`: контейнер, хранит дочерние Component и делегирует им работу

**Пример на Java:**

```java
import java.util.*;

// ===== Component: общий интерфейс =====
interface FileSystemComponent {
    String getName();
    long getSize();       // Размер в байтах
    void ls(String indent);  // Вывод дерева с отступом
}

// ===== Leaf: отдельный файл =====
class File implements FileSystemComponent {
    private final String name;
    private final long size;

    public File(String name, long size) {
        this.name = name;
        this.size = size;
    }

    @Override
    public String getName() { return name; }

    @Override
    public long getSize() { return size; }

    @Override
    public void ls(String indent) {
        System.out.println(indent + "📄 " + name + " (" + size + " байт)");
    }
}

// ===== Composite: папка с файлами и подпапками =====
class Directory implements FileSystemComponent {
    private final String name;
    private final List<FileSystemComponent> children = new ArrayList<>();

    public Directory(String name) { this.name = name; }

    public void add(FileSystemComponent component) {
        children.add(component);
    }

    public void remove(FileSystemComponent component) {
        children.remove(component);
    }

    @Override
    public String getName() { return name; }

    @Override
    public long getSize() {
        // Размер папки = сумма размеров всех дочерних элементов (рекурсивно)
        return children.stream().mapToLong(FileSystemComponent::getSize).sum();
    }

    @Override
    public void ls(String indent) {
        System.out.println(indent + "📁 " + name + " (всего: " + getSize() + " байт)");
        for (FileSystemComponent child : children) {
            child.ls(indent + "  ");   // Единообразный вызов: не важно, File или Directory!
        }
    }
}

// ===== Демонстрация =====
public class CompositeDemo {
    public static void main(String[] args) {
        // Файлы-листья
        File file1 = new File("readme.txt", 100);
        File file2 = new File("photo.jpg", 2048);
        File file3 = new File("notes.md", 512);
        File file4 = new File("script.js", 256);

        // Составные объекты
        Directory root = new Directory("/");
        Directory home = new Directory("home");
        Directory docs = new Directory("documents");

        // Строим дерево
        docs.add(file3);
        docs.add(file4);
        home.add(file1);
        home.add(file2);
        home.add(docs);        // Папка внутри папки: рекурсия
        root.add(home);

        // Единообразный вызов: клиент не отличает File от Directory!
        root.ls("");

        System.out.println("\nРазмер папки documents: " + docs.getSize() + " байт");
        System.out.println("Размер папки home: " + home.getSize() + " байт");
        System.out.println("Общий размер: " + root.getSize() + " байт");
    }
}
```

**Плюсы и минусы:**
- [+] Клиент работает единообразно с простыми и составными объектами: код проще
- [+] Легко добавлять новые виды компонентов (Open/Closed Principle)
- [+] Естественно моделирует иерархические структуры
- [-] Сложно ограничить типы дочерних элементов в Composite (например, чтобы папка содержала только файлы определённого типа)
- [-] Общий интерфейс может быть перегружен методами, которые не нужны листьям (`add()`, `remove()` в File)

**Когда применять:**
- Когда нужно представить иерархию «часть-целое» (файловая система, GUI, организационная структура)
- Когда клиентский код должен игнорировать разницу между составными и простыми объектами
- Когда структура данных рекурсивна по своей природе (дерево, граф без циклов)

**Связи с другими паттернами:**
- Builder удобен для создания сложных Composite-деревьев
- Iterator может обходить Composite-структуру (например, обход в глубину)
- Decorator имеет похожую структуру (рекурсивная композиция), но цель другая: добавление обязанностей
- Flyweight помогает экономить память, если Composite содержит множество одинаковых листьев

---

### 2.4. Decorator (Декоратор)

**Назначение:** **Динамически** добавляет объекту новую функциональность, оборачивая его в один или несколько слоёв-декораторов. В отличие от наследования, декорирование происходит во время выполнения и может быть скомбинировано произвольным образом.

**Проблема:** У вас есть класс `Notifier`, который отправляет уведомления по email. Появились требования: отправлять ещё и в SMS, в Slack, а некоторые уведомления и туда, и туда одновременно. Если решать через наследование, получится комбинаторный взрыв: `EmailNotifier`, `SmsNotifier`, `EmailAndSmsNotifier`, `EmailAndSlackNotifier`, `AllNotifiers`... Добавление нового канала приводит к экспоненциальному росту подклассов.

**Решение:** Создать класс-декоратор, который реализует тот же интерфейс, что и декорируемый объект, хранит ссылку на него и добавляет своё поведение до/после делегирования. Декораторы можно вкладывать друг в друга как «матрёшку»: порядок и комбинация определяются во время выполнения.

**Структура (UML):**
```
┌───────────────────────┐
│  Component (intf)     │
├───────────────────────┤
│ + operation()         │
└───────────────────────┘
            ▲
   ┌────────┴─────────────────┐
   │                          │
┌──┴──────────────────┐  ┌────┴─────────────────────┐
│ ConcreteComponent   │  │  BaseDecorator (abstract)│
├─────────────────────┤  ├──────────────────────────┤
│ + operation()       │  │ - wrapped: Component     │
└─────────────────────┘  │ + operation()            │
                         └──────────────────────────┘
                                      ▲
                         ┌────────────┼────────────┐
                         │            │            │
                   DecoratorA   DecoratorB   DecoratorC
```

**Участники:**
- `Component`: общий интерфейс для декорируемого объекта и декораторов
- `ConcreteComponent`: базовый объект, к которому добавляется функциональность
- `BaseDecorator`: абстрактный класс, хранящий ссылку на `Component`
- `ConcreteDecorator`: добавляет конкретную обязанность (до/после вызова wrapped)

**Пример на Java:**

```java
// ===== Component =====
interface Notifier {
    void send(String message);
}

// ===== ConcreteComponent: базовая реализация =====
class EmailNotifier implements Notifier {
    @Override
    public void send(String message) {
        System.out.println("[EMAIL] Отправка: " + message);
    }
}

// ===== BaseDecorator =====
abstract class NotifierDecorator implements Notifier {
    protected final Notifier wrapped;   // Оборачиваемый объект

    protected NotifierDecorator(Notifier wrapped) {
        this.wrapped = wrapped;
    }

    @Override
    public void send(String message) {
        wrapped.send(message);          // Делегирование по умолчанию
    }
}

// ===== ConcreteDecorators =====
class SmsNotifier extends NotifierDecorator {
    public SmsNotifier(Notifier wrapped) { super(wrapped); }

    @Override
    public void send(String message) {
        wrapped.send(message);                    // Сначала: базовое поведение
        System.out.println("[SMS]  Отправка: " + message);  // Потом: своё
    }
}

class SlackNotifier extends NotifierDecorator {
    public SlackNotifier(Notifier wrapped) { super(wrapped); }

    @Override
    public void send(String message) {
        System.out.println("[SLACK] Отправка: " + message); // Сначала: своё
        wrapped.send(message);                               // Потом: базовое
    }
}

class EncryptedNotifier extends NotifierDecorator {
    public EncryptedNotifier(Notifier wrapped) { super(wrapped); }

    @Override
    public void send(String message) {
        String encrypted = "[ЗАШИФРОВАНО] " + new StringBuilder(message).reverse();
        wrapped.send(encrypted);   // Модифицируем данные перед передачей дальше
    }
}

// ===== Демонстрация =====
public class DecoratorDemo {
    public static void main(String[] args) {
        // Базовое поведение: только Email
        Notifier simple = new EmailNotifier();
        System.out.println("--- Только Email ---");
        simple.send("Привет!");

        // Email + SMS: динамически, во время выполнения!
        Notifier emailAndSms = new SmsNotifier(new EmailNotifier());
        System.out.println("\n--- Email + SMS ---");
        emailAndSms.send("Привет!");

        // Email + SMS + Slack: комбинируем «на лету»
        Notifier allChannels = new SlackNotifier(new SmsNotifier(new EmailNotifier()));
        System.out.println("\n--- Все каналы ---");
        allChannels.send("Важное уведомление!");

        // Email с шифрованием + SMS
        Notifier encrypted = new SmsNotifier(new EncryptedNotifier(new EmailNotifier()));
        System.out.println("\n--- Шифрование + SMS ---");
        encrypted.send("Секретная строка");
    }
}
```

**Плюсы и минусы:**
- [+] Динамическое добавление обязанностей: гибче, чем статическое наследование
- [+] Комбинаторная гибкость: можно собрать любую комбинацию декораторов, как из конструктора
- [+] Каждый декоратор маленький и отвечает за одну обязанность (SRP)
- [+] Декораторы можно писать независимо друг от друга (Open/Closed Principle)
- [-] Сложно отлаживать длинные цепочки декораторов
- [-] Много мелких классов (но это плата за гибкость)
- [-] Порядок декораторов может иметь значение (нужно документировать)
- [-] Нельзя удалить конкретный декоратор из середины цепочки (только перестроить заново)

**Когда применять:**
- Когда нужно добавлять обязанности объектам динамически, незаметно для клиента
- Когда наследование невозможно (final-классы) или нежелательно (ведёт к взрыву подклассов)
- Когда нужно комбинировать поведения в произвольном порядке
- Классический пример из Java: `java.io.*`: `BufferedReader(new InputStreamReader(new FileInputStream("file.txt")))`

**Связи с другими паттернами:**
- Adapter меняет интерфейс; Decorator сохраняет интерфейс, но добавляет поведение
- Proxy тоже оборачивает объект, но управляет доступом (лайфсайкл, права), а не добавляет поведение
- Composite и Decorator имеют похожую структуру (рекурсивная композиция), но Composite агрегирует множество объектов, а Decorator ровно один
- Strategy изменяет поведение «изнутри» (смена алгоритма); Decorator: «снаружи» (обёртка)

---

### 2.5. Facade (Фасад)

**Назначение:** Предоставляет **упрощённый, унифицированный интерфейс** к сложной подсистеме (набору классов). Фасад не скрывает подсистему: он просто даёт удобную «точку входа».

**Проблема:** Сложная библиотека или подсистема состоит из десятков классов со множеством методов. Клиенту, которому нужно выполнить одну простую операцию (например, «конвертировать видео»), приходится разбираться во внутреннем устройстве подсистемы: инициализировать кодеки, настраивать потоки, управлять буферами... Это повышает порог входа, создаёт жёсткую связность и ведёт к ошибкам.

**Решение:** Создать класс-фасад, который предоставляет высокоуровневые методы (`convertVideo()`), скрывающие за собой все низкоуровневые взаимодействия с подсистемой. Клиент вызывает один метод фасада вместо десяти вызовов к разным классам.

**Структура (UML):**
```
┌─────────────────┐
│     Facade      │
├─────────────────┤
│ + operationA()  │──────────┐
│ + operationB()  │──────┐   │
└─────────────────┘      │   │
                         ▼   ▼
              ┌──────────────────────────┐
              │    Сложная подсистема     │
              ├──────────────────────────┤
              │ Class1  Class2  Class3   │
              │ Class4  Class5  Class6   │
              └──────────────────────────┘
```

**Участники:**
- `Facade`: класс с упрощёнными методами, делегирующий вызовы классам подсистемы
- `Subsystem classes`: классы, реализующие функциональность подсистемы; ничего не знают о фасаде

**Пример на Java:**

```java
// ===== Сложная подсистема: классы для конвертации видео =====
class VideoFile {
    private final String name;
    public VideoFile(String name) { this.name = name; }
    public String getName() { return name; }
}

class Codec {
    public void decode(VideoFile file) {
        System.out.println("  Декодирую: " + file.getName());
    }
}

class BitrateReader {
    public String read(VideoFile file, Codec codec) {
        System.out.println("  Читаю битрейт: " + file.getName());
        return "raw_data";
    }
    public String convert(String rawData, String targetFormat) {
        System.out.println("  Конвертирую в " + targetFormat);
        return "converted_data";
    }
}

class AudioMixer {
    public String fixAudio(String rawData) {
        System.out.println("  Корректирую звук");
        return "fixed_audio";
    }
}

class VideoWriter {
    public void write(String data, String outputFileName) {
        System.out.println("  Записываю выходной файл: " + outputFileName);
    }
}

// ===== Facade: единая точка входа =====
class VideoConverter {
    private final Codec codec = new Codec();
    private final BitrateReader reader = new BitrateReader();
    private final AudioMixer mixer = new AudioMixer();
    private final VideoWriter writer = new VideoWriter();

    // Всего один метод для клиента вместо 10+
    public void convert(String inputFile, String outputFile, String targetFormat) {
        System.out.println("=== Конвертация видео ===");
        System.out.println("Входной файл: " + inputFile);

        VideoFile file = new VideoFile(inputFile);
        codec.decode(file);
        String raw = reader.read(file, codec);
        String fixed = mixer.fixAudio(raw);
        String converted = reader.convert(fixed, targetFormat);
        writer.write(converted, outputFile);

        System.out.println("Конвертация завершена: " + outputFile);
        System.out.println("=========================");
    }
}

// ===== Демонстрация =====
public class FacadeDemo {
    public static void main(String[] args) {
        VideoConverter converter = new VideoConverter();

        // Клиенту не нужно знать о Codec, BitrateReader, AudioMixer, VideoWriter!
        converter.convert("my_video.avi", "my_video.mp4", "mp4");
    }
}
```

**Плюсы и минусы:**
- [+] Изолирует клиентов от сложности подсистемы: низкий порог входа
- [+] Уменьшает количество зависимостей клиента (вместо 10 классов: 1 фасад)
- [+] Слабая связность: изменения в подсистеме не ломают клиентов (меняется только фасад)
- [-] Фасад может стать «божественным объектом» (God Object), привязанным ко всем классам подсистемы
- [-] Фасад не запрещает прямой доступ к подсистеме: при желании клиент может обойти фасад и «залезть внутрь»

**Когда применять:**
- Когда нужно представить простой интерфейс к сложной системе
- Когда подсистема сложна для понимания или имеет много зависимостей
- Когда нужно разложить подсистему на слои: фасад становится точкой входа на каждый уровень
- Примеры в реальном мире: `JOptionPane` в Swing (фасад к сложной системе диалогов), REST-контроллер (фасад к сервисному слою)

**Связи с другими паттернами:**
- Facade часто является Singleton (один экземпляр фасада)
- Abstract Factory может использоваться для создания классов подсистемы за фасадом
- Отличие от Adapter: фасад предоставляет новый (упрощённый) интерфейс; адаптер преобразует существующий интерфейс в ожидаемый клиентом
- Отличие от Mediator: фасад это пассивная точка входа; медиатор активно координирует взаимодействие коллег

---

### 2.6. Flyweight (Легковес)

**Назначение:** Позволяет эффективно поддерживать **огромное количество мелких объектов** путём разделения их состояния на **внутреннее** (общее, неизменное, хранится в легковесе) и **внешнее** (уникальное, передаётся извне при каждом вызове).

**Проблема:** Представьте текстовый редактор, где каждая буква это объект со шрифтом, цветом и позицией. Документ в 100 000 символов = 100 000 объектов это сотни мегабайт памяти. Но большинство букв используют одни и те же шрифты и цвета! Создавать для каждой буквы свой объект расточительно.

**Решение:** Выделить повторяющееся состояние (шрифт, цвет, семейство) в **легковес (flyweight)**: разделяемый объект. Уникальное состояние (координата X, Y) передавать через параметры метода. Вместо 100 000 объектов хранить ~50 легковесов (по одному на каждую комбинацию шрифт+цвет) и 100 000 записей с координатами.

**Структура (UML):**
```
┌──────────────────────┐         ┌─────────────────────────┐
│    FlyweightFactory   │         │    Flyweight (intf)     │
├──────────────────────┤         ├─────────────────────────┤
│ - pool: Map<K, Flyw> │────────>│ + operation(extrinsic)   │
│ + getFlyweight(key)  │         └─────────────────────────┘
└──────────────────────┘                     ▲
                                    ┌────────┴────────┐
                                    │                 │
                           ConcreteFlyweight    UnsharedFlyweight
                           (разделяемый)         (не разделяемый)
```

**Участники:**
- `Flyweight`: интерфейс, через который легковесы принимают внешнее состояние
- `ConcreteFlyweight`: реализует Flyweight; хранит внутреннее состояние (общее, неизменное)
- `FlyweightFactory`: управляет пулом легковесов; создаёт новый легковес, только если такого ещё нет
- `Client`: хранит/вычисляет внешнее состояние и передаёт его легковесу

**Пример на Java:**

```java
import java.util.*;

// ===== Flyweight: хранит только внутреннее (intrinsic) состояние =====
class CharacterStyle {
    private final String font;      // Внутреннее состояние (общее)
    private final int fontSize;     // Внутреннее состояние (общее)
    private final String color;    // Внутреннее состояние (общее)

    public CharacterStyle(String font, int fontSize, String color) {
        this.font = font;
        this.fontSize = fontSize;
        this.color = color;
    }

    public void draw(char symbol, int x, int y) {  // Внешнее состояние передаётся в метод
        System.out.printf("  Буква '%c' [%s, %dpt, %s] в позиции (%d, %d)%n",
                symbol, font, fontSize, color, x, y);
    }

    // Ключ для хранения в Map: используем комбинацию внутренних полей
    public String getKey() {
        return font + "|" + fontSize + "|" + color;
    }
}

// ===== FlyweightFactory: управляет пулом легковесов =====
class StyleFactory {
    private static final Map<String, CharacterStyle> pool = new HashMap<>();

    public static CharacterStyle getStyle(String font, int fontSize, String color) {
        String key = font + "|" + fontSize + "|" + color;
        // Создаём новый легковес, только если такой комбинации ещё нет
        return pool.computeIfAbsent(key, k -> {
            System.out.println("  [Создан новый стиль: " + key + "]");
            return new CharacterStyle(font, fontSize, color);
        });
    }

    public static int getPoolSize() {
        return pool.size();
    }
}

// ===== Клиентский класс: хранит внешнее состояние =====
class Character {
    private final char symbol;          // Внешнее (extrinsic)
    private final int x, y;             // Внешнее (extrinsic)
    private final CharacterStyle style; // Ссылка на легковес (внутреннее состояние)

    public Character(char symbol, int x, int y, String font, int fontSize, String color) {
        this.symbol = symbol;
        this.x = x;
        this.y = y;
        this.style = StyleFactory.getStyle(font, fontSize, color);  // Легковес из фабрики
    }

    public void draw() {
        style.draw(symbol, x, y);
    }
}

// ===== Демонстрация =====
public class FlyweightDemo {
    public static void main(String[] args) {
        List<Character> document = new ArrayList<>();

        // Имитация текстового редактора: 10 символов, но стилей: всего 2!
        String text = "HelloWorld";
        for (int i = 0; i < text.length(); i++) {
            if (i % 2 == 0) {
                document.add(new Character(text.charAt(i), i * 10, 0,
                        "Arial", 12, "black"));
            } else {
                document.add(new Character(text.charAt(i), i * 10, 0,
                        "Times New Roman", 14, "red"));
            }
        }

        System.out.println("\n--- Отрисовка документа ---");
        for (Character ch : document) {
            ch.draw();
        }

        System.out.println("\nСоздано объектов Character: " + document.size());
        System.out.println("Создано легковесов (стилей): " + StyleFactory.getPoolSize());
        // 10 символов, но всего 2 объекта CharacterStyle: огромная экономия памяти
    }
}
```

**Плюсы и минусы:**
- [+] Колоссальная экономия памяти при большом количестве однотипных объектов
- [+] Можно хранить в памяти то, что без Flyweight пришлось бы подгружать с диска
- [-] Усложняет код (разделение состояния на внутреннее и внешнее)
- [-] Внешнее состояние нужно вычислять и передавать: дополнительные вычисления
- [-] Легковесы должны быть потокобезопасными, если разделяются между потоками

**Когда применять:**
- Когда в системе используется огромное количество мелких объектов (сотни тысяч, миллионы)
- Когда хранение каждого объекта «как есть» непозволительно расходует память
- Когда значительная часть состояния объекта может быть вынесена как внешняя
- Примеры: текстовые редакторы (глифы букв), игры (тайлы на карте, деревья в лесу), биржевые стаканы

**Связи с другими паттернами:**
- **FlyweightFactory** часто реализуется как Singleton
- Composite + Flyweight = экономия памяти при хранении деревьев с повторяющимися листьями
- State и Strategy: хорошие кандидаты на превращение в легковесы (объекты состояний/стратегий часто разделяемы)

---

### 2.7. Proxy (Заместитель)

**Назначение:** Предоставляет **суррогат (заместитель)** для другого объекта, чтобы контролировать доступ к нему. Proxy имеет тот же интерфейс, что и реальный объект, и перехватывает все вызовы к нему.

**Проблема:** Бывают ситуации, когда создавать/использовать реальный объект напрямую нежелательно или невозможно:
- Объект находится на удалённом сервере (сетевые задержки)
- Создание объекта: дорогая операция (загрузка изображения, инициализация подключения)
- Нужно контролировать права доступа к объекту
- Нужно логировать или кэшировать обращения к объекту

Во всех этих случаях нужен «заместитель», который выглядит как реальный объект, но добавляет дополнительную логику до/после обращения.

**Структура (UML):**
```
┌───────────────────────┐
│   Subject (interface) │
├───────────────────────┤
│ + request()           │
└───────────────────────┘
            ▲
   ┌────────┴────────┐
   │                 │
┌──┴────────────┐  ┌─┴─────────────────┐
│ RealSubject   │  │      Proxy        │
├───────────────┤  ├───────────────────┤
│ + request()   │  │ - realSubject     │
└───────────────┘  │ + request()       │──> realSubject.request()
                   └───────────────────┘    (до/после/вместо)
```

**Участники:**
- `Subject`: общий интерфейс для реального объекта и заместителя
- `RealSubject`: реальный объект, выполняющий полезную работу
- `Proxy`: заместитель; хранит ссылку на RealSubject, управляет его созданием и доступом

**Типы Proxy:**
- **Virtual Proxy**: откладывает создание «тяжёлого» объекта до первого обращения (lazy init)
- **Protection Proxy**: проверяет права доступа
- **Remote Proxy**: скрывает сетевое взаимодействие (RMI, REST-клиент)
- **Caching Proxy**: кэширует результаты вызовов
- **Logging Proxy**: логирует обращения

**Пример на Java: Virtual Proxy + Protection Proxy + Logging:**

```java
// ===== Subject =====
interface Image {
    void display();
    String getFileName();
}

// ===== RealSubject: «тяжёлый» объект (загрузка из файла) =====
class HighResolutionImage implements Image {
    private final String fileName;

    public HighResolutionImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk();  // Дорогая операция!
    }

    private void loadFromDisk() {
        System.out.println("  [Загрузка с диска: " + fileName + "]: 5 секунд...");
    }

    @Override
    public void display() {
        System.out.println("  Отображаю изображение: " + fileName + " (Full HD)");
    }

    @Override
    public String getFileName() {
        return fileName;
    }
}

// ===== Virtual Proxy: откладывает загрузку до первого display() =====
class LazyImageProxy implements Image {
    private final String fileName;
    private HighResolutionImage realImage;   // null, пока не потребуется

    public LazyImageProxy(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new HighResolutionImage(fileName);  // Ленивая загрузка
        }
        realImage.display();
    }

    @Override
    public String getFileName() {
        return fileName;
    }
}

// ===== Protection Proxy: проверяет права доступа =====
class ProtectionImageProxy implements Image {
    private final Image realImage;
    private final boolean isAdmin;

    public ProtectionImageProxy(Image realImage, boolean isAdmin) {
        this.realImage = realImage;
        this.isAdmin = isAdmin;
    }

    @Override
    public void display() {
        if (!isAdmin) {
            System.out.println("  ДОСТУП ЗАПРЕЩЁН! Только администратор может просматривать: "
                    + realImage.getFileName());
            return;
        }
        realImage.display();
    }

    @Override
    public String getFileName() {
        return realImage.getFileName();
    }
}

// ===== Logging Proxy: логирует вызовы =====
class LoggingImageProxy implements Image {
    private final Image realImage;

    public LoggingImageProxy(Image realImage) {
        this.realImage = realImage;
    }

    @Override
    public void display() {
        System.out.println("  [LOG] display() вызван для: " + realImage.getFileName()
                + " в " + System.currentTimeMillis());
        long start = System.nanoTime();
        realImage.display();
        long end = System.nanoTime();
        System.out.println("  [LOG] display() завершён за " + (end - start) / 1_000_000 + " мс");
    }

    @Override
    public String getFileName() {
        return realImage.getFileName();
    }
}

// ===== Демонстрация =====
public class ProxyDemo {
    public static void main(String[] args) {
        System.out.println("=== Virtual Proxy (ленивая загрузка) ===");
        Image lazyImage = new LazyImageProxy("photo.jpg");
        System.out.println("Прокси создан, изображение ещё НЕ загружено.");
        System.out.println("Имя файла доступно: " + lazyImage.getFileName());
        System.out.println("Вызываю display()...");
        lazyImage.display();   // Загрузка происходит только здесь!
        lazyImage.display();   // Повторно: без загрузки

        System.out.println("\n=== Protection Proxy (контроль доступа) ===");
        Image realImage = new HighResolutionImage("secret.png");
        Image userProxy = new ProtectionImageProxy(realImage, false);
        Image adminProxy = new ProtectionImageProxy(realImage, true);
        userProxy.display();   // Отказано
        adminProxy.display();  // Разрешено

        System.out.println("\n=== Logging Proxy (логирование) ===");
        Image loggedImage = new LoggingImageProxy(realImage);
        loggedImage.display();
    }
}
```

**Плюсы и минусы:**
- [+] Позволяет контролировать доступ к объекту прозрачно для клиента (клиент не знает о прокси)
- [+] Можно добавлять сквозную функциональность (логирование, кэширование, lazy load) без изменения RealSubject
- [+] Разные типы Proxy могут комбинироваться (обернуть Virtual Proxy в Protection Proxy)
- [-] Усложняет архитектуру: дополнительный класс
- [-] Добавляет накладные расходы на косвенный вызов
- [-] Может маскировать проблемы реального объекта (например, сетевые таймауты в Remote Proxy)

**Когда применять:**
- **Virtual Proxy**: когда объект «тяжёлый» и нужен не сразу (изображения, отчёты, документы)
- **Protection Proxy**: когда нужен контроль доступа к объекту (Spring Security proxy, `Proxy.newProxyInstance`)
- **Remote Proxy**: когда объект находится в другом адресном пространстве (RMI, EJB, микросервисы)
- **Logging/Caching Proxy**: когда нужна сквозная функциональность без AOP
- Java-примеры: `java.lang.reflect.Proxy`, Hibernate lazy-loading proxy, Spring AOP proxy

**Связи с другими паттернами:**
- Adapter меняет интерфейс; Proxy сохраняет интерфейс
- Decorator добавляет поведение; Proxy контролирует доступ/жизненный цикл
- Facade упрощает интерфейс к подсистеме; Proxy: замещает один конкретный объект

---

## 3. Поведенческие паттерны (Behavioral)

Поведенческие паттерны определяют алгоритмы и распределение ответственности между объектами. Они описывают структуру классов и **схемы их взаимодействия**: поток управления и передачи данных.

---

### 3.1. Chain of Responsibility (Цепочка обязанностей)

**Назначение:** Передаёт запрос последовательно по цепочке потенциальных обработчиков, пока один из них не обработает запрос. Позволяет **избежать жёсткой привязки** отправителя запроса к получателю.

**Проблема:** В системе есть запрос (например, HTTP-запрос, заявка на одобрение кредита, событие в GUI), который должен быть обработан одним из нескольких обработчиков, но отправитель не знает заранее, каким именно. Более того, набор обработчиков может меняться динамически. Жёстко «зашивать» конкретного обработчика в отправитель нельзя: это нарушит гибкость.

**Решение:** Связать обработчики в цепочку (каждый хранит ссылку на следующего). Отправитель передаёт запрос первому обработчику. Тот либо обрабатывает запрос сам, либо передаёт дальше по цепочке. Клиент ничего не знает о том, кто в итоге обработает запрос.

**Структура (UML):**
```
┌────────────┐         ┌───────────────────────┐
│   Client   │         │   Handler (abstract)   │
└────────────┘         ├───────────────────────┤
        │              │ - next: Handler        │
        │              │ + setNext(Handler)     │
        ▼              │ + handle(request)      │
┌─────────────────┐    └───────────────────────┘
│ Handler1        │               ▲
│ handle(request) │──next──► ┌────┴────────┐
└─────────────────┘          │             │
                      Handler2        Handler3
                      (или дальше)
```

**Участники:**
- `Handler`: абстрактный класс/интерфейс с методом `handle()` и ссылкой на следующий обработчик
- `ConcreteHandler`: конкретный обработчик: либо обрабатывает запрос, либо передаёт дальше
- `Client`: инициирует запрос и отправляет его в начало цепочки

**Пример на Java:**

```java
// ===== Класс запроса =====
class LoanRequest {
    private final String customerName;
    private final double amount;
    private final int creditScore;

    public LoanRequest(String customerName, double amount, int creditScore) {
        this.customerName = customerName;
        this.amount = amount;
        this.creditScore = creditScore;
    }

    public String getCustomerName() { return customerName; }
    public double getAmount() { return amount; }
    public int getCreditScore() { return creditScore; }
}

// ===== Handler (абстрактный) =====
abstract class LoanApprover {
    protected LoanApprover next;  // Следующее звено цепочки

    public LoanApprover setNext(LoanApprover next) {
        this.next = next;
        return next;              // Позволяет fluent-построение цепочки
    }

    public abstract void approve(LoanRequest request);

    protected void passToNext(LoanRequest request) {
        if (next != null) {
            System.out.println("  -> Передаю дальше...");
            next.approve(request);
        } else {
            System.out.println("  -> Цепочка закончилась. Заявка НЕ одобрена.");
        }
    }
}

// ===== Concrete Handlers =====
class ClerkApprover extends LoanApprover {
    @Override
    public void approve(LoanRequest request) {
        if (request.getAmount() <= 10_000) {
            System.out.println("Клерк одобрил заявку " + request.getCustomerName()
                    + " на сумму $" + request.getAmount());
        } else {
            passToNext(request);   // Сумма слишком большая: передаём дальше
        }
    }
}

class ManagerApprover extends LoanApprover {
    @Override
    public void approve(LoanRequest request) {
        if (request.getAmount() <= 100_000) {
            System.out.println("Менеджер одобрил заявку " + request.getCustomerName()
                    + " на сумму $" + request.getAmount());
        } else {
            passToNext(request);
        }
    }
}

class DirectorApprover extends LoanApprover {
    @Override
    public void approve(LoanRequest request) {
        if (request.getAmount() <= 1_000_000 && request.getCreditScore() >= 700) {
            System.out.println("Директор одобрил заявку " + request.getCustomerName()
                    + " на сумму $" + request.getAmount());
        } else {
            passToNext(request);
        }
    }
}

// ===== Демонстрация =====
public class ChainOfResponsibilityDemo {
    public static void main(String[] args) {
        // Строим цепочку: Клерк -> Менеджер -> Директор
        LoanApprover clerk = new ClerkApprover();
        clerk.setNext(new ManagerApprover())
             .setNext(new DirectorApprover());

        // Тестируем разные суммы: клиент не знает, кто обработает!
        System.out.println("=== Заявка на $5,000 ===");
        clerk.approve(new LoanRequest("Alice", 5_000, 650));

        System.out.println("\n=== Заявка на $50,000 ===");
        clerk.approve(new LoanRequest("Bob", 50_000, 680));

        System.out.println("\n=== Заявка на $500,000 ===");
        clerk.approve(new LoanRequest("Charlie", 500_000, 750));

        System.out.println("\n=== Заявка на $2,000,000 ===");
        clerk.approve(new LoanRequest("Dave", 2_000_000, 800));
    }
}
```

**Плюсы и минусы:**
- [+] Ослабляет связь между отправителем и получателем запроса
- [+] Можно динамически менять цепочку обработчиков
- [+] Каждый обработчик имеет чёткую зону ответственности (SRP)
- [-] Запрос может быть не обработан никем (если никто не взял)
- [-] Длинная цепочка замедляет обработку
- [-] Целостность цепочки: на совести клиента (легко «разорвать» ссылку)

**Когда применять:**
- Когда система должна обрабатывать запрос одним из нескольких обработчиков, неизвестных заранее
- Когда набор обработчиков должен конфигурироваться динамически
- Когда важно, чтобы запрос был обработан неявно (отправитель не знает получателя)
- Примеры: middleware в веб-фреймворках, фильтры сервлетов, логирование с разными уровнями

**Связи с другими паттернами:**
- Цепочка может быть реализована с помощью Composite (каждый элемент: композит, содержащий цепочку)
- Command часто передаётся по Chain of Responsibility
- State может динамически менять обработчика в цепочке

---

### 3.2. Command (Команда)

**Назначение:** Инкапсулирует запрос в виде **объекта-команды**. Это даёт возможность параметризовать клиентов, ставить запросы в очередь, логировать их и поддерживать отмену операций (undo).

**Проблема:** Есть операция (например, «сохранить документ», «отправить письмо», «вырезать текст»), которую нужно:
- Выполнить, но, возможно, позже (отложенное выполнение)
- Поставить в очередь на выполнение
- Логировать для аудита
- Иметь возможность отменить (undo)

Если операция это просто вызов метода, ничего этого сделать нельзя. Метод выполняется немедленно, его нельзя «положить в очередь» или отменить.

**Решение:** Каждую операцию оформить как объект, реализующий интерфейс `Command` с методом `execute()`. Объект-команда хранит все параметры, необходимые для выполнения. Отправитель (Invoker) вызывает `execute()`, не зная, как именно команда работает.

**Структура (UML):**
```
┌──────────────┐         ┌──────────────────────┐
│   Invoker    │         │  Command (interface)  │
├──────────────┤         ├──────────────────────┤
│ - command    │────────>│ + execute()           │
│ + executeCmd │         │ + undo() (опционально)│
└──────────────┘         └──────────────────────┘
                                      ▲
                             ┌────────┴────────┐
                             │ ConcreteCommand  │
                             ├──────────────────┤
                             │ - receiver       │──> ┌──────────────┐
                             │ + execute()      │    │   Receiver   │
                             │ + undo()         │    ├──────────────┤
                             └──────────────────┘    │ + action()   │
                                                     └──────────────┘
```

**Участники:**
- `Command`: интерфейс с `execute()` и опционально `undo()`
- `ConcreteCommand`: конкретная команда, связывает действие и Receiver
- `Invoker`: тот, кто запускает команду (кнопка, планировщик, очередь)
- `Receiver`: объект, который выполняет фактическую работу
- `Client`: создаёт команду и связывает её с Receiver

**Пример на Java:**

```java
import java.util.*;

// ===== Receiver: выполняет реальную работу =====
class TextEditor {
    private final StringBuilder text = new StringBuilder();
    private int cursorPosition = 0;

    public void insert(String str) {
        text.insert(cursorPosition, str);
        cursorPosition += str.length();
    }

    public void delete(int length) {
        if (cursorPosition >= length) {
            text.delete(cursorPosition - length, cursorPosition);
            cursorPosition -= length;
        }
    }

    public String getText() { return text.toString(); }
    public String getSelection(int pos, int length) {
        return text.substring(pos, Math.min(pos + length, text.length()));
    }
    public void moveCursor(int position) { this.cursorPosition = position; }
    public int getCursorPosition() { return cursorPosition; }
}

// ===== Command =====
interface Command {
    void execute();
    void undo();
}

// ===== Concrete Commands =====
class InsertCommand implements Command {
    private final TextEditor editor;
    private final String text;
    private final int position;      // Для undo нужно знать, куда вставляли

    public InsertCommand(TextEditor editor, String text) {
        this.editor = editor;
        this.text = text;
        this.position = editor.getCursorPosition();
    }

    @Override
    public void execute() {
        editor.moveCursor(position);  // Восстанавливаем позицию перед вставкой
        editor.insert(text);
    }

    @Override
    public void undo() {
        editor.moveCursor(position + text.length());
        editor.delete(text.length());
    }
}

class DeleteCommand implements Command {
    private final TextEditor editor;
    private final int length;
    private final int position;      // Для undo нужно знать, ЧТО удалили
    private String deletedText;

    public DeleteCommand(TextEditor editor, int length) {
        this.editor = editor;
        this.length = length;
        this.position = editor.getCursorPosition();
    }

    @Override
    public void execute() {
        deletedText = editor.getSelection(position - length, length);
        editor.moveCursor(position);
        editor.delete(length);
    }

    @Override
    public void undo() {
        editor.moveCursor(position - length);
        editor.insert(deletedText);
    }
}

// ===== Invoker: хранит историю команд =====
class CommandHistory {
    private final Deque<Command> history = new ArrayDeque<>();
    private final Deque<Command> redoStack = new ArrayDeque<>();

    public void execute(Command cmd) {
        cmd.execute();
        history.push(cmd);
        redoStack.clear();  // Новое действие обрывает ветку redo
    }

    public void undo() {
        if (!history.isEmpty()) {
            Command cmd = history.pop();
            cmd.undo();
            redoStack.push(cmd);
        }
    }

    public void redo() {
        if (!redoStack.isEmpty()) {
            Command cmd = redoStack.pop();
            cmd.execute();
            history.push(cmd);
        }
    }
}

// ===== Демонстрация =====
public class CommandDemo {
    public static void main(String[] args) {
        TextEditor editor = new TextEditor();
        CommandHistory history = new CommandHistory();

        System.out.println("=== Ввод текста с Undo/Redo ===");

        history.execute(new InsertCommand(editor, "Hello "));
        System.out.println("После вставки: '" + editor.getText() + "'");

        history.execute(new InsertCommand(editor, "World!"));
        System.out.println("После вставки: '" + editor.getText() + "'");

        history.undo();
        System.out.println("После undo:    '" + editor.getText() + "'");

        history.undo();
        System.out.println("После undo:    '" + editor.getText() + "'");

        history.redo();
        System.out.println("После redo:    '" + editor.getText() + "'");

        history.execute(new InsertCommand(editor, "Beautiful "));
        history.execute(new InsertCommand(editor, "World!"));
        System.out.println("После правок:  '" + editor.getText() + "'");

        history.execute(new DeleteCommand(editor, 6));  // Удаляем "World!"
        System.out.println("После удаления: '" + editor.getText() + "'");

        history.undo();
        System.out.println("После undo:     '" + editor.getText() + "'");
    }
}
```

**Плюсы и минусы:**
- [+] Отделяет источник запроса (Invoker) от исполнителя (Receiver): слабая связность
- [+] Позволяет отменять и повторять операции (undo/redo)
- [+] Можно собирать сложные команды из простых (Composite Command / Macro)
- [+] Команды можно сериализовать, логировать, ставить в очередь
- [-] Увеличивает количество классов (каждая операция: отдельный класс)
- [-] Команды могут устаревать (ссылаются на состояние, которое изменилось)

**Когда применять:**
- Когда нужно параметризовать объекты выполняемыми действиями (кнопки, пункты меню)
- Когда нужна поддержка undo/redo
- Когда нужна поддержка транзакций (выполнить серию команд атомарно)
- Когда нужно ставить операции в очередь, планировать их выполнение
- Примеры: `Runnable` / `Callable` в Java, транзакции в БД, GUI-действия

**Связи с другими паттернами:**
- Memento хранит состояние для undo внутри Command
- Composite может использоваться для создания макрокоманд
- Prototype: команды можно клонировать для вставки в историю

---

### 3.3. Interpreter (Интерпретатор)

**Назначение:** Определяет **грамматику** простого языка и предоставляет интерпретатор, который выполняет предложения этого языка. Каждое правило грамматики представлено отдельным классом.

**Проблема:** Нужно интерпретировать выражения на некотором предметно-специфичном языке (DSL): математические формулы, регулярные выражения, запросы поиска, SQL-подобные запросы, простые скрипты. Писать полноценный парсер/компилятор избыточно. Нужен простой механизм «вычислить строку по правилам».

**Решение:** Каждому правилу грамматики сопоставить класс с методом `interpret(context)`. Терминальные выражения (константы, переменные) это листья дерева. Нетерминальные выражения (сложение, умножение, AND, OR) это узлы дерева, содержащие дочерние выражения. Выражение парсится в абстрактное синтаксическое дерево (AST) и вычисляется рекурсивно.

**Структура (UML):**
```
┌──────────────────────────┐
│   Expression (interface) │
├──────────────────────────┤
│ + interpret(context)     │
└──────────────────────────┘
            ▲
   ┌────────┴────────────┐
   │                     │
┌──┴────────────────┐  ┌─┴───────────────────┐
│ TerminalExpression│  │ NonTerminalExpression│
├───────────────────┤  ├──────────────────────┤
│ (переменная, const)│  │ (+, -, AND, OR, ...) │
└───────────────────┘  │ - left: Expression   │
                       │ - right: Expression  │
                       └──────────────────────┘
```

**Участники:**
- `Expression`: интерфейс для всех узлов AST
- `TerminalExpression`: терминал (константа, переменная): не содержит дочерних выражений
- `NonTerminalExpression`: нетерминал (оператор): содержит одно или более дочерних выражений
- `Context`: глобальный контекст вычисления (таблица переменных и их значений)

**Пример на Java: калькулятор булевых выражений:**

```java
import java.util.*;

// ===== Context: хранит значения переменных =====
class Context {
    private final Map<String, Boolean> variables = new HashMap<>();

    public void setVariable(String name, boolean value) {
        variables.put(name, value);
    }

    public boolean getVariable(String name) {
        return variables.getOrDefault(name, false);
    }
}

// ===== Expression =====
interface BooleanExpression {
    boolean interpret(Context context);
}

// ===== Terminal Expressions =====
class VariableExpression implements BooleanExpression {
    private final String name;

    public VariableExpression(String name) { this.name = name; }

    @Override
    public boolean interpret(Context context) {
        return context.getVariable(name);
    }
}

class ConstantExpression implements BooleanExpression {
    private final boolean value;

    public ConstantExpression(boolean value) { this.value = value; }

    @Override
    public boolean interpret(Context context) {
        return value;
    }
}

// ===== NonTerminal Expressions =====
class AndExpression implements BooleanExpression {
    private final BooleanExpression left, right;

    public AndExpression(BooleanExpression left, BooleanExpression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public boolean interpret(Context context) {
        return left.interpret(context) && right.interpret(context);
    }
}

class OrExpression implements BooleanExpression {
    private final BooleanExpression left, right;

    public OrExpression(BooleanExpression left, BooleanExpression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public boolean interpret(Context context) {
        return left.interpret(context) || right.interpret(context);
    }
}

class NotExpression implements BooleanExpression {
    private final BooleanExpression expr;

    public NotExpression(BooleanExpression expr) { this.expr = expr; }

    @Override
    public boolean interpret(Context context) {
        return !expr.interpret(context);
    }
}

// ===== Демонстрация =====
public class InterpreterDemo {
    public static void main(String[] args) {
        // Выражение: (A AND B) OR (NOT C)
        // Где A=true, B=false, C=true => (true AND false) OR (NOT true) = false OR false = false
        BooleanExpression expr = new OrExpression(
                new AndExpression(
                        new VariableExpression("A"),
                        new VariableExpression("B")
                ),
                new NotExpression(
                        new VariableExpression("C")
                )
        );

        Context ctx = new Context();
        ctx.setVariable("A", true);
        ctx.setVariable("B", false);
        ctx.setVariable("C", true);

        System.out.println("(A AND B) OR (NOT C) = " + expr.interpret(ctx));
        // true AND false = false, NOT true = false, false OR false = false

        ctx.setVariable("B", true);
        System.out.println("(A AND B) OR (NOT C) = " + expr.interpret(ctx));
        // true AND true = true, NOT true = false, true OR false = true
    }
}
```

**Плюсы и минусы:**
- [+] Простота добавления новых правил грамматики (новый класс)
- [+] Каждый класс представляет ровно одно правило (SRP)
- [+] Структура AST естественно отражает грамматику
- [-] Для сложных языков количество классов становится неоправданно большим
- [-] Низкая производительность по сравнению со скомпилированным кодом
- [-] Нет встроенного механизма парсинга: AST нужно строить вручную или отдельным парсером

**Когда применять:**
- Когда есть простой DSL, который можно представить в виде AST
- Когда грамматика языка проста и стабильна (нечасто меняется)
- Когда производительность не критична
- Примеры: `java.util.Pattern` (регулярные выражения), `java.text.Format`, Spring Expression Language (SpEL)

**Связи с другими паттернами:**
- AST по своей структуре это Composite
- Для обхода AST часто используется Visitor (добавление новых операций без изменения классов выражений)
- Flyweight может использоваться для разделения терминалов (например, константа `true`: одна на всех)

---

### 3.4. Iterator (Итератор)

**Назначение:** Предоставляет способ **последовательного обхода** элементов коллекции (агрегата) без раскрытия её внутреннего представления.

**Проблема:** У вас есть коллекция (список, дерево, граф, хеш-таблица). Клиенту нужно перебрать все её элементы единообразно, независимо от внутренней структуры коллекции. Без итератора клиент должен знать, как пройти по списку (`for i=0..size`), по дереву (рекурсивно, в глубину), по хешу (по бакетам). Это раскрывает внутренности коллекции и дублирует код обхода.

**Решение:** Коллекция возвращает объект-итератор, который инкапсулирует логику обхода. Итератор имеет единый интерфейс (`hasNext()` + `next()`), не зависящий от типа коллекции. Клиент работает только с этим интерфейсом.

**Структура (UML):**
```
┌────────────────────────┐         ┌──────────────────────┐
│  Aggregate (interface) │         │ Iterator (interface) │
├────────────────────────┤         ├──────────────────────┤
│ + createIterator()     │────────>│ + hasNext(): boolean │
└────────────────────────┘         │ + next(): T          │
            ▲                      └──────────────────────┘
            │                                 ▲
   ┌────────┴────────┐              ┌────────┴────────┐
   │ ConcreteAggregate│              │ ConcreteIterator │
   └─────────────────┘              └──────────────────┘
```

**Участники:**
- `Iterator`: интерфейс для доступа и обхода элементов
- `ConcreteIterator`: конкретная реализация обхода
- `Aggregate`: интерфейс коллекции; возвращает Iterator
- `ConcreteAggregate`: конкретная коллекция

**Пример на Java:**

```java
import java.util.*;

// ===== Собственная коллекция: дерево поиска (BST) =====
class BinarySearchTree<T extends Comparable<T>> implements Iterable<T> {
    private Node<T> root;

    private static class Node<T> {
        T value;
        Node<T> left, right;
        Node(T value) { this.value = value; }
    }

    public void add(T value) {
        root = addRecursive(root, value);
    }

    private Node<T> addRecursive(Node<T> node, T value) {
        if (node == null) return new Node<>(value);
        int cmp = value.compareTo(node.value);
        if (cmp < 0) node.left = addRecursive(node.left, value);
        else if (cmp > 0) node.right = addRecursive(node.right, value);
        return node;
    }

    // Возвращает итератор (обход в порядке возрастания: in-order)
    @Override
    public Iterator<T> iterator() {
        return new InOrderIterator<>(root);
    }

    // ===== Конкретный итератор =====
    private static class InOrderIterator<T> implements Iterator<T> {
        private final Deque<Node<T>> stack = new ArrayDeque<>();

        InOrderIterator(Node<T> root) {
            pushLeft(root);   // Инициализация: самый левый путь
        }

        private void pushLeft(Node<T> node) {
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
        }

        @Override
        public boolean hasNext() {
            return !stack.isEmpty();
        }

        @Override
        public T next() {
            if (!hasNext()) throw new NoSuchElementException();
            Node<T> node = stack.pop();       // Берём верхний (самый левый)
            pushLeft(node.right);             // Добавляем правое поддерево
            return node.value;
        }
    }
}

// ===== Демонстрация =====
public class IteratorDemo {
    public static void main(String[] args) {
        BinarySearchTree<Integer> bst = new BinarySearchTree<>();
        bst.add(5);
        bst.add(3);
        bst.add(7);
        bst.add(1);
        bst.add(4);
        bst.add(6);
        bst.add(8);

        // Клиент не знает о структуре BST: просто использует for-each!
        System.out.print("Обход BST (in-order): ");
        for (Integer value : bst) {          // for-each использует Iterator
            System.out.print(value + " ");
        }
        System.out.println();

        // Или явно через Iterator
        Iterator<Integer> it = bst.iterator();
        System.out.print("Явный итератор:      ");
        while (it.hasNext()) {
            System.out.print(it.next() + " ");
        }
        System.out.println();
    }
}
```

**Плюсы и минусы:**
- [+] Скрывает внутреннее представление коллекции (инкапсуляция)
- [+] Позволяет иметь несколько итераторов на одной коллекции (независимые позиции обхода)
- [+] Можно реализовать разные стратегии обхода (in-order, pre-order, post-order, обход в ширину/BFS)
- [+] Единый интерфейс для всех коллекций (полиморфизм)
- [-] Для простых коллекций (ArrayList) избыточен, но Java всё равно использует Iterator для единообразия с остальными коллекциями (for-each)
- [-] Может быть менее эффективен, чем прямой доступ по индексу (для списков)

**Когда применять:**
- Когда нужно скрыть внутреннюю структуру коллекции от клиента
- Когда нужно поддерживать разные способы обхода одной коллекции
- Когда нужно единообразие в обходе разных типов коллекций
- В Java: `java.util.Iterator`, `java.lang.Iterable`: везде, где есть for-each

**Связи с другими паттернами:**
- Composite часто использует Iterator для обхода дерева
- Factory Method применяется для создания Iterator (метод `iterator()` / `createIterator()`)
- Memento может использоваться для сохранения состояния итератора

---

### 3.5. Mediator (Посредник)

**Назначение:** Централизует сложное взаимодействие между множеством объектов **(коллег)**. Вместо того чтобы объекты ссылались друг на друга напрямую (сетка зависимостей), они общаются только через посредника.

**Проблема:** В сложном UI или бизнес-процессе есть множество взаимосвязанных компонентов. Например, в форме регистрации: поле «Страна» влияет на список «Город», чекбокс «Доставка» влияет на доступность полей адреса, кнопка «Отправить» активна только при заполнении всех полей. Если каждый компонент знает о других, получается **спагетти-зависимостей**: 10 компонентов = до 90 связей. Изменение одного компонента ломает другие.

**Решение:** Ввести центральный объект-посредник. Все компоненты (коллеги) знают только о посреднике и сообщают ему о своих изменениях. Посредник принимает решение, кому из коллег и как реагировать.

**Структура (UML):**
```
┌──────────┐       ┌──────────────────────┐
│ Colleague│       │Mediator (interface)  │
│ (intf)   │       ├──────────────────────┤
├──────────┤       │ + notify(sender,evt) │
│ - mediator│─────>│                      │
└──────────┘       └──────────────────────┘
       ▲                      ▲
   ┌───┴───┐           ┌──────┴──────┐
   │       │           │             │
Colleague1 Colleague2  │  ConcreteMediator  │
                       └────────────────────┘
```

**Участники:**
- `Mediator`: интерфейс для коммуникации с коллегами
- `ConcreteMediator`: координирует взаимодействие конкретных коллег
- `Colleague`: базовый класс для всех компонентов; хранит ссылку на Mediator

**Пример на Java:**

```java
import java.util.*;

// ===== Mediator =====
interface ChatMediator {
    void sendMessage(String message, User sender);
    void addUser(User user);
}

// ===== ConcreteMediator =====
class ChatRoom implements ChatMediator {
    private final List<User> users = new ArrayList<>();

    @Override
    public void addUser(User user) {
        users.add(user);
        System.out.println("[" + user.getName() + " вошёл в чат]");
    }

    @Override
    public void sendMessage(String message, User sender) {
        // Рассылаем сообщение ВСЕМ, кроме отправителя
        for (User user : users) {
            if (user != sender) {
                user.receive(message, sender.getName());
            }
        }
    }
}

// ===== Colleague =====
abstract class User {
    protected final ChatMediator mediator;
    protected final String name;

    public User(ChatMediator mediator, String name) {
        this.mediator = mediator;
        this.name = name;
    }

    public String getName() { return name; }

    public abstract void send(String message);
    public abstract void receive(String message, String senderName);
}

// ===== ConcreteColleague =====
class ChatUser extends User {
    public ChatUser(ChatMediator mediator, String name) {
        super(mediator, name);
    }

    @Override
    public void send(String message) {
        System.out.println(name + " отправляет: " + message);
        mediator.sendMessage(message, this);  // Всё общение: через посредника!
    }

    @Override
    public void receive(String message, String senderName) {
        System.out.println(name + " получил от " + senderName + ": " + message);
    }
}

// ===== Демонстрация =====
public class MediatorDemo {
    public static void main(String[] args) {
        ChatMediator chatRoom = new ChatRoom();

        User alice = new ChatUser(chatRoom, "Alice");
        User bob = new ChatUser(chatRoom, "Bob");
        User charlie = new ChatUser(chatRoom, "Charlie");

        chatRoom.addUser(alice);
        chatRoom.addUser(bob);
        chatRoom.addUser(charlie);

        // Пользователи не знают друг о друге: только о посреднике!
        alice.send("Привет всем!");
        bob.send("Привет, Alice!");
        charlie.send("Всем доброе утро!");

        // Если бы не Mediator, каждому User пришлось бы хранить ссылки
        // на всех остальных пользователей (N*(N-1) связей).
    }
}
```

**Плюсы и минусы:**
- [+] Радикально снижает связность между компонентами (N связей вместо N²)
- [+] Централизует управление взаимодействием: легче понять, кто с кем общается
- [+] Компоненты становятся переиспользуемыми (не зависят от других компонентов)
- [+] Упрощает добавление новых коллег
- [-] Посредник может превратиться в **«божественный объект»** (God Object): монолит, знающий всё обо всех
- [-] Сложность посредника растёт с количеством коллег

**Когда применять:**
- Когда множество объектов взаимодействуют сложным, неструктурированным образом
- Когда трудно переиспользовать объект из-за его зависимости от многих других
- Когда поведение распределено между многими классами, и его нужно централизовать
- Примеры: чат-комнаты, диспетчеры событий в GUI, оркестраторы в микросервисах

**Связи с другими паттернами:**
- Facade: похож на Mediator, но Facade действует односторонне (упрощает доступ к подсистеме), а Mediator двусторонне (коллеги тоже общаются с ним)
- Observer: альтернатива Mediator для one-to-many коммуникации; Observer децентрализован, Mediator централизован
- Command часто используется для передачи через Mediator

---

### 3.6. Memento (Снимок)

**Назначение:** Сохраняет и восстанавливает предыдущее состояние объекта, **не нарушая инкапсуляцию**. Позволяет реализовать отмену операций (undo) без раскрытия внутренней структуры объекта.

**Проблема:** Нужно сохранить состояние объекта (например, текстового редактора) для последующего восстановления (undo). Если сделать все поля публичными или дать get-методы на все поля, будет нарушена инкапсуляция: любой сможет прочитать и изменить внутреннее состояние. Хочется сохранить состояние так, чтобы только сам объект-владелец мог его прочитать и восстановить.

**Решение:** Объект-владелец (Originator) создаёт объект-снимок (Memento), в который копирует своё состояние. Memento непрозрачен для всех остальных: его содержимое доступно только Originator. Хранитель (Caretaker) управляет снимками (сохраняет, возвращает), но не заглядывает в них.

**Структура (UML):**
```
┌────────────────────┐        ┌───────────────────┐        ┌──────────────────┐
│    Originator      │        │     Memento       │        │    Caretaker     │
├────────────────────┤        ├───────────────────┤        ├──────────────────┤
│ - state            │───────>│ - state (private) │        │ - mementos:List  │
│ + createMemento()  │        │ + getState()      │        │ + save(Memento)  │
│ + restore(memento) │<───────│   (package-private│        │ + undo(): Memento│
└────────────────────┘        │    или private)    │        └──────────────────┘
                              └───────────────────┘
```

**Участники:**
- `Originator`: объект, чьё состояние сохраняется и восстанавливается
- `Memento`: непрозрачный объект-снимок, хранящий состояние Originator
- `Caretaker`: управляет снимками, но не модифицирует и не читает их содержимое

**Пример на Java:**

```java
import java.util.*;

// ===== Memento: непрозрачен для всех, кроме Originator =====
class EditorMemento {
    private final String text;         // package-private (или через интерфейс с маркером)
    private final int cursorPosition;

    EditorMemento(String text, int cursorPosition) {
        this.text = text;
        this.cursorPosition = cursorPosition;
    }

    // Только Editor может получить доступ (package-private или inner class)
    String getText() { return text; }
    int getCursorPosition() { return cursorPosition; }
}

// ===== Originator =====
class Editor {
    private final StringBuilder text = new StringBuilder();
    private int cursorPosition = 0;

    public void type(String words) {
        text.insert(cursorPosition, words);
        cursorPosition += words.length();
    }

    public void moveCursor(int position) {
        this.cursorPosition = Math.max(0, Math.min(position, text.length()));
    }

    public String getContent() {
        return text.toString();
    }

    // Создаёт снимок текущего состояния
    public EditorMemento save() {
        return new EditorMemento(text.toString(), cursorPosition);
    }

    // Восстанавливает состояние из снимка
    public void restore(EditorMemento memento) {
        text.setLength(0);
        text.append(memento.getText());
        cursorPosition = memento.getCursorPosition();
    }

    @Override
    public String toString() {
        return "Текст: '" + text + "' | Курсор: " + cursorPosition;
    }
}

// ===== Caretaker =====
class History {
    private final Deque<EditorMemento> undoStack = new ArrayDeque<>();
    private final Deque<EditorMemento> redoStack = new ArrayDeque<>();

    public void save(EditorMemento memento) {
        undoStack.push(memento);
        redoStack.clear();  // Новое действие обрывает цепочку redo
    }

    public EditorMemento undo(EditorMemento currentState) {
        if (!undoStack.isEmpty()) {
            redoStack.push(currentState);
            return undoStack.pop();
        }
        return null;
    }

    public EditorMemento redo(EditorMemento currentState) {
        if (!redoStack.isEmpty()) {
            undoStack.push(currentState);
            return redoStack.pop();
        }
        return null;
    }
}

// ===== Демонстрация =====
public class MementoDemo {
    public static void main(String[] args) {
        Editor editor = new Editor();
        History history = new History();

        editor.type("Hello");
        history.save(editor.save());     // Сохраняем состояние 1
        System.out.println(editor);

        editor.type(", World!");
        history.save(editor.save());     // Сохраняем состояние 2
        System.out.println(editor);

        editor.type(" How are you?");
        System.out.println(editor);

        // Undo: возвращаемся к состоянию 2
        EditorMemento previous = history.undo(editor.save());
        if (previous != null) {
            editor.restore(previous);
        }
        System.out.println("После undo: " + editor);

        // Undo: возвращаемся к состоянию 1
        previous = history.undo(editor.save());
        if (previous != null) {
            editor.restore(previous);
        }
        System.out.println("После undo: " + editor);

        // Redo: возвращаем состояние 2
        previous = history.redo(editor.save());
        if (previous != null) {
            editor.restore(previous);
        }
        System.out.println("После redo: " + editor);
    }
}
```

**Плюсы и минусы:**
- [+] Сохраняет инкапсуляцию: только Originator может читать/писать Memento
- [+] Упрощает Originator (Caretaker берёт на себя управление историей)
- [+] Позволяет делать снимки в любой момент: не нужно продумывать интерфейс сохранения заранее
- [-] Может потреблять много памяти, если снимки большие или их много
- [-] Caretaker должен знать, когда делать снимки (ответственность за это размыта)
- [-] В языках без package-private / friend-механизмов сложно скрыть содержимое Memento от всех, кроме Originator

**Когда применять:**
- Когда нужна поддержка undo/redo операций
- Когда нужно сохранять контрольные точки (checkpoints) для отката транзакций
- Когда прямой доступ к состоянию объекта нарушит инкапсуляцию
- Примеры: сериализация объектов (`java.io.Serializable`), снимки состояния в редакторах (undo/redo), транзакционные checkpoint'ы в БД

**Связи с другими паттернами:**
- Command использует Memento для хранения состояния undo
- Iterator может использовать Memento для сохранения позиции обхода
- Memento можно реализовать через Prototype (клон Originator = его снимок)

---

### 3.7. Observer (Наблюдатель)

**Назначение:** Определяет зависимость **«один-ко-многим»** между объектами так, что при изменении состояния одного объекта **(Subject)** все зависимые объекты **(Observers)** автоматически уведомляются и обновляются.

**Проблема:** Есть источник данных (например, биржевой тикер, датчик температуры, модель данных), и несколько компонентов интерфейса (графики, таблицы, алерты), которые должны отображать актуальные данные. Если жёстко связать источник с каждым компонентом, код станет немодифицируемым: добавление нового компонента потребует изменения источника.

**Решение:** Источник данных (Subject/Publisher) хранит коллекцию подписчиков (Observers). При изменении состояния Subject оповещает всех подписчиков вызовом их метода `update()`. Подписчики могут динамически подписываться и отписываться.

**Структура (UML):**
```
┌──────────────────────┐         ┌──────────────────────┐
│  Subject (interface) │         │ Observer (interface) │
├──────────────────────┤         ├──────────────────────┤
│ + attach(Observer)   │────────>│ + update()           │
│ + detach(Observer)   │         └──────────────────────┘
│ + notifyObservers()  │                    ▲
└──────────────────────┘          ┌─────────┼─────────┐
            ▲                     │         │         │
   ┌────────┴────────┐    Observer1  Observer2  Observer3
   │ ConcreteSubject  │
   │ - state          │
   │ + getState()     │
   │ + setState()     │──> notifyObservers()
   └──────────────────┘
```

**Участники:**
- `Subject` (издатель): хранит список наблюдателей; предоставляет методы подписки/отписки
- `Observer` (подписчик): интерфейс с методом `update()`
- `ConcreteSubject`: конкретный издатель; при изменении своего состояния вызывает `notifyObservers()`
- `ConcreteObserver`: конкретный подписчик; в `update()` обновляет своё состояние

**Пример на Java:**

```java
import java.util.*;

// ===== Observer =====
interface StockObserver {
    void update(String stockSymbol, double price);
}

// ===== Subject =====
class StockMarket {
    private final Map<String, List<StockObserver>> observers = new HashMap<>();
    private final Map<String, Double> prices = new HashMap<>();

    public void subscribe(String stockSymbol, StockObserver observer) {
        observers.computeIfAbsent(stockSymbol, k -> new ArrayList<>()).add(observer);
        System.out.println("  + Подписчик добавлен на " + stockSymbol);
    }

    public void unsubscribe(String stockSymbol, StockObserver observer) {
        List<StockObserver> list = observers.get(stockSymbol);
        if (list != null) {
            list.remove(observer);
            System.out.println("  - Подписчик удалён с " + stockSymbol);
        }
    }

    public void setPrice(String stockSymbol, double price) {
        prices.put(stockSymbol, price);
        notifyObservers(stockSymbol, price);
    }

    private void notifyObservers(String stockSymbol, double price) {
        List<StockObserver> list = observers.get(stockSymbol);
        if (list != null) {
            for (StockObserver observer : list) {
                observer.update(stockSymbol, price);  // Оповещение!
            }
        }
    }
}

// ===== Concrete Observers =====
class PriceDisplay implements StockObserver {
    private final String name;

    public PriceDisplay(String name) { this.name = name; }

    @Override
    public void update(String stockSymbol, double price) {
        System.out.println("  [" + name + "] " + stockSymbol + " = $" + price);
    }
}

class AlertSystem implements StockObserver {
    private final double threshold;

    public AlertSystem(double threshold) { this.threshold = threshold; }

    @Override
    public void update(String stockSymbol, double price) {
        if (price > threshold) {
            System.out.println("  [ALERT!] " + stockSymbol + " превысил $" + threshold
                    + "! Текущая цена: $" + price);
        }
    }
}

// ===== Демонстрация =====
public class ObserverDemo {
    public static void main(String[] args) {
        StockMarket market = new StockMarket();

        // Создаём подписчиков
        StockObserver display1 = new PriceDisplay("Дисплей 1");
        StockObserver display2 = new PriceDisplay("Дисплей 2");
        StockObserver alert = new AlertSystem(150.0);

        // Подписываемся
        market.subscribe("AAPL", display1);
        market.subscribe("AAPL", display2);
        market.subscribe("AAPL", alert);
        market.subscribe("GOOGL", display1);

        System.out.println("\n=== Изменение цены AAPL ===");
        market.setPrice("AAPL", 145.0);   // 2 дисплея + алерт (не сработает)

        System.out.println("\n=== Изменение цены AAPL ===");
        market.setPrice("AAPL", 155.0);   // 2 дисплея + алерт (сработает!)

        System.out.println("\n=== Отписка display2 от AAPL ===");
        market.unsubscribe("AAPL", display2);

        System.out.println("\n=== Изменение цены AAPL ===");
        market.setPrice("AAPL", 160.0);   // Только display1 + алерт

        System.out.println("\n=== Изменение цены GOOGL ===");
        market.setPrice("GOOGL", 2800.0); // Только display1
    }
}
```

**Плюсы и минусы:**
- [+] Слабая связность: Subject не знает о конкретных классах Observer, только об интерфейсе
- [+] Динамическая подписка/отписка во время выполнения
- [+] Поддержка широковещательной рассылки (один источник → множество получателей)
- [-] Наблюдатели уведомляются в неопределённом порядке (если порядок важен: нужно управлять явно)
- [-] Возможно каскадное обновление (Observer меняет Subject, тот опять шлёт update → бесконечный цикл)
- [-] Утечка памяти, если забыть отписать Observer (Subject держит ссылку → GC не соберёт)

**Когда применять:**
- Когда изменение одного объекта требует изменения других, а их набор заранее неизвестен
- Когда объект должен оповещать другие объекты, не делая предположений об их типах
- Классические примеры: Model-View-Controller (MVC), EventListener в Java GUI, `@EventListener` в Spring, Reactive Programming

**Связи с другими паттернами:**
- Mediator централизует многостороннее взаимодействие; Observer: децентрализованное одностороннее (one-to-many)
- Singleton может быть Subject'ом (единственный источник событий)
- Observer часто комбинируется с Command (вместо прямого вызова update: команда ставится в очередь)

---

### 3.8. State (Состояние)

**Назначение:** Позволяет объекту **изменять своё поведение** при изменении его внутреннего состояния. Создаётся впечатление, что объект меняет свой класс во время выполнения.

**Проблема:** Объект (например, заказ, торговый автомат, TCP-соединение, персонаж игры) имеет несколько дискретных состояний, и его поведение радикально зависит от текущего состояния. Без паттерна код заполняется гигантскими `if-else` или `switch-case` конструкциями в каждом методе, проверяющими текущее состояние. Добавление нового состояния требует изменения всех этих методов.

**Решение:** Каждое состояние выносится в отдельный класс, реализующий общий интерфейс `State`. Контекст хранит ссылку на текущее состояние и делегирует ему все вызовы. Состояние может само переключать контекст на другое состояние.

**Структура (UML):**
```
┌───────────────────────┐         ┌───────────────────────┐
│        Context        │         │   State (interface)   │
├───────────────────────┤         ├───────────────────────┤
│ - state: State        │────────>│ + handle1()           │
│ + request1()          │         │ + handle2()           │
│ + request2()          │         └───────────────────────┘
│ + setState(State)     │                    ▲
└───────────────────────┘         ┌──────────┼──────────┐
                                  │          │          │
                            StateA     StateB     StateC
```

**Участники:**
- `Context`: объект, поведение которого зависит от состояния; хранит ссылку на текущий `State`
- `State`: интерфейс для всех состояний
- `ConcreteState`: конкретное состояние; реализует поведение, специфичное для этого состояния; может переключать Context на другое состояние

**Пример на Java: торговый автомат:**

```java
// ===== State =====
interface VendingMachineState {
    void insertCoin(VendingMachine machine);
    void selectProduct(VendingMachine machine);
    void dispense(VendingMachine machine);
    void refund(VendingMachine machine);
}

// ===== Context =====
class VendingMachine {
    private VendingMachineState noCoinState;
    private VendingMachineState hasCoinState;
    private VendingMachineState soldState;
    private VendingMachineState soldOutState;

    private VendingMachineState currentState;
    private int productCount;

    public VendingMachine(int productCount) {
        noCoinState = new NoCoinState();
        hasCoinState = new HasCoinState();
        soldState = new SoldState();
        soldOutState = new SoldOutState();

        this.productCount = productCount;
        this.currentState = productCount > 0 ? noCoinState : soldOutState;
    }

    public void setState(VendingMachineState state) { this.currentState = state; }
    public VendingMachineState getNoCoinState() { return noCoinState; }
    public VendingMachineState getHasCoinState() { return hasCoinState; }
    public VendingMachineState getSoldState() { return soldState; }
    public VendingMachineState getSoldOutState() { return soldOutState; }

    public int getProductCount() { return productCount; }
    public void releaseProduct() {
        if (productCount > 0) {
            productCount--;
            System.out.println("   Товар выдан. Осталось: " + productCount);
        }
    }

    // Делегирование текущему состоянию
    public void insertCoin()    { currentState.insertCoin(this); }
    public void selectProduct() { currentState.selectProduct(this); }
    public void dispense()      { currentState.dispense(this); }
    public void refund()        { currentState.refund(this); }
}

// ===== Concrete States =====
class NoCoinState implements VendingMachineState {
    @Override
    public void insertCoin(VendingMachine machine) {
        System.out.println("[OK] Монета принята.");
        machine.setState(machine.getHasCoinState());
    }
    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("[ОШИБКА] Сначала внесите монету!");
    }
    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("[ОШИБКА] Сначала внесите монету и выберите товар!");
    }
    @Override
    public void refund(VendingMachine machine) {
        System.out.println("[ОШИБКА] Монета не внесена: нечего возвращать.");
    }
}

class HasCoinState implements VendingMachineState {
    @Override
    public void insertCoin(VendingMachine machine) {
        System.out.println("[ОШИБКА] Монета уже внесена. Выберите товар или верните монету.");
    }
    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("[OK] Товар выбран. Выдача...");
        machine.setState(machine.getSoldState());
        machine.dispense();  // Автоматический переход к выдаче
    }
    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("[ОШИБКА] Сначала выберите товар!");
    }
    @Override
    public void refund(VendingMachine machine) {
        System.out.println("[OK] Монета возвращена.");
        machine.setState(machine.getNoCoinState());
    }
}

class SoldState implements VendingMachineState {
    @Override
    public void insertCoin(VendingMachine machine) {
        System.out.println("[ОШИБКА] Подождите, идёт выдача товара!");
    }
    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("[ОШИБКА] Идёт выдача: дождитесь завершения.");
    }
    @Override
    public void dispense(VendingMachine machine) {
        machine.releaseProduct();
        if (machine.getProductCount() > 0) {
            machine.setState(machine.getNoCoinState());
        } else {
            System.out.println("   Товар закончился!");
            machine.setState(machine.getSoldOutState());
        }
    }
    @Override
    public void refund(VendingMachine machine) {
        System.out.println("[ОШИБКА] Товар уже выдан: возврат невозможен.");
    }
}

class SoldOutState implements VendingMachineState {
    @Override
    public void insertCoin(VendingMachine machine) {
        System.out.println("[ОШИБКА] Товар закончился. Монета не принята.");
    }
    @Override
    public void selectProduct(VendingMachine machine) {
        System.out.println("[ОШИБКА] Товар закончился.");
    }
    @Override
    public void dispense(VendingMachine machine) {
        System.out.println("[ОШИБКА] Товара нет.");
    }
    @Override
    public void refund(VendingMachine machine) {
        System.out.println("[ОШИБКА] Монета не вносилась.");
    }
}

// ===== Демонстрация =====
public class StateDemo {
    public static void main(String[] args) {
        VendingMachine machine = new VendingMachine(2);  // 2 товара

        System.out.println("=== Сценарий 1: успешная покупка ===");
        machine.insertCoin();
        machine.selectProduct();

        System.out.println("\n=== Сценарий 2: возврат монеты ===");
        machine.insertCoin();
        machine.refund();

        System.out.println("\n=== Сценарий 3: последний товар ===");
        machine.insertCoin();
        machine.selectProduct();

        System.out.println("\n=== Сценарий 4: товар закончился ===");
        machine.insertCoin();
        machine.selectProduct();
    }
}
```

**Плюсы и минусы:**
- [+] Устраняет громоздкие `if-else` / `switch-case`: каждое состояние в своём классе
- [+] Добавление нового состояния = добавление нового класса (Open/Closed Principle)
- [+] Упрощает тестирование (каждое состояние тестируется изолированно)
- [+] Явно моделирует переходы между состояниями (диаграмма состояний прямо в коде)
- [-] Увеличивает количество классов (каждое состояние: отдельный класс)
- [-] Если состояний мало (2-3) и они редко меняются: паттерн избыточен
- [-] Переходы размазаны по классам состояний: сложно увидеть общую картину

**Когда применять:**
- Когда поведение объекта радикально зависит от его состояния
- Когда код заполнен `if-else`, проверяющими состояние объекта
- Когда количество состояний больше 3-4 и/или они часто меняются
- Примеры: состояния заказа (NEW → PAID → SHIPPED → DELIVERED), TCP-соединения, конечные автоматы в играх

**Связи с другими паттернами:**
- Strategy: структурный близнец State, но Strategy не управляет переходами (контекст сам выбирает стратегию); State сам переключает контекст
- Flyweight: состояния могут быть разделяемыми легковесами (без внутренних полей)
- Состояния могут быть Singleton (если у них нет полей: зачем создавать по экземпляру на контекст?)

---

### 3.9. Strategy (Стратегия)

**Назначение:** Определяет **семейство взаимозаменяемых алгоритмов**, инкапсулирует каждый из них в отдельный класс и позволяет подменять их во время выполнения. Алгоритм выбирается независимо от клиента.

**Проблема:** У вас есть задача, которую можно решить разными способами. Например, сортировка (`QuickSort`, `MergeSort`, `BubbleSort`), сжатие (`ZIP`, `RAR`, `GZIP`), расчёт скидки (`FlatDiscount`, `PercentageDiscount`, `NoDiscount`). Без паттерна код ветвится на `if (algorithm == "quick") ... else if ...` в каждом месте, где нужен разный алгоритм. Добавление нового алгоритма требует изменения всех этих мест.

**Решение:** Выделить алгоритм в отдельный класс, реализующий общий интерфейс `Strategy`. Контекст хранит ссылку на текущую стратегию и делегирует ей работу. Клиент может подменять стратегию во время выполнения.

**Структура (UML):**
```
┌───────────────────┐         ┌─────────────────────────┐
│     Context       │         │  Strategy (interface)   │
├───────────────────┤         ├─────────────────────────┤
│ - strategy: Strat │────────>│ + algorithm(data): R    │
│ + executeStrategy │         └─────────────────────────┘
│ + setStrategy()   │                      ▲
└───────────────────┘          ┌───────────┼───────────┐
                               │           │           │
                         StrategyA   StrategyB   StrategyC
```

**Участники:**
- `Strategy`: общий интерфейс для всех алгоритмов
- `ConcreteStrategy`: конкретная реализация алгоритма
- `Context`: использует стратегию; хранит ссылку на `Strategy`

**Пример на Java:**

```java
// ===== Strategy =====
interface PaymentStrategy {
    void pay(double amount);
}

// ===== Concrete Strategies =====
class CreditCardPayment implements PaymentStrategy {
    private final String cardNumber;
    private final String name;

    public CreditCardPayment(String cardNumber, String name) {
        this.cardNumber = cardNumber;
        this.name = name;
    }

    @Override
    public void pay(double amount) {
        System.out.println("Оплата $" + amount + " через КРЕДИТНУЮ КАРТУ " +
                maskCard(cardNumber) + " (" + name + ")");
    }

    private String maskCard(String number) {
        return "****-****-****-" + number.substring(number.length() - 4);
    }
}

class PayPalPayment implements PaymentStrategy {
    private final String email;

    public PayPalPayment(String email) { this.email = email; }

    @Override
    public void pay(double amount) {
        System.out.println("Оплата $" + amount + " через PayPal (" + email + ")");
    }
}

class CryptoPayment implements PaymentStrategy {
    private final String walletAddress;

    public CryptoPayment(String walletAddress) { this.walletAddress = walletAddress; }

    @Override
    public void pay(double amount) {
        System.out.println("Оплата $" + amount + " через КРИПТОКОШЕЛЁК " +
                walletAddress.substring(0, 8) + "...");
    }
}

// ===== Context =====
class ShoppingCart {
    private final List<Double> items = new ArrayList<>();

    public void addItem(double price) {
        items.add(price);
    }

    public double getTotal() {
        return items.stream().mapToDouble(Double::doubleValue).sum();
    }

    // Стратегия выбирается клиентом и передаётся в метод оплаты
    public void checkout(PaymentStrategy strategy) {
        double total = getTotal();
        if (total == 0) {
            System.out.println("Корзина пуста.");
            return;
        }
        strategy.pay(total);  // Делегирование стратегии: контекст не знает деталей
    }
}

// ===== Демонстрация =====
public class StrategyDemo {
    public static void main(String[] args) {
        ShoppingCart cart = new ShoppingCart();
        cart.addItem(29.99);
        cart.addItem(49.99);
        cart.addItem(9.99);

        System.out.println("Сумма заказа: $" + cart.getTotal());

        // Клиент выбирает стратегию во время выполнения
        cart.checkout(new CreditCardPayment("1234567890123456", "Иван Петров"));

        // Тот же контекст: другая стратегия
        cart.checkout(new PayPalPayment("ivan@example.com"));

        // Ещё одна стратегия
        cart.checkout(new CryptoPayment("0xABCDEF1234567890ABCDEF"));
    }
}
```

**Плюсы и минусы:**
- [+] Семейство алгоритмов: каждый в своём классе (SRP)
- [+] Алгоритм можно подменить на лету (во время выполнения)
- [+] Легко добавить новый алгоритм: создать класс, не трогая существующий код (OCP)
- [+] Условная логика (`if-else`) заменена полиморфизмом
- [-] Увеличивает количество классов
- [-] Клиент должен знать о различиях между стратегиями, чтобы выбрать подходящую
- [-] Для 2-3 простых вариантов: избыточен (используйте enum с лямбдами)

**Когда применять:**
- Когда есть несколько вариантов одного алгоритма
- Когда алгоритм должен варьироваться независимо от клиента
- Когда в коде есть множество условных операторов (`if-else`, `switch`) для выбора поведения
- Примеры: `Comparator<T>` в Java, способы сжатия/шифрования, стратегии расчёта налогов/скидок

**Связи с другими паттернами:**
- State: структурный близнец Strategy. Разница: в State состояния знают друг о друге и переключают контекст; в Strategy стратегии независимы и не знают друг о друге
- Bridge: стратегия на уровне архитектуры (два независимых измерения); Strategy: на уровне поведения (один аспект)
- Template Method использует наследование (скелет в базовом классе); Strategy использует композицию (алгоритм делегируется)
- Decorator меняет поведение снаружи; Strategy: изнутри

---

### 3.10. Template Method (Шаблонный метод)

**Назначение:** Определяет **скелет алгоритма** в базовом классе, перекладывая реализацию некоторых шагов на подклассы. Подклассы переопределяют шаги, не изменяя структуру самого алгоритма.

**Проблема:** Есть алгоритм с фиксированной структурой (последовательностью шагов), но некоторые шаги могут варьироваться. Например, приготовление напитка: 1) вскипятить воду, 2) заварить, 3) налить в чашку, 4) добавить добавки. Шаги 1 и 3 одинаковы для чая и кофе, шаги 2 и 4 разные. Хотим избежать дублирования общего кода в каждом подклассе, но позволить подклассам менять вариативные шаги.

**Решение:** Базовый класс реализует шаблонный метод (`final`, чтобы подклассы не сломали структуру), вызывающий последовательность шагов. Часть шагов реализована прямо в базовом классе (общая логика), часть абстрактные (подклассы обязаны реализовать), часть с реализацией по умолчанию (хуки, которые подклассы могут переопределить при желании).

**Структура (UML):**
```
┌───────────────────────────────┐
│   AbstractClass               │
├───────────────────────────────┤
│ + templateMethod()  (final)   │──> step1();
│                                 │   step2();
│ - step1()          (конкретный)│   step3();
│ # step2()          (абстрактный)│
│ # step3()          (хук)       │
└───────────────────────────────┘
                 ▲
    ┌────────────┴────────────┐
    │                         │
ConcreteClassA          ConcreteClassB
- step2()               - step2()
- step3() (опционально) - step3()
```

**Участники:**
- `AbstractClass`: определяет шаблонный метод (скелет алгоритма) и общие/вариативные шаги
- `ConcreteClass`: реализует вариативные шаги

**Пример на Java:**

```java
// ===== AbstractClass: скелет алгоритма =====
abstract class DataMiner {

    // Шаблонный метод: final, чтобы подклассы не сломали структуру алгоритма
    public final void mine(String path) {
        System.out.println("=== Анализ данных: " + path + " ===");
        String rawData = extractData(path);      // Шаг 1: абстрактный
        String parsedData = parseData(rawData);  // Шаг 2: абстрактный
        String analyzed = analyzeData(parsedData); // Шаг 3: конкретный (общий)
        sendReport(analyzed);                    // Шаг 4: хук (с реализацией по умолчанию)
        System.out.println("=== Анализ завершён ===\n");
    }

    // Абстрактные шаги: подклассы ОБЯЗАНЫ реализовать
    protected abstract String extractData(String path);
    protected abstract String parseData(String rawData);

    // Общий шаг: одинаковая логика для всех
    private String analyzeData(String data) {
        System.out.println("  [Общая логика] Анализирую данные...");
        return "Результат анализа: " + data.length() + " записей обработано";
    }

    // Хук (hook): опциональный шаг с реализацией по умолчанию
    protected void sendReport(String result) {
        System.out.println("  [По умолчанию] Отчёт сохранён локально: " + result);
    }
}

// ===== ConcreteClass 1 =====
class CsvDataMiner extends DataMiner {
    @Override
    protected String extractData(String path) {
        System.out.println("  [CSV] Извлекаю данные из CSV-файла: " + path);
        return "id,name,age\n1,Alice,30\n2,Bob,25\n3,Charlie,35";
    }

    @Override
    protected String parseData(String rawData) {
        System.out.println("  [CSV] Паршу CSV-строки...");
        return rawData.replace(",", " | ");
    }
}

// ===== ConcreteClass 2 =====
class JsonDataMiner extends DataMiner {
    @Override
    protected String extractData(String path) {
        System.out.println("  [JSON] Извлекаю данные из JSON-файла: " + path);
        return "{ \"users\": [{\"name\": \"Alice\"}, {\"name\": \"Bob\"}] }";
    }

    @Override
    protected String parseData(String rawData) {
        System.out.println("  [JSON] Паршу JSON...");
        return rawData.replace("{", "[").replace("}", "]");
    }

    // Переопределяем хук: отправляем отчёт по email вместо сохранения на диск
    @Override
    protected void sendReport(String result) {
        System.out.println("  [JSON] Отчёт отправлен по email: admin@example.com: " + result);
    }
}

// ===== Демонстрация =====
public class TemplateMethodDemo {
    public static void main(String[] args) {
        DataMiner csvMiner = new CsvDataMiner();
        csvMiner.mine("/data/report.csv");

        DataMiner jsonMiner = new JsonDataMiner();
        jsonMiner.mine("/data/report.json");
    }
}
```

**Плюсы и минусы:**
- [+] Устраняет дублирование кода (общая логика: в базовом классе)
- [+] Подклассы могут менять только вариативные части, не трогая структуру алгоритма
- [+] Шаблонный метод `final`: никто не сломает алгоритм
- [+] Хуки дают гибкость (опциональное переопределение)
- [-] Наследование создаёт жёсткую связь между базовым и дочерними классами
- [-] Алгоритм фиксирован на этапе компиляции: нельзя изменить порядок шагов во время выполнения
- [-] Можно нарушить принцип подстановки Лисков, если подкласс меняет смысл шага

**Когда применять:**
- Когда несколько классов реализуют похожий алгоритм с небольшими вариациями
- Когда нужно централизовать общую логику, избегая дублирования
- Когда нужно контролировать структуру алгоритма и разрешить подклассам менять только шаги
- Примеры: `java.io.InputStream` (read: шаблонный метод), `javax.servlet.http.HttpServlet` (doGet/doPost: вариативные шаги), `AbstractList` в Java Collections

**Связи с другими паттернами:**
- Strategy: альтернатива Template Method на композиции (Strategy делегирует весь алгоритм, Template Method только шаги)
- Factory Method часто вызывается внутри Template Method (шаблонный метод вызывает фабричный для создания продукта)
- Template Method часто эволюционирует в Strategy, когда нужно больше гибкости (рантайм-переключение)

---

### 3.11. Visitor (Посетитель)

**Назначение:** Позволяет **добавлять новые операции** к объектам сложной структуры (иерархии), не изменяя классы этих объектов. Операция выносится в отдельный класс-посетитель.

**Проблема:** У вас есть иерархия классов (например, элементы документа: `Paragraph`, `Image`, `Table`, `CodeBlock`). Вы хотите добавить новые операции над этой иерархией: экспорт в HTML, экспорт в Markdown, подсчёт слов, проверку орфографии... Если добавлять метод в каждый класс, это нарушает Open/Closed Principle и размазывает логику. Если использовать `instanceof`, это хрупко и некрасиво.

**Решение:** Каждый элемент иерархии реализует метод `accept(Visitor v)`, который вызывает у посетителя метод, соответствующий типу элемента: `v.visitParagraph(this)`, `v.visitImage(this)`. Посетитель содержит набор методов `visitXxx()`: по одному на каждый тип элемента. Новая операция = новый класс Visitor, без изменений в иерархии элементов.

**Структура (UML):**
```
┌─────────────────────────┐         ┌──────────────────────────────┐
│  Visitor (interface)    │         │  Element (interface)         │
├─────────────────────────┤         ├──────────────────────────────┤
│ + visitA(ConcreteElemA) │         │ + accept(Visitor v)          │
│ + visitB(ConcreteElemB) │         └──────────────────────────────┘
└─────────────────────────┘                        ▲
            ▲                            ┌──────────┴──────────┐
   ┌────────┴────────┐                   │                     │
   │                 │            ConcreteElemA          ConcreteElemB
ConcreteVisitor1  ConcreteVisitor2    │                     │
                                   accept(v) {          accept(v) {
                                     v.visitA(this);      v.visitB(this);
                                   }                    }
```

**Участники:**
- `Visitor`: интерфейс с методами `visit()` для каждого типа элемента
- `ConcreteVisitor`: реализует конкретную операцию
- `Element`: интерфейс с методом `accept(Visitor)`
- `ConcreteElement`: реализует `accept()`, вызывая соответствующий `visit()` у посетителя
- `ObjectStructure`: коллекция или композит элементов

**Пример на Java:**

```java
import java.util.*;

// ===== Element =====
interface DocumentElement {
    void accept(DocumentVisitor visitor);
}

// ===== Concrete Elements =====
class Paragraph implements DocumentElement {
    private final String text;

    public Paragraph(String text) { this.text = text; }
    public String getText() { return text; }

    @Override
    public void accept(DocumentVisitor visitor) {
        visitor.visit(this);   // Double dispatch: visitor.visit(Paragraph)
    }
}

class Image implements DocumentElement {
    private final String url;
    private final int width, height;

    public Image(String url, int width, int height) {
        this.url = url;
        this.width = width;
        this.height = height;
    }

    public String getUrl() { return url; }
    public int getWidth() { return width; }
    public int getHeight() { return height; }

    @Override
    public void accept(DocumentVisitor visitor) {
        visitor.visit(this);
    }
}

class Table implements DocumentElement {
    private final List<String[]> rows = new ArrayList<>();

    public void addRow(String... cells) { rows.add(cells); }
    public List<String[]> getRows() { return rows; }

    @Override
    public void accept(DocumentVisitor visitor) {
        visitor.visit(this);
    }
}

// ===== Visitor =====
interface DocumentVisitor {
    void visit(Paragraph paragraph);
    void visit(Image image);
    void visit(Table table);
}

// ===== Concrete Visitors: добавляем операции без изменения элементов! =====

// Экспорт в HTML
class HtmlExportVisitor implements DocumentVisitor {
    private final StringBuilder output = new StringBuilder();

    @Override
    public void visit(Paragraph p) {
        output.append("<p>").append(p.getText()).append("</p>\n");
    }

    @Override
    public void visit(Image img) {
        output.append("<img src=\"").append(img.getUrl())
              .append("\" width=\"").append(img.getWidth())
              .append("\" height=\"").append(img.getHeight()).append("\" />\n");
    }

    @Override
    public void visit(Table table) {
        output.append("<table border=\"1\">\n");
        for (String[] row : table.getRows()) {
            output.append("  <tr>");
            for (String cell : row) {
                output.append("<td>").append(cell).append("</td>");
            }
            output.append("</tr>\n");
        }
        output.append("</table>\n");
    }

    public String getHtml() { return output.toString(); }
}

// Подсчёт слов
class WordCountVisitor implements DocumentVisitor {
    private int wordCount = 0;

    @Override
    public void visit(Paragraph p) {
        wordCount += p.getText().split("\\s+").length;
    }

    @Override
    public void visit(Image img) {
        // Изображения не содержат слов
    }

    @Override
    public void visit(Table table) {
        for (String[] row : table.getRows()) {
            for (String cell : row) {
                wordCount += cell.split("\\s+").length;
            }
        }
    }

    public int getWordCount() { return wordCount; }
}

// ===== ObjectStructure =====
class Document {
    private final List<DocumentElement> elements = new ArrayList<>();

    public void addElement(DocumentElement element) { elements.add(element); }

    public void accept(DocumentVisitor visitor) {
        for (DocumentElement element : elements) {
            element.accept(visitor);
        }
    }
}

// ===== Демонстрация =====
public class VisitorDemo {
    public static void main(String[] args) {
        Document doc = new Document();
        doc.addElement(new Paragraph("Добро пожаловать в мир паттернов!"));
        doc.addElement(new Image("logo.png", 200, 100));
        doc.addElement(new Paragraph("Это документ, демонстрирующий Visitor."));

        Table table = new Table();
        table.addRow("Имя", "Возраст", "Город");
        table.addRow("Alice", "30", "Москва");
        table.addRow("Bob", "25", "СПб");
        doc.addElement(table);

        // Экспорт в HTML: новая операция без изменения Paragraph/Image/Table!
        HtmlExportVisitor htmlVisitor = new HtmlExportVisitor();
        doc.accept(htmlVisitor);
        System.out.println("=== HTML-экспорт ===");
        System.out.println(htmlVisitor.getHtml());

        // Подсчёт слов: ещё одна новая операция!
        WordCountVisitor wordCountVisitor = new WordCountVisitor();
        doc.accept(wordCountVisitor);
        System.out.println("=== Подсчёт слов ===");
        System.out.println("Всего слов: " + wordCountVisitor.getWordCount());
    }
}
```

**Плюсы и минусы:**
- [+] Новые операции добавляются без изменения классов элементов (Open/Closed Principle)
- [+] Собирает связанную логику в одном классе (Visitor), а не размазывает по иерархии
- [+] Посетитель может накапливать состояние по мере обхода (stateful visitor)
- [-] Добавление нового типа элемента требует изменения интерфейса Visitor и всех его реализаций
- [-] Элементы должны раскрыть достаточно данных для Visitor: может нарушиться инкапсуляция
- [-] Double dispatch сложен для понимания (но это стандартная техника)
- [-] Посетитель и элементы становятся сильно связанными (циклическая зависимость интерфейсов)

**Когда применять:**
- Когда иерархия элементов **стабильна** (редко добавляются новые типы), а операции над ней часто меняются
- Когда над элементами сложной структуры (Composite) нужно выполнять много разнородных операций
- Когда нужно отделить алгоритм от структуры данных
- Примеры: компиляторы (AST + Visitor для семантического анализа, оптимизации, кодогенерации), экспорт документов в разные форматы

**Связи с другими паттернами:**
- Composite: классическая структура для применения Visitor (обход дерева)
- Interpreter: AST часто обрабатывается через Visitor
- Iterator может использоваться внутри Visitor для обхода элементов

---

## Шпаргалка для собеседования

### Топ-10 самых спрашиваемых паттернов на собеседованиях

По статистике реальных технических собеседований на Java-разработчика:

| # | Паттерн | Частота | Почему спрашивают |
|---|---------|:------:|-------------------|
| 1 | **Singleton** | Очень часто | Самый известный паттерн. Проверяют понимание многопоточности (double-checked locking, volatile, enum) и недостатков |
| 2 | **Factory Method / Abstract Factory** | Очень часто | Проверяют понимание разницы между ними и отличие от DI/IoC |
| 3 | **Builder** | Часто | Спрашивают про fluent interface, иммутабельность, когда нужен Director |
| 4 | **Strategy** | Часто | Часто спрашивают про рефакторинг условной логики: «Как заменить if-else?» |
| 5 | **Observer** | Часто | База для понимания реактивного программирования, EventListener, publish-subscribe |
| 6 | **Decorator** | Часто | Спрашивают про отличие от Proxy и Adapter; пример с `java.io.*` |
| 7 | **Proxy** | Умеренно | Проверяют понимание AOP, lazy-loading (Hibernate), `java.lang.reflect.Proxy` |
| 8 | **Adapter** | Умеренно | Классический пример интеграции legacy-кода |
| 9 | **Template Method** | Умеренно | Спрашивают в контексте Spring (`JdbcTemplate`, `RestTemplate`), отличия от Strategy |
| 10 | **Chain of Responsibility** | Редко | Спрашивают в контексте фильтров сервлетов, middleware |

### Сводная таблица «Когда применять»

| Паттерн | Категория | Ключевой признак для применения |
|---------|-----------|-------------------------------|
| **Singleton** | Порождающий | Нужен ровно один экземпляр класса с глобальным доступом |
| **Factory Method** | Порождающий | Класс не знает заранее, объекты каких конкретных типов создавать |
| **Abstract Factory** | Порождающий | Нужно создавать семейства взаимосвязанных продуктов |
| **Builder** | Порождающий | У объекта много опциональных параметров; нужен fluent interface |
| **Prototype** | Порождающий | Создание объекта «в лоб» дороже клонирования |
| **Adapter** | Структурный | Есть полезный класс, но с несовместимым интерфейсом |
| **Bridge** | Структурный | Два независимых измерения, расширяемых через наследование |
| **Composite** | Структурный | Иерархия «часть-целое»; нужно единообразно обрабатывать листья и группы |
| **Decorator** | Структурный | Нужно динамически добавлять обязанности «поверх» объекта |
| **Facade** | Структурный | Сложная подсистема, нужен простой интерфейс для типовых сценариев |
| **Flyweight** | Структурный | Огромное количество мелких объектов: не хватает памяти |
| **Proxy** | Структурный | Нужен контроль доступа / ленивая инициализация / логирование без изменения RealSubject |
| **Chain of Responsibility** | Поведенческий | Запрос должен пройти цепочку обработчиков; отправитель не знает конечного получателя |
| **Command** | Поведенческий | Нужны undo/redo, очередь задач, отложенное выполнение |
| **Interpreter** | Поведенческий | Нужен простой DSL / язык запросов / вычисление выражений |
| **Iterator** | Поведенческий | Нужно обойти коллекцию, не раскрывая её внутренностей |
| **Mediator** | Поведенческий | Множество объектов хаотично ссылаются друг на друга: нужен «диспетчер» |
| **Memento** | Поведенческий | Нужно сохранять/восстанавливать состояние без нарушения инкапсуляции |
| **Observer** | Поведенческий | Один объект меняется → нужно автоматически оповещать множество других |
| **State** | Поведенческий | Поведение объекта кардинально зависит от состояния (конечный автомат) |
| **Strategy** | Поведенческий | Несколько взаимозаменяемых алгоритмов; нужно выбирать на лету |
| **Template Method** | Поведенческий | Общий алгоритм с фиксированной структурой, но вариативными шагами |
| **Visitor** | Поведенческий | Стабильная иерархия элементов + часто добавляемые новые операции |

### Популярные комбинации паттернов

В реальных проектах паттерны редко встречаются изолированно. Вот классические связки, которые стоит знать:

| Комбинация | Где встречается | Как работает |
|------------|-----------------|--------------|
| **Composite + Visitor** | Компиляторы, редакторы документов | Composite строит дерево (AST), Visitor обходит и выполняет операции над узлами |
| **Factory Method + Template Method** | Фреймворки (Spring, JUnit) | Template Method задаёт скелет алгоритма, Factory Method создаёт нужный продукт на одном из шагов |
| **Facade + Singleton** | Сервисный слой, API-клиенты | Facade предоставляет простой интерфейс, Singleton гарантирует единственный экземпляр фасада |
| **Observer + Mediator** | GUI-приложения (Swing, JavaFX) | Mediator централизует взаимодействие компонентов, Observer оповещает об изменениях |
| **Command + Memento** | Редакторы (undo/redo) | Command инкапсулирует действие, Memento хранит состояние «до» для отката |
| **Proxy + Decorator** | Spring AOP, middleware | Proxy контролирует доступ, Decorator добавляет поведение — вместе образуют цепочку перехватчиков |
| **Strategy + Factory Method** | Платёжные системы, алгоритмы сортировки | Factory Method выбирает и создаёт нужную Strategy по параметру |
| **Observer + Singleton** | EventBus, шина событий | Singleton-шина получает события и рассылает их подписчикам (Observer) |
| **Builder + Composite** | Построители запросов (SQL, GraphQL) | Builder пошагово собирает Composite-дерево |
| **Chain of Responsibility + Command** | Middleware, фильтры сервлетов | Команда передаётся по цепочке; каждый обработчик может выполнить/модифицировать/прервать |

### Типичные ошибки реализации

| Паттерн | Частая ошибка | Как правильно |
|---------|--------------|---------------|
| **Singleton** | Забыть `volatile` в double-checked locking | Всегда `private static volatile T instance` |
| **Singleton** | Сериализация создаёт второй экземпляр | Переопределить `readResolve()` или использовать `enum` |
| **Singleton** | Рефлексия ломает приватный конструктор | Использовать `enum` (защита на уровне JVM) |
| **Builder** | Нет валидации в `build()` | Проверять инварианты в `build()`: бросать `IllegalStateException` при некорректной комбинации |
| **Prototype** | Поверхностное клонирование вместо глубокого | Для mutable-полей клонировать рекурсивно или использовать конструктор копирования |
| **Decorator** | Сломать `equals()`/`hashCode()` цепочки | Не переопределять в декораторах или прокидывать вызовы к wrapped-объекту |
| **Observer** | Забыть отписаться: утечка памяти | Использовать `WeakReference` или явный `unsubscribe()` в `finally`/`try-with-resources` |
| **Observer** | Бесконечный цикл обновлений (A→B→A) | Добавить флаг `updating` или проверку на зацикливание |
| **Observer** | Observer вызывает `setState()` в `update()` | Вынести изменение в отдельный поток или использовать очередь событий |
| **Composite** | Вызвать `add()`/`remove()` у Leaf | Выбрасывать `UnsupportedOperationException` в Leaf (безопасный подход) |
| **State** | Контекст не обновляет ссылку на состояние | Состояние должно вызывать `context.setState(newState)` при переходе |
| **Chain of Resp.** | Никто не обработал запрос, он «упал в тишину» | Добавить последний обработчик по умолчанию (default handler) или логировать необработанные запросы |
| **Mediator** | Превратился в God Object на 5000+ строк | Разбить на несколько посредников по зонам ответственности или внедрить Observer для части взаимодействий |
| **Visitor** | Добавили новый тип элемента — сломались все Visitor'ы | Применять Visitor только к стабильным иерархиям; для динамических — использовать pattern matching (Java 17+) |
| **Flyweight** | Сделать легковес мутабельным | Внутреннее состояние легковеса **всегда иммутабельно**. Иначе изменение затронет всех клиентов |

### Типичные вопросы на собеседовании и краткие ответы

**Q: Чем Factory Method отличается от Abstract Factory?**
> **Factory Method**: один метод, создающий один тип продукта. Подклассы решают, какой именно продукт создать. **Abstract Factory**: интерфейс с набором методов, создающих целое семейство взаимосвязанных продуктов. Abstract Factory часто реализуется через несколько Factory Method. Правило большого пальца: Factory Method для одного продукта, Abstract Factory для семейства продуктов.

**Q: Adapter vs Decorator vs Proxy: в чём разница?**
> - **Adapter** меняет интерфейс (Target ≠ Adaptee). Цель: совместимость.
> - **Decorator** сохраняет интерфейс, но добавляет поведение. Цель: расширение функциональности.
> - **Proxy** сохраняет интерфейс, но контролирует доступ. Цель: управление жизненным циклом/доступом.
>
> Мнемоника: Adapter: «переходник», Decorator: «обёртка с плюшками», Proxy: «швейцар/заместитель».

**Q: Strategy vs State: как различить?**
> Структурно идентичны, разница в **намерении**:
> - **Strategy**: клиент явно выбирает стратегию. Стратегии не знают друг о друге, не переключают контекст. Один активный алгоритм сменяется другим по воле клиента.
> - **State**: контекст сам не выбирает состояние, состояния переключают контекст. Состояния знают друг о друге. Один жизненный цикл с переходами.
>
> Пример: `Collections.sort(list, comparator)`: Strategy. Торговый автомат: State.

**Q: Template Method vs Strategy: что выбрать?**
> - **Template Method**: наследование. Скелет алгоритма в базовом классе. Структура фиксирована на этапе компиляции. Меньше гибкости, но проще.
> - **Strategy**: композиция. Алгоритм делегирован отдельному объекту. Можно менять на лету. Больше гибкости, но больше кода.
>
> Правило: если алгоритм фиксирован и редко меняется → Template Method. Если нужно переключать на лету → Strategy.

**Q: Почему Singleton считают антипаттерном?**
> - Нарушает SRP (класс управляет и своей логикой, и своим созданием)
> - Создаёт глобальное состояние (неявные зависимости, сложности с тестированием)
> - Скрывает зависимости класса (их не видно в конструкторе/методах)
> - Затрудняет тестирование (нельзя замокать/подменить)
>
> Современная альтернатива: **Dependency Injection** (Spring, Guice) + scope `singleton`. Контейнер управляет жизненным циклом, а класс остаётся чистым POJO.

**Q: Какие паттерны используются в Spring Framework?**
> Spring это кладезь паттернов:
> - **Singleton** (по умолчанию scope бинов)
> - **Factory Method** (`@Bean`-методы, `FactoryBean<T>`)
> - **Template Method** (`JdbcTemplate`, `RestTemplate`, `TransactionTemplate`)
> - **Proxy** (AOP, `@Transactional`, `@Cacheable`, `@Async`)
> - **Observer** (`@EventListener`, `ApplicationEventPublisher`)
> - **Strategy** (`AuthenticationProvider`, `ViewResolver`)
> - **Chain of Responsibility** (Security Filter Chain)
> - **Adapter** (`HandlerAdapter`, `MethodArgumentResolver`)
> - **Decorator** (`BeanPostProcessor`: может обернуть бин в декоратор)

### Влияние современной Java (8+) на паттерны

Современные возможности языка **упрощают реализацию**, а иногда и полностью **заменяют** классические паттерны:

| Паттерн | Классический подход | Современная альтернатива (Java 8+) |
|---------|--------------------|-----------------------------------|
| **Command** | Класс на каждую команду | Лямбды: `Runnable`, `Consumer<T>`, `Supplier<T>`, `Function<T,R>` |
| **Strategy** | Интерфейс + набор классов-стратегий | `@FunctionalInterface` + лямбды: `list.sort((a,b) -> a.compareTo(b))` |
| **Observer** | `addListener()` + ручная рассылка | `Flow` API (Java 9+), `CompletableFuture`, Reactive Streams (RxJava, Project Reactor) |
| **Singleton** | Double-checked locking, holder | `enum` (100% защита от рефлексии и сериализации, потокобезопасность из коробки) |
| **Builder** | Ручной Builder-класс | Lombok `@Builder`, Java `record` + кастомные конструкторы |
| **Visitor** | Double dispatch, визитёры | `switch` с pattern matching (Java 17+) для sealed-иерархий: компактнее и безопаснее |
| **Template Method** | Наследование + `final`-метод | Композиция: `Consumer<T>`, `Function<T,R>` как шаги, передаваемые в метод |
| **Iterator** | Ручная реализация `hasNext()`/`next()` | `Stream<T>` + `spliterator()`, внутренние итераторы через `forEach()`, `Stream` API |
| **Chain of Resp.** | Связный список обработчиков | `Stream<T>` из обработчиков + `filter().findFirst()`, `CompletableFuture`-пайплайны |
| **Prototype** | `Cloneable` + `super.clone()` | Конструктор копирования, `record` (автоматические equals/hashCode/toString), `clone()` для record не нужен |

> **Важно:** Современные альтернативы не отменяют ценности понимания классических паттернов. Они помогают писать те же паттерны **компактнее**, но на собеседовании спросят именно классическую реализацию.

### Какие паттерны используются реже

Некоторые паттерны пришли из эпохи C++/Smalltalk и в современной Java-разработке применяются ограниченно:

| Паттерн | Почему редко используется |
|---------|--------------------------|
| **Interpreter** | Для реальных DSL используют ANTLR, парсер-генераторы. Ручной AST — только для простейших выражений. |
| **Flyweight** | Аппаратные ограничения 90-х ушли. Применяется осознанно: текстовые редакторы, игры, биржевые системы с миллионами объектов. |
| **Memento** | В чистом виде — редко. Чаще используют CQRS + Event Sourcing или просто иммутабельные DTO/record. |
| **Prototype** | `Cloneable` признан неудачным решением. Вместо клонирования — конструкторы копирования, record, MapStruct, BeanUtils. |
| **Mediator** | В микросервисах заменён брокерами сообщений (Kafka, RabbitMQ). В монолитах — оркестраторами или Observer. |

Это **не значит, что их не нужно знать**. На собеседовании могут спросить любой. Но фокус усилий лучше направить на топ-10 (Singleton, Factory Method, Abstract Factory, Builder, Strategy, Observer, Decorator, Proxy, Adapter, Template Method).

### Золотые правила работы с паттернами

> 1. **Не паттерн ради паттерна.** Сначала найдите проблему, потом подбирайте паттерн, а не наоборот.
> 2. **KISS (Keep It Simple, Stupid).** Если задачу можно решить без паттерна: решите без паттерна.
> 3. **Паттерны это словарь, а не библиотека.** Они помогают обсуждать архитектуру с коллегами («здесь нужен Strategy», «это классический Observer»), а не копировать шаблонный код.
> 4. **Не все 23 паттерна нужно знать наизусть.** Достаточно хорошо понимать 8-10 самых частых (см. таблицу выше) и иметь общее представление об остальных.
> 5. **Паттерны комбинируются.** Реальные системы редко используют паттерны изолированно. Например, Composite + Visitor, Factory Method + Template Method, Facade + Singleton.