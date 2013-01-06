Cyclomatic Complexity
=====================

Cyclomatic complexity is determined by the number of decision points in a method plus one for the method entry. The decision points are ‘if’, ‘for’, ‘for-each’, ‘while’, ‘do’, ‘catch’, ‘case’, ‘&&’, ‘||’ and ‘?:’.

Parameters
----------

CYCLOMATIC_COMPLEXITY
    threshold for max allowed cyclomatic complexity, default is 7.

Examples
--------

Too Many Dicision Points
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: objective-c

    - (void)foo:(int)bar {              // + 1
      if (bar != 0) {                   // + 1
        while (YES) {                   // + 1
          switch (bar) {
            case 1:                     // + 1
              [self soSomething];
              break;
            case 2:                     // + 1
              [self doSomethingElse];
              break;
            case 3:                     // + 1
              [self nothingToDo];
              break;
            default:
              [self huh];
              break;
          }
          int b = (0 && 1) ? 2 : 3;     // + 2
          for (int i = 0; i < 0; i++) { // + 1
            [self neverReachHere];
          }
        }
      }
    }
