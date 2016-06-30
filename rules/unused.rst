Unused
======

UnusedLocalVariable
-------------------

**Since: 0.4**

This rule detects local variables that are declared, but not used.

This rule is defined by the following class: `oclint-rules/rules/unused/UnusedLocalVariableRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/unused/UnusedLocalVariableRule.cpp>`_

**Example:**


.. code-block:: cpp

    int example(int a)
    {
        int i;          // variable i is declared, but not used
        return 0;
    }
    

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[unused local variable]")))

UnusedMethodParameter
---------------------

**Since: 0.4**

This rule detects parameters that are not used in the method.

This rule is defined by the following class: `oclint-rules/rules/unused/UnusedMethodParameterRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/unused/UnusedMethodParameterRule.cpp>`_

**Example:**


.. code-block:: cpp

    int example(int a)  // parameter a is not used
    {
        return 0;
    }
    

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[unused method parameter]")))


.. Generated on Wed Jun 29 21:59:34 2016

