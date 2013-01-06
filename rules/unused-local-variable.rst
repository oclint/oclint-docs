Unused Local Variable
=====================

Detects when a local variable is declared and/or assigned, but not used.

Examples
--------

Unused Variable
^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (int)foo {
      int a;
      return 0;
    }
