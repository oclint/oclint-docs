Convention
==========

DefaultLabelNotLastInSwitchStatement
------------------------------------

**Since: 0.6**

It is very confusing when default label is not the last label in a switch statement.

This rule is defined by the following class: `oclint-rules/rules/convention/DefaultLabelNotLastInSwitchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/DefaultLabelNotLastInSwitchStatementRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        switch (a) {
            case 1:
                break;
            default:  // the default case should be last
                break;
            case 2:
                break;
        }
    }

InvertedLogic
-------------

**Since: 0.6**

An inverted logic is hard to understand.

This rule is defined by the following class: `oclint-rules/rules/convention/InvertedLogic.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/InvertedLogic.cpp>`_

**Example:**

.. code-block:: cpp

    int example(int a)
    {
        int i;
        if (a != 0)             // if (a == 0)
        {                       // {
            i = 1;              //      i = 0;
        }                       // }
        else                    // else
        {                       // {
            i = 0;              //      i = 1;
        }                       // }

        return !i ? -1 : 1;     // return i ? 1 : -1;
    }

MissingBreakInSwitchStatement
-----------------------------

**Since: 0.6**

A switch statement without a break statement has a very large chance to contribute a bug.

This rule is defined by the following class: `oclint-rules/rules/convention/MissingBreakInSwitchStatement.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/MissingBreakInSwitchStatement.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        switch (a) {
            case 1:
                break;
            case 2:
                // do something
            default:
                break;
        }
    }

NonCaseLabelInSwitchStatement
-----------------------------

**Since: 0.6**

It is very confusing when default label is not the last label in a switch statement.

This rule is defined by the following class: `oclint-rules/rules/convention/NonCaseLabelInSwitchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/NonCaseLabelInSwitchStatementRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        switch (a) {
            case 1:
                break;
            label1:     // label in a switch statement in really confusing
                break;
            default:
                break;
        }
    }

ParameterReassignment
---------------------

**Since: 0.6**

Reassigning values to parameters is very problematic in most cases.

This rule is defined by the following class: `oclint-rules/rules/convention/ParameterReassignment.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/ParameterReassignment.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        if (a < 0)
        {
            a = 0; // reassign parameter a to 0
        }
    }

SwitchStatementsShouldHaveDefault
---------------------------------

**Since: 0.6**

Switch statements should a default statement.

This rule is defined by the following class: `oclint-rules/rules/convention/SwitchStatementsShouldHaveDefault.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/SwitchStatementsShouldHaveDefault.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        switch (a) {
            case 1:
                break;
            case 2:
                break;
            // should have a default
        }
    }

TooFewBranchesInSwitchStatement
-------------------------------

**Since: 0.6**

To increase code readability, when a switch consists of only a few branches, it's much better to use if statement.

This rule is defined by the following class: `oclint-rules/rules/convention/TooFewBranchesInSwitchStatement.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/TooFewBranchesInSwitchStatement.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        switch (a) {
            case 1:
                break;
            default:
                break;
        } // Better to use an if statement and check if variable a equals 1.
    }

**Thresholds:**

MINIMUM_CASES_IN_SWITCH
    The reporting threshold for count of case statements in a switch statement, default value is 3


