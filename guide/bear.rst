Using OCLint with Bear
======================

This document shows how to apply OCLint to the projects which use `Make <http://en.wikipedia.org/wiki/Make_(software)>`_ and other build systems in unix-like operating systems.

Prerequisite
------------

* `Bear <https://github.com/rizsotto/Bear>`_
* ``man make``
* `oclint Manual <../manual/oclint.html>`_
* `oclint-json-compilation-database Manual <../manual/oclint-json-compilation-database.html>`_

Background
----------

Bear is a very handy tool to generate compilation database during the build process. Bear is a very important supplement especially for those who don't use CMake as build system. Bear can be applied in a wider circumstances, because it injects into the build process, and intercepts the ``exec`` calls to understand the compilation details.

Generating compile_commands.json
--------------------------------

By following the instructions on `Bear README <https://github.com/rizsotto/Bear/blob/master/README.md>`_, we could have ``bear`` ready to use.

For example, if want to generate the ``compile_command.json`` for a project using ``make``, we can easily use ``bear`` by

.. code-block:: bash

    $ /path/to/bear make

What's Next
-----------

The rest of the process is as same as those who use CMake. Please refer to the `other document <cmake.html#using-compile-commands-json>`_.
