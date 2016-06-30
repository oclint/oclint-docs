Migration
=========

ReplaceWithBoxedExpression
--------------------------

**Since: 0.7**

This rule locates the places that can be migrated to the new Objective-C literals with boxed expressions.

This rule is defined by the following class: `oclint-rules/rules/migration/ObjCBoxedExpressionsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/migration/ObjCBoxedExpressionsRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void aMethod()
    {
        NSNumber *fortyTwo = [NSNumber numberWithInt:(43 - 1)];
        // NSNumber *fortyTwo = @(43 - 1);

        NSString *env = [NSString stringWithUTF8String:getenv("PATH")];
        // NSString *env = @(getenv("PATH"));
    }
        

ReplaceWithContainerLiteral
---------------------------

**Since: 0.7**

This rule locates the places that can be migrated to the new Objective-C literals with container literals.

This rule is defined by the following class: `oclint-rules/rules/migration/ObjCContainerLiteralsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/migration/ObjCContainerLiteralsRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void aMethod()
    {
        NSArray *a = [NSArray arrayWithObjects:@1, @2, @3, nil];
        // NSArray *a = @[ @1, @2, @3 ];

        NSDictionary *d = [NSDictionary dictionaryWithObjects:@[@2,@4] forKeys:@[@1,@3]];
        // NSDictionary *d = @{ @1 : @2, @3 : @4 };
    }
        

ReplaceWithNumberLiteral
------------------------

**Since: 0.7**

This rule locates the places that can be migrated to the new Objective-C literals with number literals.

This rule is defined by the following class: `oclint-rules/rules/migration/ObjCNSNumberLiteralsRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/migration/ObjCNSNumberLiteralsRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void aMethod()
    {
        NSNumber *fortyTwo = [NSNumber numberWithInt:42];
        // NSNumber *fortyTwo = @42;

        NSNumber *yesBool = [NSNumber numberWithBool:YES];
        // NSNumber *yesBool = @YES;
    }
        

ReplaceWithObjectSubscripting
-----------------------------

**Since: 0.7**

This rule locates the places that can be migrated to the new Objective-C literals with object subscripting.

This rule is defined by the following class: `oclint-rules/rules/migration/ObjCObjectSubscriptingRule.cpp <https://github.com/oclint/oclint/blob/master/oclint-rules/rules/migration/ObjCObjectSubscriptingRule.cpp>`_

**Example:**


.. code-block:: objective-c

    void aMethod(NSArray *a, NSDictionary *d)
    {
        id item = [a objectAtIndex:0];
        // id item = a[0];

        id item = [d objectForKey:@1];
        // id item = d[@1];
    }
        


.. Generated on Wed Jun 29 21:59:34 2016

