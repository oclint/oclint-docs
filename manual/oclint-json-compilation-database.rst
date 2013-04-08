oclint-json-compilation-database Manual
=======================================

``oclint-json-compilation-database`` is a helper program that eases running OCLint against a set of source code files. Instead of specifying compiler flags for each file when ``oclint`` is invoked, these compiler flags could be collected and persistently saved to ``compile_commands.json`` file in JSON Compilation Database format.

.. seealso::

    Please read `JSON Compilation Database Format Specification`_ for detail.


``oclint-json-compilation-database`` can fetch necessary information from it and kick off ``oclint`` with these compiler flags under the hook for code analysis. See the usage by typing ``oclint-json-complication-database -help``::

    usage: oclint-json-compilation-database [-h] [-v] [-i INCLUDES] [-e EXCLUDES]
                                        [oclint_args [oclint_args ...]]

    OCLint for JSON Compilation Database (compile_commands.json)

    positional arguments:
      oclint_args           arguments that are passed to OCLint invocation

    optional arguments:
      -h, --help            show this help message and exit
      -v                    show invocation command with arguments
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

Sometimes, we may be interested in a subset of entire codebase defined in ``compile_commands.json``, and just want to inspect these sources. To do that, we can use filter options to get this subset. Since ``oclint-json-compilation-database`` is written in Python, so the matching pattern needs to follow `Python regular expression syntax`_. In addition, multiple filters can be chained to get the file set we need for analysis.

OCLint Options
--------------

Remember there are `many options <oclint.html>`_ that we can use to change the behavior of OCLint itself? Sure, but we can also ask ``oclint-json-compilation-database`` to pass through these options when it invokes ``oclint`` under the hook.

Since we have all compiler options in ``compile_commands.json`` file, so this time we don't need to tell ``oclint`` about them. But by following the same idea, now, these OCLint options can be given directly to ``oclint-json-compilation-database`` by appending ``--`` separator followed by all OCLint options:

.. code-block:: none

    oclint-json-compilation-database [<filter0> ... <filterN>] -- [oclint options]

Debug Options
-------------

\-v
    show invocation command with arguments

Debug options are used for us to see the final ``oclint`` invocation command according to our settings of all filters and OCLint options. If we run the generated ``oclint`` command directly in the console, we should get the identical result as using ``oclint-json-compilation-database``.


.. _JSON Compilation Database Format Specification: http://clang.llvm.org/docs/JSONCompilationDatabase.html
.. _CMake Documentation: http://www.cmake.org/cmake/help/documentation.html
.. _Python regular expression syntax: http://docs.python.org/2/library/re.html#re-syntax
