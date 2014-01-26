Customize Rule Thresholds
=========================

Rule system in OCLint is designed to be very flexible and dynamic for various development cultures in many ways. Particularly, this document will go through customizing the behaviors of the rules by changing the thresholds.

Certain rules emit violations only when the metrics of the source code exceed the thresholds. For example, according to [McCabe76]_, a reasonable cyclomatic complexity number for a method should be less than 10. So, default threshold in CyclomaticComplexityRule is set to 10. However, this value may not be the best for a very project. For instance, a more sophisticated legacy codebase comes with high complexity, or on the other side, one team may in the middle of pushing a much more strict coding standard. For these cases, customizations can be achieved by changing thresholds.

Command Line Usages
-------------------

Customizing thresholds by appending ``-rc <threshold_name>=<new_value>`` option to the command line invocation. Multiple ``-rc``s are accepted for changing more than one thresholds. When multiple values are given to the same threshold, the last one will be taken and overrides the default or existing custom values in the configuration files. For example, in order to change cyclomatic complexity number to 15, but to lower the long line to 50, following command can be given::

    -rc CYCLOMATIC_COMPLEXITY=15 -rc LONG_LINE=50

Configuration File
------------------

When the entire team shares the same standard, it's recommended to define the thresholds in a configuration file, and check in the file into source code system. So that OCLint behaves consistently within the team. The section for changing thresholds is::

    rule-configurations:
      - key: THRESHOLD_1
        value: new_value_1
      - key: THRESHOLD_2
        value: new_value_2
      ...

For the same example, changing cyclomatic complexity number to 15 and lowering the long line threshold to 50 can also be achieved by putting the following into project's ``.oclint`` file::

    rule-configurations:
      - key: CYCLOMATIC_COMPLEXITY
        value: 15
      - key: LONG_LINE
        value: 50

Available Thresholds
--------------------

Here is a list of all thresholds defined in OCLint |release|:

+-------------------------+------------------------------------------------------------------------------------------------+---------+
|           Name          |                                          Description                                           | Default |
+=========================+================================================================================================+=========+
| CYCLOMATIC_COMPLEXITY   | Cyclomatic complexity of a method                                                              |      10 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| LONG_CLASS              | Number of lines for a C class or Objective-C interface, category, protocol, and implementation |    1000 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| LONG_LINE               | Number of characters for one line of code                                                      |     100 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| LONG_METHOD             | Number of lines for a method or function                                                       |      50 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| LONG_VARIABLE_NAME      | Number of characters for a variable name                                                       |      20 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| MAXIMUM_IF_LENGTH       | Number of lines for the ``if`` block that would prefer an early exists                         |      15 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| MINIMUM_CASES_IN_SWITCH | Count of case statements in a switch statement                                                 |       3 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| NPATH_COMPLEXITY        | NPath complexity of a method                                                                   |     200 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| NCSS_METHOD             | Number of non-commenting source statements of a method                                         |      30 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| NESTED_BLOCK_DEPTH      | Depth of a block or compound statement                                                         |       5 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| SHORT_VARIABLE_NAME     | Number of characters for a variable name                                                       |       3 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| TOO_MANY_FIELDS         | Number of fields of a class                                                                    |      20 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| TOO_MANY_METHODS        | Number of methods of a class                                                                   |      30 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+
| TOO_MANY_PARAMETERS     | Number of parameters of a method                                                               |      10 |
+-------------------------+------------------------------------------------------------------------------------------------+---------+


.. seealso::

    `OCLint configuration file <rcfile.html>`_
        Documentation for OCLint configuration file

    `Rule Selection <selectrules.html>`_
        Documentation of picking up the right rules for analysis

    `Write Own Rules <../devel/rules.html>`_
        Documentation of modifying existing rule code or even write own rules to gain more capabilities.

.. [McCabe76] McCabe, T. J. (1976). A Complexity Measure. IEEE Transactions on Software Engineering, SE-2(4), 308-320. doi:10.1109/TSE.1976.233837

