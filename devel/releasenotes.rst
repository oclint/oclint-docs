Release Notes
=============

0.7
---

*These are in-progress notes for upcoming OCLint 0.7 release.*

oclint:

* Update LLVM/Clang to 3.3
* Use clang_rt.profile library for testing
* Apply Hamcrest concept in all test cases
* Update build system settings to support more unix-list platforms, including FreeBSD
* Redesign the RuleBase interface and introduce RuleCarrier
* Redesign the RuleConfiguration by using std::map

oclint-rules:

* Introduce AST matcher rules
* Suppress warnings for

  * unused method parameters
  * high cyclomatic complexity
  * high npath complexity
  * high ncss value

* Fix #10 - CollapsableIfStatementsRule false positives
* Fix #16 - MissingBreakInSwitchStatementRule false positive
* Rule scaffolding
* Reporter scaffolding

oclint-reporters:

* Extract reporters module from core module
* Add PMDReporter
* Add XMLReporter
* Add JSONReporter

oclint-clang-tooling:

* Extract ClangTooling related frontend code to this module from core module

oclint-xcodebuild:

* Support more major compilers
* Parse xcodebuild log for CURRENT_WORKING_FOLDER
* Push source out of CURRENT_WORKING_FOLDER to the bottom of the list
* Support custom xocdebuild log path

0.6
---

oclint:

* Update LLVM/Clang to 3.2, and switch from libClang to libTooling
* Completely redesign the project

  * Use libTooling for AST generation
  * Add metrics system
  * Better rule system
  * Introduce results analysis
  * Better reporters system

* New command line interface
* HTML report has a better UI design

oclint-metrics:

* Add NCSS metric
* Add statement depth metric

oclint-rules:

* Add BitwiseOperatorInConditionalRule
* Add BrokenOddnessCheckRule
* Add CollapsibleIfStatementsRule
* Add ConstantConditionalOperatorRule
* Add DoubleNegativeRule
* Add ForLoopShouldBeWhileLoopRule
* Add GotoStatementRule
* Add MultipleUnaryOperatorRule
* Add ReturnFromFinallyBlockRule
* Add ThrowExceptionFromFinallyBlockRule
* Add DefaultLabelNotLastInSwitchStatementRule
* Add InvertedLogicRule
* Add MissingBreakInSwitchStatementRule
* Add NonCaseLabelInSwitchStatementRule
* Add ParameterReassignmentRule
* Add SwitchStatementsShouldHaveDefaultRule
* Add TooFewBranchesInSwitchStatementRule
* Add EmptyCatchStatementRule
* Add EmptyDoWhileStatementRule
* Add EmptyElseBlockRule
* Add EmptyFinallyStatementRule
* Add EmptyForStatementRule
* Add EmptySwitchStatementRule
* Add EmptyTryStatementRule
* Add EmptyWhileStatementRule
* Add RedundantConditionalOperatorRule
* Add UnnecessaryElseStatementRule
* Add UselessParenthesesRule
* Add LongClassRule
* Add LongLineRule
* Add NcssMethodCountRule
* Add NestedBlockDepthRule

oclint-json-compilation-database:

* Initial release

oclint-xcodebuild:

* Initial release

0.4.3
-----

* Added benchmark, use -stats to show
* Smarter tree traversing policy, change traversing policy based on current node type
* Extract Driver logic from main.cpp to separate class
* Load clang header files by default, there is no need to put it into the header search path manually
* Enable automatic reference counting (ARC) with -fobjc-arc flag
* Automated PackageMaker for pkg installer generation
* Code formatting

0.4.2
-----

* Add description to violations

0.4.1
-----

* Refactoring: aggressively extract methods
* Update LLVM/Clang to 3.1svn

0.4
---

* Command line options to configure input/output, compiler's behaviors, rules' thresholds and report formats
* HTML report supported
* Rule configurations supported
* Fixed the false-positive for parameters in a block implementation

0.2.6
-----

* Check AST nodes which are declared within the current file being inspected
* Separate unused method parameter rule from unused local variable rule
* For unused local variable, ignore global variables that is not in a block
* Use clang_visitChildrenWithBlock to make the code cleaner and easier to understand
* Fix the false positive for unused method parameter in a pure C function
* Fix the crash when there is no rule dylib in the folder specified
* Use lcov to replace zcov as code coverage generation framework

0.2.4
-----

* Treat warnings as violations
* Adopt new CursorExtractionUtil using awesome __block feature to replace old TestCursorUtil
* New build configuration for libclang
* New rules

  * Long parameter list
  * Long method
  * Unreachable code
  * Constant if statement
  * If statement with negated condition
  * Redundant if statement
  * Redundant local variable
  * NPath complexity

0.2
---

* Initial academic research release
