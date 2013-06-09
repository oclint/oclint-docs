Basic
=====

BitwiseOperatorInConditional
----------------------------

**Since: 0.6**

Checks for bitwise operations in conditionals. Although being written on purpose in some rare cases, bitwise operations are considered to be too "smart". Smart code is not easy to understand.

This rule is defined by the following class: `oclint-rules/rules/basic/BitwiseOperatorInConditionalRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/BitwiseOperatorInConditionalRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a, int b)
    {
        if (a | b)
        {
        }
        if (a & b)
        {
        }
    }

BrokenNilCheck
---------------

**Since: 0.7**

The broken nil check in Objective-C in some cases returns just the opposite result.

This rule is defined by the following class: `oclint-rules/rules/basic/BrokenNullCheckRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/BrokenNullCheckRule.cpp>`_

**Example:**

.. code-block:: objective-c

    + (void)compare:(A *)obj1 withOther:(A *)obj2
    {
        if (obj1 || [obj1 isEqualTo:obj2])
        {
        }

        if (!obj1 && ![obj1 isEqualTo:obj2])
        {
        }
    }

BrokenNullCheck
---------------

**Since: 0.7**

The broken null check itself will crash the program.

This rule is defined by the following class: `oclint-rules/rules/basic/BrokenNullCheckRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/BrokenNullCheckRule.cpp>`_

**Example:**

.. code-block:: cpp

    void m(A *a, B *b)
    {
        if (a != NULL || a->bar(b))
        {
        }

        if (a == NULL && a->bar(b))
        {
        }
    }

BrokenOddnessCheck
------------------

**Since: 0.6**

Checking oddness by ``x % 2 == 1`` won't work for negative numbers. Use ``x & 1 == 1``, or ``x % 2 != 0`` instead.

This rule is defined by the following class: `oclint-rules/rules/basic/BrokenOddnessCheckRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/BrokenOddnessCheckRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        if (x % 2 == 1)         // violation
        {
        }

        if (foo() % 2 == 1)     // violation
        {
        }
    }

CollapsibleIfStatements
-----------------------

**Since: 0.6**

This rule detects instances where the conditions of two consecutive if statements can combined into one in order to increase code cleanness and readability.

This rule is defined by the following class: `oclint-rules/rules/basic/CollapsibleIfStatementsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/CollapsibleIfStatementsRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(bool x, bool y)
    {
        if (x)              // these two if statements can be
        {
            if (y)          // combined to if (x && y)
            {
                foo();
            }
        }
    }

ConstantConditionalOperator
---------------------------

**Since: 0.6**

``conditional operator`` whose conditionals are always true or always false are confusing.

This rule is defined by the following class: `oclint-rules/rules/basic/ConstantConditionalOperatorRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/ConstantConditionalOperatorRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        int a = 1 == 1 ? 1 : 0;     // 1 == 1 is actually always true
    }

ConstantIfExpression
--------------------

**Since: 0.2**

``if`` statements whose conditionals are always true or always false are confusing.

This rule is defined by the following class: `oclint-rules/rules/basic/ConstantIfExpressionRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/ConstantIfExpressionRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        if (true)       // always true
        {
            foo();
        }
        if (1 == 0)     // always false
        {
            bar();
        }
    }

DeadCode
--------

**Since: 0.4**

Code after ``return``, ``break``, ``continue``, and ``throw`` statements are unreachable and will never be executed.

This rule is defined by the following class: `oclint-rules/rules/basic/DeadCodeRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/DeadCodeRule.cpp>`_

**Example:**

.. code-block:: objective-c

    void example(id collection)
    {
        for (id it in collection)
        {
            continue;
            int i1;                 // dead code
        }
        return;
        int i2;                     // dead code
    }

DoubleNegative
--------------

**Since: 0.6**

There is no point in using a double negative, it is always positive.

This rule is defined by the following class: `oclint-rules/rules/basic/DoubleNegativeRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/DoubleNegativeRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        int b1 = !!1;
        int b2 = ~~1;
    }

