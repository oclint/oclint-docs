NPath Complexity
================

The NPath complexity of a method is the number of acyclic execution paths through that method.

Parameters
----------

NPATH_COMPLEXITY
    threshold for max allowed NPath complexity, default is 200.

Examples
--------

High NPath Complexity
^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo {
      if(1) {} // 2
      if(1) {} // 4
      if(1) {} // 8
      if(1) {} // 16
      if(1) {} // 32
      if(1) {} // 64
      if(1) {} // 128
      if(1) {} // 256, BOOM!
    }
