Customizing Reports
===================

OCLint currently supports generating multiple types of reports based on the demands of different use cases. The generation for each report type is handled by a reporter. All reporters are collected in ``oclint-reporters`` module.

.. seealso::

    You can `write your own reporters <../devel/reporters.html>`_ to extend OCLint with more capabilities.

Report Options
--------------

OCLint uses plain text reporter by default, so usually we don't need to explicitly specify ``-report-type text`` flag. In order to use other reporter, add ``-report-type <report_name>`` to ``oclint`` command.

Some reports are better to be viewed in places other than the console. For example, web browser is a good place for reading HTML reports, and PMD report has a better visual rendering effect in continuous integration systems like Jenkins. In these cases, ``-o <path>`` option can help redirect the report to a file instead of console.

By combining both options, for example, outputting the result in HTML format to ``oclint_result.html`` file can be achieved by

.. code-block:: bash

    oclint -report-type html -o oclint_result.html <sources> -- <compiler_flags>

Report Types
------------

We currently have the following reporters. The names in the parentheses are the values we are going to use for ``report-type`` option.

Plain Text Report (text)
^^^^^^^^^^^^^^^^^^^^^^^^

Plain text report is designed for directly outputting results to console.

Report starts with the summary of the inspection, it consists of number of total files, number of files with violations, and number of violations for three different priorities.

The output of each violation is formatted similar to compiler errors. Each line in the report indicates a violation. It starts with the file name, line, and column of the source code that the violation occurs. The name of the violated rule is printed after, followed by the priority of the rule. OCLint also outputs descriptions if current violation has any.

`Sample text report <../_static/sample-reports/sample.txt>`_

HTML Report (html)
^^^^^^^^^^^^^^^^^^

HTML reporter is browser friendly with better readability. The entire report follows the same order as the text report, but with a nicer structure of sections, paragraphs, and annotations. Violations are highlighted with different colors according to the priority.

`Sample HTML report <../_static/sample-reports/sample.html>`_

XML Report (xml)
^^^^^^^^^^^^^^^^

XML reporter produces an XML report of the results.

.. note::

    This XML format is still being refined and is subject to change. 

`Sample XML report <../_static/sample-reports/sample.xml>`_

JSON Reporter (json)
^^^^^^^^^^^^^^^^^^^^

JSON reporter produces an JSON report of the results.

.. note::

    This JSON format is still being refined and is subject to change.

`Sample JSON report <../_static/sample-reports/sample.json>`_

PMD Reporter (pmd)
^^^^^^^^^^^^^^^^^^

Since many existing continuous integration (CI) systems support `PMD <http://pmd.sourceforge.net/>`_ for Java developers, PMD reporter outputs the XML report that follows the PMD report format. So that these CI systems can pick up the output and render better graphic results.

`Sample PMD report <../_static/sample-reports/sample-pmd.xml>`_

.. seealso::

    We feel grateful if you could help us `write plugins for continuous integration systems <../devel/openings.html#more-reporters>`_.
