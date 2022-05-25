:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Refactoring; when to do
   :name: emacsway-when-to-refactor

=================================
Когда делать refactoring в legacy
=================================

.. sectionauthor:: Ivan Zakrevsky

.. contents:: Содержание

О том, когда делать рефакторинг в унаследованном коде, от соавтора книги "Refactoring: Improving the Design of Existing Code" 1st edition by Martin Fowler, Kent Beck, John Brant, William Opdyke, Don Roberts.

    📝 "Проектирование

    Переход к проектированию в стиле ХР во многом напоминает :ref:`переход к тестированию в стиле ХР <emacsway-when-to-write-unit-tests>`.
    Вы обнаружите, что по сравнению со старым кодом, новый код выглядит совершенно по-другому.
    Вам захочется исправить все сразу.
    Не делайте этого.
    Модернизацию следует осуществлять постепенно.
    По мере добавления новой функциональности будьте готовы перед этим выполнить переработку кода.
    Когда вы разрабатываете программу в рамках ХР, вы всегда готовы вначале выполнить переработку, однако если вы осуществляете переход на ХР существующего проекта, вам придется выполнять переработку чаще.

    На ранних стадиях процесса команда должна определить долгосрочные цели переработки существующего кода.
    Возможно, в проекте используется слишком запутанная иерархия наследования классов, возможно, некоторая важная функциональность разбросана по всей системе и вы желаете собрать ее воедино.
    Сформулируйте все эти цели, запишите их на карточках и развесьте эти карточки на видных местах.
    Когда вы сможете сказать, что большая переработка закончена (для этого могут потребоваться месяцы или даже год работы в описанном «постепенном» стиле), можете устроить посвященную этому веселую вечеринку.
    Торжественно сожгите карточки.
    Хорошенько выпейте и закусите.

    Эффект этой стратегии во многом напоминает эффект стратегии тестирования по необходимости.
    Те части системы, к которым вы обращаетесь чаще всего, в скором времени будут напоминать код, изначально разрабатываемый с применением принципов ХР.
    Дополнительная нагрузка, связанная с необходимостью переработки существующего кода, в скором времени растворится в воздухе.

    Design

    Transitioning to XP design is much like :ref:`transitioning to XP testing <emacsway-when-to-write-unit-tests>`.
    You will notice that the new code feels completely different than the old code.
    You will want to fix everything at once.
    Don't.
    Take it a bit at a time.
    As you add new functionality, be prepared to refactor first.
    You are always prepared to refactor first before implementing in XP development, but you will have to do it more often as you are transitioning to XP.

    Early on in the process, have the team identify some large-scale refactoring goals.
    There may be a particularly tangled inheritance hierarchy, or a piece of functionality scattered across the system that you want to unify.
    Set these goals, put them on cards, and display them prominently.
    When you can say the big refactoring is done (it may take months or even a year of nibbling), have a big party.
    Ceremoniously burn the card.
    Eat and drink well.

    The effect of this strategy is much like the effect of the demand-driven testing strategy.
    Those parts of the system that you visit all the time in your development activities will soon feel just like the code that you are writing now.
    The overhead of extra refactorings will soon fade."

    -- "Extreme Programming Explained" 1st edition by Kent Beck, перевод ООО Издательство "Питер"

..

    📝 "Правило трех раз

    Дон Робертс (Don Roberts) однажды сказал мне следующее.
    Когда вы делаете что-то в первый раз, вы просто это делаете.
    Во второй раз вы морщитесь от повторения тех же действий, но все же делаете их.
    Наконец, делая это же в третий раз, вы начинаете рефакторинг.
    Начинайте рефакторинг после трех повторов.

    The Rule of Three

    Here's a guideline Don Roberts gave me: The first time you do something, you just do it.
    The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway.
    The third time you do something similar, you refactor.
    Or for those who like baseball: Three strikes, then you refactor."

    -- "Refactoring: Improving the Design of Existing Code" 2nd edition by Martin Fowler, Kent Beck перевод И.В. Красикова под редакцией С.Н. Тригуб

