Building OCLint
===============

This page presents you a shortcut of building OCLint release version.

.. note:: If you are looking for compiling and testing OCLint in debug mode for development purposes, please move onto `development <../devel/index.html>`_ section.

System Requirements
-------------------

#. See `LLVM System Requirements`_
#. `Apache Subversion`_
#. `CMake`_

.. Release build doesn't need git, but subversion is needed to checkout llvm/clang source code, and it's written in LLVM's requirements

Prepare LLVM/Clang
------------------

#. Checkout LLVM/Clang
    * ``cd oclint-scripts``
    * ``./checkoutLLVMClang.sh``
    * ``cd ..``
#. Build LLVM/Clang
    * ``cd oclint-scripts``
    * ``./buildClang.sh release``
    * ``cd ..``

Build OCLint
------------

#. ``cd oclint-scripts``
#. ``./buildAll.sh`` release
#. ``cd ..``

Verify Your Build
-----------------

#. ``cd build/oclint-release/bin``
#. ``./oclint``

You should get::

    $ ./oclint
    oclint: Not enough positional command line arguments specified!
    Must specify at least 1 positional arguments: See: ./oclint -help

Now, let's move onto `installation <installation.html>`_.

.. _LLVM System Requirements: http://llvm.org/docs/GettingStarted.html#requirements
.. _Apache Subversion: http://subversion.apache.org/
.. _CMake: http://www.cmake.org/
