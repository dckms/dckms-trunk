:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Encapsulation; in Golang
   :name: emacsway-golang-encapsulation

====================================================
Как сохранить Агрегат в БД не разрушая инкапсуляции?
====================================================

.. sectionauthor:: Ivan Zakrevsky

Инварианты лишены смысла своего существования в условиях дырявой, как решето, инкапсуляции.
Вопрос в том, как сохранить инкапсуляцию Агрегатов в Golang, когда нам требуется его внутреннее состояние для формирования SQL-запроса, или, наоборот, требуется установить состояние Агрегата в результате выполнения SQL-запроса.

.. contents:: Содержание


Memento pattern
===============

Memento оказался близко, но не по назначению. Суть Memento в том, что он не должен раскрывать свое состояние никому, кроме своего создателя:

    1. Preserving encapsulation boundaries. Memento avoids exposing information that only an originator should manage but that must be stored nevertheless outside the originator.
       The pattern shields other objects from potentially complex Originator internals, thereby preserving encapsulation boundaries.

    -- "Design Patterns: Elements of Reusable Object-Oriented Software" by Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides


Walker
======

Walker представляет собою модификацию паттерна Visitor с целью сохранить инкапсуляцию Агрегатов. К числу недостатков паттерна паттерна Visitor относится:

    6. Breaking encapsulation. Visitor's approach assumes that the ConcreteElement interface is powerful enough to let visitors do their job.
    As a result, the pattern often forces you to provide public operations that access an element's internal state, which may compromise its encapsulation.

    -- "Design Patterns: Elements of Reusable Object-Oriented Software" by Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides

Что будет создавать Walker в случае обхода иерархической структуры Агрегата с несколькими вложенными Сущностями?
Вероятно, это будет будет несколько SQL-запросов с параметрами, т.е. некий композитный объект, выраженный некой структурой данных.
Это лишает смысла использование Visitor, если можно сразу возвратить структуру данных, причем, абстрагированную от SQL.

Технически, можно сделать так:

.. code-block:: go

    type Walkable interface {
        Accept(Walker)
    }

    type Walker interface {
        SetField(string)
        WalkWalkable(Walkable)
        WalkUint8(uint8)
        WalkUint64(uint64)
        WalkUint(uint)
        WalkTime(time.Time)
    }


.. code-block:: go

    func (e Endorsement) Accept(walker interfaces.Walker) {
        walker.SetField("recognizerId")
        walker.WalkWalkable(e.recognizerId)
        walker.SetField("recognizerGrade")
        walker.WalkWalkable(e.recognizerGrade)
        // ...
    }

.. code-block:: go

    func (id RecognizerId) Accept(walker interfaces.Walker) {
        walker.WalkUint64(id.Value())
    }


Проблема в том, что на этапе создания SQL-запроса нам пока еще могут быть неизвестны первичные ключи Агрегатов, чтобы их можно было бы проставить в SQL-запросы их Сущностей.

Кроме того, осведомленность о способах образования SQL-запросов размазывается между Walkers и Repositories, что вызывает "Разлет Дроби" (Code Smell) в случае изменения существующего способа построения SQL (например, в случае изменения диалекта БД или в случае внедрения какого-либо QueryBuilder).
Walker начинает быть слишком осведомленным о деталях реализации Repository.

В целях достижения DRY возникает целесообразность возложить на Walker генерирование только части SQL, и освободить его от осведомленности знания таблиц в БД, что будет разрывать обязанность за построение SQL на несколько объектов и подрывать Cohesion.


Valuer & Scanner
================

- `Valuer <https://pkg.go.dev/database/sql/driver#Valuer>`__
- `Scanner <https://pkg.go.dev/database/sql#Scanner>`__

Интерфейс Scanner открывает дверь к изменяемости ValueObject, что противоречит основной его сути.
А так же открывает брешь в инкапсуляции Агрегата.

