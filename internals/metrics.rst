Metrics Module
==============

Metrics module is an isolated library that actually doesn't depend on any other OCLint modules. It means you can use this module separately in your project for metric measurements.

Cyclomatic Complexity
---------------------

Cyclomatic complexity was introduced by Thomas McCabe [25]. It is determined based on the number of decision points in a method.

NPath Complexity
----------------

NPath complexity measures the number of acyclic execution paths in a method [27]. It differs from cyclomatic complexity as it takes into account the nesting of conditional statements and multi-part boolean expressions.

Non Commenting Source Statements
--------------------------------

Non commeting source statements (NCSS) counts the number of all statements excluding comments, empty statements, empty blocks, closing brackets or semicolons after closing brackets.

Statement Depth
---------------

Statement depth is the number of nesting levels.


