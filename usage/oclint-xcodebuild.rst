Using oclint-xcodebuild
=======================

OCLint recognizes a file called ``compile_commands.json`` to figure out the compiler options for parsing each file. By having a ``compile_commands.json`` file, analyzing projects with a large codebase becomes easier. Since all compiler options are implicitly configured in Xcode workspace/project settings, and we can see what actually happens when we invoke ``xcodebuild`` in terminal, this helper program then try to extract adequate compiler options, convert them into JSON Compilation Database format, and save it into ``compile_commands.json`` file.

.. seealso:: To gain some context about JSON Compilation Database and ``compile_commands.json``, read `using oclint-json-compilation-database <oclint-json-compilation-database.html>`_.

Run xcodebuild
--------------

First of all, we need to help ourselves a little bit. ``xcodebuild`` is a command line tool that Apple provides along with the Xcode application to let us build Xcode workspace/project in the terminal.

.. seealso::

    Read Apple's official `xcodebuild Manual Page`_ from Mac Developer Library is a good starting point if you haven't done any tasks about ``xcodebuild``.

It is a quite simple task to some people by figuring out the correct options for ``xcodebuild``. However, some people may feel it's not intuitive, so be patient, and take your time. You may find many online tutorials and blog posts that may help.

Okay, we believe you are quite confidence of running ``xcodebuild`` to build your Xcode project. Now, there are three things please pay attention:

* We need to save the ``xcodebuild`` output to a log file, by convention, name it ``xcodebuild.log``. We can use ``xcodebuild <options> | tee xcodebuild.log`` to pipe every line of the output to ``xcodebuild.log`` file.
* If a source file has been built by Xcode, and it's not modified since last build, then it might not be built again when you invoke ``xcodebuild``. In other words, if it happens, this file won't be shown in the log. So you won't see it in ``compile_commands.json``. To avoid that, use clean build by removing all build products and intermediate files from the build directory. (Hope you understand what *clean build* means after spending the time on learning ``xcodebuild``.)
* ``compile_commands.json`` is platform sensitive. Whenever your environment changes, for example, upgrading your Mac OS, upgrading Xcode version, switch to another SDK, and so on, please remove the existing ``xcodebuild.log`` and ``compile_commands.json``, capture xcodebuild log again with the updated options, and re-generated new ``compile_commands.json``. Don't check ``compile_commands.json`` into your source code. Instead, always generate a new ``compile_comamnds.json`` when anything change.

Run oclint-xcodebuild
---------------------

So a ``xcodebuild.log`` file should be there properly on the root folder of your Xcode project. Simply run

.. code-block:: bash

    oclint-xcodebuild

In case your xcodebuild log is stored in a file name other than ``xcodebuild.log``, append the path to the log file like

.. code-block:: bash

    oclint-xcodebuild /path/to/xcodebuild/log

The ``compile_commands.json`` will be generated to the same folder.

What's next
-----------

Now we have ``compile_command.json`` file for our Xcode project, we can move onto `use oclint-json-compilation-database <oclint-json-compilation-database.html>`_ and use OCLint to inspect our codebase.

.. note:: ``oclint-xcodebuild`` is still an experimental project. The success of it depends various things, e.g. Mac OS X version, the Xcode version and project settings. However, since developers who use Xcode are familiar with Apple's manner of supporting only the latest version and one previous version, so ``oclint-xcodebuild`` tries to follow this convention. Your feedback is warmly welcome to help improve this helper program.

.. warning:: It's highly recommended to avoid having spaces in your file name or file path. It's a good practice, meanwhile, even though ``oclint`` itself supports spaces in path, ``oclint-json-compilation-database`` and ``oclint-xcodebuild`` still have issues handling spaces in path.

.. _xcodebuild Manual Page: https://developer.apple.com/library/mac/#documentation/Darwin/Reference/ManPages/man1/xcodebuild.1.html
