Using OCLint with xcpretty
==========================

This document goes through using xcpretty inside OCLint's workflow for analyzing the code quality for a Xcode project.

Prerequisite
------------

* `oclint Manual <../manual/oclint.html>`_
* `oclint-json-compilation-database Manual <../manual/oclint-json-compilation-database.html>`_
* `xcpretty README <https://github.com/supermarin/xcpretty/blob/master/README.md>`_

Generating json-compilation-database with xcpretty
--------------------------------------------------

Running ``xcpretty`` is quite straight forward. For example, the command below will build the project and generate the ``compile_commands.json`` file under the current folder.

.. code-block:: bash

  xcodebuild [flags] | xcpretty

If you want to preserve the raw xcodebuild output, then you can do

.. code-block:: bash

  xcodebuild [flags] | tee xcodebuild.log | xcpretty

Running oclint-json-compilation-database
----------------------------------------

Now, by having the ``compile_commands.json`` file, we can run the code analysis by simply call

.. code-block:: bash

  oclint-json-compilation-database

Or with your customizations.
