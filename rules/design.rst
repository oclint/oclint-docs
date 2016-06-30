Design
======

AvoidDefaultArgumentsOnVirtualMethods
-------------------------------------

**Since: 0.10.1**

Giving virtual functions default argument initializers tends to defeat polymorphism and introduce unnecessary complexity into a class hierarchy.

This rule is defined by the following class: `oclint-rules/rules/design/AvoidDefaultArgumentsOnVirtualMethodsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/design/AvoidDefaultArgumentsOnVirtualMethodsRule.cpp>`_

**Example:**


.. code-block:: cpp

    class Foo
    {
    public:
        virtual ~Foo();
        virtual void a(int b = 3);
        // ...
    };

    class Bar : public Foo
    {
    public:
        void a(int b);
        // ...
    };

    Bar *bar = new Bar;
    Foo *foo = bar;
    foo->a();   // default of 3
    bar->a();   // compile time error!
        

AvoidPrivateStaticMembers
-------------------------

**Since: 0.10.1**

Having static members is easier to harm encapsulation.

This rule is defined by the following class: `oclint-rules/rules/design/AvoidPrivateStaticMembersRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/design/AvoidPrivateStaticMembersRule.cpp>`_

**Example:**


.. code-block:: cpp

    class Foo
    {
        static int a;       // static field
    };
    class Bar
    {
        static int b();     // static method
    }
        


.. Generated on Wed Jun 29 21:59:34 2016

