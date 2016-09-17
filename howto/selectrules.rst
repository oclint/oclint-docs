Select OCLint Rules for Inspection
==================================

OCLint is a rule based code analysis tool. Rule system is designed to be very extensible and flexible. So it's easy to customize rules in many ways, like making particular rule set for certain projects, categorize them and load them from different locations.

By default, rules will be loaded from ``$(/path/to/bin/oclint)/../lib/oclint/rules`` directory, we name it **rule search path** or **rule loading path**. Rule search path consists of a group of dynamic libraries, with extension ``.so`` in Linux, ``.dylib`` in macOS, and ``.dll`` in Windows. These dynamic libraries can be easily re-arranged or selected into new rule set for a particular project. This *plug-and-use* rule loading mechanism - all dynamic libraries are loaded when OCLint searches through rule loading paths - makes the tool very dynamic. Dragging and dropping new rules into the rule loading paths makes them immediate available for use. And multiple rule search paths are acceptable for one project, different rule loading paths can be specified for different projects.

In addition to building own rule set, rules can be picked or filtered out from an existing rule set, like the default one shipped with OCLint release bundle. This can be achieved through command line invocation or saving as configuration file.

Command Line Usages
-------------------

Rule search path can be switched with ``-R <directory>`` option. When multiple locations can be specified, and rules in all these paths will be loaded.

Selecting rules from the rule search path by ``-rule <rule name>``. On the other side, filtering rules out by ``-disable-rule <rule name>``.

For example, when all rules except ``GotoStatement`` from rule search path ``/path/to/rules`` are applied in the analysis, following command can be used::

    oclint -R /path/to/rules -disable-rule GotoStatement

Configuration File
------------------

Rule selections can be preserved into configuration files, and check in to source code system for team sharing the same standard. The same example for configuration file::

    rule-paths:
      - /path/to/rules
    rules:
    disable-rules:
      - GotoStatement

.. seealso::
    
    `OCLint configuration file <rcfile.html>`_
        Documentation for OCLint configuration file

    `Write Own Rules <../devel/rules.html>`_
        Documentation of modifying existing rule code or even write own rules to gain more capabilities.
