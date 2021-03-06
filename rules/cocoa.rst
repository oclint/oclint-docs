Cocoa
=====

CallingProhibitedMethod
-----------------------

**Since: 0.10.1**

**Name: calling prohibited method**

When a method is declared with ``__attribute__((annotate("oclint:enforce[prohibited method]")))`` annotation, all of its usages will be prohibited.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifyProhibitedCallRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifyProhibitedCallRule.cpp>`_

**Example:**


.. code-block:: objective-c

    @interface A : NSObject
    - (void)foo __attribute__((annotate("oclint:enforce[prohibited method]")));
    @end

    @implementation A
    - (void)foo {
    }
    - (void)bar {
        [self foo]; // calling method `foo` is prohibited.
    }
    @end
    

CallingProtectedMethod
----------------------

**Since: 0.8**

**Name: calling protected method**

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
    

MissingAbstractMethodImplementation
-----------------------------------

**Since: 0.8**

**Name: missing abstract method implementation**

While Objective-C language allows abstract methods to be declared without implementations, this rule tries to verify if the subclass implements the correct abstract methods.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifySubclassMustImplementRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifySubclassMustImplementRule.cpp>`_

**Example:**


.. code-block:: objective-c

    @interface Parent

    - (void)anAbstractMethod __attribute__((annotate("oclint:enforce[abstract method]")));

    @end

    @interface Child : Parent
    @end

    @implementation Child

    /*
    // Child, as a subclass of Parent, must implement anAbstractMethod
    - (void)anAbstractMethod {}
    */

    @end
    

MissingCallToBaseMethod
-----------------------

**Since: 0.8**

**Name: missing call to base method**

When a method is declared with ``__attribute__((annotate("oclint:enforce[base method]")))`` annotation, all of its implementations (including its own and its subclasses) must call the method implementation in super class.

This rule is defined by the following class: `oclint-rules/rules/cocoa/ObjCVerifyMustCallSuperRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/cocoa/ObjCVerifyMustCallSuperRule.cpp>`_

**Example:**


.. code-block:: objective-c

    @interface UIView (OCLintStaticChecks)
    - (void)layoutSubviews __attribute__((annotate("oclint:enforce[base method]")));
    @end

    @interface CustomView : UIView
    @end

    @implementation CustomView

    - (void)layoutSubviews {
        // [super layoutSubviews]; is enforced here
    }

    @end
    

MissingHashMethod
-----------------

**Since: 0.8**

**Name: missing hash method**

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
    


.. Generated on Sat Mar  6 11:00:31 2021

