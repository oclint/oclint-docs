Overview
========

OCLint is a `static code analysis`_ tool for improving quality and reducing defects by inspecting C, C++ and Objective-C code and looking for potential problems like possible bugs, unused code, complicated code, redundant code, code smells, bad practices, and so on.

Features
--------

Static code analysis is a critical technique to detect defects that aren't visible to compilers. OCLint automates this inspection process with advanced features:

* Relying on the `abstract syntax tree`_ of the source code for better accuracy and efficiency; False positives are mostly reduced to avoid useful results sinking in them.
* Dynamically loading rules into system, even in the runtime.
* Flexible and extensible configurations ensure users in customizing the behaviors of the tool.
* Command line invocation facilitates `continuous integration`_ and continuous inspection of the code while being developed, so that technical debts can be fixed early on to reduce the maintenance cost.

Current Status
--------------

OCLint is far from finished but is being continuously improved in many aspects, e.g. accuracy, performance and usability.

OCLint started as a research project (`defense poster`_) at the `University of Houston`_. Since then, OCLint has been rewritten and grown to be a 100% open source project. OCLint is designed to serve both academia and industry. Our goal is to make it a must-have tool for developers who program in C, C++ and Objective-C languages.

OCLint is compatible with Mac OS X and various Linux distributions.

Get Started
-----------

There is a large change that pre-compiled binaries are ready for you to `download <download.html>`_. It's also recommended to start with `getting the release code <download.html>`_ and `building it <build.html>`_. We can then `install <installation.html>`_ and `run <tutorial.html>`_ OCLint.

Get Involved
------------

Please also consider `getting involved`_ in the OCLint community. All kinds of contributions, like giving feedback, start a discussion, filing bug reports, request new features, best of all, submitting a patch or two, are appreciated.

.. _static code analysis: http://en.wikipedia.org/wiki/Static_program_analysis
.. _abstract syntax tree: http://en.wikipedia.org/wiki/Abstract_syntax_tree
.. _continuous integration: http://martinfowler.com/articles/continuousIntegration.html
.. _defense poster: http://www.cs.uh.edu/news-events/thesis-defenses/2012/04.02-lQi.html
.. _University of Houston: http://www.uh.edu
.. _getting involved: http://oclint.org/community.html
