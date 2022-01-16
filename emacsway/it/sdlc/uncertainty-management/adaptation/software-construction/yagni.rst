:canonical-base-url: https://dckms.github.io/system-architecture

.. index:: YAGNI
   :name: emacsway-yagni


=====
YAGNI
=====

.. sectionauthor:: Ivan Zakrevsky

.. contents:: Содержание

Существует очень распространенная проблема, с которой сталкиваются почти все начинающие интеллектуально развитые разработчики.
Называется эта проблема ":ref:`Заимствование Проблем <emacsway-borrowing-trouble>`" (":ref:`Borrowing Trouble <emacsway-borrowing-trouble>`").
Я её иногда называю "проблемой умных людей".
Заключается она в непреодолимом желании разработчика осуществить реализацию впрок, исходя из предположения о том, что она может быть востребована в будущем.
К сожалению, чаще всего она так и остается невостребованной.
А если даже когда-нибудь и становится востребованной, то она все-равно причиняет ущерб экономике разработки.

Непонимание того, как этот ущерб образуется, является основной причиной продолжения этой практики и деградации экономики разработки.
Хороший архитектор или тимлид имеют ясное представление о причинах и составляющих этого ущерба, и способны пояснить их каждому разработчику, ведь это влияет непосредственно на темпы разработки.

Когда я узнал о YAGNI, моя персональная эффективность выросла в разы.
Этот подход хорошо сочетается с `Emergent (Incremental) Design <https://en.wikipedia.org/wiki/Emergent_Design#Emergent_design_in_agile_software_development>`__.


Когда реализовывать проектное решение
=====================================

Martin Fowler о выборе момента реализации проектного решения:

    📝 "До введения рефакторинга в свою работу я всегда искал гибкие решения.
    Для каждого технического требования я рассматривал возможности его изменения в течение срока жизни системы.
    Поскольку изменения в проекте были дорогостоящими, я старался создать проект, способный выдержать изменения, которые я мог предвидеть.
    Недостаток гибких решений в том, что за гибкость приходится платить.
    Гибкие решения сложнее обычных.
    Создаваемые по ним программы в целом труднее сопровождать, хотя и легче перенацеливать в том направлении, которое предполагалось изначально.
    И даже такие решения не избавляют от необходимости разбираться, как модифицировать проект.
    Для одной двух функций это сделать не очень трудно, но изменения происходят по всей системе.
    Если предусматривать гибкость во всех этих местах, то вся система становится значительно сложнее и дороже в сопровождении.
    Весьма разочаровывает, конечно, то, что вся эта гибкость и не нужна.
    Потребуется лишь какая то часть ее, но невозможно заранее сказать какая.

    Чтобы достичь гибкости, приходится вводить ее гораздо больше, чем требуется в действительности.
    Рефакторинг предоставляет другой подход к рискам модификации.
    Возможные изменения все равно надо пытаться предвидеть, как и рассматривать гибкие решения.
    **Но вместо реализации этих гибких решений следует задаться вопросом: "Насколько сложно будет с помощью рефакторинга преобразовать обычное решение в гибкое?"**
    **Если, как чаще всего случается, ответ будет "весьма несложно", то надо просто реализовать обычное решение.**

    Рефакторинг позволяет создавать более простые проекты, не жертвуя гибкостью, благодаря чему процесс проектирования становится более легким и менее напряженным.
    Научившись в целом распознавать то, что легко поддается рефакторингу, о гибкости решений даже перестаешь задумываться.
    Появляется уверенность в возможности применения рефакторинга, когда это понадобится.
    Создаются самые простые решения, которые могут работать, а гибкие и сложные решения по большей части не потребуются.

    Before I used refactoring, I always looked for flexible solutions.
    With any requirement I would wonder how that requirement would change during the life of the system.
    Because design changes were expensive, I would look to build a design that would stand up to the changes I could foresee.
    The problem with building a flexible solution is that flexibility costs.
    Flexible solutions are more complex than simple ones.
    The resulting software is more difficult to maintain in general, although it is easier to flex in the direction I had in mind.
    Even there, however, you have to understand how to flex the design.
    For one or two aspects this is no big deal, but changes occur throughout the system.
    Building flexibility in all these places makes the overall system a lot more complex and expensive to maintain.
    The big frustration, of course, is that all this flexibility is not needed.
    Some of it is, but it's impossible to predict which pieces those are.
    To gain flexibility, you are forced to put in a lot more flexibility than you actually need.

    With refactoring you approach the risks of change differently.
    You still think about potential changes, you still consider flexible solutions.
    **But instead of implementing these flexible solutions, you ask yourself, "How difficult is it going to be to refactor a simple solution into the flexible solution?"**
    **If, as happens most of the time, the answer is "pretty easy," then you just implement the simple solution.**

    Refactoring can lead to simpler designs without sacrificing flexibility.
    This makes the design process easier and less stressful.
    Once you have a broad sense of things that refactor easily, you don't even think of the flexible solutions.
    You have the confidence to refactor if the time comes.
    You build the simplest thing that can possibly work.
    As for the flexible, complex design, most of the time you aren't going to need it."

    -- "Refactoring: Improving the Design of Existing Code" 1st edition by Martin Fowler, Kent Beck, John Brant, William Opdyke, Don Roberts, перевод С. Маккавеева