Но есть еще один момент - метод ``Scan(src any) error`` вызывается у конкретного типа, что препятствует использованию паттерна, известного как `Special Case <https://martinfowler.com/eaaCatalog/specialCase.html>`__ или `Null Object <https://refactoring.com/catalog/introduceSpecialCase.html>`__.
Кроме того, в некоторых случаях может потребоваться преобразовать неизменяемые исторические данные для новой версии модели.
Вопрос затрагивался в разделе "4. Validating historical data" статьи "`Always-Valid Domain Model <https://enterprisecraftsmanship.com/posts/always-valid-domain-model/>`__" by Vladimir Khorikov и в разделе "6. The use of ORMs within and outside of the always-valid boundary" статьи "`Database and Always-Valid Domain Model <https://enterprisecraftsmanship.com/posts/database-always-valid-domain-model/>`__" by Vladimir Khorikov.

С другой стороны, Valuer может возвращать только примитивные типы, а значит, он не пригоден для экспорта иерархической структуры состояния Агрегата:


    It is either nil, a type handled by a database driver's NamedValueChecker interface, or an instance of one of these types:

    - int64
    - float64
    - bool
    - []byte
    - string
    - time.Time

    -- `Источник <https://pkg.go.dev/database/sql/driver#Value>`__


Reflection
==========

В документации `отсутствуют <https://pkg.go.dev/reflect#Value.FieldByName>`__ какие-либо упоминания об ограничении доступа к защищенным атрибутам структуры данных посредством рефлекции.

Может быть через рефлексию и заработало бы - я не пробовал.
Но использовать рефлексию в production для таких целей как-то не сильно хочется, в т.ч. и по соображениям производительности.
К тому же этот метод является, по сути, еще одним способом пробить брешь в инкапсуляции.


Exporter
========

Ссылки по теме:

- "`More on getters and setters <https://www.infoworld.com/article/2072302/more-on-getters-and-setters.html>`__" by Allen Holub
- "`Save and load objects without breaking encapsulation <https://stackoverflow.com/questions/24921227/save-and-load-objects-without-breaking-encapsulation>`__" at Stackoverflow

Идею можно посмотреть на примере:

.. code-block:: java
   :caption: `Example by Allen Holub <https://www.infoworld.com/article/2072302/more-on-getters-and-setters.html>`__
   :name: emacsway-code-exporter-example-1

    import java.util.Locale;

    public class Employee
    {   private Name        name;
        private EmployeeId  id;
        private Money       salary;

        public interface Exporter
        {   void addName    ( String name   );
            void addID      ( String id     );
            void addSalary  ( String salary );
        }

        public interface Importer
        {   String provideName();
            String provideID();
            String provideSalary();
            void   open();
            void   close();
        }

        public Employee( Importer builder )
        {   builder.open();
            this.name   = new Name      ( builder.provideName()     );
            this.id     = new EmployeeId( builder.provideID()       );
            this.salary = new Money     ( builder.provideSalary(),
                                          new Locale("en", "US")    );
            builder.close();
        }

        public void export( Exporter builder )
        {   builder.addName  ( name.toString()   );
            builder.addID    ( id.toString()     );
            builder.addSalary( salary.toString() );
        }

        //...
    }

Или на более лаконичном примере:

.. code-block:: java
   :caption: `Example from Stackoverflow <https://stackoverflow.com/questions/24921227/save-and-load-objects-without-breaking-encapsulation>`__
   :name: emacsway-code-exporter-example-2

    interface PersonImporter {

        public int getAge();

        public String getId();
    }

    interface PersonExporter {

        public void setDetails(String id, int age);

    }

    class Person {

        private int age;
        private String id;

        public Person(PersonImporter importer) {
            age = importer.getAge();
            id = importer.getId();
        }

        public void export(PersonExporter exporter) {
            exporter.setDetails(id, age);
        }

    }

