:canonical-base-url: https://dckms.github.io/system-architecture

.. index:: Prediction, Adaptation
   :name: emacsway-balancing-prediction-adaptation

===============================
Balancing Prediction/Adaptation
===============================

    📝 "Scrum projects do not have an up-front analysis or design phase; all work occurs within the repeated cycle of sprints.
    This does not mean, however, that design on a Scrum project is not intentional.
    An intentional design process is one in which the design is guided through deliberate, conscious decision making.
    The difference on a Scrum project is not that intentional design is thrown out, but that it is done (like everything else on a Scrum project) incrementally.
    Scrum teams acknowledge that as nice as it might be to make all design decisions up front, doing so is impossible.
    This means that on a Scrum project, design is both intentional and 
emergent.

    A big part of an organization’s becoming agile is fi nding the appropriate balance between anticipation and adaptation (Highsmith 2002).
    Figure 9.2 shows this balance along with activities and artifacts that inf l uence the balance.
    When doing up-front analysis or design, we are attempting to anticipate users’ needs.
    Because we cannot perfectly anticipate these, we will make some mistakes; some work will need to be redone.
    When we forgo analysis and design and jump immediately into coding and testing with no forethought at all, we are trying to adapt to users’ needs.
    All projects of interest will be positioned somewhere between anticipation and adaptation based on their own unique characteristics; no application will be all the way to either extreme.
    A life-critical, medical safety application may be far to the anticipation side.
    A three-person startup company building a website of information on kayak racing may be far toward the side of adaptation.

    Foretelling the agile preference for simplicity, in 1990, was speaker and author Do-While Jones. 

        I’m not against planning for the future.
        Some thought should be given to future expansion of capability.
        But when the entire design process gets bogged down in an attempt to satisfy future requirements that may never materialize, then it is time to stop and see if there isn’t a simpler way to solve the immediate problem.

        -- Jones’ 1990 article, "The Breakfast Food Cooker," remains a classic parable of what can go wrong when software developers over-design a solution. I highly recommended reading it at http://www.ridgecrest.ca.us/~do_while/toaster.htm

    Scrum teams avoid this "bogging down" by realizing that not all future needs are worth worrying about today. Many future needs may be best handled by planning to adapt as they arise."

    -- "Succeeding with Agile: Software Development Using Scrum" by Mike Cohn

..

    📝 McConnell writes, "In ten years the pendulum has swung from 'design everything' to 'design nothing.'
    But the alternative to BDUF [Big Design Up Front] isn't no design up front, it's a Little Design Up Front (LDUF) or Enough Design Up Front (ENUF)."
    This is a strawman argument.
    The alternative to designing before implementing is designing after implementing.
    Some design up-front is necessary, but just enough to get the initial implementation.
    Further design takes place once the implementation is in place and the real constraints on the design are obvious.
    Far from "design nothing," the XP strategy is "design always."

    -- "Extreme Programming Explained" 2nd edition by Kent Beck

..

    📝 "The incremental and iterative nature of Agile development can facilitate efficient technical and management processes and practices to reduce the cost associated with change.
    In comparison, projects managed at the waterfall end of the continuum seek to reduce total rework cost by minimizing the number of changes, limiting the number of control points, and baselining detailed specifications which are reviewed and traced throughout the project."

    -- "ISO/IEC/IEEE 12207:2017 Systems and software engineering - Software life cycle processes"


Alberto Brandolini about Prediction/Adaptation
==============================================

.. sectionauthor:: Андрей Ганичев

Андрей Ганичев, contributor of "`Full Modular Monolith application with Domain-Driven Design approach <https://github.com/kgrzybek/modular-monolith-with-ddd>`__", на тему поиска баланса Prediction/Adaptation:

Когда читал книгу Брандолини про "`Introducing EventStorming: An act of Deliberate Collective Learning <https://leanpub.com/introducing_eventstorming>`__" by Alberto Brandolini (та которая недописанная), обратил внимание что и он вскользь проходит по этой теме.

Глава Pretending to solve the problem writing software, раздел Embrace Change:

    📝 "...iterative development is expensive. It is the best approach for developing software in very complex, and lean-demanding domains. However, the initial starting point matters, a lot. A big refactoring will cost a lot more than iterative fine tuning (think splitting a database, vs renaming a variable). So I’ll do everything possible to start iterating from the most reasonable starting point."

    -- "`Introducing EventStorming: An act of Deliberate Collective Learning <https://leanpub.com/introducing_eventstorming>`__" by Alberto Brandolini

..

    📝 "Upfront is a terrible word in the agile jargon. It recalls memories the old times analysis phase in the worst corporate waterfall. Given this infamous legacy, the word has been banned from agile environments like blasphemy. But unfortunately …there’s always something upfront. Even the worst developer thinks before typing the firs line of code."

    -- "`Introducing EventStorming: An act of Deliberate Collective Learning <https://leanpub.com/introducing_eventstorming>`__" by Alberto Brandolini

Cм. также:

- "Essential Scrum: A Practical Guide to the Most Popular Agile Process" by Kenneth Rubin, "Chapter 3 Agile Principles :: Prediction and Adaptation"
- "Essential Scrum: A Practical Guide to the Most Popular Agile Process" by Kenneth Rubin, "Chapter 3 Agile Principles :: Balance Predictive Up-Front Work with Adaptive Just-in-Time Work"

TODO:

- https://t.me/emacsway_log/812
- https://t.me/emacsway_log/731
