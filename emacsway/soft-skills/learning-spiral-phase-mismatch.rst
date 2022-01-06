:canonical-base-url: https://dckms.github.io/system-architecture

.. index:: Soft Skills

.. index:: Learning spiral phase mismatch
   :name: emacsway-learning-spiral-phase-mismatch


==================================
Несовпадение фаз спиралей обучения
==================================

.. sectionauthor:: Ivan Zakrevsky

..

    📝 Вторая причина столь разных точек зрения на использования инструментов заключается в «спирали обучения».
    Если у вас больше 5 лет опыта, то вы наверняка замечали, что кривая обучения на самом деле выглядит не совсем так, как обычно принято представлять, а несколько иначе.
    **Я бы сказал, что кривая обучения – это скорее бесконечный процесс, который в лучшем случае будет «сходиться» к точке «идеального использования инструмента»**:

    .. figure:: _media/learning-spiral-phase-mismatch/learning-spiral.jpg
       :alt: Рис. 1: Кривая обучения vs. Спираль обучения. Изображение из статьи "Is TDD Dead. Часть 5" / Сергей Тепляков https://sergeyteplyakov.blogspot.com/2014/06/is-tdd-dead-5.html
       :align: left
       :width: 90%

       Рис. 1: Кривая обучения vs. Спираль обучения. Изображение из статьи "`Is TDD Dead. Часть 5 <https://sergeyteplyakov.blogspot.com/2014/06/is-tdd-dead-5.html>`__" / Сергей Тепляков

    Форма этой «спирали обучения» обусловлена нашей увлеченностью.
    Как только мы узнаем о новом инструменте мы начинаем его интенсивно использовать, нас «заносит» и мы начинаем его применять там, где нужно, и там, где без него было бы лучше обойтись.
    Со временем наша эйфория проходит и мы можем либо вообще отказаться от него («Все, паттерны проектирования не нужны!») или же перейти на новый уровень понимания и использовать инструмент более рационально.

    Разные люди находятся на разных точках «спирали обучения», что также усложняет взаимопонимание.
    К тому же, у разных людей точка «правильного» понимания (линия «правильного понимания» на графике справа) находится на разном уровне, что проявляется в том, что кто-то полностью отказывается от инструмента («TDD не нужен!», или «IoC не нужен!», «или ОО не нужно» и т.п.), а кто-то продолжает упорно использовать инструмент не по назначению.

    -- "`Is TDD Dead. Часть 5 <https://sergeyteplyakov.blogspot.com/2014/06/is-tdd-dead-5.html>`__" / Сергей Тепляков

Такое простое объяснение профессиональных конфликтов.
У одного специалиста - девиация в сторону паттернов, у другого - в сторону алгоритмов.
И не могут поделить что важнее.

Кстати, это так же объясняет то, почему соискатель и интервьюер часто не находят друг друга.

Психолог, нобелевский лауреат Даниэль Канеман выделил «правило пик-конец» нашей памяти.
Мы помним прошлое неравномерно.
Наибольший вес мы придаем двум видам событий: тем, что вызвали максимальные эмоции и тем, которые произошли недавно.

Но, как было сказано:

    📝 кривая обучения – это скорее бесконечный процесс, который в лучшем случае будет «сходиться» к точке «идеального использования инструмента».

    -- "`Is TDD Dead. Часть 5 <https://sergeyteplyakov.blogspot.com/2014/06/is-tdd-dead-5.html>`__" / Сергей Тепляков

Иными словами, чем шире полнота знаний, тем меньше степень "увлеченности" отдельными аспектами этих знаний, и лучше сбалансированность решений.
Т.е., лечится это, опять же, :ref:`увеличением охвата знаний <emacsway-knowledge-in-psychology>`.

.. _emacsway-martin-fowler-16-patterns-in-32-lines:

Кстати, именно это явление описывал M.Fowler в своей статье "Is Design Dead?":

    📝 "The essence of this argument is that patterns are often over-used. The world is full of the legendary programmer, fresh off his first reading of GOF  who includes sixteen patterns in 32 lines of code. I remember one evening, fueled by a very nice single malt, running through with Kent a paper to be called "Not Design Patterns: 23 cheap tricks" We were thinking of such things as use an if statement rather than a strategy. The joke had a point, patterns are often overused, but that doesn't make them a bad idea. The question is how you use them."

    -- "`Is Design Dead? <https://martinfowler.com/articles/designDead.html#PatternsAndXp>`__" by M.Fowler


См. также:

- "`Эффект недавнего <https://ru.wikipedia.org/wiki/%D0%AD%D1%84%D1%84%D0%B5%D0%BA%D1%82_%D0%BD%D0%B5%D0%B4%D0%B0%D0%B2%D0%BD%D0%B5%D0%B3%D0%BE>`__"

.. seealso::

   - ":ref:`emacsway-knowledge-in-psychology`"