Замечательный вариант, но проблема в том, что он использует интерефейсы, и это получается слишком многословно - требуется декларировать сам тип (структуру), интерфейс, сеттеры.
Вряд ли кто-то будет этим заниматься, когда можно просто обязать Агрегат вернуть простую структуру.

:ref:`Второй <emacsway-code-exporter-example-2>` из приведенных примеров содержит пакетированный сеттер, что делает его несколько менее многословным.
Пример реализации:

.. literalinclude:: _media/aggregate-encapsulation/exporter_1.go
   :language: go

Внутренние объекты структуры  должны иметь сеттеры.
Реализовать эти объекты можно по разному - как структуру или как примитивный тип.
Но в первом случае у нас даже плоская Сущность будет экспортировать двухуровневую структуру, что вносит неудобство, но при этом структура позволяет использовать параметрический полиморфизм (generics) для повышения ее реиспользования.
А во втором случае, хотя объект Exporter и будет "наследоваться" от примитивного типа, но будет требовать преобразование типов в определенных случаях, что также вносит определенное неудобство.

Немного смущает смешивание парадигм FP и OOP для ValueObject.
Хотя ValueObject и остается неизменяемым, но сам факт того, что функционально чистый объект вызывает мутирующие методы другого объекта, вызывает состояние легкого смущения.
Возникает вопрос - почему функционально чистый объект не может просто взять и вернуть другой функционально чистый объект?
Если бы Golang поддерживать Generics для методов, тогда могло бы получиться что-то похожее на ``Recognizer.Export[T](exporterFactory function(attr1, attr2, attr3) T) T``.

Наличие сеттеров в интерфейсе Exporter означает наличие мутирующего метода, который должен принимать экземпляр своего типа по указателю.
Это значит, что и сам экземпляр должен передаваться по указателю, иначе появится ошибка "Type does not implement interface (SetState method has pointer receiver)", см. статью "`Method Pointer Receivers in Interfaces <https://sentry.io/answers/interface-pointer-receiver/>`__" by Evan Hicks.
В Golang это значит, что `в некоторых случаях <https://stackoverflow.com/questions/50830676/set-an-int-pointer-to-an-int-value-in-go>`__ потребуется сперва проинициализировать переменную, и только потом создать указатель на ее адрес.
В качестве меры спасения можно использовать функции-конструкоры, возвращающие указатель, иначе формирование в подобном стиле иерархической структуры с вложенными коллекциями структур превращается в довольно ресурсосжигающую задачу.

    💬️ "Цель архитектуры программного обеспечения — уменьшить человеческие трудозатраты на создание и сопровождение системы.

    The goal of software architecture is to minimize the human resources required to build and maintain the required system."

    -- "Clean Architecture: A Craftsman's Guide to Software Structure and Design" by Robert C. Martin, перевод ООО Издательство "Питер"

Использование такого подхода в тестовых кейсах делает их несколько более многословными.

Можно было бы сказать, что тестировать нужно по принципам :ref:`черного ящика <emacsway-tdd-black-box>`, т.е. только внешнее поведение.
Совершенно верно, но только нам требуется не только внешнее поведение, но и достоверность сохранения введенной в конструктор Агрегата информации в БД.

    💬️ "Давно известно, что простота тестирования является характерным признаком хорошей архитектуры.
    Шаблон «Скромный объект» — хороший пример, потому что раздел между легко и тяжело тестируемыми частями часто совпадает с архитектурными границами.
    Раздел между Презентаторами и Представлениями -- одна из таких границ, но существует много других.

    It has long been known that testability is an attribute of good architectures.
    The Humble Object pattern is a good example, because the separation of the behaviors into testable and non-testable parts often defines an architectural boundary.
    The Presenter/View boundary is one of these boundaries, but there are many others."

    -- "Clean Architecture: A Craftsman's Guide to Software Structure and Design" by Robert C. Martin, перевод ООО Издательство "Питер"

