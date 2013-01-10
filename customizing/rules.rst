Customizing Rules
=================

OCLint is a rule based code analysis tool. Rule system is designed to be very extensible and flexible. So it's easy to customize rules in many ways, like making particular ruleset for certain projects, categorize them and load them from different locations, change the behavior of rules during runtime. You can even easily write your own custom rules, and plug them into OCLint system without rebuilding OCLint. You can find how to customize rules in this document, and how to custom rules in another page.

Selecting Rules for Inspection
------------------------------

By default, rules will be loaded from ``$(/path/to/bin/oclint)/../lib/oclint/rules`` directory, we name it **rule search path**. You can change the rule search path with ``-R <directory>`` option. Multiple locations can be specified, and rules in all these directories will be loaded.

Rule directory consists of a group of dynamic libraries, with extension ``.so`` in Linux and ``.dylib`` in Mac OS X. You can easily copy a subset of these rules into another folder, and use this new ruleset for particular projects. We call this *plug-and-use* rule loading mechanism - all dynamic libraries are loaded when OCLint searches through rule loading paths. So, when certain rules do not suite your project, simply remove them; and dragging and dropping new rules into the rule loading paths makes them immediate available for use.

Rule Thresholds
---------------

Certain rules emit violations only when the metrics of the source code exceed the thresholds. For example, according to [McCabe76]_, a reasonable cyclomatic complexity number for a method should be less than 10. So, default threshold in CyclomaticComplexityRule is set to 10. However, this value may not be the best for your project, you might either be okay with a more complicated codebase or you decide to push your team hard with a more restrict threshold. Then you can change this threshold by using ``-rc CYCLOMATIC_COMPLEXITY=<new_value>`` option.

Here is a list of all thresholds defined in OCLint |release|:

CYCLOMATIC_COMPLEXITY
    Cyclomatic complexity of a method, default value is 10
LONG_CLASS
    Number of lines for a C++ class or Objective-C interface, category, protocol, and implementation, default value is 1000
LONG_LINE
    Number of characters for one line of code, default value is 100
LONG_METHOD
    Number of lines for a method or function, default value is 50
MINIMUM_CASES_IN_SWITCH
    Count of case statements in a switch statement, default value is 3
NPATH_COMPLEXITY
    NPath complexity of a method, default value is 200
NCSS_METHOD
    Number of non-commenting source statements of a method, default value is 30
NESTED_BLOCK_DEPTH
    Depth of a block or compound statement, default value is 5

.. Write your own rules

.. [McCabe76] McCabe, T. J. (1976). A Complexity Measure. IEEE Transactions on Software Engineering, SE-2(4), 308-320. doi:10.1109/TSE.1976.233837
