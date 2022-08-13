:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Encapsulation; in Golang
   :name: emacsway-golang-domain-file-structure

==================================
Файловая структура Доменной модели
==================================

.. sectionauthor:: Ivan Zakrevsky

О причинах образования такой файловой структуры.

.. contents:: Содержание


Зачем в каждом Bounded Context директория internal?
===================================================

Доменная модель должна быть инкапсулирована.
Другим Bounded Contexts должны быть доступны только CQRS-Commands и Public Domain Events (Integration Events).


Почему агрегаты резмещены в собственных директориях?
====================================================

Причины две:

1. Чтобы подчеркнуть High Cohesion, см. главу "Chapter Five. A Model Expressed in Software :: Modules" книги "Domain-Driven Design: Tackling Complexity in the Heart of Software" by Eric Evans.
2. В Golang это необходимо для реализации :ref:`инкапсуляции Агрегата <emacsway-golang-encapsulation>`, чтобы ограничить доступ к защищенным атрибутам Агрегата извне.

..

    💬 "МОДУЛИ дают возможность посмотреть на модель с разных сторон:
    во-первых, можно изучить подроб­ности устройства модуля, не вникая в сложное целое;
    во-вторых, удобно рассматривать взаимоотношения между модулями, не вдаваясь в детали их внутреннего устройства.

    <...>

    То, что при делении на модули должна соблюдаться низкая внешняя зависимость (low coupling) при высокой внутренней связности (high cohesion)- это общие слова.
    Определения зависимости и связности грешат уклоном в чисто технические, количест­венные критерии, по которым их якобы можно измерить, подсчитав количество ассо­циаций и взаимодействий.
    Но это не просто механические характеристики подразде­ления кода на модули, а идейные концепции.
    Человек не может одновременно удер­живать в уме слишком много предметов (отсюда низкая внешняя зависимость).
    А плохо связанные между собой фрагменты информации так же трудно понять, как неструктурированную "кашу" из идей (отсюда высокая внутренняя связность).

    MODULES give people two views of the model:
    They can look at detail within a MODULE without being overwhelmed by the whole, or they can look at relationships between MODULES in views that exclude interior detail.

    <...>

    It is a truism that there should be low coupling between MODULES and high cohesion within them.
    Explanations of coupling and cohesion tend to make them sound like technical metrics, to be judged mechanically based on the distributions of associations and interactions. Yet it isn't just code being divided into MODULES, but concepts.
    There is a limit to how many things a person can think about at once (hence low coupling).
    Incoherent fragments of ideas are as hard to understand as an undifferentiated soup of ideas (hence high cohesion)."

    -- "Domain-Driven Design: Tackling Complexity in the Heart of Software" by Eric Evans, перевод В.Л. Бродового


Почему Сущности Агрегатов выделены в отдельные директории?
==========================================================

Чтобы логически выделить связанные этой Сущностью объекты.
Не очень удобно рассматривать винегрет вложенных объектов различных Сущностей, поскольку они нерелевантны в момент рассмотрения и повышают когнитивную нагрузку.

Впрочем, это решение является пока что экспериментальным и не окончательным.

Есть у этого решения контраргумент, который заключается в том, что Сущность, хотя и кратковременно, но может отдаваться наружу Агрегата, если при этом она остается неизменяемой.

    💬️ "Группируйте СУЩНОСТИ и ОБЪЕКТЫ-ЗНАЧЕНИЯ в АГРЕГАТЫ и определяйте границы каждого из них.
    Выберите о дин объект-СУЩНОСТЬ и сделайте его корневым.
    Осуществляйте все обращения к объектам в границах АГРЕГАТА только через его корневой объект.
    Разрешайте внешним объектам хранить ссылки только на корневой объект.
    **Ссылки на внутренние объекты АГРЕГАТА следует передавать только во временное пользование, на время одной операции.**
    **Поскольку доступ к объектам АГРЕГАТА кон­тролируется через корневой объект, неожиданные изменения внутренних объектов невозможны.**
    В такой схеме разумно требовать удовлетворения всех инвариантов для объектов в АГРЕГАТЕ и для всего АГРЕГАТА в целом при любом изменении состояния.

    Cluster the ENTITIES and VALUE OBJECTS into AGGREGATES and define boundaries around each.
    Choose one ENTITY to be the root of each AGGREGATE, and control all access to the objects inside the boundary through the root.
    Allow external objects to hold references to the root only.
    **Transient references to internal members can be passed out for use within a single operation only.**
    **Because the root controls access, it cannot be blindsided by changes to the internals.**
    This arrangement makes it practical to enforce all invariants for objects in the AGGREGATE and for the AGGREGATE as a whole in any state change."

    -- "Domain-Driven Design: Tackling Complexity in the Heart of Software" by Eric Evans, перевод В.Л. Бродового

