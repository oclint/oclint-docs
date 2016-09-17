System Requirements
===================

OCLint can be compiled on all unix-like systems, theoretically. Latest macOS, FreeBSD, and major Linux distributions are tested and recommended.

LLVM System Requirements
------------------------

OCLint is based on `libTooling`_ for parsing source code and generating `Abstract Syntax Tree`_ (AST) generation. Prior to compiling OCLint, we need to compile LLVM/Clang. Check out `LLVM System Requirements`_ for requirements. These requirements are very fundamental development tools that probably you already have them.

OCLint System Requirements
--------------------------

Some tools are emphasized here, you may want to double check and make sure the toolkit is ready when you need it.

#. `Apache Subversion`_
#. `Git`_
#. `CMake`_
#. `LTP GCOV Extension`_ (lcov)
#. `OpenSSL`_ (only for analytics-enabled build)

Extra Notes
-----------

Notes for macOS
^^^^^^^^^^^^^^^

`Homebrew`_ is highly recommended for macOS users. When we have ``homebrew`` installed, we can simply get all the dependencies by

.. code-block:: bash

    brew install subversion git cmake lcov openssl

Notes for Ubuntu
^^^^^^^^^^^^^^^^

All Ubuntu users should be able to get all the dependencies by ``apt-get``, for example:

.. code-block:: bash

    apt-get install subversion git cmake lcov libssl-dev

Notes for Fedora
^^^^^^^^^^^^^^^^

We should be able to get all the dependencies by ``yum``, for example:

.. code-block:: bash

    yum install gcc-c++ make git subversion cmake lcov openssl-devel

Notes for Python 2.6
^^^^^^^^^^^^^^^^^^^^

``argparse`` module is required, and install it by

.. code-block:: bash

    sudo easy_install argparse

The installation of ``argparse`` module can be checked by

.. code-block:: bash

    python -c "import argparse; print argparse"

.. _libTooling: http://clang.llvm.org/docs/LibTooling.html
.. _Abstract Syntax Tree: http://en.wikipedia.org/wiki/Abstract_syntax_tree
.. _LLVM System Requirements: http://llvm.org/docs/GettingStarted.html#requirements
.. _Apache Subversion: http://subversion.apache.org/
.. _Git: http://git-scm.com/
.. _CMake: http://www.cmake.org/
.. _LTP GCOV Extension: http://ltp.sourceforge.net/coverage/lcov.php
.. _Homebrew: http://mxcl.github.com/homebrew/
.. _OpenSSL: https://www.openssl.org/
