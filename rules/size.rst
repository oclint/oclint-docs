Size
====

CyclomaticComplexity
--------------------

**Since: 0.4**

Cyclomatic complexity is determined by the number of linearly independent paths through a program's source code. In other words, cyclomatic complexity of a method is measured by the number of decision points, like ``if``, ``while``, and ``for`` statements, plus one for the method entry.

The experiments McCabe, the author of cyclomatic complexity, conclude that methods in the 3 to 7 complexity range are quite well structured. He also suggest the cyclomatic complexity of 10 is a reasonable upper limit.

This rule is defined by the following class: `oclint-rules/rules/size/CyclomaticComplexityRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/CyclomaticComplexityRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a, int b, int c) // 1
    {
        if (a == b)                   // 2
        {
            if (b == c)               // 3
            {
            }
            else if (a == c)          // 3
            {
            }
            else
            {
            }
        }
        for (int i = 0; i < c; i++)   // 4
        {
        }
        switch(c)
        {
            case 1:                   // 5
                break;
            case 2:                   // 6
                break;
            default:                  // 7
                break;
        }
    }

**Thresholds:**

CYCLOMATIC_COMPLEXITY
    The cyclomatic complexity reporting threshold, default value is 10

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high cyclomatic complexity]")))

**References:**

McCabe (December 1976). `"A Complexity Measure" <http://www.literateprogramming.com/mccabe.pdf>`_. *IEEE Transactions on Software Engineering: 308–320*

LongClass
---------

**Since: 0.6**

Long class generally indicates that this class tries to so many things. Each class should do one thing and one thing well.

This rule is defined by the following class: `oclint-rules/rules/size/LongClassRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/LongClassRule.cpp>`_

**Example:**

.. code-block:: cpp

    class Foo
    {
        void bar()
        {
            // 1001 lines of code
        }
    }

**Thresholds:**

LONG_CLASS
    The class size reporting threshold, default value is 1000

LongLine
--------

**Since: 0.6**

When number of characters for one line of code is very long, it largely harm the readability. Break long line of code into multiple lines.

This rule is defined by the following class: `oclint-rules/rules/size/LongLineRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/LongLineRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        int a012345678901234567890123456789012345678901234567890123456789012345678901234567890123456789;
    }

**Thresholds:**

LONG_LINE
    The long line reporting threshold, default value is 100

LongMethod
----------

**Since: 0.4**

Long method generally indicates that this method tries to so many things. Each method should do one thing and one thing well.

This rule is defined by the following class: `oclint-rules/rules/size/LongMethodRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/LongMethodRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        cout << "hello world";
        cout << "hello world";
        // repeat 48 times
    }

**Thresholds:**

LONG_METHOD
    The long method reporting threshold, default value is 50

NcssMethodCount
---------------

**Since: 0.6**

This rule counts number of lines for a method by counting Non Commenting Source Statements (NCSS). NCSS only takes actual statements into consideration, in other words, ignores empty statements, empty blocks, closing brackets or semicolons after closing brackets. Meanwhile, statement that is break into multiple lines contribute only one count.

This rule is defined by the following class: `oclint-rules/rules/size/NcssMethodCountRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/NcssMethodCountRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()          // 1
    {
        if (1)              // 2
        {
        }
        else                // 3
        {
        }
    }

**Thresholds:**

NCSS_METHOD
    The high NCSS method reporting threshold, default value is 30

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high ncss method]")))

NestedBlockDepth
----------------

**Since: 0.6**

This rule indicates blocks nested more deeply than the upper limit.

This rule is defined by the following class: `oclint-rules/rules/size/NestedBlockDepthRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/NestedBlockDepthRule.cpp>`_

**Example:**

.. code-block:: cpp

    if (1)
    {               // 1
        {           // 2
            {       // 3
            }
        }
    }

**Thresholds:**

NESTED_BLOCK_DEPTH
    The depth of a block or compound statement reporting threshold, default value is 5

NPathComplexity
---------------

**Since: 0.4**

NPath complexity is determined by the number of execution paths through that method. Compared to cyclomatic complexity, NPath complexity has two outstanding characteristics: first, it distinguish between different kinds of control flow structures; second, it takes the various type of acyclic paths in a flow graph into consideration.

Based on studies done by the original author in AT&T Bell Lab, an NPath threshold value of 200 has been established for a method.

This rule is defined by the following class: `oclint-rules/rules/size/NPathComplexityRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/NPathComplexityRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example()
    {
        // complicated code that is hard to understand
    }

**Thresholds:**

NPATH_COMPLEXITY
    The NPath complexity reporting threshold, default value is 200

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high npath complexity]")))

**References:**

Brian A. Nejmeh  (1988). `"NPATH: a measure of execution path complexity and its applications" <http://dl.acm.org/citation.cfm?id=42379>`_. *Communications of the ACM 31 (2) p. 188-200*

TooManyFields
-------------

**Since: 0.7**

A class with too many fields indicates it does too many things and is lack of proper abstraction. It can be resigned to have fewer fields.

This rule is defined by the following class: `oclint-rules/rules/size/TooManyFieldsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/TooManyFieldsRule.cpp>`_

**Example:**

.. code-block:: cpp

    class c
    {
        int a, b;
        int c;
        // ...
        int l;
        int m, n;
        // ...
        int x, y, z;

        void m() {}
    };

**Thresholds:**

TOO_MANY_FIELDS
    The reporting threshold for too many fields, default value is 20

TooManyMethods
--------------

**Since: 0.7**

A class with too many methods indicates it does too many things and hard to read and understand. It usually contains complicated code, and should be refactored.

This rule is defined by the following class: `oclint-rules/rules/size/TooManyMethodsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/TooManyMethodsRule.cpp>`_

**Example:**

.. code-block:: cpp

    class c
    {
        int a();
        int b();
        int c();
        // ...
        int l();
        int m();
        int n();
        // ...
        int x();
        int y();
        int z();
        int aa();
        int ab();
        int ac();
        int ad();
        int ae();
    };

**Thresholds:**

TOO_MANY_METHODS
    The reporting threshold for too many methods, default value is 30

TooManyParameters
-----------------

**Since: 0.7**

Methods with too many parameters are hard to understand and maintain, and are thirsty for refactorings, like `Replace Parameter With method <http://www.refactoring.com/catalog/replaceParameterWithMethod.html>`_, `Introduce Parameter Object <http://www.refactoring.com/catalog/introduceParameterObject.html>`_, or `Preserve Whole Object <http://www.refactoring.com/catalog/preserveWholeObject.html>`_.

This rule is defined by the following class: `oclint-rules/rules/size/TooManyParametersRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/TooManyParametersRule.cpp>`_

**Example:**

.. code-block:: cpp

    void example(int a, int b, int c, int d, int e, int f,
        int g, int h, int i, int j, int k, int l)
    {
    }

**Thresholds:**

TOO_MANY_PARAMETERS
    The reporting threshold for too many parameters, default value is 10

**References:**

Fowler, Martin (1999). *Refactoring: Improving the design of existing code.* Addison Wesley.
