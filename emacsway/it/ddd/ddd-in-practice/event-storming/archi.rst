:canonical-base-url: https://dckms.github.io/system-architecture


.. index::
   single: ArchiMate; in Event Storming
   single: Archi; in Event Storming
   single: Event Storming; with Archi
   single: Event Storming; with ArchiMate
   :name: emacsway-event-storming-archi

=========================
Event Storming with Archi
=========================

.. sectionauthor:: Ivan Zakrevsky

.. contents:: Содержание


Обзор инструментов
==================

`PlantUML <https://github.com/tmorin/plantuml-libs/blob/master/distribution/eventstorming/README.md>`__ достаточно быстро исчерпал свои возможности и диаграммы стали нечитаемыми и неуправляемым.
Попытки выровнять диаграмму штатными средствами оказались безуспешниыми.
На разных серверах диаграмма отображалась по-разному.

Сервис Miro вынуждает архитектурно-значимую информацию покидать периметр безопасности, образует лицензионную зависимость и находится под давлением геополитических факторов.
Как и PlantUML, не позволяет находить границы микросервисов ввиду `отсутствия в нем модели <https://c4model.com/#Modelling>`__.

Неплохие надежды подает `domorobo.to <https://domorobo.to/>`__, но он пока еще сыроват.


Archi
=====

В процессе поиска внимание привлекла внимание диаграмма на "Figure 13: Event Storming Model" of "Agile Architecture Modeling Using the ArchiMate® Language" (см. `здесь <https://publications.opengroup.org/g20e>`__, `здесь <https://nicea.nic.in/sites/default/files/Agile_Architecture_Modelling_Using_Archimate.pdf>`__ или `здесь <https://nicea.nic.in/download-files.php?nid=247>`__).

`Model used by Jean-Baptiste Sarrodie for presentation "Enterprise Architecture Modelling with ArchiMate in an Agile at Scale Programme" <https://community.opengroup.org/archimate-user-community/home/-/issues/8>`__

Попробовал сделать Event Storming в Archi, и обнаружил, что он делается с такой же легкостью, как и в Miro.
Разве что для публикации своих изменений другим участникам нужно сделать 5 кликов мышкой.
Технически, это можно автоматизировать по регулярному расписанию, используя `jArchi <https://www.archimatetool.com/plugins/>`__.
А вот изменения других участников уже и так подтягиваются по настраиваемому регулярному расписанию фоновым процессом.

Нотации (т.е. цвета) Event Storming практически идентичны нотациям "`C.1.10 Business Process Cooperation Viewpoint <https://pubs.opengroup.org/architecture/archimate31-doc/apdxc.html#_Toc10045506>`__".


Достоинства Archi для Event Storming
====================================

#. On-Premise. Архитектурно-значимая информация не покидает закрытый периметр безопасности.
#. Open Source under MIT License
#. Наличие модели позволяет:

   #. Определять границы не только Ограниченных Контекстов, но и Микросервисов. Это является следствием наличия модели и возможности классифицировать связи, выделять из них связи, образующие Сoupling & Сohesion, и с математической точностью определять наилучшую форму границ микросервисов.
   #. Рассматривать любой элемент диаграммы в различных представлениях, например, мгновенно перейти с Context Map на Event Storming. См. вкладку "Properties" выбранного элемента, секция "Analisis".
   #. Отслеживать трассировку как до выбранного элемента, так и после него. См. окно Window-Navigator и две кнопки: "Show target relations" и "Show source relations".
   #. При разбиении большой диаграммы на части по некому признаку (например, по базовым сценариям использования), изменение в одной диаграмме (например, изменение целевого элемента связи) будет автоматически отражено на всех остальных диаграммах, что удешевляет сопровождение таких диаграмм. А при добавлении нового элемента из модели в диаграмму, вместе с ним добавляются и все существующие в модели его связи к уже добавленным в диаграмму элементам.

#. Использование Git открывает следующие возможности:

   #. Историрование. Возможность восстановления одного из предыдущих состояний. Журналирование изменений.
   #. Версионирование и ответвления - параллельная разработка различных версий решения.
   #. Коллективная разработка. Доступ к информации задается обычной конфигурацией git-сервера (обычно средствами GitHub и GitLab).

#. Использование `Motivation Elements <https://pubs.opengroup.org/architecture/archimate31-doc/chap06.html#_Toc10045334>`__ (Stakeholder, Driver, Assessment, Goal, Outcome, Principle, Requirement, and Constraint) позволяет осуществлять визуализацию факторов влияния на решение, а также фиксацию трассировки требований.
   Возможность воплощения принципов `Twin Peak Model <https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6470589>`__.
   В процессе проработки одной из альтернатив, обнаруживаются ее ограничения и новые драйверы, которые влияют на требования.
   В визуальном виде аналитическая информация воспринимается намного легче, чем обычная свалка требований в PBI.
