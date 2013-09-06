Checking Out Code
=================

This document helps get the latest source code of OCLint, its submodules and dependencies. We will also describe the preferred structure of your codebase in this document.

.. note:: There is a summary of necessary terminal commands at the bottom of this document, here is the free ride for skipping all the detail and `going directly to there <#summary>`_.

OCLint GitHub Repositories
--------------------------

All source code of OCLint and its submodules are hosted at `GitHub <https://github.com/oclint>`_.

oclint/oclint
^^^^^^^^^^^^^

This repository hosts the OCLint source code, which consists of core, metrics, rules, and reporters modules. Check out the code by

.. code-block:: bash

    git clone https://github.com/oclint/oclint.git

It will create a ``oclint`` folder in current directory, let's give it an alias name ``OCLINT_HOME``.

oclint/oclint-json-compilation-database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This repository contains the Python code for ``oclint-json-compilation-database``.

Go into the ``OCLINT_HOME`` folder, and check out this repository in there:

.. code-block:: bash

    git clone https://github.com/oclint/oclint-json-compilation-database.git

oclint/oclint-xcodebuild
^^^^^^^^^^^^^^^^^^^^^^^^

Code for ``ocling-xcodebuild`` has been pushed to this repository. Go to the ``OCLINT_HOME`` folder, and check out the code:

.. code-block:: bash

    git clone https://github.com/oclint/oclint-xcodebuild.git

.. note:: ``oclint/oclint`` is pretty much everything you need if you are interested in OCLint development. The other two helper programs support OCLint to ease developers in certain ways. They are standalone programs themselves. Check out them when you want to improve them or you are willing to use the development version OCLint in your environment. Also, in order to run `dogfooding <dogfooding.html>`_, you still need to checkout ``oclint/oclint-json-compilation-database``.

LLVM/Clang Codebase
-------------------

LLVM/Clang has its own code structure, and the detail information can be found at Clang's `Get Started <http://clang.llvm.org/get_started.html>`_ page. We also provide a script that checks out all LLVM/Clang repositories into correct location.

.. code-block:: bash

    cd oclint-scripts
    ./clang checkout
    cd ..

In addition, ``clang`` script does more than that:

* First, ``./clang update`` can update the existing LLVM/Clang checkout.
* Second, you can check out a branch codebase other than the trunk codebase by ``./clang checkout -branch <branch_name>``

googltest/googlemock
--------------------

Google C++ Testing and Mocking Frameworks are used for testing OCLint. OCLint follows `Test Driven Development <http://en.wikipedia.org/wiki/Test-driven_development>`_ (TDD), so checkout them before we work on this codebase and want to make sure the modifications do not break the other pieces of code.

We also provide a script ``googleTest``:

* Check out the code simply by ``./googleTest checkout``
* Update the codebase by ``./googleTest update``

Summary
-------

Sum up, to check out all OCLint modules and dependencies, we could execute the following commands:

.. code-block:: bash

    git clone https://github.com/oclint/oclint.git
    cd oclint
    git clone https://github.com/oclint/oclint-json-compilation-database.git
    git clone https://github.com/oclint/oclint-xcodebuild.git
    cd oclint-scripts
    ./clang checkout
    ./googleTest checkout
    cd .. # back to the root folder of OCLint codebase

To update the entire codebase, we can do:

.. code-block:: bash

    cd oclint # start from OCLint root directory
    git pull origin master
    cd oclint-json-compilation-database
    git pull origin master
    cd ../oclint-xcodebuild
    git pull origin master
    cd ../oclint-scripts
    ./clang update
    ./googleTest update
    cd .. # back to OCLint root directory

So now, we OCLint directory might be like this::

    oclint
    |-README
    |-build
    |-googletest
    |-llvm
    |-oclint-core
    |---include
    |---lib
    |---test
    |-oclint-driver
    |---include
    |---lib
    |-oclint-json-compilation-database
    |-oclint-metrics
    |---include
    |---lib
    |---test
    |-oclint-rules
    |---include
    |---lib
    |---rules
    |---template
    |---test
    |-oclint-reporters
    |---reporters
    |---template
    |---test
    |-oclint-scripts
    |-oclint-xcodebuild
