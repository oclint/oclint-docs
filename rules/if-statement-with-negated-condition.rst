If Statement With Negated Condition
===================================

In an “if” expression with an “else” block, avoid negation in the condition to make the code easier to read.

Examples
--------

Negated Condition
^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (bar != 0) {
        [self diff];
      }
      else {
        [self same];
      }

      /* should be refactored to
      if (bar == 0) {
        [self same];
      }
      else {
        [self diff];
      }
      */
    }
