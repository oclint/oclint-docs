Compiling and Testing
=====================

We will go through some steps to build dependencies, compile and test OCLint in this document. In general, if you have followed the codebase structure as described in `this document <checkout.html>`_, we have scripts to gather all required steps and run them in order to facilitate the entire process.

.. warning:: if you need a release version OCLint binary for production use, please read `Building OCLint <../intro/build.html>`_ instead.

.. note:: This document presumes your current working directory is ``oclint/oclint-scripts``.

Building LLVM/Clang
-------------------

We could build LLVM/Clang in debug mode with assertions by

.. code-block:: bash

    ./clang build

Debug mode binaries contain additional data to aid debugging, but lowers program performances. It's recommended to build Clang in debug mode when we work on the analysis engine, metrics, and rules. These debug information may help a lot in some circumstances.

On the other side, if our work is related to violations, reporters, and surrounding submodules, we can still use debug mode, and we can also choose release mode that enables optimizations for better performance. To build LLVM/Clang in release mode, append ``release`` to the script as

.. code-block:: bash

    ./clang build -release

It takes a while to build LLVM/Clang (probably much longer than a cup of coffee time). By default, this script builds the code by simultaneously using all the CPU resources. But this can be changed by explicitly specifying number of concurrent processes for the compilation, like

.. code-block:: bash

    ./clang build -j <num>

The LLVM/Clang build can be found at ``oclint/build/llvm`` directory, and its installation is located at ``oclint/build/llvm-install`` folder.

Building googletest/googlemock
------------------------------

Building Google C++ Testing and Mocking Frameworks is easy:

.. code-block:: bash

    ./googleTest build

Compiling and Testing OCLint
----------------------------

OCLint uses CMake as build system. We can find CMakeLists.txt in each module and its include sub-folders.

``test`` script would compiles and tests OCLint core module, metrics module, rules module, and reporters module. With module name given, the script tests only for the particular module, otherwise, it tries to test all modules. Core module and metrics module can be compiled independently. However, rules module depends on both core and metrics modules, and reporters module depends on core module. When ``test`` script works with all modules, the required sequence is automatically enforced.

``test`` script has a ``-clean`` option to remove old build intermediate files.

``test`` script shows the CMake configuration process, compilation progress, and test results in order. It generates code coverage report in the end. When something goes wrong, scripts stop immediately. The possible reason of a failed build could be:

* CMake configuration failed
* Build failed
* Test failed
* Code coverage failed

Testing All Modules
^^^^^^^^^^^^^^^^^^^

Test every modules:

.. code-block:: bash

    ./test

Test all modules with clean build:

.. code-block:: bash

    ./test -clean

Testing Core Module
^^^^^^^^^^^^^^^^^^^

Test core module:

.. code-block:: bash

    ./test core

Test core module with clean build:

.. code-block:: bash

    ./test core -clean

Testing Metrics Module
^^^^^^^^^^^^^^^^^^^^^^

Test metrics module:

.. code-block:: bash

    ./test metrics

Test metrics module with clean build:

.. code-block:: bash

    ./test metrics -clean

Testing Rules Module
^^^^^^^^^^^^^^^^^^^^

Test rules module:

.. code-block:: bash

    ./test rules

Test rules module with clean build:

.. code-block:: bash

    ./test rules -clean

Testing Reporters Module
^^^^^^^^^^^^^^^^^^^^^^^^

Test reporters module:

.. code-block:: bash

    ./test reporters

Test reporters module with clean build:

.. code-block:: bash

    ./test reporters -clean

Reviewing Test Results
^^^^^^^^^^^^^^^^^^^^^^

We could always go back and review our test results (unless we have cleaned test directory with ``-clean`` option or delete that folder manually). There is an easy way to do it with ``-show`` option to the ``test`` script.

By default, it shows the test results for all modules. We can also explicitly specify the module name as an option to it. For example, show test result for all modules:

.. code-block:: bash

    ./test -show

Show test results for core module:

.. code-block:: bash

    ./test core -show 

Show test results for metrics module:

.. code-block:: bash

    ./test metrics -show

Show test results for rules module:

.. code-block:: bash

    ./test rules -show

Show test results for reporters module:

.. code-block:: bash

    ./test reporters -show
