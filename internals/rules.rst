Rules Module
============

OCLint is a rule based tools. Rules are dynamic libraries that can be easily loaded into system during runtime. It largely makes the tool very extensible. In addition, by following `Open/Close Principle <http://en.wikipedia.org/wiki/Open/closed_principle>`_, OCLint is very open to new rules by dynamically loading extended rules without modifying or recompiling itself,

All the rules are implemented as a subclass of ``RuleBase``. They generally fall in two big categories - rules by reading the source code line by line, and the ones by recognizing patterns in the abstract syntax tree (AST).

Rules that belong to the first category can leverage the abstract class ``AbstractSourceCodeReaderRule`` to go through each line of the source code.

For rules that are interested in AST, we provide two detail approaches - AST visitor and AST matcher.

In AST visitor approach, by following the `Visitor Pattern <http://en.wikipedia.org/wiki/Visitor_pattern>`_, the entire AST is traversed recursively from the root of the tree. Each node is visited in a `depth-first preorder traversal <http://en.wikipedia.org/wiki/Tree_traversal>`_. The visitor usually returns after all nodes are visited. However, we can interrupt the traversal by intent, for example, when we are only curious about if certain patterns exist rather than how many of them, in this case, whenever that pattern is matched, we could stop the visitor to avoid wasting more resources, so that the performance is improved.

Tree traversal is very mature and powerful, we can achieve almost everything with it. But it's not that intuitive to some extents. So, AST matcher, on the other hand, can help write lightweight code with better readability.

The way to think about AST matcher to AST is like XPath to XML. Specific patterns in AST are described in a simple, concise, and descriptive representation. Although it's implemented by AST visitor under the hook, the matcher expression makes it more friendly when people who read the code try to understand what the rule actually does. For example, in order to find an if statement, we can simple write our matcher like

.. code-block:: c++

    ifStmt()

When we want to narrow our search criteria for a particular group of if statements, let's say, a if statement with a binary operator that compares if two variables are equal, then we can extend the above matcher to

.. code-block:: c++

    ifStmt(hasCondition(binaryOperator(hasOperatorName("&&"))))

It can be read just like a sentence.

Using AST matchers has more restrictions than AST visitor, and it takes much longer time in analysis, this could lower the performance of the tool. So, we always have to consider the trade-off, and choose wisely.
