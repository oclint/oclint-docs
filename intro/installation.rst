Installation
============

No matter you have downloaded a pre-compiled binary distribution or have built OCLint from scratch by yourself, now you should have an OCLint release with which file tree similar to this::

    oclint-release
    |-bin
    |-lib
    |---clang
    |-----3.3
    |-------include
    |-------lib
    |---oclint
    |-----rules
    |-----reporters

In fact, you can execute ``oclint`` from ``bin`` directory now.

In order to easily invoke all OCLint executables, it's recommended to install OCLint to ``PATH``, the environment variable that tells system which directories to search for executable files.

Option 1: Directly Add to PATH
------------------------------

You can add OCLint release folder directly to ``PATH`` by appending the following code block into your ``.bashrc`` or ``.bash_profile`` that is read when terminal launches.

.. code-block:: bash

    OCLINT_HOME=/path/to/oclint-release
    export PATH=$OCLINT_HOME/bin:$PATH

Option 2: Copy OCLint to System PATH
------------------------------------

You can also copy OCLint to system ``PATH``. There is an example that presumes ``/usr/local/bin`` is in the ``PATH``.

#. ``sudo cp bin/oclint* /usr/local/bin/`` (require root permission)
#. ``sudo cp -rp lib/* /usr/local/lib/`` (require root permission)

Dependency libraries are required to be put into correct directory, because ``oclint`` executable searches ``$(/path/to/bin/oclint)/../lib/clang``, ``$(/path/to/bin/oclint)/../lib/oclint/rules`` and ``$(/path/to/bin/oclint)/../lib/oclint/reporters`` for required builtin headers and dynamic libraries.

Verify Installation
-------------------

Open a new command line terminal, and simply execute ``oclint``, you should get::

    $ oclint
    oclint: Not enough positional command line arguments specified!
    Must specify at least 1 positional arguments: See: ./oclint -help

That's it -- you can now move onto `tutorial <tutorial.html>`_.
