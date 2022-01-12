:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Unit Test; when to write
   :name: emacsway-when-to-write-unit-tests

================================
Когда писать Unit Tests в legacy
================================

.. sectionauthor:: Ivan Zakrevsky

О том, когда писать юнит-тесты в унаследованном коде, от автора xUnit (sUnit):

    📝 "Тестирование

    Когда вы приступите к приведению существующего кода в соответствие с требованиями ХР, тестирование станет для вас, наверное, наиболее разочаровывающим процессом.
    Код, написанный до того, как вы пишете тесты, кажется пугающим.
    Вы никогда не знаете, где именно вы находитесь и в каком направлении без опасений можно сделать шаг.
    "Что, если я отредактирую эту строку? Будет ли это изменение безопасным?" Вы не уверены в этом.

    Как только вы начинаете писать тесты, картина меняется.
    Вы уверены в новом коде.
    Вы не задумываетесь перед тем, как внести в него изменения.
    Для вас это становится даже приятным.

    Переход от старого кода к новому коду — это как выход из темноты на солнечный свет.
    Вы начнете ловить себя на том, что вы избегаете работать со старым кодом.
    Вы должны сопротивляться этой тенденции.
    Единственным способом обрести контроль над ситуацией в данном случае является переработка старого кода в соответствии с новыми более прогрессивными правилами.
    В противном случае в темноте начнут скапливаться страшные чудовища, которые в любой момент могут выпрыгнуть наружу.
    Оставляя старый код в прежнем состоянии, вы получаете риск, величину которого сложно оценить.

    **В подобной ситуации возникает соблазн вернуться несколько назад и написать тесты для всего существующего кода.**
    **Не делайте этого.**
    **Тесты для старого кода следует писать по мере надобности.**

    - Если вы хотите добавить новую функциональность в не тестированный код, вначале напишите тесты для существующей функциональности.
    - Если вы намерены исправить ошибку в старом коде, сначала напишите тест.
    - Если вы намерены переработать участок старого кода, сначала напишите все необходимые тесты.

    Вы обнаружите, что вначале разработка несколько замедлится.
    Вы будете тратить существенно больше времени на написание тестов, чем требуется для этого в рамках обычной ХР, и у вас появится ощущение, что вы формируете новую функциональность более медленно, чем раньше.

    Однако разделы системы, к которым вы обращаетесь чаще всего, части, которые привлекают к себе наибольшее внимание, а также новые возможности системы в обозримом будущем будут тщательно протестированы.
    В скором времени части системы, использующиеся чаще других, будут выглядеть, как будто они с самого начала написаны с применением ХР.

    Testing

    Testing is perhaps the most frustrating area when you are shifting existing code to XP.
    The code written before you have tests is scary.
    You never know quite where you stand.
    Will this change be safe? You're not sure.

    As soon as you start writing the tests, the picture changes.
    You have confidence in the new code.
    You don't mind making changes.
    In fact, it's kind of fun.

    Shifting between old code and new code is like night and day.
    You will find yourself avoiding the old code.
    You have to resist this tendency.
    The only way to gain control 96in this situation is to bring all the code forward.
    Otherwise ugly things will grow in the dark.
    You will have risks of unknown magnitude.

    **In this situation, it is tempting to try to just go back and write the tests for all the existing code.**
    **Don't do this.**
    **Instead, write the tests on demand.**

    - When you need to add functionality to untested code, write tests for its current functionality first.
    - When you need to fix a bug, write a test first.
    - When you need to refactor, write tests first.

    What you will find is that development feels slow at first.
    You will spend much more time writing tests than you do in normal XP, and you will feel like you make progress on new functionality more slowly than before.
    However, the parts of the system that you visit all the time, the parts that attract attention and new features, will quickly be thoroughly tested.
    Soon, the parts of the system that are used most will feel like they were written with XP."

    -- "Extreme Programming Explained" 1st edition by Kent Beck, перевод ООО Издательство "Питер"


.. seealso::

   - ":ref:`emacsway-when-to-refactor`"
