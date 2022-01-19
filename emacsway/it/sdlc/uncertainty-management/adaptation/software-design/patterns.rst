:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Patterns; in Agile
   :name: emacsway-agile-patterns


================================
Role of Design Patterns in Agile
================================

.. sectionauthor:: Ivan Zakrevsky

.. contents:: Содержание

Немного о Паттернах Проектирования.
Нужны ли они?

Паттерны могут приносить пользу экономике разработки, а могут приносить и вред, если не понимать их назначения и злоупотреблять ими.
Как говорится, молотком можно гвоздь забить, а можно и пальцы отбить.

Любое проектное решение должно исходить из :ref:`принципов управления сложностью <emacsway-primary-technical-imperative>`.
Добавление паттерна может увеличивать уровень косвенности системы, что тоже имеет свою стоимость.

Посмотрим, к примеру, мотивацию Mediator pattern:

    📝 "Mediator promotes loose **coupling** by keeping objects from referring to each other explicitly,
    and it lets you vary their interaction independently."

    -- "Design Patterns: Elements of Reusable Object-Oriented Software" by Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides

Лекарство не должно быть хуже болезни.
Внося сложность в систему, мы должны обретать возможность управлять еще большим уровнем сложности, т.е. решение должно быть оправданным.

По этому поводу хорошо :ref:`рассуждал Kent Beck <emacsway-kent-beck-constantine's-law>`.

И по этому поводу хорошо :ref:`говорил Martin Fowler о 16 Паттернах в 32 строках кода <emacsway-martin-fowler-16-patterns-in-32-lines>`.

Вопрос применения паттернов - это вопрос баланса между уровнем управляемой им сложности и уровнем привносимой им сложности.
При дисбалансе бизнес и технических интересов, злоупотребление паттернами может привести к экономически неоправданному переусложению системы: https://t.me/emacsway_log/124

Тем не менее, Паттерны Проектирования являются :ref:`обобщением и систематизацией практики <emacsway-knowledge-vs-opinion-in-psychology>`.
Их не выдумывают - их обобщают.
Это значит, что незнание конкретного паттерна еще не означает неосознанного его применения.


Составляющие экономического эффекта применения паттернов
========================================================

Паттерны способны значительно улучшить экономику разработки при разумном их применении.
Экономическая их эффективность складывается из двух составляющих:

1. Индивидуальная
2. Коллективная

Рассмотрим каждый из них по отдельности.


Индивидуальная составляющая
---------------------------

