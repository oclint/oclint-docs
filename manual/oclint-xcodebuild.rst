oclint-xcodebuild Manual
========================

``oclint-xcodebuild`` is a helpful program that extracts adequate compiler options from ``xcodebuild`` execution log, converts them into JSON Compilation Database format, and save it into ``compile_commands.json`` file.

.. seealso::

    Read Apple's official `xcodebuild Manual Page`_ from Mac Developer Library. To understand how ``oclint-xcodebuild`` can be applied in your workflow, please move onto `Using OCLint with xcodebuild <../guide/xcodebuild.html>`_ document.

Running oclint-xcodebuild
---------------------

If a ``xcodebuild.log`` file is at the current working directory. Simply run

.. code-block:: bash

    oclint-xcodebuild

In case the xcodebuild log is stored in a file with name other than ``xcodebuild.log``, append the path to the log file like

.. code-block:: bash

    oclint-xcodebuild /path/to/xcodebuild/log

The ``compile_commands.json`` will be generated to the current working directory.

.. warning:: It's highly recommended to avoid having spaces in your file name or file path. It's a good practice. Meanwhile, even though ``oclint`` itself supports spaces in path, ``oclint-json-compilation-database`` and ``oclint-xcodebuild`` still have issues handling spaces in path.

.. note:: ``oclint-xcodebuild`` is still an experimental project. The success of it depends on various things, e.g. Mac OS X version, the Xcode version and project settings. However, since developers who use Xcode are familiar with Apple's manner of supporting only the latest version and one previous version, so ``oclint-xcodebuild`` tries to follow this convention. Your feedback is warmly welcome to help improve this helper program.

.. _xcodebuild Manual Page: https://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/xcodebuild.1.html
