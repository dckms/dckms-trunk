:canonical-base-url: https://dckms.github.io/system-architecture

.. index::
   single: Immutability; in Value Object
   :name: emacsway-immutability-in-value-object

============
Immutability
============

Что делать, если ЯП не поддерживает неизменяемость?
===================================================


Когда язык программирования не поддерживает неизменяемость, то странствующий Value Object копируется:

    💬 В принципе два объекта Человек могут и не нуждаться в собственных экземплярах объекта-имени.
    Один и тот же объект Имя может совместно использоваться двумя объектами Человек (в каждом будет содержаться указатель на один и тот же экземпляр Имени ), и при этом никаких изменений в их поведении или способе идентификации не потребуется.
    То есть, они будут работать правильно, пока у одного человека не изменится имя.
    Тогда так же изменится имя и другого человека!
    Чтобы этого избежать и сделать совместное использование объекта безопасным, его нужно сделать неизменяемым запрещенным для любых изменений иначе как путем полной замены. 

    Та же проблема возникает, когда объект передает один из своих атрибутов другому объекту в качестве аргумента или возвращаемого значения.
    Со странствующим объектом может случиться все, что угодно, за то время, пока он не находится под контролем владельца.
    3НАЧЕНИЕ (VALUE) может измениться таким образом, что будет поврежден и объект-владелец путем искажения его инвариантов.
    Чтобы избежать этого, передаваемый объект делают неизменяемым или же передают его КОПИЮ.

    In fact, the two Person objects might not need their own name instances.
    The same Name object could be shared between the two Person objects (each with a pointer to the same name instance) with no change in their behavior or identity.
    That is, their behavior will be correct until some change is made to the name of one person. Then the other person's name would change also!
    To protect against this, in order for an object to be shared safely, it must be immutable: it cannot be changed except by full replacement. 

    The same issues arise when an object passes one of its attributes to another object as an argument or return value.
    Anything could happen to the wandering object while it is out of control of its owner.
    The VALUE could be changed in a way that corrupts the owner, by violating the owner's invariants.
    This problem is avoided either by making the passed object immutable, or by passing a copy.

    -- "Domain-Driven Design: Tackling Complexity in the Heart of Software" by Eric Evans, перевод В.Л. Бродового
