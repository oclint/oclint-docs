Size
====

DeepNestedBlock
---------------

**Since: 0.6**

**Name: deep nested block**

This rule indicates nested blocks deeper than the threshold.

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
    The depth of a block or compound statement reporting threshold, default value is 5.

HighCyclomaticComplexity
------------------------

**Since: 0.4**

**Name: high cyclomatic complexity**


Cyclomatic complexity is determined by the number of linearly independent paths
through a program's source code. In other words, cyclomatic complexity of a method
is measured by the number of decision points, like ``if``, ``while``, and ``for``
statements, plus one for the method entry.

The McCabe 1976 paper concludes that methods in the 3 to 7 complexity range
are quite well structured. It is also suggested that
the cyclomatic complexity of 10 is a reasonable upper limit.
        

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
    The cyclomatic complexity reporting threshold, default value is 10.

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high cyclomatic complexity]")))


**References:**

McCabe (December 1976). `"A Complexity Measure" <http://www.literateprogramming.com/mccabe.pdf>`_.
*IEEE Transactions on Software Engineering: 308–320*
        
HighNPathComplexity
-------------------

**Since: 0.4**

**Name: high npath complexity**


NPath complexity is determined by the number of execution paths through that method.
Compared to cyclomatic complexity, NPath complexity has two outstanding characteristics:
first, it distinguishes between different kinds of control flow structures;
second, it takes the various type of acyclic paths in a flow graph into consideration.

Based on studies done by the original author in AT&T Bell Lab,
an NPath threshold value of 200 has been established for a method.
        

This rule is defined by the following class: `oclint-rules/rules/size/NPathComplexityRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/NPathComplexityRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example()
    {
        // complicated code that is hard to understand
    }
        

**Thresholds:**

NPATH_COMPLEXITY
    The NPath complexity reporting threshold, default value is 200.

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high npath complexity]")))


**References:**

Brian A. Nejmeh  (1988). `"NPATH: a measure of execution path complexity and its applications"
<https://dl.acm.org/doi/10.1145/42372.42379>`_. *Communications of the ACM 31 (2) p. 188-200*
        
HighNcssMethod
--------------

**Since: 0.6**

**Name: high ncss method**

This rule counts the Non-Commenting Source Statements (NCSS) of a method. NCSS only takes actual statements into consideration. In other words, it ignores empty statements, empty blocks, closing brackets, semicolons after closing brackets, and others. Meanwhile, a statement that is broken into multiple lines is counted only once.

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
    The high NCSS method reporting threshold, default value is 30.

**Suppress:**

.. code-block:: cpp

    __attribute__((annotate("oclint:suppress[high ncss method]")))

LongClass
---------

**Since: 0.6**

**Name: long class**

Long class generally indicates that it does too many things. Each class should be cohesive: does one thing and that one thing well.

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
    The class size reporting threshold, default value is 1000.

LongLine
--------

**Since: 0.6**

**Name: long line**

Long lines are hard to read. Break them into multiple lines.

This rule is defined by the following class: `oclint-rules/rules/size/LongLineRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/LongLineRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example()
    {
        int a012345678901234567890123456789...1234567890123456789012345678901234567890123456789;
    }
        

**Thresholds:**

LONG_LINE
    The long line reporting threshold, default value is 100.

LongMethod
----------

**Since: 0.4**

**Name: long method**

Long method generally indicates that this method tries to do many things. Each method should do one thing and that one thing well.

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
    The long method reporting threshold, default value is 50.

TooManyFields
-------------

**Since: 0.7**

**Name: too many fields**

A class with too many fields indicates it does too many things and lacks proper abstraction. It can be redesigned to have fewer fields.

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
    The reporting threshold for too many fields, default value is 20.

TooManyMethods
--------------

**Since: 0.7**

**Name: too many methods**

A class with too many methods indicates it does too many things and is hard to read and understand. It usually contains complicated code, and should be refactored.

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
    The reporting threshold for too many methods, default value is 30.

TooManyParameters
-----------------

**Since: 0.7**

**Name: too many parameters**

Methods with too many parameters are hard to understand and maintain, and are thirsty for refactorings, like `Replace Parameter With method <https://www.refactoring.com/catalog/replaceParameterWithMethod.html>`_, `Introduce Parameter Object <https://www.refactoring.com/catalog/introduceParameterObject.html>`_, or `Preserve Whole Object <https://www.refactoring.com/catalog/preserveWholeObject.html>`_.

This rule is defined by the following class: `oclint-rules/rules/size/TooManyParametersRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/size/TooManyParametersRule.cpp>`_

**Example:**


.. code-block:: cpp

    void example(int a, int b, int c, int d, int e, int f,
        int g, int h, int i, int j, int k, int l)
    {
    }
        

**Thresholds:**

TOO_MANY_PARAMETERS
    The reporting threshold for too many parameters, default value is 10.


**References:**

Fowler, Martin (1999). *Refactoring: Improving the design of existing code.* Addison Wesley.
        

.. Generated on Wed Dec 30 09:22:10 2020

