Empty If Statement
==================

Empty If Statement finds instances where a condition is checked but nothing is done about it.

Examples
--------

If Has Empty Block
^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (bar == 0) {
        // empty
      }
    }

If Block Is Null Statement
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (bar == 0);
    }

Else Has Empty Block
^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (bar == 0) {
        NSLog("Greetings!");
      }
      else {
        // empty
      }
    }

Else Block Is Null Statement
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (bar == 0) {
        NSLog("Greetings!");
      }
      else;
    }
