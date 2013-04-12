Writing Custom Reporters
========================

Currently we have multiple types of reporters, like plain text and HTML. To enable extended capabilities, custom reporters are easily implemented for your own supports.

We have a ``oclint-reporters`` module, and all reporters are recommended to add to this module.

New reporters need to inherit ``Reporter`` interface. We will implement two methods that are required by the interface.

First of all, give the new reporter an identifier in ``name`` method. Then give the same name with ``-report-type`` option to ``oclint`` main program in order to use this new reporter later.

Then implement logic in ``report`` method. We have a ``outstream`` as a output stream on hand. In addition, all the information the new reporter needs is in the ``Results`` class.

Lastly, there is one small extra effort that is not defined in the interface, but is required when OCLint tries to load this reporter. Please copy and paste the code below, and replace ``YourNewReporter`` with your class name.

.. code-block:: c++

    extern "C" Reporter* create()
    {
      return new YourNewReporter();
    }

That's it. Now compile your new reporter and link it against ``OCLintCore`` library into a new dynamic library. We have a CMake macro ``BUILD_DYNAMIC_REPORTER`` to make this part easier.

.. seealso:: `Reporter scaffolding <scaffolding.html#creating-reporters-with-scaffolding>`_ is the tool for accelerating this process, it helps create the reporter source code from template and corresponding build configurations. As developers, we only need to think about the logic of rendering results.

Put the generated dynamic library into ``$(/path/to/bin/oclint)/../lib/oclint/reporters`` along with other reporter libraries. Done!
