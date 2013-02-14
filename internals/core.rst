Core Module
===========

Core module is the engine of OCLint. In general, it dispatches the tasks to other modules in order, drives the work flow of the entire analysis process, and generates outputs.

When OCLint is invoked, it reads the source code files and parses them into abstract syntax tree (AST), it also loads rules and chosen reporter.

Rules then analyze deeply into each AST representation of the source code, and find smelly AST nodes that match the predefined patterns.

During the inspection, certain metrics are calculated to have a better understanding of the source code. In addition, some rules ask for threshold configurations in order to decide whether to emit violations.

All violations are collected into a set, and are eventually sent to the reporter. Selected reporter will then convert violation set and related statistic summarization into certain type of report for output.

Following is a brief description of each component in the core module:

CommandLineOptions
    Extends command line arguments on top of LibTooling and defines new options for OCLint.
Processor
    Takes over ``ASTContext``, initializes ``ViolationSet`` and ``RuleCarrier``, and then applies all loaded rules for analysis, finally, pushes the ``ViolationSet`` into ``Results``.
Reporter
    Defines the interface of all reporters.
Results
    Is essentially a collection of ``ViolationSet``. Plus some methods to find statistic results inside all violations.
RuleBase
    Defines the base interface of all rules.
RuleCarrier
    As its name implies, it carries the AST of the source code and a violation set. When it is initialized in ``Processor``, it takes an immutable AST context and an empty violation set. Then, it is examined through all rules. Each rule traverses the AST context and focus on a specific aspect. When it finds a matched pattern, a violation will be pushed to violation set. Eventually, a *contaminated* RuleVarrier will return back with all violations for diagnostic.
RuleConfiguration
    Statically stores custom thresholds for rules.
RuleSet
    When selected rules are loaded, they are collected into this ``RuleSet``.
Version
    Contains the current version identifier, can be used in places, like reporters, where version is a differentiator.
Violation
    Is a container of all details about a violation, like the violated rule, path of the source code, start line and column number, end line and column number, and sometimes, a helper diagnostic message or suggestion.
ViolationSet
    Is a collection of violations.
