Open Projects
=============

This page shows the the roadmap of this project. We warmly welcome all sorts of contributions. Please use `oclint-dev mailing list <https://groups.google.com/group/oclint-dev>`_ for the best discussion channel, and use it for more ideas and suggestions.

.. seealso::

    Tasks in the pipeline, under discussion and being implemented can be found at `GitHub Issues <https://github.com/oclint/oclint/issues>`_ page.



More Rules
----------

Rules are always welcome.

More Reporters
--------------

Reporters are also great welcome. We also plan to support major continuous integration systems, e.g. TeamCity and CruiseControl, by adding reporters and/or implementing plugins.

More Metrics
------------

More interesting metrics can help developers measure their source code in different aspects. In addition to existing metrics, we are planning to add more metrics, like Weighted Method Count (WMC), Tight Class Cohesion (TCC), Access to Foreign Data (ATFD), Assignment-Branch-Condition (ABC), and so on.

OCLint's metrics module is actually a cohesive library, it can be reused in your project without any OCLint dependencies. So, the new introduced metrics should only depend on abstract syntax tree representation.

Package Manager Build
---------------------

We hope to provide native support for major package mangers, like homebrew for Mac and APT for Debian and its derived distributions.

Xcode Plugin/Addon/Extension
----------------------------

We are happy with existing `oclint-xcodebuild <../guide/oclint-xcodebuild.html>`_, but we also want to provide a graphic interface for Xcode users. The idea is either being a Xcode plugin to be able to invoke OCLint inside Xcode, or being a standalone extension to open a Xcode workspace/project, select scheme, target, and other settings, then show source code with inline analysis results.

Research Interests
------------------

OCLint started as a research project, so some ideas here can be explored much more with critical thinking. In addition, the tool can continue leveraging the research conclusions for higher accuracy, better performance, more reasonable software metrics, and so on.

Source Code Metrics
    More metrics could be explored and benefit the quality of source code.
Control Flow Graphic Engine
    A strong control flow graphic engine can help with a better understand of the order that statements, expressions, and functions are evaluated or executed. For instance, goto statements force program to jump to a different statement, if statements execute a branch of statements only if certain conditions are met, while statements run the code inside a loop iteratively, etc. It helps increase the analysis accuracy and avoid false positives. We have applied control flow analysis in some existing rules, but we would like to have an engine to gain a more comprehensive understanding of the source code.
Data Flow Engine
    Data flow provides global information about how a procedure manipulates its data, such as the use, declaration and dependency of the data. For example, a new value could be assigned to an existing variable, and the memory address of a pointer can be reallocated. It is easier to detect the data flow in runtime. However, certain dynamic behaviors of the data can be also determined in static code analysis with data flow engine. Data flow engine is a big supplement to control flow engine.
Code Duplication Detection
    Duplicated code is problematic, the command text-based duplication detection could be highly improved with source code logic based duplication detection.
Refactoring Suggestions
    In addition to detecting code defects that break our defined rule set, we hope to provide you suggestions of how to improve your code by refactoring. We hope to do it smartly and intelligently that the suggestions will be given after fully analyzing the context of the rot code.
Design Patterns Recognition
    It's helpful to know the design patterns we have applied in our codebase.
Type Inference
    We know we can sometimes cheat to let compilers happy with certain things. This is a very dangerous practice. But, on the other hand, sometimes, we also want to take the advantages of the dynamic of programming languages, like void pointer in C and C++, and ``id`` in Objective-C, even though they are static typed languages. In fact, we believe type inference, the technique of automatically deduce, either partially or fully, the type even at compile time. However, this largely increase the false positive in static code analysis. Luckily, as the development of programming language techniques, type inference is introduced as a technique to automatically deduce, either partially or fully, the type of an expression at compile time. Many static typed languages have type inference capabilities builtin nowadays, so that as a developer, even though it's a static typed language, but you could omit the type annotations without explicitly telling the compiler the type. In this case, we can apply the same technique in static code analysis in order to lower false positive, and improve the accuracy at the same time.

