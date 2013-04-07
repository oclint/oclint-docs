Using oclint-json-compilation-database
======================================

``oclint-json-compilation-database`` is a helper program that eases running OCLint against a set of source code files. Instead of specifying compiler flags for each file when ``oclint`` is invoked, these compiler flags could be collected and persistently saved into JSON Compilation Database format. ``oclint-json-compilation-database`` fetches necessary information from it and kicks off ``oclint`` with these compiler flags under the hook for code analysis.

JSON Compilation Database
-------------------------

A JSON Compilation Database, file name ``compile_commands.json``, maintains a list of source code files with related build options. For each source file, working directory and command for compiling the source code are explicitly given. For example:

.. code-block:: json

    [
        {
          "directory": "/Projects/oclint/build",
          "command": "/Projects/llvm/bin/clang++   -D__STDC_LIMIT_MACROS -D__STDC_CONSTANT_MACROS  -O0 -g -fno-rtti -Wno-c++11-extensions -fPIC -I/Projects/llvm/include -I/Projects/oclint/headers -o CMakeFiles/oclint.dir/main.cpp.o -c /Projects/oclint/main.cpp",
          "file": "/Projects/oclint/main.cpp"
        },
        {
          "directory": "/Projects/oclint/build/impl/core",
          "command": "/Projects/llvm/bin/clang++   -D__STDC_LIMIT_MACROS -D__STDC_CONSTANT_MACROS  -O0 -g -fno-rtti -Wno-c++11-extensions -fPIC -I/Projects/llvm/include -I/Projects/oclint/headers -o CMakeFiles/OCLintCore.dir/Violation.cpp.o -c /Projects/oclint/impl/core/Violation.cpp",
          "file": "/Projects/oclint/impl/core/Violation.cpp"
        },
        {
          "directory": "/Projects/oclint/build/impl/core",
          "command": "/Projects/llvm/bin/clang++   -D__STDC_LIMIT_MACROS -D__STDC_CONSTANT_MACROS  -O0 -g -fno-rtti -Wno-c++11-extensions -fPIC -I/Projects/llvm/include -I/Projects/oclint/headers -o CMakeFiles/OCLintCore.dir/ViolationSet.cpp.o -c /Projects/oclint/impl/core/ViolationSet.cpp",
          "file": "/Projects/oclint/impl/core/ViolationSet.cpp"
        }
    ]

See `JSON Compilation Database Format Specification`_ with more precise defination.

Generating JSON Compilation Database
------------------------------------

There are three approaches for generating JSON Compilation Database - writing our own, using CMake, and using OCLint xcodebuild helper program.

Writing Our Own
^^^^^^^^^^^^^^^

We can follow the format defined in `JSON Compilation Database Format Specification`_, and write our own ``compile_commands.json`` file. It is convenient when we have only a few sources to inspect.

Other than this, we certainly need some tools' help when we have a large project.

Using CMake
^^^^^^^^^^^

`CMake`_ is a cross-platform build system. It can also help generate the required ``compile_commands.json`` compilation database.

Read `CMake Documentation`_ about how to use CMake as our build system.

We need to tell CMake that we are expecting ``compile_commands.json`` to be generated, so that when CMake converts its ``CMakeLists.txt`` to regular ``Makefile``, it outputs ``compile_commands.json`` file for us along the way. To do this, add one extra option to our CMake command, for example:

.. code-block:: bash

    cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON path/to/source-root

As a result, the ``compile_commands.json`` file is generated in current folder.

We can leave it here in the build directory, and use ``-p`` option for ``oclint`` to `specify this file <oclint.html#compile-command-database>`_.

But in order to use ``oclint-json-compilation-database``, it's required to copy or link this file to our source directory, for example:

.. code-block:: bash

    ln -s `pwd`/compile_commands.json /path/to/source-root

Using OCLint xcodebuild Helper Program
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you are a Xcode user, then we have a helper program that extracts adequate compiler options and convert them into ``compile_commands.json`` file. Read `how to use oclint-xcodebuild <oclint-xcodebuild.html>`_ for instructions.

oclint-json-compilation-database Usage
--------------------------------------

Since we have ``compile_commands.json`` file copied or linked, we can now simply run ``oclint-json-compilation-database`` in our source directory. It reads the ``compile_commands.json`` file, get the list of all source files, and pass them to ``oclint`` for analysis.

See the usage by typing ``oclint-json-complication-database -help``::

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
^^^^^^^^^^^^^^

\-i INCLUDES, -include INCLUDES, --include INCLUDES
    Extract files matching pattern from ``compile_commands.json`` or prior matching result
\-e EXCLUDES, -exclude EXCLUDES, --exclude EXCLUDES
    Remove files matching pattern from ``compile_commands.json`` or prior matching result

Sometimes, we may be interested in a subset of entire codebase defined in ``compile_commands.json``, and just want to inspect these sources. To do that, we can use filter options to get this subset. Since ``oclint-json-compilation-database`` is written in Python, so the matching pattern needs to follow `Python regular expression syntax`_. In addition, multiple filters can be chained to get the file set we need for analysis.

OCLint Options
^^^^^^^^^^^^^^

Remember there are `many options <oclint.html>`_ that we can use to change the behavior of OCLint itself? Sure, but we can also ask ``oclint-json-compilation-database`` to pass through these options when it invokes ``oclint`` under the hook.

Since we have all compiler options in ``compile_commands.json`` file, so this time we don't need to tell ``oclint`` about them. But by following the same idea, now, these OCLint options can be given directly to ``oclint-json-compilation-database`` by appending ``--`` separator followed by all OCLint options:

.. code-block:: none

    oclint-json-compilation-database [<filter0> ... <filterN>] -- [oclint options]

Debug Options
^^^^^^^^^^^^^

\-v
    show invocation command with arguments

Debug options are used for us to see the final ``oclint`` invocation command according to our settings of all filters and OCLint options. If we run the generated ``oclint`` command directly in the console, we should get the identical result as using ``oclint-json-compilation-database``.


.. _JSON Compilation Database Format Specification: http://clang.llvm.org/docs/JSONCompilationDatabase.html
.. _CMake: http://www.cmake.org/
.. _CMake Documentation: http://www.cmake.org/cmake/help/documentation.html
.. _Python regular expression syntax: http://docs.python.org/2/library/re.html#re-syntax

