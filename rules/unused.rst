Unused
======

UnusedLocalVariable
-------------------

**Since: 0.6**

This rule detects local variables that are declared, but not used.

This rule is defined by the following class: `oclint-rules/rules/unused/UnusedLocalVariable.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/unused/UnusedLocalVariable.cpp>`_

**Example:**

.. code-block:: cpp

    int example(int a)
    {
        int i;          // variable i is declared, but not used
        return 0;
    }

UnusedMethodParameter
---------------------

**Since: 0.6**

This rule detects parameters that are not used in the method.

This rule is defined by the following class: `oclint-rules/rules/unused/UnusedMethodParameter.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/unused/UnusedMethodParameter.cpp>`_

**Example:**

.. code-block:: cpp

    int example(int a)  // parameter a is not used
    {
        return 0;
    }

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[unused method parameter]")))

