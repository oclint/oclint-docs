.. _how-it-works-oclint:

How It Works
============

OCLint checks source code against rules, and produces a report.

#. Pass input files and program options to OCLint
#. OCLint hands the input file off to parser in libclang
#. OCLint gets an Abstract Syntax Tree (AST) from libclang
#. Traverse AST, for each of the node, apply every rule in the ruleset and check for problems. The whole AST only be traversed once. For each of the nodes in AST, apply all rules in RuleSet to it.
#. The violations are now stored in the ViolationSet, and OCLint will choose a reporter to render output.
