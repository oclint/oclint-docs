Metrics Module
==============

Metrics module is an isolated library. THis module actually doesn't depend on any other OCLint modules. It means we can use this module separately in other projects that also measure the metrics of the source code.

Cyclomatic Complexity
---------------------

Cyclomatic complexity was introduced by Thomas McCabe. It is determined based on the number of decision points in a method.

NPath Complexity
----------------

NPath complexity measures the number of acyclic execution paths in a method. It differs from cyclomatic complexity as it takes into account the nesting of conditional statements and multi-part boolean expressions.

Non Commenting Source Statements
--------------------------------

Non commeting source statements (NCSS) counts the number of all statements excluding comments, empty statements, empty blocks, closing brackets or semicolons after closing brackets.

Statement Depth
---------------

Statement depth is the number of nesting levels.


