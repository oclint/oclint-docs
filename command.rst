.. _command-oclint:

Command Line Usage
==================

You can invoke OCLint in terminal and continuous integration systems. By passing arguments to the executable binary, you can configure OCLint to behave in the way you want.

They are two types of parameters, which are compiler options and OCLint configuration flags. You can always type oclint -help to see a list of usages like followings.

.. code-block:: bash

    [user@localhost ~]$ oclint -help
    OVERVIEW: OCLint, a static code analysis tool for Objective-C and related languages

    USAGE: oclint [options] <input files>

    OPTIONS:
      -D <macro>               - Predefine the specified macro
      -F <directory>           - Add directory to framework include search path
      -I <directory>           - Add directory to include search path
      -R <directory>           - Add directory to rule loading path
      -arch <arch_name>        - Specify which architecture (e.g. ppc, i386, x86_64, armv7) the compilation
                                 should targets.
      -help                    - Display available options (-help-hidden for more)
      -include <file>          - Include file before parsing
      -isysroot <directory>    - Add directory to SYSTEM include search path
      -o <file>                - Write output to <file>
      -rc <paramemter>=<value> - Change the baheviour of rules
      -stats                   - Enable statistics output from program
      Choose report type:
        -text                  - Plain text report
        -html                  - HTML formatted report
      -version                 - Display the version of this program
      -x <value>               - Input language type

Compiler Options
----------------

For compiler options, OCLint uses exactly same ones as Clang does (and compatible with most gcc flags). Most frequently used flags are ``-D``, ``-F``, ``-I``, ``-arch``, ``-include``, ``-isysroot``, and ``-x``.

OCLint Configurations
---------------------

The behavior of the tool can be configured by followings:

\-R
    By default, rules will be loaded from /usr/lib/oclint/rules. You can add multiple rule loading paths by using this flag. Rules can be loaded from multiple paths, but please aware that, once custom rule loading path is given, no matter one or many, default rules won’t be loaded any more. If default rules are needed, please either copy the default rules from /usr/lib/oclint/rules to your custom rule loading path, or use -R /usr/lib/oclint/rules to add it to the rule loading path again.

\-rc
    Parameters to change the behavior of rules. Options set here will be stored in memory, and postpone to the execution of each rules. To know the parameters for different rules, please check out the detail page for `certain rules <rules/index.html>`_.

\-o
    Path of output file. Without this flag, report will be printed to console.

\-text or -html
    Format of report, only one type could be selected for one invocation. Plain text report is the default.