..

    📝 "It is worth, at this point, returning to Fowler's distinction [Fowler 2019] between code refactoring and architectural restructuring. Fowler would strongly promote the view that code refactoring requires no justification; rather it is part of a developer's "day job". This does not mean that we have to take on a massive code restructuring exercise for a legacy codebase; on the contrary, there may be no reason whatsoever to restructure the code for a stable legacy project. However, that said, developers should refactor their code when the opportunity arises. Such activity constitutes a "Type 2" decision as documented in [Ries 2011].

    Architectural refactoring (restructuring), however, often requires explicit investment because the required effort is significant. In such cases, it is incumbent on development teams and architects to "sell" the refactoring in monetary, time, or customer success terms. For example, "if we perform refactoring A, the build for Product B will be reduced by seven minutes, resulting in us being able to deploy C times more frequently per day"; or, "implementing refactoring D will directly address key Customer E's escalated pain point; their annual subscription and support fee is $12 million per annum". Note, however, that claims that "refactoring F will make us G% more productive" should be avoided as software productivity is notoriously difficult to measure."

    - [Fowler 2019] Refactoring: Improving the Design of Existing Code, by Martin Fowler, January 2019, published by Addison-Wesley
    - [Ries 2011] The Lean Startup: How Constant Innovation Creates Radically Successful Businesses, by Eric Ries, October 2011, published by Portfolio Penguin

    -- "Open Agile Architecture™" by The Open Group, Chapter "`6.5.1. Justifying Ongoing Investment in Architectural Refactoring <https://pubs.opengroup.org/architecture/o-aa-standard-single/#KLP-CAR-justifying>`__"


.. index::
   single: Refactoring; don't tell to manager
   :name: emacsway-refactoring-don't-tell-to-manager

Что делать, если бизнес не выделяет ресурсов на рефакторинг кода?
=================================================================

Что делать, если бизнес не выделяет ресурсов на рефакторинг кода?
Martin Fowler дает совет по этому вопросу:

    📝 "Конечно, многие говорят, что главное для них качество, а на самом деле главное для них – выполнение графика работ.
    В таких случаях я даю несколько спорный совет: не говорите им ничего!

    Подрывная деятельность? Не думаю.
    Разработчики программного обеспечения – это профессионалы.
    Наша работа состоит в том, чтобы создавать эффективные программы как можно быстрее.
    По моему опыту, рефакторинг значительно способствует быстрому созданию приложений.
    Если мне надо добавить новую функцию, а проект плохо согласуется с модификацией, то быстрее сначала изменить его структуру, а потом добавлять новую функцию.
    Если требуется исправить ошибку, то необходимо сначала понять, как работает программа, и я считаю, что быстрее всего можно сделать это с помощью рефакторинга.
    Руководитель, подгоняемый графиком работ, хочет, чтобы я сделал свою работу как можно быстрее; как мне это удастся – мое дело.
    Самый быстрый путь – рефакторинг, поэтому я и буду им заниматься.

    Of course, many people say they are driven by quality but are more driven by schedule.
    In these cases I give my more controversial advice: Don't tell!

    Subversive? I don't think so.
    Software developers are professionals.
    Our job is to build effective software as rapidly as we can.
    My experience is that refactoring is a big aid to building software quickly.
    If I need to add a new function and the design does not suit the change, I find it's quicker to refactor first and then add the function.
    If I need to fix a bug, I need to understand how the software works—and I find refactoring is the fastest way to do this.
    A schedule-driven manager wants me to do things the fastest way I can; how I do it is my business.
    The fastest way is to refactor; therefore I refactor."

    -- "Refactoring: Improving the Design of Existing Code" by Martin Fowler, Kent Beck, John Brant, William Opdyke, Don Roberts, перевод С. Маккавеева

Иными словами, если refactoring не влияет на сроки спринта, то нет необходимости вообще посвящать менеджеров в этот вопрос.
А если refactoring влияет на сроки, то в этой статье подробно рассказывается, как снизить его стоимость в балансе краткосрочных и долгосрочных интересов: "`Technical Debt <https://www.martinfowler.com/bliki/TechnicalDebt.html>`__" by M.Fowler.


.. seealso::

   - ":ref:`emacsway-yagni`"
   - ":ref:`emacsway-when-to-write-unit-tests`"
   - ":ref:`emacsway-planning-technical-task`"
   - ":ref:`emacsway-agile-balancing-business-technical-concerns`"
   - ":ref:`emacsway-software-development-economics-literature`"
