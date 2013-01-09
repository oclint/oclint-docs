Customizing Reports
===================

OCLint supports plain text report and HTML report today.

Report module will be extracted from core module to make it easier for developing custom report renderers. In addition, some report types are under development for largely used continuous integration system, and they are high priority tasks in the current release cycle.

Report Options
--------------

Usually you don't need to explicit specify ``-text`` flag as plain text report is the default. In order to see HTML report, add ``-html`` to OCLint command.

Since browser is a good place to view HTML report, it is better to be redirected the output to a file instead of console. It's easy with ``-o <path>`` option.

Plain Text Report
-----------------

Plain text report is designed for direct console output.

Report starts with the summary of the inspection, it consists of 

The output of each violation is formatted similar to compiler errors. Each line in the report indicates a violation. It starts with the file name, line, and column of the source code that the violation stands for. The name of the violated rule is printed after, followed by the priority of the rule. OCLint also outputs descriptions to the console if current violation has any.

HTML Report
-----------

HTML reporter is browser friendly with better readability. The entire report follows the same order as the text report, but with a nicer structure of sections, paragraphs, and annotations. Violations are highlighted with different colors according to the priority.
