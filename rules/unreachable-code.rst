Unreachable Code
================

Code after the return, break, continue and goto statements is not reachable.

Examples
--------

Code After Return
^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      id anArray;
      for (id item in anArray) {
        return;
        int i = 1;
        i++;
      }
    }

Code After Break
^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (int)foo {
      while(1) {
        break;
        int i = 1;
        i++;
      }
      return 0;
    }

Code After Continue
^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (int)foo {
      do {
        continue;
        int i = 1;
        i++;
      } while(1);
      return 0;
    }