Простое и понятное определение дает Сергей Тепляков:

    📝 "Существует простая лакмусовая бумажка принципа YAGNI: **выделение лишних абстракций (и любое другое усложнение) оправдано лишь в том случае, если стоимость их выделения в будущем будет существенно дороже, чем сейчас**."

    -- "`Принцип YAGNI <http://sergeyteplyakov.blogspot.com/2016/08/yagni.html>`__", Сергей Тепляков

Там же присутствует и другой немаловажный момент:

    📝 "Хороший дизайн заключается в простом решении, когда изменения требований ведут к линейным трудозатратам."

    -- "`Принцип YAGNI <http://sergeyteplyakov.blogspot.com/2016/08/yagni.html>`__", Сергей Тепляков

Решение о выборе момента реализации зависит от условий конкретного проекта и :ref:`характера кривой стоимости изменения его кода <emacsway-agile-development-essence>`, который, в свою очередь, зависит от уровня команды, :ref:`качества кода <emacsway-agile-software-design>` и других объективных причин для каждого конкретного случая.
Для принятия решения достаточно просто сравнить затраты на реализацию сейчас и потом.


Экономический ущерб от преждевременной реализации
=================================================

Как оценить финансово стоимость от преждевременного усложения программы (преждевременная реализация, введение излишнего уровня абстракции, косвенности и т.п.)?

    📝 "Пример

    Представьте, что вы занимаетесь программированием фактически в одиночку.
    Вы видите, что добавление в программу некоторой возможности обойдется вам в $10.
    Вы ожидаете, что вы сможете заработать на этой возможности приблизительно $15.
    Таким образом, чистая текущая ценность (Net Present Value, NPV) добавления в программу данной возможности составит $5.

    Представьте, что вы не можете сказать точно, какова будет на самом деле ценность рассматриваемой вами возможности, — вы можете лишь предположить, что заказчик будет готов заплатить за нее $15.
    В действительности этот параметр может отличаться от предполагаемого вами значения на 100% в обе стороны.
    Теперь предположим, что если вы соберетесь добавлять данную возможность спустя год от текущего момента, то это все равно будет стоить вам те же $10 (см. главу 5).

    Какова будет ценность стратегии, в рамках которой вы не будете реализовывать эту возможность прямо сейчас, а подождете в течение года?
    В настоящее время средняя процентная ставка составляет около 5% годовых.
    С учетом этой процентной ставки искомая ценность составит около $7,87.

    Следовательно, стратегия годичного ожидания, прежде чем добавить в программу новую возможность, *нам выгоднее* [в оригинальном переводе: обойдется нам дороже], чем если бы мы, ничего не ожидая, прямо сейчас инвестировали деньги в разработку данной возможности (напомню, что на текущий момент соответствующая NVP составляет $5).
    Почему? В настоящее время мы находимся в неопределенности и не можем точно сказать, будет ли данная возможность действительно полезна для нашего заказчика и сможет ли он прямо сейчас начать зарабатывать на ней деньги.
    Если мы реализуем возможность прямо сейчас и возможность окажется действительно полезной, то наш заказчик через год получит за счет этого определенную прибыль.
    Однако может оказаться, что для нашего заказчика эта возможность не представляет никакой ценности, и поэтому, отказавшись на текущий момент от ее реализации, мы можем сэкономить собственные ресурсы.

    Говоря проще, варианты помогают нам избавиться от нежелательного риска.

    Example

    Suppose you're programming merrily along and you see that you could add a feature that would cost you $10.
    You figure the return on this feature (its net present value) is somewhere around $15.
    So the net present value of adding this feature is $5.

    Suppose you knew in your heart that it wasn't clear at all how much this new feature would be worth—it was just your guess, not something you really knew was worth $15 to the customer.
    In fact, you figure that its value to the customer could vary as much as 100% from your estimate.
    Suppose further (see Chapter 5, Cost of Change, page 21) that it would still cost you about $10 to add that feature one year from now.

    What would be the value of the strategy of just waiting, of not implementing the feature now?
    Well, at the usual interest rates of about 5%, the options theory calculator cranks out a value of $7.87.

    The option of waiting is worth more than the value (NPV = $5) of investing now to add the feature.
    Why? With that much uncertainy, the feature certainly might be much more valuable to the customer, in which case you're no worse off waiting than you would have been by implementing it now.
    Or it could be worth zilch—in which case you've saved the trouble of a worthless exercise.

    In the jargon of trading, options "eliminate downside risk."

    -- "Extreme Programming Explained" 1st edition by Kent Beck, "Chapter 3. Economics of Software Development", перевод ООО Издательство "Питер"

Плюс к этому добавляется ущерб от упущенной выгоды:

    📝 "By expending our effort on the piracy pricing software we didn't build some other feature.
    If we'd instead put our energy into building the sales software for weather risks, we could have put a full storm risks feature into production and be generating revenue two months earlier.
    This **cost of delay** due to the presumptive feature is two months revenue from storm insurance."

    -- "`Yagni <https://martinfowler.com/bliki/Yagni.html>`__" by Martin Fowler

