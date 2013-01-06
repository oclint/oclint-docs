Constant If Statement
=====================

If statements that are always true or always false.

Examples
--------

Always True
^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      if (YES) {
        [self bar];
      }
    }

Constant Variable
^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      if (1.23) {
        [self bar];
      }
    }

Constant Comparison Result
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      if (1 == 1) { // always true
        [self bar];
      }
    }

Constant Conditioanl Result
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      if (1 ? 0 : [self whatever]) { // always false no matter the result of whatever() method
        [self bar];
      }
    }

