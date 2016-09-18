Installation
============

Both pre-compiled binary distribution and local build bundle should end up with an OCLint release with which file tree similar to this::

    oclint-release
    |-bin
    |-lib
    |---clang
    |-----<llvm/clang version>
    |-------include
    |-------lib
    |---oclint
    |-----rules
    |-----reporters
    |-include
    |---c++
    |-----v1

Even without installation, ``oclint`` is able to be invoked directly from ``bin`` directory now.

In order to ease the invocation, it's recommended to add OCLint's ``bin`` folder to system ``PATH``, the environment variable that tells system which directories to search for executable files.

Option 1: Directly Adding to PATH
---------------------------------

Following code snippet is an example for the ``.bashrc`` or ``.bash_profile`` file that is sourced when terminal launches.

.. code-block:: bash

    OCLINT_HOME=/path/to/oclint-release
    export PATH=$OCLINT_HOME/bin:$PATH

Option 2: Copying OCLint to System PATH
---------------------------------------

A few directories are supposed to be in the system ``PATH`` already, to mention a few, ``/usr/local/bin``, ``/usr/bin``, ``/bin``, etc. Therefore, it's also possible to copy the OCLint binaries into one of these folders, and move the dependencies over. As an example, presumes ``/usr/local/bin`` is in the ``PATH`` (may require root permission).

#. ``cp bin/oclint* /usr/local/bin/``
#. ``cp -rp lib/* /usr/local/lib/``

Dependency libraries are required to be put into appropriate directory, because ``oclint`` executable searches ``$(/path/to/bin/oclint)/../lib/clang``, ``$(/path/to/bin/oclint)/../lib/oclint/rules`` and ``$(/path/to/bin/oclint)/../lib/oclint/reporters`` for builtin headers and dynamic libraries by default.

Option 3: Homebrew Tap
---------------------------------------

macOS users can install `our homebrew tap <homebrew.html>`_

Verifying Installation
----------------------

Open a new terminal prompt, and execute ``oclint`` directly from there and expect message similar to below::

    $ oclint
    oclint: Not enough positional command line arguments specified!
    Must specify at least 1 positional arguments: See: oclint -help

That's it -- if OCLint is pretty new to you, `tutorial <tutorial.html>`_ would lead you by applying the tool to a sample code, and explaining a few concepts along the way.
