Core Module
===========

Core module can be treated as the engine of OCLint. In general, it dispatches the tasks to other modules in order, drives the work flow of the entire analysis process, and generates outputs.

When OCLint is invoked with your inputs, it reads the source code files and parses them into abstract syntax tree, it also loads rules and selected reporter. 

Rules then analyze deeply into each abstract syntax tree representation of the source code received, and find smelly code that matches the predefined patterns. 

During the inspection, certain metrics are calculated to have a better understanding of the source code. In addition, some rules will ask for threshold configurations in order to decide whether emit violations.

All violations are collected into set, and are eventually sent to reporter. Selected reporter will the convert violation set and related statistic summarization into certain type of report for output.

Following is a brief description of each component in the core module:

CommandLineOptions
    Extends command line arguments on top of LibTooling with OCLint specified options.
Processor
    Takes over ``ASTContext``, initializes ``ViolationSet`` and ``RuleCarrier``, and then applies all loaded rules for analysis, finally, push the ``ViolationSet`` into ``Results``.
Reporter
    Defines the ``Reporter`` interface.
Results
    Is a collection of ``ViolationSet`` for all source code. Plus some methods to find statistic result inside all violations.
RuleBase
    Defines the base interface of all rules.
RuleCarrier
    As its name implies, it carries the abstract syntax tree of the source code and a violation set. When it is initialized in ``Processor``, it takes an empty violation set. Then, it is examined through all rules. Each rule traverses the context and focus on a specific aspect. When it finds a matched pattern, a violation will be pushed to violation set. Eventually, a *contaminated* RuleVarrier will return back with all violations for diagnostic.
RuleConfiguration
    Stores custom thresholds for rules.
RuleSet
    When selected rules are loaded, they are collected into this ``RuleSet``.
Version
    With the current version identifier, can be used in places where version is a differentiator, like reporters.
Violation
    Is a container of all details about a violation, like the violated rule, path of the source code, start line/column, end line/column, and sometimes, a helper diagnostic message or suggestion.
ViolationSet
    Contains violations.
