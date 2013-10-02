Suppress OCLint Warnings
========================

There are two scenarios you might want to suppress an warning:

* the standard for certain code measurement is controversial
* it is a false positive

There are several methods you could consider to suppress OCLint rule violations:

* If the warning you need to suppress also appeals to other OCLint users, e.g. a false positive

  * Patch test cases, amend the rule to make tests pass, and submit a pull request. Your help would be greatly appreciated by everyone
  * Open an issue on github or discuss with us in the mailing list

* If the standard of your project is slightly different from OCLint default settings

  * Consider `change those rules' thresholds <../customizing/rules.html#rule-thresholds>`_ according to your standard

* If certain rules are really annoying for your projects

  * `Add these rules into blacklist <selectrules.html>`_
  * `Remove them from the rule search path <../customizing/rules.html#selecting-rules-for-inspection>`_

* If it is a case-by-case thing, and only particular places need to be suppressed

  * `Use annotations <suppress.html#annotations>`_
  * `Use !OCLint comment <suppress.html#comment>`_

Annotations
-----------

By adding annotations to the source code, you can communicate with OCLint and order it to discard certain types of rule violations. However, for a better code quality purposes, not every rule can be suppressed. Currently, you can suppress the following warnings:

* unused method parameter
* high cyclomatic complexity
* high npath complexity
* high ncss method

In addition to these rules, please feel free to modify the implementation of other rules to enable this feature by yourself.

Annotation Syntax
^^^^^^^^^^^^^^^^^

You can suppress one rule like this::

  __attribute__((annotate("oclint:suppress[unused method parameter]")))


Or, you can suppress multiple rules at the same time, like this::

  __attribute__((annotate("oclint:suppress[high cyclomatic complexity]"), annotate("oclint:suppress[high npath complexity]"), annotate("oclint:suppress[high ncss method]")))

OCLint also allows you to suppress all supported rule warnings by::

  __attribute__((annotate("oclint:suppress")))

.. warning::

  Only supported rule warnings can be suppressed. In other words, if suppress feature is not enabled for a particular rule, e.g. ``long method``, then neither ``__attribute__((annotate("oclint:suppress[long method]")))`` nor ``__attribute__((annotate("oclint:suppress")))`` will help. In this case, we believe long methods are always the culprit of so many other code smells, thus we intent to discard the support for it. However, again, you can quickly learn how to enable it by looking at other supported rules.

Examples
^^^^^^^^

.. code-block:: objective-c

  bool __attribute__((annotate("oclint:suppress"))) aMethod(
      int aParameter __attribute__((annotate("oclint:suppress[unused method parameter]"))))
  {
      // code

      return true;
  }

  - (IBAction)turnoverValueChanged:
        (id) __attribute__((annotate("oclint:suppress[unused method parameter]"))) sender
  {
      [self calculateTurnover];
  }

  - (void)dismissAllViews:(id) __attribute__((annotate("oclint:suppress"))) currentView
          parentView:(id) __attribute__((annotate("oclint:suppress"))) parentView
          __attribute__((annotate("oclint:suppress")))
  {
      [self dismissTurnoverView];
      // plus 30+ lines of code of dismissing other views
  }