#. Богатое интеграционное API позволяет использовать модель для автоматизированной её сверки с реализацией или для генерации кода.
#. В `Archi можно также делать C4 Model <https://www.archimatetool.com/blog/2020/04/18/c4-model-architecture-viewpoint-and-archi-4-7/>`__, используя единую модель и для C4 Model, и для Event Storming.
#. `В Archi можно сделать Context Map <https://community.opengroup.org/archimate-user-community/home/-/issues/8>`__, используя единую модель с Event Storming.


Недостатки
==========

Резольв конфликта слияния через GUI для каждой отдельной диаграммы возможен только путем выбора одной из двух версии целиком - либо своей, либо сливаемой.
При просмотре версий диаграммы их различия никак визуально не выделяются и не подсвечиваются.

Сама модель сохраняется в файл ``.git/temp.archimate``.
Преобразуется она в файлы Git репозитория только в момент коммита.
Этот момент нужно учитывать, т.к. изменения модели в Archi не отражаются мгновенно в файлах Git репозитория и, наоборот, изменения в файлах Git репозитория не отражаются мгновенно в модели Archi.

Мне известны два способа слить диаграммы в случае конфликта без утраты изменений обоих её версий.


Средствами Git
--------------

Резольва конфликта слияния средствами Git `на уровне текстовых файлов <https://github.com/archi-contribs/archi-grafico-plugin/wiki/Merge-two-(or-more)-models>`__" (см. описание `GRAFICO format <https://github.com/archi-contribs/archi-grafico-plugin/wiki/GRAFICO-explained>`__).
Не самый простой, но самый действенный вариант.
Впрочем, к нему быстро привыкаешь.

Чаще всего конфликты возникают в файлах диаграмм (Views), и их резольв усложняется тем, что в них присутствуют только идентификаторы конфликтующих элементоа.
И эти идентификаторы не сообщают никакой информации о своих элементах.
Чтобы определить смысл элемента по его идентификатору, можно предварительно (т.к. в процессе слияния элемент может быть уже удален из модели) заэкспортировать модель в \*.CSV файлы.
Как вариант, можно также сохранить модель в \*.archimate файл, если модель относительно небольшая, и затем использовать поиск по файлу.
Можно создать копию файловой структуры Git репозитория перед слиянием и грепать по её файлам.


Штатный механизм слияния модели
-------------------------------

Сохраняем модель одного бранча в \*.archimate файл, а затем импортируем её в выбранную модель другого бранча.
Этот вариант дает меньше контроля над процессом слияния, но и уменьшает вероятность допущения ошибки.


Избегание конфликтов
--------------------

Резольв конфликта в Archi нетривиальный, и лучше его избегать.
На практике обычно кто-то один управляет доской в один момент времени, и, в случае необходимости, передает управление другому участнику.

Частые интеграции и блокировки организационными мерами позволяют снизить вероятность возникновения конфликта.


Установка
=========

Дистрибутив: https://www.archimatetool.com/download/

`Документация <https://www.archimatetool.com/downloads/Archi%20User%20Guide.pdf>`__ Archi.

Плагин коллективной разработки `coArchi <https://www.archimatetool.com/plugins/#coArchi>`__ (`Source Code <https://github.com/archimatetool/archi-modelrepository-plugin>`__). `Документация <https://github.com/archimatetool/archi-modelrepository-plugin/wiki>`__ к плагину.

Актуальное `руководство по генерации RSA-ключей <https://github.com/archimatetool/archi-modelrepository-plugin/wiki/SSH-Authentication>`__.


Определение границ микросервисов
================================

Изначально мы допускаем, что один микросервис == один агрегат.
Находим "болтливые" микросервисы.
Пробуем объединить болтливые микросервисы в общий микросервис и сравниваем, как изменились совокупный Coupling (внешние связи микросервиса(ов)) & Cohesion (к-т реиспользования агрегатов внутри одного микросервиса).
Например, если у нас совокупный Coupling упал на 5 единиц, при этом Cohesion возрос, то объединение микросервисов оправдано.

Для этого, в каждом микросервисе выделяем отдельную директорию _coupling и _cohesion.
А также создаем отдельную директорию для каждого агрегата и связанной с ним логикой (той самой, которая будет вынесена из текущего микросервиса вместе с агрегатом, если такое понадобится, например, все представления (ReadModels) агрегата).

Дополнительная информация:

