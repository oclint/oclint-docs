Empty
=====

EmptyCatchStatement
-------------------

**Since: 0.6**

**Name: empty catch statement**

This rule detects instances where an exception is caught, but nothing is done about it.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyCatchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyCatchStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example()
    {
        try
        {
            int* m= new int[1000];
        }
        catch(...)                  // empty catch statement, this swallows an exception
        {
        }
    }
        

EmptyDoWhileStatement
---------------------

**Since: 0.6**

**Name: empty do/while statement**

This rule detects instances where do-while statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyDoWhileStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyDoWhileStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example()
    {
        do
        {                           // empty do-while statement
        } while(1);
    }
        

EmptyElseBlock
--------------

**Since: 0.6**

**Name: empty else block**

This rule detects instances where an else statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyElseBlockRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyElseBlockRule.cpp>`_

**Example:**


.. code-block:: cpp

    int example(int a)
    {
        if (1)
        {
            return a + 1;
        }
        else                // empty else statement, can be safely removed
        {
        }
    }
        

EmptyFinallyStatement
---------------------

**Since: 0.6**

**Name: empty finally statement**

This rule detects instances where a finally statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyFinallyStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyFinallyStatementRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void example()
    {
        Foo *foo;
        @try
        {
            [foo bar];
        }
        @catch(NSException *e)
        {
            NSLog(@"Exception occurred: %@", [e description]);
        }
        @finally            // empty finally statement, probably forget to clean up?
        {
        }
    }
        

EmptyForStatement
-----------------

**Since: 0.6**

**Name: empty for statement**

This rule detects instances where a for statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyForStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyForStatementRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void example(NSArray *array)
    {
        for (;;)                // empty for statement
        {
        }

        for (id it in array)    // empty for-each statement
        {
        }
    }
        

EmptyIfStatement
----------------

**Since: 0.2**

**Name: empty if statement**

This rule detects instances where a condition is checked, but nothing is done about it.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyIfStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyIfStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example(int a)
    {
        if (a == 1)                  // empty if statement
        {
        }
    }
        

EmptySwitchStatement
--------------------

**Since: 0.6**

**Name: empty switch statement**

This rule detects instances where a switch statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptySwitchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptySwitchStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example(int i)
    {
        switch (i)              // empty switch statement
        {
        }
    }
        

EmptyTryStatement
-----------------

**Since: 0.6**

**Name: empty try statement**

This rule detects instances where a try statement is empty.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyTryStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyTryStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example()
    {
        try                     // but this try statement is empty
        {
        }
        catch(...)
        {
            cout << "Exception is caught!";
        }
    }
        

EmptyWhileStatement
-------------------

**Since: 0.6**

**Name: empty while statement**

This rule detects instances where a while statement does nothing.

This rule is defined by the following class: `oclint-rules/rules/empty/EmptyWhileStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/empty/EmptyWhileStatementRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example(int a)
    {
        while(a--)              // empty while statement
        {
        }
    }
        


.. Generated on Wed Dec 30 09:22:10 2020

