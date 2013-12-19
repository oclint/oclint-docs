Redundant
=========

RedundantConditionalOperator
----------------------------

**Since: 0.6**

This rule detects three types of redundant conditional operators:

#. true expression and false expression are returning true/false or false/true respectively;
#. true expression and false expression are the same constant;
#. true expression and false expression are the same variable expression.

They are usually introduced by mistake, and should be simplified.

This rule is defined by the following class: `oclint-rules/rules/redundant/RedundantConditionalOperatorRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/RedundantConditionalOperatorRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a, int b, int c)
    {
        bool b1 = a > b ? true : false;     // true/false: bool b1 = a > b;
        bool b2 = a > b ? false : true;     // false/true: bool b2 = !(a > b);
        int i1 = a > b ? 1 : 1;             // same constant: int i1 = 1;
        float f1 = a > b ? 1.0 : 1.00;      // equally constant: float f1 = 1.0;
        int i2 = a > b ? c : c;             // same variable: int i2 = c;
    }

RedundantIfStatement
--------------------

**Since: 0.4**

This rule detects unnecessary if statements.

This rule is defined by the following class: `oclint-rules/rules/redundant/RedundantIfStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/RedundantIfStatementRule.cpp>`_

**Example:**

.. code-block:: cpp

    bool example(int a, int b)
    {
        if (a == b)             // this if statement is redundant
        {
            return true;
        }
        else
        {
            return false;
        }                       // the entire method can be simplified to return a == b;
    }

RedundantLocalVariable
----------------------

**Since: 0.4**

This rule detects cases where a variable declaration is immediately followed by a return of that variable.

This rule is defined by the following class: `oclint-rules/rules/redundant/RedundantLocalVariableRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/RedundantLocalVariableRule.cpp>`_

**Example:**

.. code-block:: cpp

    int example(int a)
    {
        int b = a * 2;
        return b;   // variable b is returned immediately after its declaration,
    }               // can be simplified to return a * 2;

RedundantNilCheck
-----------------

**Since: 0.7**

C/C++-style null check in Objective-C like ``foo != nil && [foo bar]`` is redundant, since sending a message to a nil object in this case simply returns a false-y value.

This rule is defined by the following class: `oclint-rules/rules/redundant/RedundantLocalVariableRuleRedundantNilCheck.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/RedundantNilCheck.cpp>`_

**Example:**

.. code-block:: objective-c

    + (void)compare:(A *)obj1 withOther:(A *)obj2
    {
        if (obj1 && [obj1 isEqualTo:obj2]) // if ([obj1 isEqualTo:obj2]) is okay
        {
        }
    }

UnnecessaryElseStatement
------------------------

**Since: 0.6**

When an if statement block ends with a return statement, or all branches in the if statement block end with return statements, then the else statement is unnecessary. The code in the else statement can be run without being in the block.

This rule is defined by the following class: `oclint-rules/rules/redundant/UnnecessaryElseStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/UnnecessaryElseStatementRule.cpp>`_

**Example:**

.. code-block:: cpp

    bool example(int a)
    {
        if (a == 1)                 // if (a == 1)
        {                           // {
            cout << "a is 1.";      //     cout << "a is 1.";
            return true;            //     return true;
        }                           // }
        else                        //
        {                           //
            cout << "a is not 1."   // cout << "a is not 1."
        }                           //
    }

UselessParentheses
------------------

**Since: 0.6**

This rule detects useless parentheses.

This rule is defined by the following class: `oclint-rules/rules/redundant/UselessParenthesesRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/redundant/UselessParenthesesRule.cpp>`_

**Example:**

.. code-block:: cpp

    int example(int a)
    {
        int y = (a + 1);    // int y = a + 1;
        if ((y > 0))        // if (y > 0)
        {
            return a;
        }
        return (0);         // return 0;
    }
