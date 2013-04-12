Coding Standards
================

Please help us with consistent coding standards for a number of reasons:

* Reduce the maintenance cost
* Improve the readability
* Ship source code as a product, in fact, it's an art

Although there is no restricted rules to be followed in all instances, it's still highly recommended that when you implement new code or fix existing code, use the same style that is already being used in other places of the codebase.

Naming Convention
-----------------

In general, use `camel case <http://en.wikipedia.org/wiki/CamelCase>`_.

Class names
    Should be nouns and start with an upper case letter, like ``EmptyIfStatementRule``.
Variable names
    Should be nouns, and start with a lower case letter, like ``ifStmt``. Names for class attributes (fields, members) are recommended with a underscore as prefix, like ``_carrier``.
Function names
    Should be verbs, start with a lower case letter, like ``applyLoopCompoundStmt``.

Use Spaces Instead of Tabs
--------------------------

Treat Compiler Warnings Like Errors
-----------------------------------

Don't Use ``else`` after ``return``
-----------------------------------

Having ``else`` or ``else if`` after statements that interrupt control flow, like ``return``, ``break``, ``continue``, etc, is confusing. It warms the readability, and sometimes, it's hard to understand. We have a rule implemented about this, so `dogfooding <dogfooding.html>`_ can help identify them.

Don't Use Inverted Logic
------------------------

To make code easier to understand, code like

.. code-block:: c++

    if (!foo())
    {
        doSomething();
    }
    else
    {
        doSomethingElse();
    }

Should be changed to

.. code-block:: c++

    if (foo())
    {
        doSomethingElse();
    }
    else
    {
        doSomething();
    }

No States in Rules
------------------
