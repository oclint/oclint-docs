Installation
============

No matter you download a pre-compiled binary distribution or build OCLint from scratch by yourself, now you should have an OCLint release with which file tree similar to this::

    oclint-release
    |-bin
    |-lib
    |---clang
    |-----3.2
    |-------include
    |-------lib
    |---oclint
    |-----rules

In fact, you can execute ``oclint`` from ``bin`` directory now. In order to easily get access to OCLint, it's recommended to install OCLint to ``PATH``, the environment variable that tells system which directories to search for executable files.

Option 1: Add Directly to PATH
------------------------------

You can add OCLint release folder directly to ``PATH`` by appending the following code block into your ``.bashrc`` or ``.bash_profile`` that will be read when terminal is launched.

.. code-block:: bash

    OCLINT_HOME=/path/to/oclint-release
    export PATH=$OCLINT_HOME/bin:$PATH

Option 2: Copy OCLint to System PATH
------------------------------------

You can also copy OCLint to system ``PATH``, the following example presumes ``/usr/local/bin`` is in the ``PATH``.

#. ``sudo cp bin/oclint* /usr/local/bin/`` (require root permission)
#. ``sudo cp -rp lib/* /usr/local/lib/`` (require root permission)

Dependent libraries is required to be put into correct directory, since ``oclint`` executable searches ``$(/path/to/bin/oclint)/../lib/clang`` and ``$(/path/to/bin/oclint)/../lib/oclint/rules`` for required builtin headers and dynamic libraries.

Verify Installation
-------------------

Open a new command line terminal, and simply execute ``oclint``, you should get::

    $ oclint
    oclint: Not enough positional command line arguments specified!
    Must specify at least 1 positional arguments: See: ./oclint -help

That's it -- you can now move onto `tutorial <tutorial.html>`_.
