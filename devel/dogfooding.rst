Eating Your Own Dog Food
========================

OCLint, being a static code analysis tool that helps maintain high code quality, always applies itself against its own source code to demonstrate the quality and capabilities of itself. This process is called dogfooding. Dogfooding gives us confidence. At the same time, when we are careless and don't pay attention to certain things, dogfooding alerts us immediately.

For every software products, it's impossible to say they are bug-free or smell-free. But dogfooding is a very good practice to lower the change of being exploded to defects. Along with the growth of OCLint rule set, we always keep our code away from violating any of these rules.

Requirements
------------

We always highly recommend building the local OCLint version, and then use it for dogfooding the very codebase that this binary is built from. We also need to be the latest debug version of OCLint with assertions on.

The easiest way of preparing the qualified binary is by running the scripts below. It actually invokes the ``dogFooding`` process automatically when the binary is ready.

.. code-block:: bash

    cd oclint-scripts
    ./ci -reset
    ./ci -setup

Dogfooding
----------

Kick off the dogfooding process by calling ``dogFooding`` script in ``oclint-scripts`` folder, like

.. code-block:: bash

    cd oclint-scripts
    ./dogFooding

This will use CMake to configure the modules with ``CMAKE_EXPORT_COMPILE_COMMANDS`` on for generating ``compile_commands.json`` files. ``oclint-json-compilation-database`` follows after that to analyze the source code and generate dogfooding reports. It takes a while to finish the entire inspection process. When it's done, the report will be outputted on terminal.

By default, ``dogFooding`` script analyzes all modules. The script could work for one single module by the given module name.

Enabling Clang Static Analyzer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

During the dogfooding process, it's also possible to enable Clang Static Analyzer to analyze the codebase in addition to OCLint itself.

Pass ``-enable-clang-static-analyzer`` option to the script, and it redirects the message to OCLint for enabling the integrated Clang Static Analyzer.

Reviewing Dogfooding Reports
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By passing ``-show`` option to the ``dogFooding`` script, it prints out the existing dogfooding reports. Again, by default, it shows all modules, and can be more specific by by given a module name.

.. note::

    Please help to keep your fork of OCLint codebase free from code smells. Before submit a patch or open a pull request, please make sure to run dogfooding and fix all violations. Great thanks.
