Naming
======

LongVariableName
----------------

**Since: 0.7**

**Name: long variable name**

Variables with long names harm readability.

This rule is defined by the following class: `oclint-rules/rules/naming/LongVariableNameRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/naming/LongVariableNameRule.cpp>`_

**Example:**


.. code-block:: cpp

    void aMethod()
    {
        int reallyReallyLongIntegerName;
    }
    

**Thresholds:**

LONG_VARIABLE_NAME
    The long variable name reporting threshold, default value is 20.

ShortVariableName
-----------------

**Since: 0.7**

**Name: short variable name**

A variable with a short name is hard to understand what it stands for.

This rule is defined by the following class: `oclint-rules/rules/naming/ShortVariableNameRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/naming/ShortVariableNameRule.cpp>`_

**Example:**


.. code-block:: cpp

    void aMethod(int i)  // i is short
    {
        int ii;          // ii is short
    }
    

**Thresholds:**

SHORT_VARIABLE_NAME
    The short variable name reporting threshold, default value is 3.


.. Generated on Sat Mar  6 11:00:31 2021