О чем это говорит?
Это говорит о том, что если мы разместим Сущность в одном пакете с Агрегатом, то это значит, что Агрегату не требуются публичные методы для того, чтобы иметь доступ к своей Сущности.
Это значит, что Агрегат обладает другим уровнем доступа, нежели посторонние клиенты.
Это значит, что посторонние клиенты не получат доступа к мутирующим методам Сущности только потому, что они нужны Агрегату.

Но здесь возникает другой вопрос - следовать ли `Law of Demeter <https://ru.wikipedia.org/wiki/%D0%97%D0%B0%D0%BA%D0%BE%D0%BD_%D0%94%D0%B5%D0%BC%D0%B5%D1%82%D1%80%D1%8B>`__ внутри Агрегата?
Следует ли ограничивать прямой доступ Агрегата к Сущностям его Сущностей?
Плоская структура файлов Агрегата не позволяет это обеспечить.


Почему в директории Агрегата нет директории для его Объектов-значений?
======================================================================

Причина, по которой эта директория была вначале, заключалась в необходимости реализации ациклического графа зависимостей с целью исключения циклических импортов.
Это было связано с тем, что Сущности Агрегата имели собственную директорию.
Например, Агрегат может быть осведомлен о своей Сущности, а Сущность может быть осведомлена об Объекте-значении Агрегата.

По этой причине, все Объекты-значения Агрегата/Сущности были выделены в отдельную директорию внутри директории Агрегата/Сущности.
Иначе пришлось бы абсолютно все Cущности и Объекты-значения Агрегата разметить плоским списком в одной директории, что затрудняло навигацию по файловой структуре.

Позже я обнаружил еще один способ решения проблемы циклического импорта - для этого было достаточно, чтобы Агрегат заимствовавал Объект-значение у Сущности, а не наоборот.
В крайнем случае, внутри директории Агрегата можно делать директорию ``shared``, ``common``, или ``aggregate_name``, для реализации ациклического графа зависимостей.
Этот вариант также может оказаться востребованным, если Доменные События расположены в поддиректории, например, ``events``, и используют Объекты-значения Агрегатов.
В таком случае, директория для совместно используемых Объектов-значений может иметь название (в дополнение к уже перечисленным) ``exportable``, ``public``.
Ну а чтобы не появлялись в импортах ``public2``, ``public3``, ``public4``..., можно использовать импорт с точкой в пакет их агрегата, и уже оттуда импортировать в клиентский пакет.

    All Value Objects which are part of a Customer live in another subpackage named value. I have to do this because in Go circular dependencies are not allowed. If I would put the Value Objects into the customer package then Commands and Events in domain would import the Value Objects from customer and functions in customer would import Commands and Events from domain. Having them in a subpackage additionally gives more privacy for the Value Objects. Not even functions of the Customer Aggregate can access private parts or create/modify a value without using the proper methods.

    -- "`Implementing Domain-Driven Design and Hexagonal Architecture with Go (2) <https://medium.com/@TonyBologni/implementing-domain-driven-design-and-hexagonal-architecture-with-go-2-efd432505554>`__" by Anton Stöckl -- Part 2 -- How I implement tactical DDD patterns -- the Domain layer.


Еще одним способом предотвращения циклических импортов является использование интерфейсов, размещенных в отдельном пакете либо продублированных у своих клиентов.
Интерфейс дает то, что требуется сигнатурой методов клиента, не тащит за собой кучу зависимостей, необходимых для реализации, и даже может быть объявлен локально у своего клиента.


Почему Доменные События размещены в директории Агрегата и его Сущностей?
========================================================================

Альтернативным вариантом является размещение Доменных Событий `отдельно от Агрегатов <https://github.com/dotnet-architecture/eShopOnContainers/tree/ce50bb8a2f1fa30e419d9a6863d19eb9999e9ef8/src/Services/Ordering/Ordering.Domain/Events>`__.

Но удобней информация воспринимается тогда, когда следствие расположено ближе к своей причине.

При этом, поскольку Доменные События выражают взаимоотношения между Агрегатами, удобно иметь возможность рассматривать их `не вдаваясь <https://github.com/VaughnVernon/IDDD_Samples_NET/blob/master/iddd_agilepm/Domain.Model/Products/ProductDiscussionInitiated.cs>`__ в детали внутреннего устройства Агрегатов.

Точно так же Интеграционные (Публичные Доменные) События, выражающие взаимоотношения между Ограниченными Контекстами, расположены в единой директории порождающего их Ограниченного Контекста.
