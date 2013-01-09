Using oclint
============

When you invoke OCLint, it normally does rule loading, compilation, analysis, and report generation. The options allow you to change the behavior of each step to certain ways that meet your requirement.

See all supported options in OCLint |release| by typing ``oclint -help``::

    USAGE: oclint [options] <source0> [... <sourceN>]

    OPTIONS:
      -R=<directory>              - Add directory to rule loading path
      -fatal-assembler-warnings   - Consider warnings as error
      -help                       - Display available options (-help-hidden for more)
      -max-priority-1=<threshold> - The max allowed number of priority 1 violations
      -max-priority-2=<threshold> - The max allowed number of priority 2 violations
      -max-priority-3=<threshold> - The max allowed number of priority 3 violations
      -o=<path>                   - Write output to <path>
      -p=<string>                 - Build path
      -rc=<paramemter>=<value>    - Override the default baheviour of rules
      -stats                      - Enable statistics output from program
      Choose report type:
        -text                     - Plain text report
        -html                     - HTML formatted report
      -version                    - Display the version of this program

    -p <build-path> is used to read a compile command database.

        For example, it can be a CMake build directory in which a file named
        compile_commands.json exists (use -DCMAKE_EXPORT_COMPILE_COMMANDS=ON
        CMake option to get this output). When no build path is specified,
        a search for compile_commands.json will be attempted through all
        parent paths of the first input file . See:
        http://clang.llvm.org/docs/HowToSetupToolingForLLVM.html for an
        example of setting up Clang Tooling on a source tree.

    <source0> ... specify the paths of source files. These paths are
        looked up in the compile command database. If the path of a file is
        absolute, it needs to point into CMake's source tree. If the path is
        relative, the current working directory needs to be in the CMake
        source tree and the file must be in a subdirectory of the current
        working directory. "./" prefixes in the relative files will be
        automatically removed, but the rest of a relative path must be a
        suffix of a path in the compile command database.

    For more information, please visit http://oclint.org

Rule Loading Options
--------------------

\-R <directory>
    Rule loading path can be changed by using ``-R`` option. Multiple rule loading paths can be specified to load rules from more than one directories. By default, OCLint searches ``$(/path/to/bin/oclint)/../lib/oclint/rules`` for the dyanmic libraries that contain rules.
\-rc <paramemter>=<value>
    Certain rules have default threshold to decide whether to emit violations. These thresholds can be changed by ``-rc`` option with a key-value pair.

More detail on changing the behavior in rules loading process during runtime can be found in `customizing rules <../customizing/rules.html>`_ page.

Compilation Options
-------------------

OCLint needs to know the specific compiler options for the files inspecting. There are two alternatives, specify the compiler options or use compile command database.

Giving Compiler Options
^^^^^^^^^^^^^^^^^^^^^^^

Compiler options can be given directly to OCLint for compilation process. It's straight forward by appending ``--`` separator following by all compier options after OCLint options and sources:

.. code-block:: none

    oclint [oclint options] <source0> [... <sourceN>] -- [compiler options]

For example, if you are compiling a file named by following command:

.. code-block:: bash

    clang -x objective-c -arch armv7 -std=gnu99 -fobjc-arc -O0 -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.0.sdk -g -I./Pods/Headers -c RPActivityIndicatorManager.m

(Wow, it's longer than expectation.)

Then when you analyze this code, your OCLint command will be:

.. code-block:: bash

    oclint [oclint options] RPActivityIndicatorManager.m -- -x objective-c -arch armv7 -std=gnu99 -fobjc-arc -O0 -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS6.0.sdk -g -I./Pods/Headers -c

Compile Command Database
^^^^^^^^^^^^^^^^^^^^^^^^

\-p <build-path>
    Choose the build directory in which a file named compile_commands.json exists. When no build path is specified, a search for compile_commands.json will be attempted through all parent paths of the first input file.

OCLint requires this compilation database to understand specific build options for each file. Currently it supports compile_commands.json file. See `oclint-json-compilation-database <oclint-json-compilation-database.html>`_ for detail. If you are working with Xcode, `oclint-xcodebuild <oclint-xcodebuild.html>`_ can generate the required compile_database.json file for you with your little help.

Inspection Options
------------------

Of course, specify all the source files you want to inspect. Multiple files can be analyzed with one invocation.

Report Options
--------------

\-o <path>
    Instead of piping output to console, ``-o`` will redirect the report to the <path> you specified.
\-text
    Use plain text report, this is the default
\-html
    Use HTML report for better readability

See `customizing reports <../customizing/reports.html>`_ for detail.

Exit Status Options
-------------------

\-max-priority-1 <threshold>
    The max allowed number of priority 1 violations
\-max-priority-2 <threshold>
    The max allowed number of priority 2 violations
\-max-priority-3 <threshold>
    The max allowed number of priority 3 violations

This option helps in continuous integration and other build systems. When the number of violations in one of these priorities is larger than the largest tolerance, OCLint will return with an exit status code other than 0 (code zero means normal termination) to notify a high volume of violations. By default, less than 20 priority 3 violations are allowed, 10 violations is maximum for priority 2, and no priority 1 violation is ever tolerated. Too many violations result in bad code quality, if that happens, OCLint return with an exit code of 3.

OCLint returns with one of the four exit codes below

* **0** - SUCCESS
* **1** - RULE_NOT_FOUND
* **2** - ERROR_WHILE_PROCESSING
* **3** - VIOLATIONS_EXCEED_THRESHOLD

Other Options
-------------

\-version
    Show version information about OCLint, LLVM and some environment variables.
