Convention
==========

AvoidBranchingStatementAsLastInLoop
-----------------------------------

**Since: 0.7**

Having branching statement as the last statement inside a loop is very confusing, and could largely be forgetting of something and turning into a bug.

This rule is defined by the following class: `oclint-rules/rules/convention/AvoidBranchingStatementAsLastInLoopRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/AvoidBranchingStatementAsLastInLoopRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        for (int i = 0; i < 10; i++)
        {
            if (foo(i))
            {
                continue;
            }
            break;      // this break is confusing
        }
    }

CoveredSwitchStatementsDontNeedDefault
--------------------------------------

**Since: 0.8**

When a switch statement covers all possible cases, a default label is not needed and should be removed. If the switch is not fully covered, the SwitchStatementsShouldHaveDefault rule will report.

This rule is defined by the following class: `oclint-rules/rules/convention/CoveredSwitchStatementsDontNeedDefaultRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/CoveredSwitchStatementsDontNeedDefaultRule.cpp>`_

**Example:**

.. code-block:: cpp

    typedef enum {
        value1 = 0,
        value2 = 1
    } eValues;
    
    void aMethod(eValues a)
    {
        switch(a)
        {
            case value1:
                break;
            case value2:
                break;
            default:          // this break is obsolete because all
                break;        // values of variable a are already covered.
        }
    }

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

**Since: 0.4**

An inverted logic is hard to understand.

This rule is defined by the following class: `oclint-rules/rules/convention/InvertedLogicRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/InvertedLogicRule.cpp>`_

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

JumbledIncrementer
------------------

**Since: 0.7**

Jumbled incrementers are usually typos. If it's done on purpose, it's very confusing for code readers.

This rule is defined by the following class: `oclint-rules/rules/convention/JumbledIncrementerRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/JumbledIncrementerRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        for (int i = 0; i < 10; i++)
        {
            for (int j = 0; j < 20; i++ /* what?! */)
            {
            }
        }
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

This rule is defined by the following class: `oclint-rules/rules/convention/ParameterReassignmentRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/ParameterReassignmentRule.cpp>`_

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

Switch statements should have a default statement.

This rule is defined by the following class: `oclint-rules/rules/convention/SwitchStatementsShouldHaveDefaultRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/SwitchStatementsShouldHaveDefaultRule.cpp>`_

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

To increase code readability, when a switch consists of only a few branches, it's much better to use an if statement instead.

This rule is defined by the following class: `oclint-rules/rules/convention/TooFewBranchesInSwitchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/TooFewBranchesInSwitchStatementRule.cpp>`_

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
    The reporting threshold for count of case statements in a switch statement, default value is 3.


