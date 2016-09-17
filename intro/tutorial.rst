Tutorial
========

This tutorial walks you through the inspection of a piece of small but smelly C++ source code. By the end of this tutorial, you should be able to

* apply OCLint on a single file
* configure OCLint with very basic compiler flags
* understand the output

Throughout this tutorial, we will also lead you to the detail pages if you are interested in certain steps and are willing to know more.

Something Smells Here
---------------------

Create a ``sample.cpp`` file with the content below:

.. code-block:: c++

    int main() {
        int i = 0, j = 1;
        if (j) {
            if (i) {
                return 1;
                j = 0;
            }
        }
        return 0;
    }

Building Sample Code (Optional)
-------------------------------

It is actually not necessary to build the code prior to run OCLint against it. However, since finding the correct arguments becomes one of the most frequently asked questions, this step is trying to help convert the compiler flags to the ones that OCLint requires.

.. note:: This step, however, doesn't intent to show how to find the correct compiler flags, thus, some level of knowledge about compiler flags is a prerequisite.

.. code-block:: bash

    $ CC -c sample.cpp // step 1: compiling generates sample.o
    $ CC -o sample sample.o // step 2: linking generates sample executable file

    // Change CC to your favorite compiler that is GCC-compatible, e.g. g++ and clang++

    $ ./sample // execute the binary
    $ echo $? // output of 0 probably means the code has been successfully built

We just took two sequential steps to generate the binary, step 1 compiles the code, and step 2 links. We are only interested in step 1 because that's all compiler flags we need to give to OCLint. Here in this case, the compiler flag is ``-c``, and inspected source file is ``sample.cpp``.

If you cannot pass through this step, don't give up, there are some tools try to help, like `CMake <../guide/cmake.html>`_ and `Bear <../guide/bear.html>`_ (for Make). In addition, we also provide two helper programs `oclint-json-compilation-database <../manual/oclint-json-compilation-database.html>`_ and `oclint-xcodebuild <../guide/oclint-xcodebuild.html>`_ (for Xcode users) could help find the arguments for OCLint.

Checking Single File
--------------------

OCLint checks a single file using the following format:

.. code-block:: none

    oclint [options] <source> -- [compiler flags]

So, the command that applies to the sample source is

.. code-block:: bash

    $ oclint sample.cpp -- -c

To change OCLint behavior, change the ``[options]`` before the source; to alter the compiler behavior, change the ``[compiler flags]`` after the ``--`` separator. A complicated example might look like this:

.. code-block:: bash

    $ oclint -report-type html -o report.html sample.cpp -- -D__STDC_CONSTANT_MACROS -D__STDC_LIMIT_MACROS -I/usr/include -I/usr/local/include -c

For detail about OCLint options, see `oclint manual <../manual/oclint.html>`_.

For Projects with Multiple Files
--------------------------------

The approach described in the previous section works perfectly for a single file or a few files. The inspection process is fast, and making changes to arguments is easy.

While working on a project with a group of source files, inspecting the entire project at once and having a single report is preferred.

When all sources share the same compiler flags, we can do

.. code-block:: none

    oclint [options]  <source0> [... <sourceN>] -- [compiler flags]

However, each source file may have different compiler flags. In this case, by reading from the **compilation database**, OCLint can recognize the list of source files for analysis, along with the compiler flags used for each time during the compilation phase. It can be considered as a condensed Makefile. So, in this case

.. code-block:: none

    oclint -p <build-path> [other options]  <source0> [... <sourceN>]

A more handy helper program that comes with OCLint is `oclint-json-compilation-database <../manual/oclint-json-compilation-database.html>`_. If you use OCLint to analyze projects, for most of the time, you will deal with ``oclint-json-compilation-database`` instead, and indirectly talk to ``oclint``.

For people who work on a Mac with Xcode as IDE, you may find `Using OCLint with xcodebuild <../guide/xcodebuild.html>`_ and `Using OCLint in Xcode <../guide/xcode.html>` documents are helpful.

We also provide guidances for people who use `CMake <../guide/cmake.html>`_ and `make <../guide/bear.html>`_ as their build system.

Understanding Report
--------------------

By applying OCLint against the above sample, with the default text reporter, the output is similar to this::

    Processing: /path/to/sample.cpp.
    OCLint Report

    Summary: TotalFiles=1 FilesWithViolations=1 P1=0 P2=1 P3=1

    /path/to/sample.cpp:4:9: collapsible if statements P3
    /path/to/sample.cpp:9:17: dead code P2

    [OCLint (http://oclint.org) v0.8]

Basically, the following information can be found in the report:

* Summary

  * total files
  * files with violations
  * number of priority 1 violations
  * number of priority 2 violations
  * number of priority 3 violations

* A list of violations

  * path to the source file
  * line number
  * column number
  * violated rule
  * priority
  * message (if any)

* Compiler diagnostics

  * compiler errors if any
  * compiler warning if any
  * clang static analyzer results when it is enabled

* OCLint information

  * website
  * release version

Read more about `picking up the right reporter <../howto/selectreporters.html>`_.

Next, more detail information can be found with comprehensive `manuals <../manual/index.html>`_ and `user guides <../guide/index.html>`_. In addition, a few `how-to documents <../howto/index.html>`_ can help speed things up a little bit in several aspects.

.. _static code analysis: http://en.wikipedia.org/wiki/Static_program_analysis
