Download
========

All release downloads can be found at `OCLint website download page`_.

Choosing the Right Version
--------------------------

Development
    We keep our codebase stable by running continuous integrations on various platforms. Thus, it's safe to use the latest development version and get access to new features. However, certain things are under development and may not meet release standard.

Stable
    Latest official release is the most stable version, and meanwhile, is easier to get support from the entire community.

Previous
    Previous release is the second latest stable version, you can still get support from us. But pay attention, it will be archived when next version releases. In addition, deferring upgrading your development toolset is a type of technical debt that you should avoid.

Unsupported
    Choosing archived versions without supports.

This documentation is updated for OCLint version |version|.

Choosing Pre-Compiled Binaries
------------------------------

Pre-compiled binaries are considered to ease you get started. OCLint binaries depend on very little and fundamental system standard libraries. Each should properly works on the platform it specifies. However, there are rare cases that these binaries do not suit you well. If the compiled binary doesn't work on your machine, consider building OCLint locally.

When download process is finished, see `installation <installation.html>`_ document for next step.

Choosing Source Code
--------------------

All source code releases contain every module that is necessary for compilation and execution.

Different from development codebase, in which all dependencies are caught up to the latest version and debug flags are enabled, in released codebase, everything is finalized and optimized for that particular version.

Read `how to build OCLint <build.html>`_ when you have source code on hand.


.. _OCLint website download page: http://oclint.org/downloads.html
