Using OCLint with xctool
========================

This document goes through the happy path of using OCLint to analyze the code quality of a Xcode project with xctool.

Prerequisite
------------

* `oclint Manual <../manual/oclint.html>`_
* `oclint-json-compilation-database Manual <../manual/oclint-json-compilation-database.html>`_
* `xctool README <https://github.com/facebook/xctool/blob/master/README.md>`_

Background
----------

``xctool`` is a drop-in replacement for Apple's ``xcodebuild``. It makes building Xcode projects much easier. It eases continuous integration in many ways as well. ``xctool`` supports generating the report in JSON Compilation Database format, which can be used by OCLint to understand all the compiler flags in order to analyze the code.

Running xctool with json-compilation-database Reporter
------------------------------------------------------

Running ``xctool`` is quite straight forward. For example, the command below will build the project and generate the ``compile_commands.json`` file under the current folder.

.. code-block:: bash

  path/to/xctool.sh \
    -project YourProject.xcodeproj \
    -scheme YourScheme \
    -reporter json-compilation-database:compile_commands.json \
    build

``xctool`` also supports an ``.xctool-args`` file to preserve the command arguments, like workspace, scheme, configuration, etc. If we have ``.xctool-args`` ready, then we could simply run

.. code-block:: bash

  xctool -reporter json-compilation-database:compile_commands.json build

to get the ``compile_commands.json`` file.

We can use ``xctool clean`` to clean the build in order to have a full list of all compiling files the next time we call ``xctool build``.

Running oclint-json-compilation-database
----------------------------------------

Now, by having the ``compile_commands.json`` file, we can run the code analysis by simply call

.. code-block:: bash

  oclint-json-compilation-database

Or with your customizations.

.. seealso::

    With the great help from ``xctool``, you could even `show OCLint warnings in Xcode <xcode.html>`_.
