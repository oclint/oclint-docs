Redundant Local Variable
========================

Local variables that are immediately returned is unnecessary, which add nothing to the comprehensibility of a method, and can be simplified.

Examples
--------

Redundant Local Variable
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (int)foo {
      int i = 1;
      return i;

      // can be simplified to:
      // return 1;
    }
