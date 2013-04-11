Using OCLint with CMake
=======================

This document shows how to apply OCLint to the projects which use CMake as build system.

Prerequisite
------------

* `CMake <http://www.cmake.org/>`_
* `oclint Manual <../manual/oclint.html>`_
* `oclint-json-compilation-database Manual <../manual/oclint-json-compilation-database.html>`_

Background
----------

CMake is able to generate JSON Compilation Database file ``compile_commands.json`` with no hassle at all. If a project uses CMake as its build system, then applying OCLint is a quite easy task.

Generating compile_comamnds.json
--------------------------------

Simply add ``-DCMAKE_EXPORT_COMPILE_COMMANDS=ON`` to the existing ``cmake`` command, like

.. code-block:: bash

    cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON path/to/source-root

As a result, the ``compile_commands.json`` file is generated in the CMake build folder.

That's it!

Using compile_commands.json
---------------------------

We can leave the ``compile_commands.json`` file here in the build directory, and use ``-p`` option to `specify this file <../manual/oclint.html#compilation-database>`_  for ``oclint``.

But in order to use ``oclint-json-compilation-database``, it's required to copy or link this file to our source directory, for example:

* copy the file

.. code-block:: bash
    
    cp `pwd`/compile_commands.json /path/to/source-root

* link the file

.. code-block:: bash

    ln -s `pwd`/compile_commands.json /path/to/source-root

Running OCLint
--------------

Now we can use ``oclint`` by

.. code-block:: bash

    oclint -p <build path> <source0> [... <sourceN>]

``build path`` is the path to the folder that contains ``compile_commands.json``.

In addition, we can use ``oclint-json-compilation-database`` for code analysis. In this case, simply enter

.. code-block:: bash

    oclint-json-compilation-database

For advanced usage, detail instructions can be found in `oclint <../manual/oclint.html>`_ and `oclint-json-compilation-database <../manual/oclint-json-compilation-database.html>`_ manuals respectively.
