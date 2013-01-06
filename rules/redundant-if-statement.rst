Redundant If Statement
======================

This rule reports instances of unnecessary if statements that can be simplified to a single assignment or return statement.

Examples
--------

Simplify Return
^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (BOOL)foo:(int)bar {
      if (bar == 1) {
        return YES;
      }
      else {
        return NO;
      }

      // can be simplified to:
      // return bar == 1;
    }

Simplify Assign
^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (BOOL)foo:(int)bar {
      BOOL b;
      if (bar == 1) {
        b = NO;
      }
      else {
        b = YES;
      }

      // can be simplified to:
      // b = (bar != 1);
    }