- "`Using domain analysis to model microservices <https://docs.microsoft.com/en-us/azure/architecture/microservices/model/domain-analysis>`__"
- "`Identifying microservice boundaries <https://docs.microsoft.com/en-us/azure/architecture/microservices/model/microservice-boundaries>`__"
- "`Bounded Contexts are NOT Microservices <https://vladikk.com/2018/01/21/bounded-contexts-vs-microservices/>`__" by Vladik Khononov
- "`Tackling Complexity in Microservices <https://vladikk.com/2018/02/28/microservices/>`__" by Vladik Khononov
- "Learning Domain-Driven Design: Aligning Software Architecture and Business Strategy" 1st Edition by Vlad Khononov
- "Balancing Coupling in Software Design: Successful Software Architecture in General and Distributed Systems" by Vladislav Khononov


Интеграция
==========

Из коробки Archi уже поддерживает экспорт модели в \*.CSV файл.

Существует ряд плагинов, которые облегчают интеграцию:

- https://www.archimatetool.com/plugins/#exArchi
- https://github.com/archi-contribs/script-plugin
- https://github.com/archi-contribs/database-plugin

С помощью этих плагинов Archi позволяет выгружать свою модель в RDBMS, в Excel, а также позволяет обращаться к модели через консольный интерфейс, используя SQL-подобный синтаксис.

С помощью этих плагинов очень легко генерировать PBI, Acceptance Criteria, BDD-specification или тестовые кейсы из `требований <https://pubs.opengroup.org/architecture/archimate31-doc/chap06.html#_Toc10045345>`__ модели, а из диаграммы Event Storming и C4 Model - генерировать код микросервисов или автоматизировать сверку модели с кодом.

Archimatetool использует Grafico format файлов:

    📝 "GRAFICO stands for "Git Friendly Archi File Collection" and is a way to persist an ArchiMate model in a bunch of XML files (one file per ArchiMate element or view)."

    -- https://github.com/archi-contribs/archi-grafico-plugin/wiki/GRAFICO-explained


Генерация документации
----------------------

- "`Автоматизируем работу с ArchiMate в CI пайплайнах <https://habr.com/ru/post/583314/>`__" / Maxim Levchenko
- `Docker container <https://hub.docker.com/r/woozymasta/archimate-ci-image>`__ и `GH Action <https://github.com/marketplace/actions/deploy-archi-report>`__ для публикации Archimate модели на `GitHub <https://woozymasta.github.io/archimate-ci-image-example/?view=6875>`__/`GitLab <https://woozymasta.gitlab.io/archimate-ci-image-example/?view=6213>`__ Pages. `Source Code <https://github.com/WoozyMasta/archimate-ci-image>`__.
- `archi-htmlreport-docker <https://github.com/abes-esr/archi-htmlreport-docker>`__ (`example <https://github.com/abes-esr/archi-model-example>`__)
- `Others... <https://hub.docker.com/search?q=ArchiMate>`__


Стикеры
=======

В Archi есть `доска со стикерами <https://devlog.archimatetool.com/2010/11/04/sketch/>`__ (см. New Sketch View на `стр. 110 документации <https://www.archimatetool.com/downloads/Archi%20User%20Guide.pdf>`__).

Можно делать Event Storming обычными стикерами, а не только используя "`C.1.10 Business Process Cooperation Viewpoint <https://t.me/emacsway_log/253>`__".

Можно проводить сеанс Example Mapping и автоматизировать генерацию BDD-specification или тестовых кейсов.


C4 Model
========

Event Storming гармонично сочетается с C4 Model, о чем говорил Сергей Баранов в своем `докладе <https://habr.com/ru/company/oleg-bunin/blog/537862/>`__.
И вот тут еще одно интересное открытие - Simon Brown собственноручно `ссылается <https://c4model.com/>`__ на статью Jean-Baptiste Sarrodie о том, `как делать C4 Model в Archi <https://www.archimatetool.com/blog/2020/04/18/c4-model-architecture-viewpoint-and-archi-4-7/>`__.

Там же Simon Brown ссылается на Guide `Agile Architecture Modeling Using the ArchiMate® Language <https://publications.opengroup.org/g20e>`__ на сайте OMG о том, как использовать C4 Model и Event Storming в Open Agile Architecture, используя Archi.
Jean-Baptiste Sarrodie собственноручно выложил `демонстрационную модель C4 Model и Event Storming в Archi <https://community.opengroup.org/archimate-user-community/home/-/issues/8>`__.


Archimatetool troubleshooting
=============================

