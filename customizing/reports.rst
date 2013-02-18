Customizing Reports
===================

OCLint currently supports plain text report and HTML report.

Report module is extracted from core module to make it easier for developing custom report renderers.

Report Options
--------------

Usually we don't need to explicit specify ``-report-type text`` flag as plain text report is the default. In order to see HTML report, add ``-report-type html`` to ``oclint`` command.

Since browser is a good place to view HTML report. HTML report is better to be redirected to a file instead of console. It's easy to achieve this with ``-o <path>`` option.

Plain Text Report
-----------------

Plain text report is designed for direct console output.

Report starts with the summary of the inspection, it consists of number of total files, number of files with violations, and number of violations of three priorities.

The output of each violation is formatted similar to compiler errors. Each line in the report indicates a violation. It starts with the file name, line, and column of the source code that the violation stands for. The name of the violated rule is printed after, followed by the priority of the rule. OCLint also outputs descriptions if current violation has any.

HTML Report
-----------

HTML reporter is browser friendly with better readability. The entire report follows the same order as the text report, but with a nicer structure of sections, paragraphs, and annotations. Violations are highlighted with different colors according to the priority.

.. seealso::

    You can `write your own reporters <../devel/reporters.html>`_ to extend OCLint with more capabilities.
