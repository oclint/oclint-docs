Long Parameter List
===================

Long parameter lists can indicate that a new object should be created to wrap the numerous parameters.

Parameters
----------

NUMBER_OF_PARAMETERS
    threshold for max allowed number of parameters in a method declaration, default is 3.

Examples
--------

Long Parameter List
^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)param1 param2:(int)param2 param3:(int)param3 param4:(int)param4 {
      [self bar];
    }