Возникает целесообразность облегчить метод экспортирования, придав ему сигнатуру ``Recognizer.Export() RecognizerState`` вместо ``Recognizer.ExportTo(ex RecognizerExporter)``.
Получится что-то типа DTO с тем лишь отличием, что он пересекает не сетевые границы, а границы инкапсуляции Агрегата.
В Golang этот вариант выглядит чуть более привлекательным, хотя и менее OOP, но зато не контрастирует с FP принципами Value Object.

О таком же принципе этом писал Robert C. Martin:

    💬️ "Презентаторы являются разновидностью шаблона проектирования «Скромный объект» (Humble Object), помогающего выявлять и защищать архитектурные границы.

    Presenters are a form of the Humble Object pattern, which helps us identify and protect architectural boundaries."

    💬️ "Обычно через границы данные передаются в виде простых структур.
    При желании можно использовать простейшие структуры или объекты передачи данных (Data Transfer Objects; DTO).
    Данные можно также передавать в вызовы функций через аргументы.
    Или упаковывать их в ассоциативные массивы или объекты.
    Важно, чтобы через границы передавались простые, изолированные структуры данных.
    Не нужно хитрить и передавать объекты сущностей или записи из базы данных.
    Структуры данных не должны нарушать правило зависимостей.

    Например, многие фреймворки для работы с базами данных возвращают ответы на запросы в удобном формате.
    Их можно назвать «представлением записей».
    Такие представления записей не должны передаваться через границы внутрь.
    Это нарушает правило зависимостей, потому что заставляет внутренний круг знать что-то о внешнем круге.
    Итак, при передаче через границу данные всегда должны принимать форму, наиболее удобную для внутреннего круга.

    Typically the data that crosses the boundaries consists of **simple data structures**.
    You can use **basic structs or simple data transfer objects** if you like.
    Or the data can simply be arguments in function calls.
    Or you can pack it into a hashmap, or construct it into an object.
    The important thing is that isolated, **simple data structures** are passed across the boundaries.
    We don't want to cheat and pass Entity objects or database rows.
    We don't want the data structures to have any kind of dependency that violates the Dependency Rule.

    For example, many database frameworks return a convenient data format in response to a query.
    We might call this a "row structure."
    We don't want to pass that row structure inward across a boundary.
    Doing so would violate the Dependency Rule because it would force an inner circle to know something about an outer circle.

    Thus, when we pass data across a boundary, it is always in the form that is most convenient for the inner circle."

    💬️ "Он также переносит данные из базы данных Database в память сущностей Entities через интерфейс DataAccessInterface.
    По завершении UseCaseInteractor забирает данные из сущностей Entities и конструирует из них другой простой Java-объект OutputData.
    Затем объект OutputData передается через интерфейс OutputBoundary презентатору Presenter.

    It also uses the DataAccessInterface to bring the data used by those Entities into memory from the Database.
    Upon completion, the UseCaseInteractor gathers data from the Entities and constructs the OutputData as another **plain old Java object**.
    The OutputData is then passed through the OutputBoundary interface to the Presenter."

    -- "Clean Architecture: A Craftsman's Guide to Software Structure and Design" by Robert C. Martin, перевод ООО Издательство "Питер"

.. literalinclude:: _media/aggregate-encapsulation/exporter_2.go
   :language: go

Недостатком такого решения, который я успел обнаружить, является то, что клиент не имеет возможности определить структуру экспортируемого объекта, в отличии от варианта с интерфейсом.
Это затрудняет создание обобщенных классов, например, `обобщенного композитного первичного ключа <https://martinfowler.com/eaaCatalog/identityField.html>`__.
В результате плодятся промежуточные структуры, которые затем нужно преобразовывать к нужному виду.

В проекте реализованы оба варианта для наглядности, на примере Агрегатов Recognizer и Endorsed.
Но код первого варианта выглядит несколько устрашающе, и трудоемкость его поддержания неоправданно завышена.
Поэтому, в других Агрегатах применяется только второй вариант.

