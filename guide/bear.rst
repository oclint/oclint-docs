Using OCLint with Bear
======================

This document shows how to apply OCLint to the projects which use `Make <http://en.wikipedia.org/wiki/Make_(software)>`_ and other build systems in Linux operating system.

.. note::

    Bear currently works in Linux. Mac OS is not supported yet.

Prerequisite
------------

* `Bear <https://github.com/rizsotto/Bear>`_
* ``man make``
* `oclint Manual <../manual/oclint.html>`_
* `oclint-json-compilation-database Manual <../manual/oclint-json-compilation-database.html>`_

Background
----------

Bear is a very handy tool to generate compilation database during the build process. Bear is a very important supplement especially for those who don't use CMake as build system. Bear can be applied in a larger circumstances, because it injects into the build process, and intercepts the ``exec`` calls to understand the compilation details.

Generating compile_comamnds.json
--------------------------------

By following the instructions on `Bear README <https://github.com/rizsotto/Bear/blob/master/README.md>`_, we could have ``bear`` ready to use.

For example, if want to generate the ``compile_command.json`` for a project using ``make``, we can easily use ``bear`` by

.. code-block:: bash

    $ /path/to/bear -b /path/to/libear.so -- make

Testing Against Bear Itself
---------------------------

Even though Bear uses CMake, we can still apply Bear to itself when we actually call the ``make``. In my case, I will go to ``/Project/Bear/build`` folder and run

.. code-block:: bash

    $ /Projects/Bear/install/bin/bear -b /Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -- make

Bear outputs the ``compile_commands.json`` like the followings (with git SHA ``cbc579a2ccd110c43de5b2de36ff68d190734abb``):

.. code-block:: json

    [
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DSERVER -I/Projects/Bear/build/src -o CMakeFiles/bear.dir/stringarray.c.o -c /Projects/Bear/src/stringarray.c",
      "file": "/Projects/Bear/src/stringarray.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DSERVER -I/Projects/Bear/build/src -o CMakeFiles/bear.dir/protocol.c.o -c /Projects/Bear/src/protocol.c",
      "file": "/Projects/Bear/src/protocol.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DSERVER -I/Projects/Bear/build/src -o CMakeFiles/bear.dir/main.c.o -c /Projects/Bear/src/main.c",
      "file": "/Projects/Bear/src/main.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DSERVER -I/Projects/Bear/build/src -o CMakeFiles/bear.dir/output.c.o -c /Projects/Bear/src/output.c",
      "file": "/Projects/Bear/src/output.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DSERVER -I/Projects/Bear/build/src -o CMakeFiles/bear.dir/json.c.o -c /Projects/Bear/src/json.c",
      "file": "/Projects/Bear/src/json.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -Dear_EXPORTS -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DCLIENT -fPIC -I/Projects/Bear/build/src -o CMakeFiles/ear.dir/stringarray.c.o -c /Projects/Bear/src/stringarray.c",
      "file": "/Projects/Bear/src/stringarray.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -Dear_EXPORTS -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DCLIENT -fPIC -I/Projects/Bear/build/src -o CMakeFiles/ear.dir/protocol.c.o -c /Projects/Bear/src/protocol.c",
      "file": "/Projects/Bear/src/protocol.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -Dear_EXPORTS -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DCLIENT -fPIC -I/Projects/Bear/build/src -o CMakeFiles/ear.dir/environ.c.o -c /Projects/Bear/src/environ.c",
      "file": "/Projects/Bear/src/environ.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/src",
      "command": "/usr/bin/gcc -Dear_EXPORTS -D_GNU_SOURCE -DDEFAULT_PRELOAD_FILE=/Projects/Bear/install/lib/x86_64-linux-gnu/libear.so -DDEFAULT_SOCKET_FILE=/tmp/bear.socket -DDEFAULT_OUTPUT_FILE=compile_commands.json -DCLIENT -fPIC -I/Projects/Bear/build/src -o CMakeFiles/ear.dir/execs.c.o -c /Projects/Bear/src/execs.c",
      "file": "/Projects/Bear/src/execs.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/unit_test",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DCLIENT -DSERVER -I/Projects/Bear/test/unit_test/../../src -o CMakeFiles/unit_test.dir/main.c.o -c /Projects/Bear/test/unit_test/main.c",
      "file": "/Projects/Bear/test/unit_test/main.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/unit_test",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DCLIENT -DSERVER -I/Projects/Bear/test/unit_test/../../src -o CMakeFiles/unit_test.dir/__/__/src/stringarray.c.o -c /Projects/Bear/src/stringarray.c",
      "file": "/Projects/Bear/src/stringarray.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/unit_test",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DCLIENT -DSERVER -I/Projects/Bear/test/unit_test/../../src -o CMakeFiles/unit_test.dir/__/__/src/protocol.c.o -c /Projects/Bear/src/protocol.c",
      "file": "/Projects/Bear/src/protocol.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/unit_test",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DCLIENT -DSERVER -I/Projects/Bear/test/unit_test/../../src -o CMakeFiles/unit_test.dir/__/__/src/json.c.o -c /Projects/Bear/src/json.c",
      "file": "/Projects/Bear/src/json.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/unit_test",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -DCLIENT -DSERVER -I/Projects/Bear/test/unit_test/../../src -o CMakeFiles/unit_test.dir/__/__/src/environ.c.o -c /Projects/Bear/src/environ.c",
      "file": "/Projects/Bear/src/environ.c"
    }
    ,
    {
      "directory": "/Projects/Bear/build/test/exec_anatomy",
      "command": "/usr/bin/gcc -D_GNU_SOURCE -I/Projects/Bear/build/test/exec_anatomy/../../src -o CMakeFiles/exec_anatomy.dir/main.c.o -c /Projects/Bear/test/exec_anatomy/main.c",
      "file": "/Projects/Bear/test/exec_anatomy/main.c"
    }
    ]

What's Next
-----------

The rest of the process is as same as those who use CMake. Please refer to the `other document <cmake.html#using-compile-commands-json>`_.
