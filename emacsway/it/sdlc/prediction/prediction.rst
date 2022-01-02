:canonical-base-url: https://dckms.github.io/system-architecture

.. index:: Prediction
   :name: emacsway-prediction

====================
Что такое Prediction
====================

К Prediction относится ряд активностей на основе правил логического вывода, предшествующих производству системного инкремента и направленных на заблаговременное разрешение неопределенности требований.
К ним относятся Business/System Requirements Definition and Analysis, Architecture Definition, Design Definition, разработка макетов UX/UI-Design, Estimation и Planning.

В Scrum эти активности традиционно выражаются в событиях, предшествующих Definition Of Ready (DOR):

- Со стороны Product Owner:
    - Reveal needs of stakeholders
    - Creating PBI
- Со стороны Team:
    - PBR
    - Planning
    - Spike

Основная проблема Prediction заключается в том, что характер роста стоимости прогнозирования, в зависимости от его точности, близок к экспоненциальному.
В то время как характер роста бизнес-выгод от точности прогнозирования близок к логарифмическому.
Пересечение этих графиков образует предел экономической целесообразности разрешения неопределенности путем прогнозирования.

    📝 "There is a fundamental truth to work breakdown structure estimation - the only way to estimate using a work breakdown structure to really accurately to get the number right is to implement the project.
    Then you'll have the estimate.

    The cost of improving the estimate, the initial work breakdown estimation, the cost of refining that grows exponentially.
    With every next layer you want to take it down.
    And the benefit of doing that does not grow exponentially.
    It grows logarithmically.

    Managers understand there is an extremely high cost involved with refining the estimate."

    -- `"YOW! 2016 Robert C. Martin - Effective Estimation (or: How not to Lie)" at 33:15 <https://youtu.be/eisuQefYw_o?t=1995>`__

Robert C. Martin упомянул о таком способе обработки неопределенности, как реализовать проект (или системный инкремент).
Это уже другой, эмпирический (т.е. опытным путем) способ обработки неопределенности, который называется :ref:`Adaptation <emacsway-adaptation>` и составляет основу итеративной разработки.
Чем сложнее предметная область проекта, тем раньше наступает предел экономической целесообразности Prediction.
