Writing Your Own Reporters
==========================

Currently we have text and HTML format reporters, custom reporters are easily implemented to support your own need.

We have a ``oclint-reporters`` module, and all reporters is recommended to add to this module.

Your reporters need to inherent ``Reporter`` interface and implement two methods that it defines.

First of all, give your reporter an identifier in ``name`` method. Then give the same name with ``-report-type`` option to ``oclint`` main program in order to use this new reporter later.

Then implement your reporter in ``report`` method. You will be given a ``outstream`` as a output stream. In addition, all the information your reporter needs is in the ``Results`` class.

Lastly, there is one small extra effort that is not defined in the interface, but is required when OCLint tries to load your reporter. Please copy and paste the code below, and replace ``YourNewReporter`` with your class name.

.. code-block:: c++

    extern "C" Reporter* create()
    {
      return new YourNewReporter();
    }

That's it. Now compile your new reporter and link it against ``OCLintCore`` library into a new dynamic library. We have a CMake macro ``BUILD_DYNAMIC_REPORTER`` to have this part easier.

Put the generated dynamic library into ``$(/path/to/bin/oclint)/../lib/oclint/reporters`` along with other reporter libraries. Done!