ForLoopShouldBeWhileLoop
------------------------

**Since: 0.6**

Under certain circumstances, some ``for`` loops can be simplified to while loops to make code more concise.

This rule is defined by the following class: `oclint-rules/rules/basic/ForLoopShouldBeWhileLoopRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/ForLoopShouldBeWhileLoopRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a)
    {
        for (; a < 100;)
        {
            foo(a);
        }
    }

GotoStatement
-------------

**Since: 0.6**

`"Go To Statement Considered Harmful" <http://www.cs.utexas.edu/users/EWD/ewd02xx/EWD215.PDF>`_

This rule is defined by the following class: `oclint-rules/rules/basic/GotoStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/GotoStatementRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        A:
            a();
        goto A;     // Considered Harmful, Considered Silly, Considered Stupid... ;)
    }

**References:**

Edsger Dijkstra (March 1968). `"Go To Statement Considered Harmful" <http://www.cs.utexas.edu/users/EWD/ewd02xx/EWD215.PDF>`_. *Communications of the ACM* (PDF) 11 (3): 147–148. doi:10.1145/362929.362947.

MisplacedNilCheck
-----------------

**Since: 0.7**

The nil check is misplaced. In Objective-C, sending a message to a nil pointer simply does nothing. But code readers may be confused about the misplaced nil check.

This rule is defined by the following class: `oclint-rules/rules/basic/MisplacedNullCheckRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/MisplacedNullCheckRule.cpp>`_

**Example:**

.. code-block:: objective-c

    + (void)compare:(A *)obj1 withOther:(A *)obj2
    {
        if ([obj1 isEqualTo:obj2] && obj1)
        {
        }

        if (![obj1 isEqualTo:obj2] || obj1 == nil)
        {
        }
    }

MisplacedNullCheck
------------------

**Since: 0.7**

The null check is misplaced. In C and C++, sending a message to a null pointer could crash the app. When null is misplaced, either the check is useless or it's incorrect.

This rule is defined by the following class: `oclint-rules/rules/basic/MisplacedNullCheckRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/MisplacedNullCheckRule.cpp>`_

**Example:**

.. code-block:: cpp

    void m(A *a, B *b)
    {
        if (a->bar(b) && a != NULL) // violation
        {
        }

        if (a->bar(b) || !a)        // violation
        {
        }
    }

MultipleUnaryOperator
---------------------

**Since: 0.6**

Multiple unary operator can always be confusing and should be simplified.

This rule is defined by the following class: `oclint-rules/rules/basic/MultipleUnaryOperatorRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/MultipleUnaryOperatorRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        int b = -(+(!(~1)));
    }

ReturnFromFinallyBlock
----------------------

**Since: 0.6**

Returning from a finally block is not recommended.

This rule is defined by the following class: `oclint-rules/rules/basic/ReturnFromFinallyBlockRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/ReturnFromFinallyBlockRule.cpp>`_

**Example:**

.. code-block:: objective-c

    void example()
    {
        @try
        {
            foo();
        }
        @catch(id ex)
        {
            bar();
        }
        @finally
        {
            return;         // this can discard exceptions.
        }
    }

ThrowExceptionFromFinallyBlock
------------------------------

**Since: 0.6**

Throwing exceptions within a ``finally`` block may mask other exceptions or code defects.

This rule is defined by the following class: `oclint-rules/rules/basic/ThrowExceptionFromFinallyBlockRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/basic/ThrowExceptionFromFinallyBlockRule.cpp>`_

**Example:**

.. code-block:: objective-c

    void example()
    {
        @try {;}
        @catch(id ex) {;}
        @finally {
            id ex1;
            @throw ex1;                              // this throws an exception
            NSException *ex2 = [NSException new];
            [ex2 raise];                             // this throws an exception, too
        }
    }

