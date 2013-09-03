Compiling and Testing
=====================

We will go through some steps to build dependencies, compile and test OCLint in this document. In general, if you have followed the codebase structure as described in `this document <checkout.html>`_, we have scripts to gather all required steps and run them in order to facilitate the entire process.

.. warning:: if you need a release version OCLint binary for production use, please read `Building OCLint <../intro/build.html>`_ instead.

.. note:: This document presumes your current working directory is ``oclint/oclint-scripts``.

Building LLVM/Clang
-------------------

We could build LLVM/Clang in debug mode with assertions by

.. code-block:: bash

    ./buildClang.sh

Debug mode binaries contain additional data to aid debugging, but lowers program performances. It's recommended to build Clang in debug mode when we work on the analysis engine, metrics, and rules. These debug information may help a lot in some circumstances.

On the other side, if our work is related to violations, reporters, and surrounding submodules, we can still use debug mode, and we can also choose release mode that enables optimizations for better performance. To build LLVM/Clang in release mode, append ``release`` to the script as

.. code-block:: bash

    ./buildClang.sh release

It takes a while to build LLVM/Clang (probably much longer than a cup of coffee time). By default, this script builds the code by simultaneously using all the CPU resources. If building on one single core is preferred, e.g. for debugging build system issues, explicitly specify the number of cores to 1, like

.. code-block:: bash

    CPU_CORES=1 ./buildClang.sh

The LLVM/Clang build can be found at ``oclint/build/llvm`` directory, and its installation is located at ``oclint/build/llvm-install`` folder.

Building googletest/googlemock
------------------------------

Building Google C++ Testing and Mocking Frameworks is easy:

.. code-block:: bash

    ./buildGoogleTest.sh

Compiling and Testing OCLint
----------------------------

OCLint uses CMake as build system. We can find CMakeLists.txt in each module and its include sub-folders.

There are four scripts, ``testCore.sh``, ``testMetrics.sh``, ``testRules.sh``, and ``testReporters.sh`` for compiling and testing OCLint core module, metrics module, rules module, and reporters module respectively. Core module and metrics module can be compiled independently. However, rules module depends on both core and metrics modules, and reporters module depends on core module.

Each script has a ``clean`` option to remove old build intermediate files.

Scripts will show the CMake configuration process, compilation progress, and test results in order. ``testCore.sh`` will generate code coverage report in the end. When something goes wrong, scripts stop immediately with the following return code:

* **1** - CMake configuration failed
* **2** - Build failed
* **3** - Test failed
* **4** - Code coverage failed (for core module only)

Testing Core Module
^^^^^^^^^^^^^^^^^^^

Test core module:

.. code-block:: bash

    ./testCore.sh

Test core module with clean build:

.. code-block:: bash

    ./testCore.sh clean

In addition to the test results, code coverage report can be found in ``oclint/build/oclint-core-test/coveragereport`` folder. Please read the report by opening ``index.html`` with your browser.

Testing Metrics Module
^^^^^^^^^^^^^^^^^^^^^^

Test metrics module:

.. code-block:: bash

    ./testMetrics.sh

Test metrics module with clean build:

.. code-block:: bash

    ./testMetrics.sh clean

Testing Rules Module
^^^^^^^^^^^^^^^^^^^^

Test rules module:

.. code-block:: bash

    ./testRules.sh

Test rules module with clean build:

.. code-block:: bash

    ./testRules.sh clean

Testing Reporters Module
^^^^^^^^^^^^^^^^^^^^^^^^

Test reporters module:

.. code-block:: bash

    ./testReporters.sh

Test reporters module with clean build:

.. code-block:: bash

    ./testReporters.sh clean

Reviewing Test Results
^^^^^^^^^^^^^^^^^^^^^^

We could always go back and review our test results (unless we have cleaned test directory with ``clean`` option or delete that folder manually). There is an easy way to do it with ``showTestResults.sh`` script. It uses ``less`` utility to display the test results on terminal.

By default, it shows the test results for core module. We can also explicitly specify ``core`` as an option to it, like

.. code-block:: bash

    ./showTestResults.sh
    ./showTestResults.sh core

Show test results for metrics module:

.. code-block:: bash

    ./showTestResults.sh metrics

Show test results for rules module:

.. code-block:: bash

    ./showTestResults.sh rules

Show test results for reporters module:

.. code-block:: bash

    ./showTestResults.sh reporters




