Long Method
===========

Long method are indications that this method may be trying to do too much.

Parameters
----------

METHOD_LENGTH
    threshold for max allowed number of statements in a method, default is 6.

Examples
--------

Long Method
^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {
      if (1) {}
      if (2) {}
      if (3) {}
      if (4) {}
      if (5) {}
      if (6) {}
      if (7) {}
    }
