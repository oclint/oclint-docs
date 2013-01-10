Customizing Reports
===================

OCLint currently supports plain text report and HTML report.

Report module will be extracted from core module to make it easier for developing custom report renderers. In addition, some report types are under development for largely used continuous integration system, and they are high priority tasks in the next release cycle (version 0.7).

Report Options
--------------

Usually you don't need to explicit specify ``-text`` flag as plain text report is the default. In order to see HTML report, add ``-html`` to ``oclint`` command.

Since browser is a good place to view HTML report. HTML report is better to be redirected to a file instead of console. It's easy to achieve this with ``-o <path>`` option.

Plain Text Report
-----------------

Plain text report is designed for direct console output.

Report starts with the summary of the inspection, it consists of number of total files, number of files with violations, and number of violations of three priorities.

The output of each violation is formatted similar to compiler errors. Each line in the report indicates a violation. It starts with the file name, line, and column of the source code that the violation stands for. The name of the violated rule is printed after, followed by the priority of the rule. OCLint also outputs descriptions if current violation has any.

HTML Report
-----------

HTML reporter is browser friendly with better readability. The entire report follows the same order as the text report, but with a nicer structure of sections, paragraphs, and annotations. Violations are highlighted with different colors according to the priority.
