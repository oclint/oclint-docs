Set Up OCLint in MinGW Environment
==================================

This page presents our effort of porting OCLint to MinGW environment.

.. note:: Certain features are not fully tested with MinGW environment, and your comments are welcome.

System Requirements
-------------------

#. MinGW
#. MSYS
#. GCC and G++ Toolchain
#. Python
#. Git
#. Apache Subversion
#. CMake

Cleaning Up
-----------

Cleaning by making sure the ``build`` folder, ``llvm`` folder, ``googletest`` folder and ``oclint-json-compilation-database`` folder are deleted.

Release Build
-------------

The release build is produced by:

.. code-block:: bash

    ./ci -setup -release

This is actually a wrapper task consisting of:

.. code-block:: bash

    cd ..
    git clone https://github.com/oclint/oclint-json-compilation-database
        # check out oclint-json-compilation-database code
    cd oclint-scripts
    ./clang co              # check out LLVM/Clang code
    ./clang build -release  # build Clang
    ./build -release        # build OCLint
    ./bundle                # bundle everything and be ready to use

Running Tests
-------------

Tests can tell if OCLint is stable on MinGW environment:

.. code-block:: bash

    ./googleTest co     # check out GoogleTest code
    ./googleTest build  # build GoogleTest
    ./test              # test all modules

Keeping Up To Date
------------------

Update OCLint itself by ``git pull``, and same thing for ``oclint-json-compilation-database`` module.

Update Clang and GoogleTest by ``./clang update`` and ``./googleTest update`` respectively.

Verifying the Build
-------------------

By calling the binary

.. code-block:: bash

    ./build/oclint-<major>.<minor>.dev.<git-hash>/bin/oclint.exe

The following error message is expected::

    oclint: Not enough positional command line arguments specified!
    Must specify at least 1 positional arguments: See: ./oclint -help

.. seealso::

    `OCLint manual <../manual/oclint.html>`_
        Manual for OCLint main binary

    `Building OCLint in Unix-Like Environment <../intro/build.html>`_
        Documentation of building OCLint on Linux and Mac

    `Testing OCLint in Unix-Like Environment <../devel/compiletest.html>`_
        Documentation of compiling and testing OCLint on Linux and Mac