И ущерб от роста стоимости сопровождения системы в связи с переусложнением:

    📝 "The cost of delay is one cost that a successful presumptive feature imposes, but another is the **cost of carry**.
    The code for the presumptive feature adds some complexity to the software, this complexity makes it harder to modify and debug that software, thus increasing the cost of other features."

    -- "`Yagni <https://martinfowler.com/bliki/Yagni.html>`__" by Martin Fowler

Виды стоимостей, образующих экономический ущерб от преждевременной реализации, хорошо разбираются в статье "`Yagni <https://martinfowler.com/bliki/Yagni.html>`__" by Martin Fowler:

    - cost of build
    - cost of delayed value (ущерб упущенной выгоды)
    - cost of carry
    - cost of other features
    - cost of removing
    - cost of repair
    - on-going costs of working around its difficulties

    -- "`Yagni <https://martinfowler.com/bliki/Yagni.html>`__" by Martin Fowler


В каких случаях момент реализации не стоит откладывать
======================================================

    📝 "Если стоимость сегодняшнего решения высока, вероятность того, что оно окажется правильным, низка, вероятность того, что завтра вы найдете лучший способ решить проблему, высока, а стоимость внесения изменений в дизайн завтра низка, то мы можем прийти к выводу, что если сегодня мы можем обойтись без решения, значит, мы ни в коем случае не должны принимать это решение сегодня.
    Именно такой подход используется в рамках ХР.
    "Количество сложностей ровно на один день и не более того".

    Однако некоторые факторы могут стереть наши выводы в порошок.
    Если затраты, которые возникнут в случае, если мы будем принимать решение завтра, существенно больше сегодняшних, значит, мы должны принять решение сегодня в надежде на то, что завтра мы окажемся правы.
    Если инерция дизайна достаточно низка (над проектом работают очень-очень умные люди), значит, у дизайна, формируемого по мере разработки, остается все меньше и меньше преимуществ.
    Если вы действительно очень хороший провидец, значит, вы можете спроектировать все без исключения с самого начала, а затем приступать к реализации готового завершенного плана.
    Однако для всех остальных обычных людей я не вижу иной альтернативы, кроме той, в рамках которой предлагается проектировать сегодня только то, что требует проектирования именно сегодня, и откладывать на завтра то, что можно спроектировать завтра.

    If the cost of today's decision is high, and the probability of its being right is low, and the probability of knowing a better way tomorrow is high, and the cost of putting in the design tomorrow is low, then we can conclude that we should never make a design decision today if we don't need it today.
    In fact, that is what XP concludes.
    "Sufficient to the day are the troubles thereof."

    Now, several factors can make the above evaluation null and void.
    If the cost of making the change tomorrow is very much higher, then we should make the decision today on the off chance that we are right.
    If the inertia of the design is low enough (for example, you have really, really smart people), then the benefits of just-in-time design are less.
    If you are a really, really good guesser, then you could go ahead and design everything today.
    For the rest of us, however, I don't see any alternative to the conclusion that today's design should be done today and tomorrow's design should be done tomorrow."

    -- "Extreme Programming Explained" 1st edition by Kent Beck, "Chapter 17. Design Strategy", перевод ООО Издательство "Питер"


.. index::
   single: Literature; about YAGNI
   :name: emacsway-yagni-literature

Литература о YAGNI
==================

- "`Принцип YAGNI <http://sergeyteplyakov.blogspot.com/2016/08/yagni.html>`__" / Сергей Тепляков
- "`Yagni <https://martinfowler.com/bliki/Yagni.html>`__" (хорошо разъясняет виды экономических ущербов: "cost of build", "cost of delay", "cost of carry", "cost of repair", "cost of removing")
- "`Technical Debt <https://martinfowler.com/bliki/TechnicalDebt.html>`__"
- "`Technical Debt Quadrant <https://martinfowler.com/bliki/TechnicalDebtQuadrant.html>`__"
- "`Design Payoff Line <https://martinfowler.com/bliki/DesignPayoffLine.html>`__"
- "Extreme Programming Explained" 1st edition by Kent Beck
    - "Chapter 3. Economics of Software Development"
    - "Chapter 17. Design Strategy"
    - "Chapter 20. Retrofitting XP"
    - "Chapter 24. What Makes XP Hard"
- "Refactoring: Improving the Design of Existing Code" 1st (and 2nd) edition by Martin Fowler, Kent Beck, John Brant, William Opdyke, Don Roberts
    - "Chapter 2. Principles in Refactoring"
- "Working Effectively with Legacy Code" by Michael C. Feathers


.. seealso::

   - ":ref:`emacsway-borrowing-trouble`"
   - ":ref:`emacsway-when-to-refactor`"
   - ":ref:`emacsway-when-to-write-unit-tests`"
   - ":ref:`emacsway-agile-solid`"
   - ":ref:`emacsway-agile-software-design`"
   - ":doc:`/emacsway/it/sdlc/uncertainty-management/adaptation/crash-course-in-software-development-economics`"
