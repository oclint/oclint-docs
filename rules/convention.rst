Convention
==========

AssignIvarOutsideAccessors
--------------------------

**Since: 0.8**

**Name: ivar assignment outside accessors or init**

This rule prevents assigning an ivar outside of getters, setters, and ``init`` method.

This rule is defined by the following class: `oclint-rules/rules/convention/ObjCAssignIvarOutsideAccessorsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/ObjCAssignIvarOutsideAccessorsRule.cpp>`_

**Example:**


.. code-block:: objective-c

    @interface Foo : NSObject
    {
        int _bar;
    }
    @property (assign, nonatomic) int bar;
    @end
    @implementation Foo
    @synthesize bar = _bar;
    - (void)doSomething {
        _bar = 3; // access _bar outside its getter, setter or init
    }
    @end
        

AvoidBranchingStatementAsLastInLoop
-----------------------------------

**Since: 0.7**

**Name: avoid branching statement as last in loop**

Having branching statement as the last statement inside a loop is likely a bug.

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
        

DestructorOfVirtualClass
------------------------

**Since: 0.8**

**Name: destructor of virtual class**

This rule enforces the destructor of a virtual class must be virtual.

This rule is defined by the following class: `oclint-rules/rules/convention/DestructorOfVirtualClassRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/DestructorOfVirtualClassRule.cpp>`_

**Example:**


.. code-block:: cpp

    class Base { // class Base should have a virtual destructor ~Base()
        public: virtual void f();
    };
    class Child : public Base {
        public: ~Child();  // destructor ~Child() should be virtual
    };
        

InvertedLogic
-------------

**Since: 0.4**

**Name: inverted logic**

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
        

MisplacedDefaultLabel
---------------------

**Since: 0.6**

**Name: ill-placed default label in switch statement**

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
        

MissingBreakInSwitchStatement
-----------------------------

**Since: 0.6**

**Name: missing break in switch statement**

A switch case without a break statement is likely a bug.

This rule is defined by the following class: `oclint-rules/rules/convention/MissingBreakInSwitchStatementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/MissingBreakInSwitchStatementRule.cpp>`_

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
        

MissingDefaultStatement
-----------------------

**Since: 0.6**

**Name: missing default in switch statements**

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
        

NonCaseLabelInSwitchStatement
-----------------------------

**Since: 0.6**

**Name: non case label in switch statement**

It is very confusing when label becomes part of the switch statement.

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

**Name: parameter reassignment**

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
        

PreferEarlyExit
---------------

**Since: 0.8**

**Name: prefer early exits and continue**

Early exits can reduce the indentation of a block of code, so that reader do not have to remember all the previous decisions, therefore, makes it easier to understand the code.

This rule is defined by the following class: `oclint-rules/rules/convention/PreferEarlyExitRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/PreferEarlyExitRule.cpp>`_

**Example:**


.. code-block:: cpp

    int *doSomething(int a) {
      if (!foo(a) && bar(a) && doOtherThing(a)) {
        // ... some really long code ....
      }

      return 0;
    }

    // is preferred as

    int *doSomething(int a) {
      if (foo(a)) {
        return 0;
      }

      if (!bar(a)) {
        return 0;
      }

      if (!doOtherThing(a)) {
        return 0;
      }

      // ... some long code ....
    }
        

ProblematicBaseClassDestructor
------------------------------

**Since: 0.10.2**

**Name: base class destructor should be virtual or protected**

Make base class destructor public and virtual, or protected and nonvirtual

This rule is defined by the following class: `oclint-rules/rules/convention/BaseClassDestructorShouldBeVirtualOrProtectedRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/convention/BaseClassDestructorShouldBeVirtualOrProtectedRule.cpp>`_

**Example:**


.. code-block:: cpp

    class Base
    {
    public:
        ~Base(); // this should be either protected or virtual
    }
    class C : public Base
    {
        virtual ~C();
    }
        


**References:**

Sutter & Alexandrescu (November 2004).
`"C++ Coding Standards: 101 Rules, Guidelines, and Best Practices"
<http://gotw.ca/publications/c++cs.htm>`_. *Addison-Wesley Professional*
        
TooFewBranchesInSwitchStatement
-------------------------------

**Since: 0.6**

**Name: too few branches in switch statement**

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

UnnecessaryDefaultStatement
---------------------------

**Since: 0.8**

**Name: unnecessary default statement in covered switch statement**

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
        


.. Generated on Wed Dec 30 09:22:10 2020

