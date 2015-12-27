oclint Manual
=============

When we invoke OCLint, it normally does rule loading, compilation, analysis, and report generation. The options allow us to change the behavior of each step to certain ways that meet our requirements.

See all supported options in OCLint |release| by typing ``oclint -help``::

    USAGE: oclint [options] <source0> [... <sourceN>]

    OPTIONS:
      -R=<directory>                - Add directory to rule loading path
      -disable-rule=<rule name>     - Disable rules
      -enable-clang-static-analyzer - Enable Clang Static Analyzer, and integrate results into OCLint report
      -enable-global-analysis       - Compile every source, and analyze across global contexts (depends on number of source files, could results in high memory load)
      -help                         - Display available options (-help-hidden for more)
      -list-enabled-rules           - List enabled rules
      -max-priority-1=<threshold>   - The max allowed number of priority 1 violations
      -max-priority-2=<threshold>   - The max allowed number of priority 2 violations
      -max-priority-3=<threshold>   - The max allowed number of priority 3 violations
      -o=<path>                     - Write output to <path>
      -p=<string>                   - Build path
      -rc=<parameter>=<value>       - Override the default behavior of rules
      -report-type=<name>           - Change output report type
      -rule=<rule name>             - Explicitly pick rules
      -version                      - Display the version of this program

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
    Rule loading path can be changed by using ``-R`` option. Multiple rule loading paths can be specified to load rules from more than one directories. By default, OCLint searches ``$(/path/to/bin/oclint)/../lib/oclint/rules`` for the dynamic libraries that contain rules.
\-disable-rule <rule name>
    This option gives the capability to deactivate rules by their names even though they are loaded into the system. This option can be chained multiple times to further narrow down.
\-rc <parameter>=<value>
    Certain rules have threshold to decide whether to emit violations. These thresholds can be changed by ``-rc`` option with a key-value pair.

More detail on changing the behavior in rules loading process during runtime can be found in `rule selection <../howto/selectrules.html>`_ and `threshold customization <../howto/thresholds.html>`_ pages.

Compilation Options
-------------------

For the sources that are being inspected, OCLint needs to know the compiler options for each of them. These options are the same arguments for actual compilers, like gcc or clang. There are two alternatives for passing the options to OCLint, namely specifying the compiler options directly to OCLint and using compilation database.

Giving Compiler Options
^^^^^^^^^^^^^^^^^^^^^^^

Compiler options can be given directly to OCLint. It's quite straight forward, after all OCLint options and sources, append ``--`` separator followed by all compiler options:

.. code-block:: none

    oclint [oclint options] <source0> [... <sourceN>] -- [compiler options]

For example, if we are compiling a file by the following ``clang`` command:

.. code-block:: bash

    clang -x objective-c -arch armv7 -std=gnu99 -fobjc-arc -O0 -isysroot /Developer/SDKs/iPhoneOS6.0.sdk -g -I./Pods/Headers -c RPActivityIndicatorManager.m

(Wow, it's longer than expectation.)

Then when we analyze this code, our OCLint command will be:

.. code-block:: bash

    oclint [oclint options] RPActivityIndicatorManager.m -- -x objective-c -arch armv7 -std=gnu99 -fobjc-arc -O0 -isysroot /Developer/SDKs/iPhoneOS6.0.sdk -g -I./Pods/Headers -c

Compilation Database
^^^^^^^^^^^^^^^^^^^^

\-p <build-path>
    Choose the build directory in which a file named compile_commands.json exists. When no build path is specified, a search for compile_commands.json will be attempted through all parent paths of the first input file.

If no compiler options are given explicitly, OCLint requires this compilation database to understand specific build options for each source file. Currently it supports ``compile_commands.json`` file. See `oclint-json-compilation-database <oclint-json-compilation-database.html>`_ for detail.

Sources Options
------------------

We specify the path to all the source files we want to inspect. Multiple files can be analyzed with one invocation.

Report Options
--------------

\-o <path>
    Instead of piping output to console, ``-o`` will redirect the report to the <path> you specified.
\-report-type <name>
    Change output report type, by default, plain text report is used

See `picking up the right reporter <../howto/selectreporters.html>`_ for detail.

Exit Status Options
-------------------

\-max-priority-1 <threshold>
    The max allowed number of priority 1 violations
\-max-priority-2 <threshold>
    The max allowed number of priority 2 violations
\-max-priority-3 <threshold>
    The max allowed number of priority 3 violations

This option helps continuous integration and other build systems. OCLint returns with one of the five exit codes below

* **0** - SUCCESS
* **1** - RULE_NOT_FOUND
* **2** - REPORTER_NOT_FOUND
* **3** - ERROR_WHILE_PROCESSING
* **4** - ERROR_WHILE_REPORTING
* **5** - VIOLATIONS_EXCEED_THRESHOLD

OCLint always return code zero for success execution with the number of violations under an acceptable range. Exit code other than zero means there are something wrong.

For example, when the compilation process fails, an exit code of 3 will be returned. It means either the compiler options have not been set correctly, or the source code has errors.

When the number of violations in any of the priorities is larger than the maximum tolerance, OCLint returns with an exit status code of 5. By default, less than 20 priority 3 violations are allowed, 10 violations is maximum for priority 2, and no priority 1 violation can be tolerated. Too many violations result in bad code quality, if that happens, OCLint intends to fail the build system.

Global Analysis Options
-----------------------

\-enable-global-analysis
    enable OCLint global analysis

With global analysis enabled, entire context of all given source code files is hold in the memory, and is available to the current analyzing file. This enables metrics calculation and other analyses that require cross-reference of the other files in the same project, which improves the accuracy of the analysis. However, global analysis results in high memory load, and may end up with long analysis duration, so it's designed for powerful machines and is enabled only by users' intents.

Clang Static Analyzer Options
-----------------------------

\-enable-clang-static-analyzer
    enable Clang Static Analyzer

When Clang Static Analyzer is enabled, OCLint will invoke it under the hook along with the process, collect its results, and emit them with the reporter. Notice that, by invoking Clang Static Analyzer, it will significantly increase the total analysis time.

Debug Options
-------------

\-debug
    invoke OCLint in debug mode.

If OCLint is built in the debug model, ``-debug`` outputs deeper message from OCLint invocation. It prints messages that can help understand the overall progress of OCLint analysis. Please aware that this is only available when OCLint is built with debug flag on.

Other Options
-------------

\-version
    Show version information about OCLint, LLVM and some environment variables.