Начнем с первой, индивидуальной составляющей.
Каким образом применение паттернов может повысить персональную эффективность разработчика? Вот что говорит по этому поводу автор книг "Implementation Patterns" и "Smalltalk Best Practice Patterns" Kent Beck:

    📝 "Я обратил внимание на один важный эффект, который, я надеюсь, смогут принять во внимание и другие.
    Если на основе постоянно повторяющихся действий формулируются правила, дальнейшее применение этих правил становится неосознанным и автоматическим.
    Естественно, ведь это проще, чем обдумывать все за и все против того или иного действия с самого начала.
    Благодаря этому повышается скорость работы, и если в дальнейшем вы сталкиваетесь с исключением или проблемой, которая не вписывается ни в какие правила, у вас появляется дополнительное время и энергия для того, чтобы в полной мере применить свои творческие способности.

    Именно это произошло со мной, когда я писал книгу Smalltalk Best Practice Patterns (Лучшие паттерны Smalltalk).
    В какой-то момент я решил просто следовать правилам, описываемым в моей книге.
    В начале это несколько замедлило скорость моей работы, — мне требовалось дополнительное время, чтобы вспомнить то или иное правило, или написать новое правило.
    Однако по прошествии недели я заметил, что с моих пальцев почти мгновенно слетает код, над разработкой которого ранее мне приходилось некоторое время размышлять.
    Благодаря этому у меня появилось дополнительное время для анализа и важных размышлений о дизайне.

    Существует еще одна связь между TDD и паттернами: TDD является методом реализации дизайна, основанного на паттернах.
    Предположим, что в определенном месте разрабатываемой системы мы хотим реализовать паттерн Strategy (Стратегия).
    Мы пишем тест для первого варианта и реализуем его, создав метод.
    После этого мы намеренно пишем тест для второго варианта, ожидая, что на стадии рефакторинга мы придем к паттерну Strategy (Стратегия).
    Мы с Робертом Мартином (Robert Martin) занимались исследованием подобного стиля TDD.
    Проблема состоит в том, что дизайн продолжает вас удивлять.
    Идеи, которые на первый взгляд кажутся вам вполне уместными, позже оказываются неправильными.
    Поэтому я не рекомендую целиком и полностью доверять своим предчувствиям относительно паттернов.
    Лучше думайте о том, что, по-вашему, должна делать система, позвольте дизайну оформиться так, как это необходимо.

    The effect that I have noticed, and which I hope others find, is that by reducing repeatable behavior to rules, applying the rules becomes rote and mechanical.
    This is quicker than redebating everything from first principles all the time.
    When along comes an exception, or a problem that just doesn't fit any of the rules, you have more time and energy to generate and apply creativity.

    This happened to me when writing the Smalltalk Best Practice Patterns.
    At some point I decided just to follow the rules I was writing.
    It was much slower at first, to be looking up the rules, or to be stopping to write a new rule.
    After a week, however, I discovered that code was ripping off my fingertips that would have required a pause for thought before.
    This gave me more time and attention for bigger thoughts about design and analysis.
    Another relationship between TDD and patterns is TDD as an implementation method for pattern-driven design.
    Say we decide we want a Strategy for something.
    We write a test for the first variant and implement it as a method.
    Then we consciously write a test for the second variant, expecting the refactoring phase to drive us to a Strategy.
    Robert Martin and I did some research into this style of TDD.
    The problem is that the design keeps surprising you.
    Perfectly sensible design ideas turn out to be wrong.
    Better just to think about what you want the system to do, and let the design sort itself out later."

    -- "Test-Driven Development By Example" by Kent Beck, перевод П. Анджан


Коллективная составляющая
-------------------------

Перейдем ко второй, коллективной составляющей.
Каким именно образом паттерны могут повысить экономическую эффективность разработки?

Когда в печать вышла книга "Patterns of Enterprise Application Architecture" (PoEAA) by Martin Fowler, David Rice, Matthew Foemmel, Edward Hieatt, Robert Mee, Randy Stafford, то David Heinemeier Hansson прочитал ее одним из первых, и реализовал эти паттерны в виде Ruby On Rails (RoR).
Использование этого фреймворка, и реализованных им паттернов, позволило:

- снизить негативный эффект ":ref:`Закона Брукса <emacsway-brooks's-law>`"
- уменьшить порог вхождения новых разработчиков в проект
- переместить фокус внимания разработчиков от Domain-independent knowledge к `Domain knowledge <https://en.wikipedia.org/wiki/Domain_knowledge>`__

В итоге, разработка на RoR дала многократный (на то время) прирост темпов разработки, что вызвало вирусный интерес к PoEAA и массовое клонирование RoR на многие языки программирования.

Иными словами, паттерны осуществляют унификацию решений типовых проблем, что способствует удешевлению достижения коллективного понимания устройства системы, путем минимизации затрат времени на синхронизацию и обобщение мнений.

По мере формирования коллективной знаний в области системной архитектуры, стали обнажаться архитектурные недостатки RoR, и по этому поводу даже были сняты два поучительных и заслуживающих внимания сериала:

1. "`Is TDD Dead? <https://martinfowler.com/articles/is-tdd-dead/>`__"
2. "`A Conversation with Badri Janakiraman about Hexagonal Rails <https://martinfowler.com/articles/badri-hexagonal/>`__"

Однако, сам факт достижения высокой экономической эффективности от использования паттернов PoEAA был очевиден, и этот факт оказал существенное влияние на формирование современного состояния области знаний системной архитектуры.

    📝 "In most successful software projects, the expert developers working on that project have a shared understanding of the system design.
    **This shared understanding is called 'architecture.'**
    This understanding includes how the system is divided into components and how the components interact through interfaces.
    These components are usually composed of smaller components, but the architecture only includes the components and interfaces that are understood by all the developers."

    -- `Ralph Johnson <https://martinfowler.com/ieeeSoftware/whoNeedsArchitect.pdf>`__


