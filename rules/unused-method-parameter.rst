Unused Method Parameter
=======================

Detects parameters of methods that never be used.

Examples
--------

Unused Parameter
^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (int)foo:(int)a {
      return 0;
    }
