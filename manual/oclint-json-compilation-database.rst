oclint-json-compilation-database Manual
=======================================

``oclint-json-compilation-database`` is a helper program that eases running OCLint against a set of source code files. Instead of specifying compiler flags for each file when ``oclint`` is invoked, these compiler flags could be collected and persistently saved to ``compile_commands.json`` file in JSON Compilation Database format.

.. seealso::

    Please read `JSON Compilation Database Format Specification`_ for detail.


``oclint-json-compilation-database`` can fetch necessary information from ``compile_commands.json`` and kick off ``oclint`` with these compiler flags under the hook for code analysis. See the usage by typing ``oclint-json-complication-database -help``::

    usage: oclint-json-compilation-database  [-h] [-v] [-debug] [-i INCLUDES]
                                             [-e EXCLUDES]
                                             [oclint_args [oclint_args ...]]

    OCLint for JSON Compilation Database (compile_commands.json)

    positional arguments:
      oclint_args           arguments that are passed to OCLint invocation

    optional arguments:
      -h, --help            show this help message and exit
      -v                    show invocation command with arguments
      -debug, --debug       invoke OCLint in debug mode
      -i INCLUDES, -include INCLUDES, --include INCLUDES
                            extract files matching pattern
      -e EXCLUDES, -exclude EXCLUDES, --exclude EXCLUDES
                            remove files matching pattern

Filter Options
--------------

\-i INCLUDES, -include INCLUDES, --include INCLUDES
    Extract files matching pattern from ``compile_commands.json`` or prior matching result
\-e EXCLUDES, -exclude EXCLUDES, --exclude EXCLUDES
    Remove files matching pattern from ``compile_commands.json`` or prior matching result

Sometimes, we may be interested in only a subset of entire codebase defined in ``compile_commands.json``, and just want to inspect these sources. To do that, we can use filter options to get this subset. Since ``oclint-json-compilation-database`` is written in Python, so the matching pattern needs to follow `Python regular expression syntax`_. In addition, multiple filters can be chained to get the file set we need for analysis.

For example, if files like ``Debug.m``, ``Port.m`` along with all tests files (saved under ``Test`` folder) need to be filtered out, try the following command or something similar:

.. code-block:: none

  oclint-json-compilation-database -e Debug.m -e Port.m -e Test

OCLint Options
--------------

Remember there are `many options <oclint.html>`_ that we can use to change the behavior of OCLint itself? Sure, and we can also ask ``oclint-json-compilation-database`` to pass through these options when it invokes ``oclint`` under the hook.

Since all compiler options are defined in ``compile_commands.json`` file, we don't need to tell ``oclint`` about them this time. But by following the same idea, now, the OCLint options can be given to ``oclint-json-compilation-database`` by appending ``--`` separator followed by all OCLint options:

.. code-block:: none

    oclint-json-compilation-database [<filter0> ... <filterN>] -- [oclint options]

Debug Options
-------------

\-v
    show invocation command with arguments
\-debug
    invoke OCLint in debug mode

``oclint-json-compilation-database`` generates ``oclint`` command with corresponding options based on our settings of all filters and OCLint options, and eventually call ``oclint`` for us. Debug option ``-v`` outputs the final ``oclint`` invocation command, it's helpful for debugging purposes, because if we run the generated ``oclint`` command directly in the console, we will get the identical result same as using ``oclint-json-compilation-database``.

More than that, if OCLint is built in the debug model, ``-debug`` outputs deeper message from OCLint invocation. It prints messages that can help understand the overall progress of OCLint analysis. Please aware that this is only available when OCLint is built with debug flag on.


.. _JSON Compilation Database Format Specification: http://clang.llvm.org/docs/JSONCompilationDatabase.html
.. _CMake Documentation: http://www.cmake.org/cmake/help/documentation.html
.. _Python regular expression syntax: http://docs.python.org/2/library/re.html#re-syntax

