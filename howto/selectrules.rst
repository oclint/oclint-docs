Select OCLint Rules for Inspection
==================================

OCLint is a rule based code analysis tool. Rule system is designed to be very extensible and flexible. So it's easy to customize rules in many ways, like making particular ruleset for certain projects, categorize them and load them from different locations, change the behavior of rules during runtime. We can even easily write our own custom rules, and plug them into OCLint system without rebuilding OCLint. We can find how to customize rules in this document, and how to custom rules in another page.

Selecting Rules for Inspection
------------------------------

By default, rules will be loaded from ``$(/path/to/bin/oclint)/../lib/oclint/rules`` directory, we name it **rule search path**. We can change the rule search path with ``-R <directory>`` option. Multiple locations can be specified, and rules in all these directories will be loaded.

Rule directory consists of a group of dynamic libraries, with extension ``.so`` in Linux and ``.dylib`` in Mac OS X. We can easily copy a subset of these rules into another folder, and use this new ruleset for particular projects. We call this *plug-and-use* rule loading mechanism - all dynamic libraries are loaded when OCLint searches through rule loading paths. So, when certain rules do not suite our project, simply remove them; and dragging and dropping new rules into the rule loading paths makes them immediate available for use.

