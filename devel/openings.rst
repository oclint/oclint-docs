Open Projects
=============

This page contains a TODO list in a large picture. You can understand it as a road map. Some of them are small, but some are infinitely big. Implementation schedule of these projects are very flexible, we also release partial progress of some big projects if they look good and provide benefits to users.

OCLint started as a research project, so in addition to the features that are designed for industrial usage, there are some projects here that could be very interesting research projects in their own right. Users can leverage the research results for higher accuracy, better performance, more reasonable software metrics, and so on.

In any case, we welcome all contributions. If you are thinking one of them, please send an email to `oclint-dev mailing list <https://groups.google.com/group/oclint-dev>`_, so that we know this is being worked on. Please use the same mailing list to suggest more projects to this page.

More Rules
----------

Rules are always welcome.

More Reporters
--------------

Reporters are also great welcome. We also plan to support major continuous integration systems, e.g. Jenkins and TeamCity, by adding reporters and/or implementing plugins.

More Metrics
------------

More interesting metrics can help developers measure their source code in different aspects. In addition to existing metrics, we are planning to add more metrics, like Weighted Method Count (WMC), Tight Class Cohesion (TCC), Access to Foreign Data (ATFD), Assignment-Branch-Condition (ABC), and so on.

OCLint's metrics module is actually a cohesive library, it can be reused in your project without any OCLint dependencies. So, the new introduced metrics should only depend on abstract syntax tree representation.

Better Build System
-------------------

Using bash scripts to organize the build system is not as good as letting the build system handles this by itself. We already use CMake in every modules, so now, we need to figure out a way to let CMake handle all projects under the OCLint umbrella.

Xcode Plugin/Addon/Extension
----------------------------

We are happy with existing `oclint-xcodebuild <../usage/oclint-xcodebuild.html>`_, but we also want to provide a graphic interface for Xcode users. The idea is either being a Xcode plugin to be able to invoke OCLint inside Xcode, or being a standalone extension to open a Xcode workspace/project, select scheme, target, and other settings, then show source code with inline analysis results.

Control Flow Graphic Engine
---------------------------

A strong control flow graphic engine can help with a better understand of the order that statements, expressions, and functions are evaluated or executed. For instance, goto statements force program to jump to a different statement, if statements execute a branch of statements only if certain conditions are met, while statements run the code inside a loop iteratively, etc. It helps increase the analysis accuracy and avoid false positives.

We have applied control flow analysis in some existing rules, but we would like to have an engine to gain a more comprehensive understanding of the source code.

Data Flow Engine
----------------

Data flow provides global information about how a procedure manipulates its data, such as the use, declaration and dependency of the data. For example, a new value could be assigned to an existing variable, and the memory address of a pointer can be reallocated.

It is easier to detect the data flow in runtime. However, certain dynamic behaviors of the data can be also determined in static code analysis with data flow engine. Data flow engine is a big supplement to control flow engine.

Code Duplication and Logic Duplication Detection
------------------------------------------------

We hope to apply `Rabin–Karp string search algorithm <http://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_string_search_algorithm>`_ in code duplication detection.

When it comes to logic duplication detection, there are many interesting experiments that we can conduct. But first of all, your humbled author has to admit that currently I don't have a complete definition of logic duplication. But let's think about the following interesting case:

Let's say, 20 years ago, long before I join my current company, a senior developer had written a method like this

.. code-block:: c++

    void foo(int x, int y)
    {
         cout << x - y;
         cout << x * y;
    }

And 10 years ago, he left the company. But his code is still in a base level library.

I joined this company after my graduation from college, 10 years after he left the company, so almost all my teammates even don't know the existence of the method above. And one day, I occasionally write something like this

.. code-block:: c++

    void bar()
    {
        cout << 1 + 2;
        cout << 1 - 2;
        cout << 1 * 2;
        cout << 1 / 2;
    }

Now, in this case, I really hope to be informed that I can change my code to

.. code-block:: c++

    void bar()
    {
        cout << 1 + 2;
        foo(1, 2);
        cout << 1 / 2;
    }

This might not be a perfect example, but I hope you can feel a little bit about the meaning of ``logic duplication`` here. This is a valuable feature to many organizations that have to maintain large codebase, especially with many legacy code. In order to find out the logic duplication in the early stage of development can truly help them reduce the high maintenance in the future.

Refactoring Suggestions
-----------------------

In addition to detecting code defects that break our defined rule set, we hope to provide you suggestions of how to improve your code by refactoring. We hope to do it smartly and intelligently that the suggestions will be given after fully analyzing the context of the rot code.

Design Patterns Extraction
--------------------------

It's helpful to know the design patterns we have applied in our codebase.

Type Inference
--------------

We know we can sometimes cheat to let compilers happy with certain things. This is a very dangerous practice.

But, on the other hand, sometimes, we also want to take the advantages of the dynamic of programming languages, like void pointer in C and C++, and ``id`` in Objective-C, even though they are static typed languages.

In fact, we believe type inference, the technique of automatically deduce, either partially or fully, the type even at compile time.

However, this largely increase the false positive in static code analysis.

Luckily, as the development of programming language techniques, type inference is introduced as a technique to automatically deduce, either partially or fully, the type of an expression at compile time. Many static typed languages have type inference capabilities builtin nowadays, so that as a developer, even though it's a static typed language, but you could omit the type annotations without explicitly telling the compiler the type.

In this case, we can apply the same technique in static code analysis in order to lower false positive, and improve the accuracy at the same time.
