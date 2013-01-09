Using oclint-json-compilation-database
======================================

OCLint needs a compilation database to figure out the compiler options for parsing each file, so that it can run more accurate analysis on an intermediate representation of the source code. This document provides instructions about generaing ``compile_commands.json`` (JSON Compilation Database), and use ``oclint-json-compilation-database`` for code analysis.

JSON Compilation Database
-------------------------

A JSON Compilation Database, file name ``compile_commands.json``, maintains a list of source code files with related build options. For each source file, working directory and command for compiling the source code are explicitly givin. For example:

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

Using CMake
-----------

`CMake`_ is a cross-platform build system. It can also help generate the required ``compile_commands.json`` compilation database.



.. _JSON Compilation Database Format Specification: http://clang.llvm.org/docs/JSONCompilationDatabase.html
.. _CMake: http://www.cmake.org/