- "`Список ошибок <https://github.com/archimatetool/archi/blob/master/com.archimatetool.editor/src/com/archimatetool/editor/model/messages.properties>`__"
- Расположение незакоммиченной, но сохраненной модели: ``.git/temp.archimate``.
- "`Archi 4.7 (or superior) can't save a model or (if using coArchi) can't import, refresh or publish a model but instead gives "Error in model" <https://github.com/archimatetool/archi/wiki/Archi-4.7-%28or-superior%29-can%27t-save-a-model-or-%28if-using-coArchi%29-can%27t-import%2C-refresh-or-publish-a-model-but-instead-gives-%22Error-in-model%22>`__"

..
    ArchiMate, трассировка требований и Agile.

    В одном из предыдущих сообщений ( https://t.me/emacsway_log/501 ), рассматривался стандарт ISO/IEC/IEEE 12207:2017 SDLC в отношении применения автоматизированных средств управления требованиями в Agile-моделе разработки, с целью обеспечения трассировки:

    📝 "Where possible [during agile projects], bidirectional traceability is enabled and enforced by integrated automated systems and procedures for requirements management, architecture and design, configuration management, measurement, and information management."
    - ISO/IEC/IEEE 12207:2017(E)

    Существует множество систем управления требованиями, но есть одна бесплатная и с открытым исходным кодом, которая позволяет управлять описанием архитектуры интегрированно, как в problem space, так и в solution space. Причем, осуществлять это коллективно.

    Мне как-то подвернулась интересная вводная статья по этому вопросу:

    "ArchiMate Cookbook"
    - https://www.hosiaisluoma.fi/blog/archimate/

    Можно скачать в pdf:
    - http://www.hosiaisluoma.fi/ArchiMate-Cookbook.pdf

    Примеры от Visual-Paradigm:
    - https://www.visual-paradigm.com/guide/archimate/full-archimate-viewpoints-guide/

    Примеры от Sparxsystems:
    - https://sparxsystems.com/resources/user-guides/15.2/model-domains/languages/archimate.pdf

    Документация ArchiMate по этому вопросу:

    "Motivation Elements" 
    - https://pubs.opengroup.org/architecture/archimate3-doc/chap06.html

    Статья Alexander Teterkin ( @teterkin ) по этому вопросу:

    "Хорошая архитектура и ArchiMate"
    - https://hostco.ru/news/khoroshaya-arkhitektura-i-archimate/

    --

    Archimatetool - бесплатный инструмент, с открытым исходным кодом, который позволяет управлять описанием архитектуры интегрированно, как в problem space, так и в solution space. Причем, осуществлять это коллективно.

    --

    Давайте по порядку. Во-первых, у Event Storming есть несколько уровней (https://ddd-crew.github.io/Event Storming-glossary-cheat-sheet/):
    1. Pig Picture
    2. Process modelling
    3. Design-Level

    Часть этих уровней относится к исследованию домена, другая часть - к моделированию.

    Сам OA-Standard среди целей Event Storming приводит не только исследование домена, но и "Shared understanding of the problem and potential solutions" https://pubs.opengroup.org/architecture/o-aa-standard-single/#event-storming-workshop

    Во-вторых. Если Archi - это инструмент документирования, то документирования чего именно? Бизнесс-процессы ведь документируются? Нотации (цвета) Event Storming практически ничем не отличаются от нотаций "C.1.10 Business Process Cooperation Viewpoint (https://pubs.opengroup.org/architecture/archimate31-doc/apdxc.html#_Toc10045506)", именно поэтому, порог вхождения в Archi после Event Storming практически нулевой (в пределах погрешности). Только Archi, в отличии от Event Storming, позволяет обнаруживать не только границы Bounded Contexts, но еще и границы микросервисов.

    В наше время Scaled Agile, использование подхода API/Design First просто неизбежно, т.к. это решает проблему Брукса и воплощает предложение Харлана Миллза: https://dckms.github.io/system-architecture/emacsway/it/team-topologies/harlan-mills%27-proposal.html . Именно по этой причине, если еще лет 10 назад были популярны системы, генерирующие документацию по коду, то сегодня мы наблюдаем бум систем, генерирующих микросервисы по документации API, диаграммам C4 Model или BPMN, а так же по нотациям Event Storming (domorobo). Наглядный пример: https://goa.design/

    Тут можно вспомнить про документирование изменений системы, чему у ArchiMate посвящен целый раздел: https://pubs.opengroup.org/architecture/archimate31-doc/chap13.html#_Toc10045451

    Event Storming все чаще начинает использоваться именно как средство документирования системы, в т.ч. в известных reference applications и даже в литературе.

    В добавок ко всему, ключевая задача Scaled Agile - это решение проблемы Брукса и достижения автономности команд. Именно поэтому мы сегодня наблюдаем бум Team-First Architecture. А это выдвигает на первое место поиск Bounded Contexts еще до включения команд в работу, чем и занимается Event Storming.



