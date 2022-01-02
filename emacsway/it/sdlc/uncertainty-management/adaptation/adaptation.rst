:canonical-base-url: https://dckms.github.io/system-architecture

.. index:: Adaptation
   :name: emacsway-adaptation


====================
Что такое Adaptation
====================

.. contents:: Содержание


Суть Адаптации
==============

Суть Adaptation заключается в том, что мы не пытаемся разрешить неопределенность заблаговременно путем логического вывода, а, в противовес :ref:`Prediction <emacsway-prediction>`, разрешаем неопределенность опытным, экспериментальным путем.
Выдвигаем гипотезу, реализуем её в виде системного инкремента, инспектируем результат на основе практической обратной связи, и определяем, каким образом нам нужно адаптировать системный инкремент, если с первого раза не удалось удовлетворить ожидания.
Полученные практическим способом знания являются входными аргументами для следующей :ref:`итерации <emacsway-iterative-development>`.

    📝 "\"Iteration\" here means applying a function to itself."

    -- "Concrete Mathematics: A Foundation for Computer Science" 2nd edition by Ronald L. Graham, Donald E. Knuth, Oren Patashnik


Назначение Адаптации
====================

Рость неопределенности приводит к росту стоимости Prediction по мере роста его точности.
Там, где график роста стоимости Adaptation (в зависимости от размера) проекта пересекает график роста стоимости Prediction (в зависимости от точности), возникает экономическая целесообразность обрабатывать неопределенность эмпирически, т.е. путем проведения эксперимента - спроектировали, реализовали, попробовали на практике, и адаптировали реализацию на основании практического фидбека.
В этом - суть :ref:`итерации <emacsway-iterative-development>`.
Prediction при этом не исчезает полностью, а понижает свою точность и дополняется адаптацией.
Для наилучшего экономического эффекта важно правильно выбрать баланс между Prediction и Adaptation, а так же обеспечить роста стоимости Adaptation близкий к горизонтальной асимптоте.

Это и есть та самая причина, по которой выбор SDLC-модели является неотъемлемой частью процесса проектирования, и изучается архитектурой.
Ведь различные SDLC-модели (итеративные, инкрементальные, спиральные, гибридные, каскадные), реализованные в виде Scrum, RUP, SAFe, BDUF etc., обладают различным соотношением Prediction vs. Adaptation, имеют разные подходы к масштабированию команд и различные ограничения.
Выбор SDLC-модели сильно зависит от ситуативного контекста проектирования.
Повторюсь, основная цель итеративной разработки - удешевить стоимость проектирования в условиях неопределенности.

Об этом Брукс писал в Мифическом человеко-месяце когда еще до появления Agile Manifesto:

    📝 "Therefore the most important function that software builders do for their clients is the :ref:`iterative <emacsway-iterative-development>` **extraction and refinement of the product requirements**...

    I would go a step further and assert that it is really impossible for clients, even those working with software engineers, to specify completely, precisely, and correctly the exact requirements of a modern software product before having built and tried some versions of the product they are specifying.

    Therefore one of the most promising of the current technological efforts, and one which attacks the essence, not the accidents, of the software problem, is the development of approaches and tools for rapid prototyping of systems as part of the :ref:`iterative <emacsway-iterative-development>` **specification of requirements**."

    -- "The Mythical Man-Month Essays on Software Engineering Anniversary Edition" by Frederick P. Brooks, Jr.

Конечно, сугубо семантически, термин ":ref:`requirements <emacsway-agile-requirements>`" немного вводит в заблуждение в Agile, ведь заранее требования к продукту неизвестны полностью, и они изменяются по мере реализации продукта.
А в таком случае, как они могут что-то требовать?
Вы, наверное, встречали картинку с треугольником "`Iron Triangle <https://www.atlassian.com/agile/agile-at-scale/agile-iron-triangle>`__" (Requirements/Scope, Cost, Time), где в waterfall он обращен вершиной Requirements вниз (константная область), а в Agile - вверх (переменная область). The iron triangle of planning:

.. figure:: _media/adaptation/iron-triangle.png
   :alt: Iron Triangle. The image source is "Agile Software Requirements: Lean Requirements Practices for Teams, Programs, and the Enterprise" by Dean Leffingwell
   :align: left
   :width: 90%

   Iron Triangle. The image source is "Agile Software Requirements: Lean Requirements Practices for Teams, Programs, and the Enterprise" by Dean Leffingwell

Итеративная разработка востребована, когда невозможно достигнуть полноты (Complete) требований (set of :ref:`requirements <emacsway-agile-requirements>`).

    📝 "Complete. The set of requirements needs no further amplification because it contains everything pertinent to the definition of the system or system element being specified. In addition, the set contains no To Be Defined (TBD), To Be Specified (TBS), or To Be Resolved (TBR) clauses. Resolution of the TBx designations may be iterative and there is an acceptable timeframe for TBx items, determined by risks and dependencies."

    -- "ISO/IEC/IEEE 29148:2018 Systems and software engineering - Life cycle processes - Requirements engineering"

Но это и не требуется стандартом по SDLC:

    📝 "To deal with the **issues of incompletely known requirements** and inaccurate estimates, a number of other types of models have been proposed: :ref:`incremental <emacsway-incremental-development>`, :ref:`spiral <emacsway-spiral-development>`, :ref:`iterative <emacsway-iterative-development>`, and :ref:`evolutionary (adaptive) <emacsway-evolutionary-development>`.

    <...>

    The \":ref:`evolutionary model <emacsway-evolutionary-development>`\" is intended to deal with **incomplete knowledge of requirements**."

    -- "ISO/IEC/IEEE 12207:2017 Systems and software engineering - Software life cycle processes"

Как можно заметить, неполнота требований здесь первична, и именно для её разрешения и применяются такие SDLC-модели, как :ref:`incremental <emacsway-incremental-development>`, :ref:`spiral <emacsway-spiral-development>`, :ref:`iterative <emacsway-iterative-development>`, and :ref:`evolutionary (adaptive) <emacsway-evolutionary-development>`.

Интересно, что, во времена появления термина User Story, полнота требований так же не требовалась старым стандартом:

    📝 "The SRS may need to evolve as the development of the software product progresses. It may be impossible to specify some details at the time the project is initiated.

    <...>

    Requirements should be specified as completely and thoroughly as is known at the time, even if evolutionary revisions can be foreseen as inevitable. The fact that they are incomplete should be noted."

    -- "IEEE Std 830-1998, IEEE Std 830-1993 IEEE Recommended Practice for Software Requirements Specifications"

Таким образом, использование термина :ref:`requirements <emacsway-agile-requirements>`, несмотря на то, что вызывает вопросы относительно семантики, никоим образом не противоречит использованию его в Agile SDLC-моделе, которая, кстати, описана тем же стандартом - ISO/IEC/IEEE 12207:2017, в разделах "5.4.2. Life cycle model for the software system" и "Annex H".


.. seealso::

   - ":ref:`emacsway-iterative-development`"
   - ":ref:`emacsway-agile-development`"
   - ":doc:`../../models/agile/index`"
   - ":ref:`emacsway-agile-requirements`"
