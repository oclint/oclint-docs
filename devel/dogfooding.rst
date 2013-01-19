Eating Your Own Dog Food
========================

OCLint, being a static code analysis tool that helps maintain high code quality, applied itself against its own source code to demonstrate the quality and capabilities of itself. This gives us confidence. At the same time, when we are careless and don't pay attention to certain things, dogfooding alerts us immediately.

For every software products, it's impossible to say they are bug-free or smell-free. But dogfooding is a very good practice to lower the change of being exploded to defects. Along with the growth of OCLint rule set, we always keep our code away from violating any of these rules.

Requirements
------------

You just need a release version of OCLint with ``oclint-json-compilation-database`` helper program. Please refer `Building OCLint <../intro/build.html>`_ for instructions. After building binaries and libraries for each module, please remind to call ``buildRelease.sh`` script that automatically gathers all parts from different modules, and assembles them properly in ``oclint-release`` directory.

Dogfooding
----------

Kick off the dogfooding process by calling ``dogFooding.sh`` script in ``oclint-scripts`` folder, like

.. code-block:: bash

    cd oclint-scripts
    ./dogFooding.sh

This will use CMake to configure the modules with ``CMAKE_EXPORT_COMPILE_COMMANDS`` on for generating ``compile_commands.json`` files. ``oclint-json-compilation-database`` follows after that to analyze the source code and generate dogfooding reports. It takes a while to finish the entire inspection process. When it's done, the report will be outputted on terminal.

Please help to keep your fork of OCLint codebase free from code smells. Before submit a patch or open a pull request, please make sure to run dogfooding and fix all violations. Great thanks.
