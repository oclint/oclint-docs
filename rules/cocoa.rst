Cocoa
=====

ObjCVerifyIsEqualHash
---------------------

**Since: 0.8**

When ``isEqual`` method is overridden, ``hash`` method must be overridden, too.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifyIsEqualHashRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifyIsEqualHashRule.cpp>`_

**Example:**

.. code-block:: objective-c

    @implementation BaseObject

    - (BOOL)isEqual:(id)obj {
        return YES;
    }

    /*
    - (int)hash is missing; If you override isEqual you must override hash too.
    */

    @end

ObjCVerifyMustCallSuper
-----------------------

**Since: 0.8**

When a method is declared with ``__attribute__((annotate("oclint:enforce[must call super]")))`` annotation, all of its implementations (including its own and its sub classes) must call the method implementation in super class.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifyMustCallSuperRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifyMustCallSuperRule.cpp>`_

**Example:**

.. code-block:: objective-c

    @interface UIView (OCLintStaticChecks)
    - (void)layoutSubviews __attribute__((annotate("oclint:enforce[must call super]")));
    @end

    @interface CustomView : UIView
    @end

    @implementation CustomView

    - (void)layoutSubviews {
        // [super layoutSubviews]; is enforced here
    }

    @end

ObjCVerifyProtectedMethod
-------------------------

**Since: 0.8**

Even though there is no ``protected`` in Objective-C language level, in a design's perspective, we sometimes hope to enforce a method only be used inside the class itself or by its subclass. This rule mimics the ``protected`` behavior, and alerts developers when a method is called outside its access scope.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifyProtectedMethodRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifyProtectedMethodRule.cpp>`_

**Example:**

.. code-block:: objective-c

    @interface A : NSObject
    - (void)foo __attribute__((annotate("oclint:enforce[protected method]")));
    @end

    @interface B : NSObject
    @property (strong, nonatomic) A* a;
    @end

    @implementation B
    - (void)bar {
        [self.a foo]; // calling protected method foo from outside A and its subclasses
    }
    @end

ObjCVerifySubclassMustImplement
-------------------------------

**Since: 0.8**

Due to the Objective-C language tries to postpone making decisions to the runtime as much as possible, an abstract method is okay to be declared but without implementations. This rule tries to verify the subclass implement the correct abstract method.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifySubclassMustImplementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifySubclassMustImplementRule.cpp>`_

**Example:**

.. code-block:: objective-c

    @interface Parent

    - (void)anAbstractMethod __attribute__((annotate("oclint:enforce[subclass must implement]")));

    @end

    @interface Child : Parent
    @end

    @implementation Child

    /*
    // Child, as a subclass of Parent, must implement anAbstractMethod
    - (void)anAbstractMethod {}
    */

    @end
